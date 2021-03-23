---
title: Capitolo 1-Introduzione ad Azure RTO NetX POP3
description: L'API client POP3 NetX Duo è progettata per fornire un sistema di trasporto della posta elettronica per le piccole workstation per accedere ai maildrops client sui server POP3 per il recupero della posta client.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4d41da1e1e87e59c5c40674a58b288ac62ec8c78
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821752"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pop3"></a><span data-ttu-id="0239c-103">Capitolo 1-Introduzione ad Azure RTO NetX POP3</span><span class="sxs-lookup"><span data-stu-id="0239c-103">Chapter 1 - Introduction to Azure RTOS NetX POP3</span></span>

<span data-ttu-id="0239c-104">Il Post Office Protocol versione 3 (POP3) è un protocollo progettato per fornire un sistema di trasporto della posta elettronica per le piccole workstation per accedere ai client maildrops sui server POP3 per il recupero della posta client.</span><span class="sxs-lookup"><span data-stu-id="0239c-104">The Post Office Protocol Version 3 (POP3) is a protocol designed to provide a mail transport system for small workstations to access Client maildrops on POP3 Servers for retrieving Client mail.</span></span> <span data-ttu-id="0239c-105">POP3 utilizza i servizi Transmission Control Protocol (TCP) per eseguire il trasferimento della posta.</span><span class="sxs-lookup"><span data-stu-id="0239c-105">POP3 utilizes Transmission Control Protocol (TCP) services to perform mail transfer.</span></span> <span data-ttu-id="0239c-106">Per questo motivo, POP3 è un protocollo di trasferimento del contenuto altamente affidabile.</span><span class="sxs-lookup"><span data-stu-id="0239c-106">Because of this, POP3 is a highly reliable content transfer protocol.</span></span>

<span data-ttu-id="0239c-107">Tuttavia, POP3 non fornisce operazioni estese alla gestione della posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0239c-107">However, POP3 is does not provide extensive operations on mail handling.</span></span> <span data-ttu-id="0239c-108">In genere, la posta elettronica viene scaricata dal client e quindi eliminata dal alla maildrop. del server.</span><span class="sxs-lookup"><span data-stu-id="0239c-108">Typically, mail is downloaded by the Client and then deleted from the Server’s maildrop.</span></span>

## <a name="netx-duo-pop3-client-requirements"></a><span data-ttu-id="0239c-109">Requisiti del client POP3 di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="0239c-109">NetX Duo POP3 Client Requirements</span></span>

### <a name="client-requirements"></a><span data-ttu-id="0239c-110">Requisiti del client</span><span class="sxs-lookup"><span data-stu-id="0239c-110">Client Requirements</span></span>

<span data-ttu-id="0239c-111">L'API client POP3 NetX richiede un'istanza IP di NetX Duo creata in precedenza usando *nx_ip_create* e un pool di pacchetti NETX creato in precedenza usando *nx_packet_pool_create*.</span><span class="sxs-lookup"><span data-stu-id="0239c-111">The NetX POP3 Client API requires a previously created NetX Duo IP instance using *nx_ip_create* and a previously created NetX packet pool using *nx_packet_pool_create*.</span></span> <span data-ttu-id="0239c-112">Poiché il client POP3 NetX Duo usa i servizi TCP, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di usare l'API client POP3 di NETX Duo nella stessa istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="0239c-112">Because the NetX Duo POP3 Client utilizes TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using the NetX Duo POP3 Client API on that same IP instance.</span></span> <span data-ttu-id="0239c-113">Il client POP3 utilizza un socket TCP per connettersi a un server POP3 sulla porta POP3 del server.</span><span class="sxs-lookup"><span data-stu-id="0239c-113">The POP3 Client uses a TCP socket to connect to a POP3 Server on the Server’s POP3 port.</span></span> <span data-ttu-id="0239c-114">Questa impostazione viene in genere impostata sulla *porta nota 110, anche se per l'utilizzo di questa porta non è necessario alcun client POP3 né server.*</span><span class="sxs-lookup"><span data-stu-id="0239c-114">This is typically set at the *well-known port 110, though neither POP3 Client nor Server are required to use this port.*</span></span>

<span data-ttu-id="0239c-115">Le dimensioni del pool di pacchetti usato per la creazione del client POP3 sono configurabili dall'utente in termini di payload del pacchetto e numero di pacchetti disponibili.</span><span class="sxs-lookup"><span data-stu-id="0239c-115">The size of the packet pool used in creating the POP3 Client is user configurable in terms of packet payload and number of packets available.</span></span> <span data-ttu-id="0239c-116">Se il pacchetto viene usato solo nel servizio di creazione client POP3, il payload del pacchetto non deve essere superiore a 100-120 byte a seconda della lunghezza del nome utente e della password oppure del digest APOP.</span><span class="sxs-lookup"><span data-stu-id="0239c-116">If the packet is used only in the POP3 Client create service, the packet payload need not be more than 100-120 bytes depending on the length of username and password, or APOP digest.</span></span> <span data-ttu-id="0239c-117">Il comando utente con il nome utente dell'host locale è probabilmente il messaggio più grande inviato dal client POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-117">The USER command with the local host’s user name is probably the largest message sent by the POP3 Client.</span></span> <span data-ttu-id="0239c-118">È possibile condividere lo stesso pool di pacchetti nella nx_ip_create (pool di pacchetti predefinito IP) perché la operatiosn interna IP non richiede un payload di pacchetti molto grande per l'invio e la ricezione di dati di controllo TCP.</span><span class="sxs-lookup"><span data-stu-id="0239c-118">It is possible to share the same packet pool in the nx_ip_create (IP default packet pool) since the IP internal operatiosn do not require very large packet payload for sending and receiving TCP control data.</span></span>

<span data-ttu-id="0239c-119">Tuttavia, non è in genere vantaggioso che il driver Ethernet usi lo stesso pool di pacchetti del pool di pacchetti client POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-119">However, it is not generally advantageous for the Ethernet driver to use the same packet pool as the POP3 Client packet pool.</span></span> <span data-ttu-id="0239c-120">In genere, il payload del payload del pool di pacchetti di ricezione viene impostato come MTU dell'istanza IP (in genere 1500 byte) dell'interfaccia di rete che è molto più grande dei messaggi client POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-120">Generally, the payload of the receive packet pool payload is set the IP instance MTU (typically 1500 bytes) of the network interface which is much larger than POP3 Client messages.</span></span> <span data-ttu-id="0239c-121">I messaggi POP3 in arrivo normalmente sono dimensioni dei dati più grandi, quindi i messaggi del client POP3 in uscita</span><span class="sxs-lookup"><span data-stu-id="0239c-121">Incoming POP3 messages would usually be much larger data size then outgoing POP3 Client messages</span></span>

## <a name="netx-duo-pop3-client-creation"></a><span data-ttu-id="0239c-122">Creazione del client POP3 di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="0239c-122">NetX Duo POP3 Client Creation</span></span>

<span data-ttu-id="0239c-123">Per la creazione del client POP3 sono disponibili due servizi.</span><span class="sxs-lookup"><span data-stu-id="0239c-123">There are two services for creating the POP3 Client.</span></span> <span data-ttu-id="0239c-124">Il servizio consigliato è *nxd_pop3_client_create* che accetta un tipo di dati indirizzo NXD_ADDRESS che accetta indirizzi IPv4 o IPv6 per il server POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-124">The recommended service is *nxd_pop3_client_create* which takes an NXD_ADDRESS address data type that accepts IPv4 or IPv6 addresses for the POP3 server.</span></span> <span data-ttu-id="0239c-125">L'altro client POP3 crea il servizio, *nx_pop3_client_create*, accetta solo indirizzi IPv4 per il server POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-125">The other POP3 Client create service, *nx_pop3_client_create*, only accepts IPv4 addresses for the POP3 server.</span></span> <span data-ttu-id="0239c-126">Entrambi i servizi associano la porta TCP socket e si connettono al server POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-126">Both services bind the TCP socket port and connect with the POP3 server.</span></span>

<span data-ttu-id="0239c-127">Dopo la connessione al server POP3, l'applicazione client POP3 può chiamare *nx_pop3_client _mail_items_get* per ottenere il numero di elementi di posta che si siedono nella relativa casella alla maildrop.:</span><span class="sxs-lookup"><span data-stu-id="0239c-127">After connecting with the POP3 server, the POP3 Client application can call *nx_pop3_client _mail_items_get* to obtain the number of mail items sitting in its maildrop box:</span></span>

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items, ULONG *maildrop_total_size);
```

<span data-ttu-id="0239c-128">Se uno o più elementi si trovano nel client alla maildrop., l'applicazione può ottenere le dimensioni di un elemento di posta elettronica specifico usando il servizio *nx_pop3_client_get_mail_item* :</span><span class="sxs-lookup"><span data-stu-id="0239c-128">If one or more items are in the Client maildrop, the application can obtain the size of a specific mail item, using the *nx_pop3_client_get_mail_item* service:</span></span>

```C
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *item_size);
```

<span data-ttu-id="0239c-129">Il primo elemento di posta in alla maildrop. è in corrispondenza dell'indice 1.</span><span class="sxs-lookup"><span data-stu-id="0239c-129">The first mail item in the maildrop is at index 1.</span></span>

<span data-ttu-id="0239c-130">Per ottenere il messaggio di posta elettronica effettivo, l'applicazione può chiamare il servizio *nx_pop3_client_mail_item_get_message_data* per recuperare i pacchetti dei messaggi di posta elettronica fino a quando il servizio non indica che l'ultimo pacchetto viene ricevuto dall'argomento di input final_packet:</span><span class="sxs-lookup"><span data-stu-id="0239c-130">To get the actual mail message, the application can call the *nx_pop3_client_mail_item_get_message_data* service to retrieve the mail message packets until the service indicates the last packet is received by the final_packet input argument:</span></span>

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

<span data-ttu-id="0239c-131">Per eliminare un elemento di posta elettronica specifico, l'applicazione chiama *nx_pop3_client_mail_item_delete* con lo stesso indice usato nella chiamata *nx_pop3_client_get_mail_item* precedente.</span><span class="sxs-lookup"><span data-stu-id="0239c-131">To delete a specific mail item, the application calls *nx_pop3_client_mail_item_delete* with the same index as used in the preceding *nx_pop3_client_get_mail_item* call.</span></span>

<span data-ttu-id="0239c-132">Il client può essere eliminato utilizzando il servizio *nx_pop3_client_delete* .</span><span class="sxs-lookup"><span data-stu-id="0239c-132">The Client can be deleted using the *nx_pop3_client_delete* service.</span></span> <span data-ttu-id="0239c-133">Si noti che l'applicazione deve eliminare il pool di pacchetti client POP3 usando il servizio *nx_packet_pool_delete* non è più usato.</span><span class="sxs-lookup"><span data-stu-id="0239c-133">Note it is up to the application to delete the POP3 Client packet pool using the *nx_packet_pool_delete* service there is no longer has any use for it.</span></span>

## <a name="netx-duo-pop3-client-constraints"></a><span data-ttu-id="0239c-134">Vincoli client POP3 di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="0239c-134">NetX Duo POP3 Client Constraints</span></span>

<span data-ttu-id="0239c-135">Sono presenti alcuni vincoli nell'implementazione del client POP3 NetX Duo:</span><span class="sxs-lookup"><span data-stu-id="0239c-135">There are some constraints in the NetX Duo POP3 Client implementation:</span></span>

1. <span data-ttu-id="0239c-136">Il client POP3 NetX Duo non supporta il comando AUTH, Sebbene implementi l'autenticazione APOP usando DIGEST-MD5 per lo scambio di autenticazione del server client.</span><span class="sxs-lookup"><span data-stu-id="0239c-136">The NetX Duo POP3 Client does not support the AUTH command although it does implement APOP authentication using DIGEST-MD5 for the Client Server authentication exchange.</span></span>
2. <span data-ttu-id="0239c-137">Il client POP3 NetX Duo non implementa tutti i comandi POP3 (ad esempio, i comandi TOP o UIDL).</span><span class="sxs-lookup"><span data-stu-id="0239c-137">NetX Duo POP3 Client does not implement all POP3 commands (e.g. the TOP or UIDL commands).</span></span> <span data-ttu-id="0239c-138">Di seguito è riportato un elenco di comandi che supporta:</span><span class="sxs-lookup"><span data-stu-id="0239c-138">Below is a list of commands it does support:</span></span>
   - <span data-ttu-id="0239c-139">NOOP</span><span class="sxs-lookup"><span data-stu-id="0239c-139">NOOP</span></span>
   - <span data-ttu-id="0239c-140">RSET</span><span class="sxs-lookup"><span data-stu-id="0239c-140">RSET</span></span>

## <a name="netx-duo-pop3-client-login"></a><span data-ttu-id="0239c-141">Accesso client POP3 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="0239c-141">NetX Duo POP3 Client Login</span></span>

<span data-ttu-id="0239c-142">Un client POP3 NetX Duo deve autenticarsi (login) a un server POP3 per accedere a un alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="0239c-142">A NetX Duo POP3 Client must authenticate itself (login) to a POP3 Server to access a maildrop.</span></span> <span data-ttu-id="0239c-143">Questa operazione può essere eseguita usando i comandi USER/PASS e fornendo un nome utente e una password noti al server POP3 oppure usando il comando APOP e il digest MD5 descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="0239c-143">It can do so either by using the USER/PASS commands and providing a username and password known to the POP3 Server, or by using the APOP command and MD5 digest described below.</span></span>

<span data-ttu-id="0239c-144">Il nome utente è in genere un nome di dominio completo (contiene una parte locale e un nome di dominio, separati da un carattere "@").</span><span class="sxs-lookup"><span data-stu-id="0239c-144">The username is typically a fully qualified domain name (contains a local-part and a domain name, separated by an ‘@’ character).</span></span> <span data-ttu-id="0239c-145">Quando si usa l'utente dei comandi POP3 e si passa, il client invia il nome utente e la password non crittografati tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="0239c-145">When using the POP3 commands USER and PASS, the Client is sending its username and password unencrypted over the Internet.</span></span>

<span data-ttu-id="0239c-146">Per evitare i rischi di sicurezza derivanti da nome utente e password non crittografati, il client POP3 NetX Duo può essere configurato per l'uso dell'autenticazione APOP impostando il parametro *APOP_authentication* nel servizio *nxd_pop3_client_create* :</span><span class="sxs-lookup"><span data-stu-id="0239c-146">To avoid the security risk of clear texting username and password, the NetX Duo POP3 Client can be configured to use APOP authentication by setting the *APOP_authentication* parameter in the *nxd_pop3_client_create* service:</span></span>

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication,
    NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address, ULONG server_port,
    CHAR *client_name,
    CHAR *client_password);
```

<span data-ttu-id="0239c-147">O per le applicazioni solo IPv4, il servizio *nx_pop3_client_create* :</span><span class="sxs-lookup"><span data-stu-id="0239c-147">Or for IPv4 only applications, the *nx_pop3_client_create* service:</span></span>

```C
UINT  nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address,
    ULONG server_port, CHAR *client_name,
    CHAR *client_password);
```

<span data-ttu-id="0239c-148">Quando il client invia il comando APOP, accetta come unico argomento un digest MD5 contenente il dominio del server, l'ora locale e l'ID processo estratti dal messaggio di saluto del server, più la password del client.</span><span class="sxs-lookup"><span data-stu-id="0239c-148">When the Client sends the APOP command, it takes as its only argument an MD5 digest containing the server domain, local time and process ID extracted from the Server greeting, plus the Client password.</span></span> <span data-ttu-id="0239c-149">Il server POP3 creerà un digest MD5 contenente le stesse informazioni e se il digest MD5 corrisponde al digest MD5 del client, il client viene autenticato.</span><span class="sxs-lookup"><span data-stu-id="0239c-149">The POP3 Server will create an MD5 digest containing the same information and if its MD5 digest matches the Client’s MD5 digest, the Client is authenticated.</span></span>

<span data-ttu-id="0239c-150">Se l'autenticazione di APOP ha esito negativo, il client POP3 di NetX Duo tenterà l'autenticazione utente/PASS.</span><span class="sxs-lookup"><span data-stu-id="0239c-150">If APOP authentication fails, NetX Duo POP3 Client will attempt USER/PASS authentication.</span></span>

## <a name="the-pop3-client-maildrop"></a><span data-ttu-id="0239c-151">Alla maildrop. client POP3</span><span class="sxs-lookup"><span data-stu-id="0239c-151">The POP3 Client Maildrop</span></span>

<span data-ttu-id="0239c-152">Posta elettronica client viene archiviato in un server POP3 in una cassetta postale o "alla maildrop.".</span><span class="sxs-lookup"><span data-stu-id="0239c-152">Client mail is stored on a POP3 Server in a mailbox or “maildrop.”</span></span> <span data-ttu-id="0239c-153">Un alla maildrop. client in un server POP3 viene rappresentato come un elenco basato su 1 di elementi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0239c-153">A Client maildrop on a POP3 Server is represented as a 1 based list of mail items.</span></span> <span data-ttu-id="0239c-154">Ovvero, a ogni messaggio viene fatto riferimento dal relativo indice nell'elenco alla maildrop. con il primo elemento di posta in corrispondenza dell'indice 1 (diverso da zero).</span><span class="sxs-lookup"><span data-stu-id="0239c-154">That is, each mail is referred to by its index in the maildrop list with the first mail item at index 1 (not zero).</span></span> <span data-ttu-id="0239c-155">I comandi POP3 fanno riferimento a elementi di posta elettronica specifici in base al relativo indice nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="0239c-155">POP3 commands refer to specific mail items by their index in this list.</span></span>

## <a name="the-pop3-protocol-state-machine"></a><span data-ttu-id="0239c-156">Macchina a Stati del protocollo POP3</span><span class="sxs-lookup"><span data-stu-id="0239c-156">The POP3 Protocol State Machine</span></span>

<span data-ttu-id="0239c-157">Il protocollo POP3 richiede che sia il client che il server mantengano lo stato della sessione POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-157">The POP3 protocol requires that both Client and Server maintain the state of the POP3 session.</span></span> <span data-ttu-id="0239c-158">Innanzitutto, il client tenta di connettersi al server POP3.</span><span class="sxs-lookup"><span data-stu-id="0239c-158">First, the Client attempts to connect to the POP3 Server.</span></span> <span data-ttu-id="0239c-159">Se ha esito positivo, immette nel protocollo POP3 con tre stati distinti definiti da RFC 1939.</span><span class="sxs-lookup"><span data-stu-id="0239c-159">If successful it enters into the POP3 protocol which has three distinct states defined by RFC 1939.</span></span> <span data-ttu-id="0239c-160">Lo stato iniziale è lo stato di autorizzazione in cui deve identificarsi con il server.</span><span class="sxs-lookup"><span data-stu-id="0239c-160">The initial state is the Authorization state in which it must identify itself to the Server.</span></span> <span data-ttu-id="0239c-161">Nello stato di autorizzazione, il client POP3 può emettere solo l'utente e i comandi PASS e, in questo ordine, oppure il comando APOP.</span><span class="sxs-lookup"><span data-stu-id="0239c-161">In the Authorization state, the POP3 Client can only issue the USER and the PASS commands, and in that order, or the APOP command.</span></span>

<span data-ttu-id="0239c-162">Una volta autenticato il client POP3, la sessione client entra nello stato della transazione.</span><span class="sxs-lookup"><span data-stu-id="0239c-162">Once the POP3 Client is authenticated, the Client session enters the Transaction state.</span></span> <span data-ttu-id="0239c-163">In questo stato il client può scaricare e richiedere l'eliminazione della posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0239c-163">In this state, the Client can download and request mail deletion.</span></span> <span data-ttu-id="0239c-164">I comandi consentiti nello stato della transazione sono LIST, STAT, RETR, DELE, RSET e QUIT.</span><span class="sxs-lookup"><span data-stu-id="0239c-164">The commands allowed in the Transaction state are LIST, STAT, RETR, DELE, RSET and QUIT.</span></span> <span data-ttu-id="0239c-165">In genere il client POP3 invia un comando STAT seguito da una serie di comandi RETR (uno per ogni elemento di posta nel relativo alla maildrop.).</span><span class="sxs-lookup"><span data-stu-id="0239c-165">Typically the POP3 Client sends a STAT command followed by a series of RETR commands (one for each mail item in its maildrop).</span></span>

<span data-ttu-id="0239c-166">Una volta che il client ha eseguito il comando QUIT, la sessione POP3 entra nello stato di aggiornamento in cui avvia la disconnessione TCP dal server.</span><span class="sxs-lookup"><span data-stu-id="0239c-166">Once the Client issues the QUIT command, the POP3 session enters the Update state in which it initiates the TCP disconnect from the Server.</span></span> <span data-ttu-id="0239c-167">Per scaricare la posta in un altro momento, l'applicazione client POP3 può chiamare nx_pop3_client_mail_items_get per verificare la presenza di nuovi messaggi di posta elettronica in alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="0239c-167">To download mail at another time, the POP3 Client application can call nx_pop3_client_mail_items_get to check for new mail in the maildrop.</span></span>

### <a name="pop3-server-reply-codes"></a><span data-ttu-id="0239c-168">Codici di risposta del server POP3</span><span class="sxs-lookup"><span data-stu-id="0239c-168">POP3 Server Reply Codes</span></span>

- <span data-ttu-id="0239c-169">+ OK il server usa questa risposta per accettare un comando client.</span><span class="sxs-lookup"><span data-stu-id="0239c-169">+OK The Server uses this reply to accept a Client command.</span></span> <span data-ttu-id="0239c-170">Il server può includere informazioni aggiuntive dopo ' + OK ', ma non può presupporre che il client elabori tali informazioni, tranne nel caso di download dei dati del messaggio di posta elettronica o dei comandi LIST o DELE.</span><span class="sxs-lookup"><span data-stu-id="0239c-170">The Server can include additional information after the ‘+OK’ but cannot assume the Client will process this information, except in the case of downloading mail message data or the LIST or DELE commands.</span></span> <span data-ttu-id="0239c-171">Nel secondo caso, l'argomento "argument" dopo il comando fa riferimento all'indice dell'elemento di posta elettronica nel client alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="0239c-171">In the latter case, the ‘argument’ after the command references the index of the mail item in the Client maildrop.</span></span>
- <span data-ttu-id="0239c-172">-ERR il server usa questa risposta per rifiutare un comando client.</span><span class="sxs-lookup"><span data-stu-id="0239c-172">-ERR The Server uses this reply to reject a Client command.</span></span> <span data-ttu-id="0239c-173">Il server può inviare ulteriori informazioni dopo '-ERR ', ma non può presupporre che il client elabori le informazioni.</span><span class="sxs-lookup"><span data-stu-id="0239c-173">The Server may send additional information following the ‘-ERR’ but cannot assume the Client will process this information.</span></span>

### <a name="sample-pop3-client---server-session"></a><span data-ttu-id="0239c-174">Sessione client POP3 di esempio-server</span><span class="sxs-lookup"><span data-stu-id="0239c-174">Sample POP3 Client - Server Session</span></span>

<span data-ttu-id="0239c-175">**Esempio di POP3 di base che usa USER/PASS:**</span><span class="sxs-lookup"><span data-stu-id="0239c-175">**Basic POP3 example using USER/PASS:**</span></span>

```
S: <wait for connection on TCP port 110>
C: <open connection>
S: +OK POP3 server ready <1896.697170952@dbc.mtview.ca.us>
C: USER mrose
S: +OK mrose is valid
C: PASS mvan99
S: +OK mrose is logged in
C: STAT
S: +OK 2 320
C: RETR 1
S: +OK 120 octets
S: <the POP3 server sends message 1>
S: .
C: DELE 1
S: +OK message 1 deleted
C: RETR 2
S: +OK 200 octets
S: <the POP3 server sends message 2>
S: .
C: DELE 2
S: +OK message 2 deleted
C: QUIT
S: +OK POP3 server signing off (maildrop empty)
C: <close connection>
S: <wait for next connection>
```

<span data-ttu-id="0239c-176">**Esempio di POP3 di base con APOP (e LIST anziché STAT):**</span><span class="sxs-lookup"><span data-stu-id="0239c-176">**Basic POP3 example using APOP (and LIST instead of STAT):**</span></span>

```
S: <wait for connection on TCP port 110>
C: <open connection>
S: +OK POP3 server ready <1896.697170952@dbc.mtview.ca.us>
C: APOP mrose c4c9334bac560ecc979e58001b3e22fb
S: +OK mrose's maildrop has 2 messages (320 octets)
C: LIST
S: +OK 2 messages (320 octets)
S: 1 120
S: 2 200
S: .
C: RETR 1
S: +OK 120 octets
S: <the POP3 server sends message 1>
S: .
C: DELE 1
S: +OK message 1 deleted
C: RETR 2
S: +OK 200 octets
S: <the POP3 server sends message 2>
S: .
C: DELE 2
S: +OK message 2 deleted
C: QUIT
S: +OK dewey POP3 server signing off (maildrop empty)
C: <close connection>
S: <wait for next connection>
```

## <a name="rfcs-supported-by-netx-duo-pop3-client"></a><span data-ttu-id="0239c-177">RFC supportate dal client POP3 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="0239c-177">RFCs Supported by NetX Duo POP3 Client</span></span>

<span data-ttu-id="0239c-178">NetX Duo client POP3 è conforme a RFC 1939.</span><span class="sxs-lookup"><span data-stu-id="0239c-178">NetX Duo Client POP3 is compliant with RFC 1939.</span></span>
