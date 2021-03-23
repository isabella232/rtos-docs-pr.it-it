---
title: Capitolo 3-Descrizione dei servizi client DNS di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi DNS di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9634adab3944c29f64d26dd688b5053dc1bd9bcb
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821920"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dns-client-services"></a><span data-ttu-id="6e992-103">Capitolo 3-Descrizione dei servizi client DNS di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6e992-103">Chapter 3 - Description of Azure RTOS NetX Duo DNS Client Services</span></span>

<span data-ttu-id="6e992-104">Questo capitolo contiene una descrizione di tutti i servizi DNS di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="6e992-104">This chapter contains a description of all Azure RTOS NetX DNS services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="6e992-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="6e992-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="6e992-106">**nx_dns_authority_zone_start_get** *ricercare l'inizio di una zona di autorità associata al nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="6e992-106">**nx_dns_authority_zone_start_get** *Look up the start of a zone of authority associated with the specified host name*</span></span>

- <span data-ttu-id="6e992-107">**nx_dns_cache_initialize** *inizializzare una cache DNS.*</span><span class="sxs-lookup"><span data-stu-id="6e992-107">**nx_dns_cache_initialize** *Initialize a DNS Cache.*</span></span>

- <span data-ttu-id="6e992-108">**nx_dns_cache_notify_clear** *cancellare la funzione di notifica completa della cache.*</span><span class="sxs-lookup"><span data-stu-id="6e992-108">**nx_dns_cache_notify_clear** *Clear the cache full notify function.*</span></span>

- <span data-ttu-id="6e992-109">**nx_dns_cache_notify_set** *impostare la funzione di notifica completa della cache.*</span><span class="sxs-lookup"><span data-stu-id="6e992-109">**nx_dns_cache_notify_set** *Set the cache full notify function.*</span></span>

- <span data-ttu-id="6e992-110">**nx_dns_cname_get** *cercare il nome di dominio canonico per l'alias del nome di dominio di input*</span><span class="sxs-lookup"><span data-stu-id="6e992-110">**nx_dns_cname_get** *Look up the canonical domain name for the input domain name alias*</span></span>

- <span data-ttu-id="6e992-111">**nx_dns_create** *creare un'istanza del client DNS*</span><span class="sxs-lookup"><span data-stu-id="6e992-111">**nx_dns_create** *Create a DNS Client instance*</span></span>

- <span data-ttu-id="6e992-112">**nx_dns_delete** *eliminare un'istanza del client DNS*</span><span class="sxs-lookup"><span data-stu-id="6e992-112">**nx_dns_delete** *Delete a DNS Client instance*</span></span>

- <span data-ttu-id="6e992-113">**nx_dns_domain_name_server_get** *cercare i server dei nomi autorevoli per la zona del dominio di input*</span><span class="sxs-lookup"><span data-stu-id="6e992-113">**nx_dns_domain_name_server_get** *Look up the authoritative name servers for the input domain zone*</span></span>

- <span data-ttu-id="6e992-114">**nx_dns_domain_mail_exchange_get** *cercare lo scambio di posta associato al nome host specificato.*</span><span class="sxs-lookup"><span data-stu-id="6e992-114">**nx_dns_domain_mail_exchange_get** *Look up the mail exchange associated the specified host name.*</span></span>

- <span data-ttu-id="6e992-115">**nx_dns_domain_service_get** *cercare i servizi associati al nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="6e992-115">**nx_dns_domain_service_get** *Look up the service(s) associated with the specified host name*</span></span>

- <span data-ttu-id="6e992-116">**nx_dns_get_serverlist_size** *restituiscono le dimensioni dell'elenco di server client DNS*</span><span class="sxs-lookup"><span data-stu-id="6e992-116">**nx_dns_get_serverlist_size** *Return the size of the DNS Client server list*</span></span>

- <span data-ttu-id="6e992-117">**nx_dns_info_by_name_get** l' *indirizzo IP restituito, le query sulle porte sul nome host di input*</span><span class="sxs-lookup"><span data-stu-id="6e992-117">**nx_dns_info_by_name_get** *Return IP address, port querying on input host name*</span></span>

- <span data-ttu-id="6e992-118">**nx_dns_ipv4_address_by_name_get** *cercare l'indirizzo IPv4 dal nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="6e992-118">**nx_dns_ipv4_address_by_name_get** *Look up the IPv4 address from the specified host name*</span></span>

- <span data-ttu-id="6e992-119">**nxd_dns_ipv6_address_by_name_get** *cercare l'indirizzo IPv6 dal nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="6e992-119">**nxd_dns_ipv6_address_by_name_get** *Look up the IPv6 address from the specified host name*</span></span>

- <span data-ttu-id="6e992-120">**nx_dns_host_by_address_get** *funzione wrapper per nxd_dns_host_by_address_get per cercare un nome host da un indirizzo IP specificato (supporta solo indirizzi IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6e992-120">**nx_dns_host_by_address_get** *Wrapper function for nxd_dns_host_by_address_get to look up a host name from a specified IP address (supports only IPv4 addresses)*</span></span>

- <span data-ttu-id="6e992-121">**nxd_dns_host_by_address_get** *cercare un indirizzo IP dal nome host di input (supporta indirizzi IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6e992-121">**nxd_dns_host_by_address_get** *Look up an IP address from the input host name (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="6e992-122">**nx_dns_host_by_name_get** *funzione wrapper per nxd_dns_host_by_address_get per cercare un nome host dall'indirizzo specificato (supporta solo indirizzi IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6e992-122">**nx_dns_host_by_name_get** *Wrapper function for nxd_dns_host_by_address_get to look up a host name from the specified address (supports only IPv4 addresses)*</span></span>

- <span data-ttu-id="6e992-123">**nxd_dns_host_by_name_get** *cercare un indirizzo IP dal nome host di input (supporta indirizzi IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6e992-123">**nxd_dns_host_by_name_get** *Look up an IP address from the input host name (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="6e992-124">**nx_dns_host_text_get** *cercare i dati di testo per il nome di dominio di input*</span><span class="sxs-lookup"><span data-stu-id="6e992-124">**nx_dns_host_text_get** *Look up the text data for the input domain name*</span></span>

- <span data-ttu-id="6e992-125">**nx_dns_packet_pool_set** *impostare il pool di pacchetti client DNS*</span><span class="sxs-lookup"><span data-stu-id="6e992-125">**nx_dns_packet_pool_set** *Set the DNS Client packet pool*</span></span>

- <span data-ttu-id="6e992-126">**nx_dns_server_add** *funzione wrapper per* NXD_DNS_SERVER_ADD *aggiungere un server DNS all'indirizzo specificato all'elenco client (supporta solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6e992-126">**nx_dns_server_add** *Wrapper function for* nxd_dns_server_add *to add a DNS Server at the specified address to the Client list (supports only IPv4)*</span></span>

- <span data-ttu-id="6e992-127">**nxd_dns_server_add** *aggiungere un server DNS dell'indirizzo IP specificato all'elenco dei server client (supporta indirizzi sia IPv4 che IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6e992-127">**nxd_dns_server_add** *Add a DNS Server of the specified IP address to the Client server list (supports both IPv4 or IPv6 addresses)*</span></span>

- <span data-ttu-id="6e992-128">**nx_dns_server_get** *restituire il server DNS nell'elenco client (supporta solo indirizzi IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6e992-128">**nx_dns_server_get** *Return the DNS Server in the Client list (supports only IPv4 addresses)*</span></span>

- <span data-ttu-id="6e992-129">**nxd_dns_server_get** *restituire il server DNS nell'elenco client (supporta gli indirizzi IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6e992-129">**nxd_dns_server_get** *Return the DNS Server in the Client list (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="6e992-130">**nx_dns_server_remove** *funzione wrapper per nxd_dns_server_remove per rimuovere un server DNS dall'elenco client*</span><span class="sxs-lookup"><span data-stu-id="6e992-130">**nx_dns_server_remove** *Wrapper function for nxd_dns_server_remove to remove a DNS Server from the Client list*</span></span>

- <span data-ttu-id="6e992-131">**nxd_dns_server_remove** *rimuovere un server DNS dell'indirizzo IP specificato dall'elenco client (supporta gli indirizzi IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6e992-131">**nxd_dns_server_remove** *Remove a DNS Server of the specified IP address from the Client list (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="6e992-132">**nx_dns_server_remove_all** *rimuovere tutti i server DNS dall'elenco client*</span><span class="sxs-lookup"><span data-stu-id="6e992-132">**nx_dns_server_remove_all** *Remove all DNS Servers from the Client list*</span></span>

## <a name="nx_dns_authority_zone_start_get"></a><span data-ttu-id="6e992-133">nx_dns_authority_zone_start_get</span><span class="sxs-lookup"><span data-stu-id="6e992-133">nx_dns_authority_zone_start_get</span></span>

<span data-ttu-id="6e992-134">Cercare l'inizio della zona di autorità per l'host di input</span><span class="sxs-lookup"><span data-stu-id="6e992-134">Look up the start of the zone of authority for the input host</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-135">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-135">Prototype</span></span>
```C
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,                                        
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="6e992-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-136">Description</span></span>

<span data-ttu-id="6e992-137">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo SOA con il nome di dominio specificato per ottenere l'inizio della zona di autorità per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="6e992-137">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SOA with the specified domain name to obtain the start of the zone of authority for the input domain name.</span></span> <span data-ttu-id="6e992-138">Il client DNS copia i record SOA restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-138">The DNS Client copies the SOA record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

> [!NOTE]
> <span data-ttu-id="6e992-139">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-139">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="6e992-140">Nel client DNS di NetX Duo, il tipo di record SOA, NX_DNS_SOA_ENTRY, viene salvato come parametri di 7 4 byte, totale di 28 byte:</span><span class="sxs-lookup"><span data-stu-id="6e992-140">In NetX Duo DNS Client, the SOA record type, NX_DNS_SOA_ENTRY, is saved as seven 4 byte parameters, totaling 28 bytes:</span></span>

- <span data-ttu-id="6e992-141">**nx_dns_soa_host_mname_ptr** Puntatore all'origine dati primaria per questa zona.</span><span class="sxs-lookup"><span data-stu-id="6e992-141">**nx_dns_soa_host_mname_ptr** Pointer to primary source of data for this zone.</span></span>
- <span data-ttu-id="6e992-142">**nx_dns_soa_host_rname_ptr** Puntatore alla cassetta postale responsabile di questa zona</span><span class="sxs-lookup"><span data-stu-id="6e992-142">**nx_dns_soa_host_rname_ptr** Pointer to mailbox responsible for this zone</span></span>
- <span data-ttu-id="6e992-143">**nx_dns_soa_serial** Numero di versione zona</span><span class="sxs-lookup"><span data-stu-id="6e992-143">**nx_dns_soa_serial** Zone version number</span></span>
- <span data-ttu-id="6e992-144">**nx_dns_soa_refresh** Intervallo di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="6e992-144">**nx_dns_soa_refresh** Refresh interval</span></span>
- <span data-ttu-id="6e992-145">**nx_dns_soa_retry** Intervallo tra i tentativi di query SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-145">**nx_dns_soa_retry** Interval between SOA query retries</span></span>
- <span data-ttu-id="6e992-146">**nx_dns_soa_expire** Durata dell'ora di scadenza di SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-146">**nx_dns_soa_expire** Time duration when SOA expires</span></span>
- <span data-ttu-id="6e992-147">**nx_dns_soa_minmum** Campo TTL minimo nei messaggi di risposta DNS del nome host SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-147">**nx_dns_soa_minmum** Minimum TTL field in SOA hostname DNS reply messages</span></span>

<span data-ttu-id="6e992-148">L'archiviazione di due record SOA è illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="6e992-148">The storage of a two SOA records is shown below.</span></span> <span data-ttu-id="6e992-149">I record SOA contenenti dati a lunghezza fissa vengono immessi a partire dall'inizio del buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-149">The SOA records containing fixed length data are entered starting at the top of the buffer.</span></span> <span data-ttu-id="6e992-150">I puntatori MNAME e RNAME puntano ai dati a lunghezza variabile (nomi host) archiviati nella parte inferiore del buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-150">The pointers MNAME and RNAME point to the variable length data (host names) which are stored at the bottom of the buffer.</span></span> <span data-ttu-id="6e992-151">Vengono immessi record SOA aggiuntivi dopo il primo record ("record SOA aggiuntivi...") e i dati a lunghezza variabile vengono archiviati sopra i dati a lunghezza variabile dell'ultima voce ("dati di lunghezza variabile SOA aggiuntivi"):</span><span class="sxs-lookup"><span data-stu-id="6e992-151">Additional SOA records are entered after the first record (“additional SOA records…”) and their variable length data is stored above the last entry’s variable length data (“additional SOA variable length data”):</span></span>

![Archiviazione di due record SOA](media/image4.png)

<span data-ttu-id="6e992-153">Se l'input *record_buffer* non può contenere tutti i dati SOA nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-153">If the input *record_buffer* cannot hold all the SOA data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="6e992-154">Con il numero di record SOA restituiti in \**record_count,* l'applicazione può analizzare i dati da *record_buffer* ed estrarre l'inizio delle stringhe del nome host dell'autorità di zona.</span><span class="sxs-lookup"><span data-stu-id="6e992-154">With the number of SOA records returned in \**record_count,* the application can parse the data from *record_buffer* and extract the start of zone authority host name strings.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-155">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-155">Input Parameters</span></span>

- <span data-ttu-id="6e992-156">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-156">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-157">**HOST_NAME** Puntatore al nome host per cui ottenere i dati SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-157">**host_name** Pointer to host name to obtain SOA data for</span></span>
- <span data-ttu-id="6e992-158">**record_buffer** Puntatore alla posizione in cui estrarre i dati SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-158">**record_buffer** Pointer to location to extract SOA data into</span></span>
- <span data-ttu-id="6e992-159">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-159">**buffer_size** Size of buffer to hold SOA data</span></span>
- <span data-ttu-id="6e992-160">**record_count** Puntatore al numero di record SOA recuperati</span><span class="sxs-lookup"><span data-stu-id="6e992-160">**record_count** Pointer to the number of SOA records retrieved</span></span>
- <span data-ttu-id="6e992-161">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-161">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-162">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-162">Return Values</span></span>

- <span data-ttu-id="6e992-163">**NX_SUCCESS** (0x00) ha ottenuto i dati SOA</span><span class="sxs-lookup"><span data-stu-id="6e992-163">**NX_SUCCESS** (0x00) Successfully obtained SOA data</span></span>
- <span data-ttu-id="6e992-164">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-164">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-165">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-165">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-166">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-166">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-167">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-167">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-168">NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-168">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-169">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-169">Allowed From</span></span>

<span data-ttu-id="6e992-170">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-170">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-171">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-171">Example</span></span>
```C
UCHAR  record_buffer[50];
UINT   record_count;   
NX_DNS_SOA_ENTRY *nx_dns_soa_entry_ptr;

/* Request the start of authority zone(s) for the specified host. */
status =  nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com",  
                                          record _buffer, sizeof(record_buffer), 
                                          &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
         error_counter++;
}
else 
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SOA data 
       is returned in soa_buffer. */

    /* Set a local pointer to the SOA buffer. */
    nx_dns_soa_entry_ptr = (NX_DNS_SOA_ENTRY *) record_buffer;

    printf("------------------------------------------------------\n");
    printf("Test SOA: \n");
    printf("serial = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_serial );
    printf("refresh = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_refresh );
    printf("retry = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_retry );
    printf("expire = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_expire );
    printf("minmum = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_minmum );

    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr)
    {
        printf("host mname = %s\n", 
               nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr);
    }
    else
    {
        printf("host mame is not set\n");
    }

    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr)
    {
        printf("host rname = %s\n", 
               nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr);
    }
    else
    {
     
        printf("host rname is not set\n");
    }
}

[Output]
----------------------------------------------------
Test SOA: 
serial = 2012111212
refresh = 7200
retry = 1800
expire = 1209600
minmum = 300
host mname = ns1.www.my_example.com
host rname = dns-admin.www.my_example.com
```

## <a name="nx_dns_cache_initialize"></a><span data-ttu-id="6e992-172">nx_dns_cache_initialize</span><span class="sxs-lookup"><span data-stu-id="6e992-172">nx_dns_cache_initialize</span></span>

<span data-ttu-id="6e992-173">Inizializzare la cache DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-173">Initialize the DNS Cache</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-174">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-174">Prototype</span></span>
```C
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                            VOID *cache_ptr, UINT cache_size);
```

### <a name="description"></a><span data-ttu-id="6e992-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-175">Description</span></span>

<span data-ttu-id="6e992-176">Questo servizio crea e Inizializza una cache DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-176">This service creates and initializes a DNS Cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-177">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-177">Input Parameters</span></span>

- <span data-ttu-id="6e992-178">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-178">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="6e992-179">**cache_ptr** Puntatore alla cache DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-179">**cache_ptr** Pointer to DNS Cache.</span></span>
- <span data-ttu-id="6e992-180">**cache_size** Dimensioni della cache DNS, in byte.</span><span class="sxs-lookup"><span data-stu-id="6e992-180">**cache_size** Size of DNS Cache, in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-181">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-181">Return Values</span></span>

- <span data-ttu-id="6e992-182">Cache DNS **NX_SUCCESS** (0x00) inizializzata correttamente</span><span class="sxs-lookup"><span data-stu-id="6e992-182">**NX_SUCCESS** (0x00) DNS Cache successfully initialized</span></span>
- <span data-ttu-id="6e992-183">NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-183">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="6e992-184">Il puntatore della cache NX_DNS_CACHE_ERROR (0xB7) non è valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-184">NX_DNS_CACHE_ERROR (0xB7) Invalid Cache pointer.</span></span>
- <span data-ttu-id="6e992-185">NX_PTR_ERROR (0x07) puntatore DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-185">NX_PTR_ERROR (0x07) Invalid DNS pointer.</span></span> 
- <span data-ttu-id="6e992-186">La cache NX_DNS_ERROR (messaggi 0XA0) non è allineata a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="6e992-186">NX_DNS_ERROR (0xA0) Cache is not 4-byte aligned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-187">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-187">Allowed From</span></span>

<span data-ttu-id="6e992-188">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-188">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-189">Example</span></span>
```C
/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, &dns_cache, 2048);

/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a><span data-ttu-id="6e992-190">nx_dns_cache_notify_clear</span><span class="sxs-lookup"><span data-stu-id="6e992-190">nx_dns_cache_notify_clear</span></span>

<span data-ttu-id="6e992-191">Cancella la funzione di notifica completa della cache DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-191">Clear the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-192">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-192">Prototype</span></span>
```C
UINT nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```

### <a name="description"></a><span data-ttu-id="6e992-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-193">Description</span></span>

<span data-ttu-id="6e992-194">Questo servizio Cancella la funzione di notifica completa della cache.</span><span class="sxs-lookup"><span data-stu-id="6e992-194">This service clears the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-195">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-195">Input Parameters</span></span>

- <span data-ttu-id="6e992-196">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-196">**dns_ptr** Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-197">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-197">Return Values</span></span>

- <span data-ttu-id="6e992-198">Notifica della cache DNS **NX_SUCCESS** (0x00) impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="6e992-198">**NX_SUCCESS** (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="6e992-199">NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido</span><span class="sxs-lookup"><span data-stu-id="6e992-199">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="6e992-200">NX_PTR_ERROR (0x07) puntatore DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-200">NX_PTR_ERROR (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-201">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-201">Allowed From</span></span>

<span data-ttu-id="6e992-202">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-202">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-203">Example</span></span>
```C
/* Clear the DNS Cache full notify function. */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a><span data-ttu-id="6e992-204">nx_dns_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="6e992-204">nx_dns_cache_notify_set</span></span>

<span data-ttu-id="6e992-205">Impostare la funzione di notifica completa della cache DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-205">Set the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-206">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-206">Prototype</span></span>
```C
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr,
                            VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a><span data-ttu-id="6e992-207">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-207">Description</span></span>

<span data-ttu-id="6e992-208">Questo servizio imposta la funzione di notifica completa della cache.</span><span class="sxs-lookup"><span data-stu-id="6e992-208">This service sets the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-209">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-209">Input Parameters</span></span>

- <span data-ttu-id="6e992-210">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-210">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="6e992-211">**cache_full_notify_cb** Funzione di callback da richiamare quando la cache diventa piena.</span><span class="sxs-lookup"><span data-stu-id="6e992-211">**cache_full_notify_cb** The callback function to be invoked when cache become full.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-212">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-212">Return Values</span></span>

- <span data-ttu-id="6e992-213">Notifica della cache DNS **NX_SUCCESS** (0x00) impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="6e992-213">**NX_SUCCESS** (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="6e992-214">NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido</span><span class="sxs-lookup"><span data-stu-id="6e992-214">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="6e992-215">NX_PTR_ERROR (0x07) puntatore DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-215">NX_PTR_ERROR (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-216">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-216">Allowed From</span></span>

<span data-ttu-id="6e992-217">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-217">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-218">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-218">Example</span></span>
```C
/* Set the DNS Cache full notify function. */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set. */
```

## <a name="nx_dns_cname_get"></a><span data-ttu-id="6e992-219">nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="6e992-219">nx_dns_cname_get</span></span>

<span data-ttu-id="6e992-220">Cercare il nome canonico per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="6e992-220">Look up the canonical name for the input hostname</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-221">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-221">Prototype</span></span>
```C
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                     UCHAR *record_buffer, UINT buffer_size, 
                     ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-222">Description</span></span>

<span data-ttu-id="6e992-223">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES viene definito in *nxd_dns. h*, questo servizio invia una query di tipo CNAME con il nome di dominio specificato per ottenere il nome di dominio canonico.</span><span class="sxs-lookup"><span data-stu-id="6e992-223">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined in *nxd_dns.h*, this service sends a query of type CNAME with the specified domain name to obtain the canonical domain name.</span></span> <span data-ttu-id="6e992-224">Il client DNS copia la stringa CNAME restituita nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-224">The DNS Client copies the CNAME string returned in the DNS Server response into the *record_buffer* memory location.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-225">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-225">Input Parameters</span></span>

- <span data-ttu-id="6e992-226">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-226">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-227">**HOST_NAME** Puntatore al nome host per cui ottenere i dati CNAME</span><span class="sxs-lookup"><span data-stu-id="6e992-227">**host_name** Pointer to host name to obtain CNAME data for</span></span>
- <span data-ttu-id="6e992-228">**record_buffer** Puntatore alla posizione in cui estrarre i dati CNAME</span><span class="sxs-lookup"><span data-stu-id="6e992-228">**record_buffer** Pointer to location to extract CNAME data into</span></span>
- <span data-ttu-id="6e992-229">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati CNAME</span><span class="sxs-lookup"><span data-stu-id="6e992-229">**buffer_size** Size of buffer to hold CNAME data</span></span>
- <span data-ttu-id="6e992-230">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-230">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-231">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-231">Return Values</span></span>

- <span data-ttu-id="6e992-232">**NX_SUCCESS** (0x00) ha ottenuto i dati CNAME</span><span class="sxs-lookup"><span data-stu-id="6e992-232">**NX_SUCCESS** (0x00) Successfully obtained CNAME data</span></span>
- <span data-ttu-id="6e992-233">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-233">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-234">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-234">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-235">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-235">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-236">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-236">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-237">NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido</span><span class="sxs-lookup"><span data-stu-id="6e992-237">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-238">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-238">Allowed From</span></span>

<span data-ttu-id="6e992-239">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-239">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-240">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-240">Example</span></span>
```C
CHAR            record _buffer[50];

/* Request the canonical name for the specified host. */
status =  nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                                   record_buffer, sizeof(record_buffer), 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and 
   the canonical host name is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test CNAME: %s\n", record_buffer);
} 

[Output]
----------------------------------------------------
Test CNAME: my_example.com
```

##  <a name="nx_dns_create"></a><span data-ttu-id="6e992-241">nx_dns_create</span><span class="sxs-lookup"><span data-stu-id="6e992-241">nx_dns_create</span></span>

<span data-ttu-id="6e992-242">Creare un'istanza del client DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-242">Create a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-243">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-243">Prototype</span></span>
```C
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```
### <a name="description"></a><span data-ttu-id="6e992-244">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-244">Description</span></span>

<span data-ttu-id="6e992-245">Questo servizio crea un'istanza del client DNS per l'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-245">This service creates a DNS Client instance for the previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e992-246">L'applicazione deve garantire che il payload dei pacchetti del pool di pacchetti utilizzato dal client DNS sia sufficientemente grande per il numero massimo di messaggi DNS a 512 byte, più le intestazioni UDP, IP e Ethernet.</span><span class="sxs-lookup"><span data-stu-id="6e992-246">The application must ensure that the packet payload of the packet pool used by the DNS Client is large enough for the maximum 512 byte DNS message, plus UDP, IP and Ethernet headers.</span></span> <span data-ttu-id="6e992-247">Se il client DNS crea il proprio pool di pacchetti, viene definito da NX_DNS_PACKET_PAYLOAD e NX_DNS_PACKET_POOL_SIZE.</span><span class="sxs-lookup"><span data-stu-id="6e992-247">If the DNS Client creates its own packet pool, this is defined by NX_DNS_PACKET_PAYLOAD and NX_DNS_PACKET_POOL_SIZE.</span></span>

<span data-ttu-id="6e992-248">Se l'applicazione client DNS preferisce fornire un pool di pacchetti creato in precedenza, il payload per il client DNS IPv4 deve essere di 512 byte per il DNS massimo più 20 byte per l'intestazione IP, 8 byte per l'intestazione UDP e 14 byte per l'intestazione Ethernet.</span><span class="sxs-lookup"><span data-stu-id="6e992-248">If the DNS Client application prefers to supply a previously created packet pool, the payload for IPv4 DNS Client should be 512 bytes for the maximum DNS plus 20 bytes for the IP header, 8 bytes for the UDP header and 14 bytes for the Ethernet header.</span></span> <span data-ttu-id="6e992-249">Per IPv6, l'unica differenza è che l'intestazione IP è 40 byte, pertanto il pacchetto deve contenere l'intestazione IPv6 di 40 byte.</span><span class="sxs-lookup"><span data-stu-id="6e992-249">For IPv6 the only difference is the IP header is 40 bytes, therefore the packet needs to accommodate the IPv6 header of 40 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-250">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-250">Input Parameters</span></span>

- <span data-ttu-id="6e992-251">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-251">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-252">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-252">**ip_ptr** Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="6e992-253">**Domain_name** Puntatore al nome di dominio per l'istanza DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-253">**domain_name** Pointer to domain name for DNS instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-254">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-254">Return Values</span></span>

- <span data-ttu-id="6e992-255">Creazione DNS riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="6e992-255">**NX_SUCCESS** (0x00) Successful DNS create</span></span>
- <span data-ttu-id="6e992-256">Errore di creazione DNS **NX_DNS_ERROR** (messaggi 0XA0)</span><span class="sxs-lookup"><span data-stu-id="6e992-256">**NX_DNS_ERROR** (0xA0) DNS create error</span></span>
- <span data-ttu-id="6e992-257">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-257">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-258">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-258">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-259">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-259">Allowed From</span></span>

<span data-ttu-id="6e992-260">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-260">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-261">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-261">Example</span></span>
```C
/* Create a DNS Client instance. */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created. */
```

## <a name="nx_dns_delete"></a><span data-ttu-id="6e992-262">nx_dns_delete</span><span class="sxs-lookup"><span data-stu-id="6e992-262">nx_dns_delete</span></span>

<span data-ttu-id="6e992-263">Eliminare un'istanza del client DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-263">Delete a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-264">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-264">Prototype</span></span>
```C
UINT nx_dns_delete(NX_DNS *dns_ptr);
```
### <a name="description"></a><span data-ttu-id="6e992-265">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-265">Description</span></span>

<span data-ttu-id="6e992-266">Questo servizio Elimina un'istanza del client DNS creata in precedenza e libera le risorse.</span><span class="sxs-lookup"><span data-stu-id="6e992-266">This service deletes a previously created DNS Client instance and frees up its resources.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-267">Se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definito e al client DNS è stato assegnato un pool di pacchetti definito dall'utente, spetta all'applicazione eliminare il pool di pacchetti client DNS se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="6e992-267">If NX_DNS_CLIENT_USER_CREATE_PACKET_POOL is defined and the DNS Client was assigned a user defined packet pool, it is up to the application to delete the DNS Client packet pool if it no longer needs it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-268">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-268">Input Parameters</span></span>

- <span data-ttu-id="6e992-269">**dns_ptr** Puntatore a un'istanza del client DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-269">**dns_ptr** Pointer to previously created DNS Client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-270">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-270">Return Values</span></span>

- <span data-ttu-id="6e992-271">Eliminazione del client DNS riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="6e992-271">**NX_SUCCESS** (0x00) Successful DNS Client delete.</span></span>
- <span data-ttu-id="6e992-272">NX_PTR_ERROR (0x07) un puntatore client IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-272">NX_PTR_ERROR (0x07) Invalid IP or DNS Client pointer.</span></span>
- <span data-ttu-id="6e992-273">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="6e992-273">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-274">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-274">Allowed From</span></span>

<span data-ttu-id="6e992-275">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-275">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-276">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-276">Example</span></span>
```C
/* Delete a DNS Client instance. */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted. */
```

## <a name="nx_dns_domain_name_server_get"></a><span data-ttu-id="6e992-277">nx_dns_domain_name_server_get</span><span class="sxs-lookup"><span data-stu-id="6e992-277">nx_dns_domain_name_server_get</span></span>

<span data-ttu-id="6e992-278">Cercare i server dei nomi autorevoli per la zona del dominio di input</span><span class="sxs-lookup"><span data-stu-id="6e992-278">Look up the authoritative name servers for the input domain zone</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-279">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-279">Prototype</span></span>
```C
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-280">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-280">Description</span></span>

<span data-ttu-id="6e992-281">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo NS con il nome di dominio specificato per ottenere i server dei nomi per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="6e992-281">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type NS with the specified domain name to obtain the name servers for the input domain name.</span></span> <span data-ttu-id="6e992-282">Il client DNS copia i record NS restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-282">The DNS Client copies the NS record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

> [!NOTE]
> <span data-ttu-id="6e992-283">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-283">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="6e992-284">Nel client DNS di NetX Duo il tipo di dati NS, NX_DNS_NS_ENTRY, viene salvato come parametri a 2 4 byte:</span><span class="sxs-lookup"><span data-stu-id="6e992-284">In NetX Duo DNS Client the NS data type, NX_DNS_NS_ENTRY, is saved as two 4-byte parameters:</span></span>

- <span data-ttu-id="6e992-285">**nx_dns_ns_ipv4_address** Indirizzo IPv4 del server dei nomi</span><span class="sxs-lookup"><span data-stu-id="6e992-285">**nx_dns_ns_ipv4_address** Name server’s IPv4 address</span></span>
- <span data-ttu-id="6e992-286">**nx_dns_ns_hostname_ptr** Puntatore al nome host del server dei nomi</span><span class="sxs-lookup"><span data-stu-id="6e992-286">**nx_dns_ns_hostname_ptr** Pointer to the name server’s hostname</span></span>

<span data-ttu-id="6e992-287">Il buffer riportato di seguito contiene quattro record NX_DNS_NS_ENTRY.</span><span class="sxs-lookup"><span data-stu-id="6e992-287">The buffer shown below contains four NX_DNS_NS_ENTRY records.</span></span> <span data-ttu-id="6e992-288">Il puntatore alla stringa del nome host in ogni voce punta alla stringa del nome host corrispondente nella metà inferiore del buffer:</span><span class="sxs-lookup"><span data-stu-id="6e992-288">The pointer to host name string in each entry points to the corresponding host name string in the bottom half of the buffer:</span></span>

![Contiene quattro record NX_DNS_NS_ENTRY](media/image5.png)

<span data-ttu-id="6e992-290">Se il *record_buffer* di input non può contenere tutti i dati NS nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-290">If the input *record_buffer* cannot hold all the NS data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="6e992-291">Con il numero di record NS restituiti in \**record_count,* l'applicazione può analizzare l'indirizzo IP e il nome host di ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="6e992-291">With the number of NS records returned in \**record_count,* the application can parse the IP address and host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-292">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-292">Input Parameters</span></span>

- <span data-ttu-id="6e992-293">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-293">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-294">**HOST_NAME** Puntatore al nome host per cui ottenere i dati NS</span><span class="sxs-lookup"><span data-stu-id="6e992-294">**host_name** Pointer to host name to obtain NS data for</span></span>
- <span data-ttu-id="6e992-295">**record_buffer** Puntatore alla posizione in cui estrarre i dati NS</span><span class="sxs-lookup"><span data-stu-id="6e992-295">**record_buffer** Pointer to location to extract NS data into</span></span>
- <span data-ttu-id="6e992-296">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati NS</span><span class="sxs-lookup"><span data-stu-id="6e992-296">**buffer_size** Size of buffer to hold NS data</span></span>
- <span data-ttu-id="6e992-297">**record_count** Puntatore al numero di record NS recuperati</span><span class="sxs-lookup"><span data-stu-id="6e992-297">**record_count** Pointer to the number of NS records retrieved</span></span>
- <span data-ttu-id="6e992-298">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-298">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-299">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-299">Return Values</span></span>

- <span data-ttu-id="6e992-300">**NX_SUCCESS** (0x00) ha ottenuto i dati NS</span><span class="sxs-lookup"><span data-stu-id="6e992-300">**NX_SUCCESS** (0x00) Successfully obtained NS data</span></span>
- <span data-ttu-id="6e992-301">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-301">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-302">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-302">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-303">NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido</span><span class="sxs-lookup"><span data-stu-id="6e992-303">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="6e992-304">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-304">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-305">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-305">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-306">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-306">Allowed From</span></span>

<span data-ttu-id="6e992-307">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-307">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-308">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-308">Example</span></span>
```C
#define RECORD_COUNT    10

ULONG  record_buffer[50];
UINT   record_count;          
NX_DNS_NS_ENTRY  *nx_dns_ns_entry_ptr[RECORD_COUNT];

/* Request the name server(s) for the specified host. */
status =  nx_dns_domain_name_server_get(&client_dns, (UCHAR *)" www.my_example.com ",  
                                        record_buffer, sizeof(record_buffer),  
                                        &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and NS data
   is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test NS: ");
    printf("record_count = %d \n", record_count);      

    /* Get the name server. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)
                               (record_buffer + i * sizeof(NX_DNS_NS_ENTRY)); 

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                      nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address  >> 24,
                      nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 16 & 0xFF,                   
                      nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 8 & 0xFF,
                     nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address & 0xFF);
        if(nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr)
        {
            printf("hostname = %s\n", 
                    nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr);
                }
        else
            printf("hostname is not set\n");
    }
}

[Output]
------------------------------------------------------
Test NS: record_count = 4 
record 0: IP address: 192.2.2.10
hostname = ns2.www.my_example.com
record 1: IP address: 192.2.2.11
hostname = ns1.www.my_example.com
record 2: IP address: 192.2.2.12
hostname = ns3.www.my_example.com
record 3: IP address: 192.2.2.13
hostname = ns4.www.my_example.com
```

## <a name="nx_dns_domain_mail_exchange_get"></a><span data-ttu-id="6e992-309">nx_dns_domain_mail_exchange_get</span><span class="sxs-lookup"><span data-stu-id="6e992-309">nx_dns_domain_mail_exchange_get</span></span>

<span data-ttu-id="6e992-310">Cerca lo scambio di posta/i per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="6e992-310">Look up the mail exchange(s) for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-311">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-311">Prototype</span></span>
```C
UINT nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                     VOID *record_buffer,                                        
                                     UINT buffer_size, 
                                     UINT *record_count, 
                                     ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-312">Description</span></span>

<span data-ttu-id="6e992-313">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo MX con il nome di dominio specificato per ottenere lo scambio di posta elettronica per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="6e992-313">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type MX with the specified domain name to obtain the mail exchange for the input domain name.</span></span> <span data-ttu-id="6e992-314">Il client DNS copia i record MX restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-314">The DNS Client copies the MX record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-315">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-315">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="6e992-316">Nel client DNS di NetX Duo, il tipo di record di scambio di posta, NX_DNS_MAIL_EXCHANGE_ENTRY, viene salvato come quattro parametri, per un totale di 12 byte:</span><span class="sxs-lookup"><span data-stu-id="6e992-316">In NetX Duo DNS Client, the mail exchange record type, NX_DNS_MAIL_EXCHANGE_ENTRY, is saved as four parameters, totaling 12 bytes:</span></span>

- <span data-ttu-id="6e992-317">**nx_dns_mx_ipv4_address** Indirizzo IPv4 di Exchange per posta elettronica 4 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-317">**nx_dns_mx_ipv4_address** Mail exchange IPv4 address 4 bytes</span></span>
- <span data-ttu-id="6e992-318">**nx_dns_mx_preference** Preferenza 2 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-318">**nx_dns_mx_preference** Preference 2 bytes</span></span>
- <span data-ttu-id="6e992-319">**nx_dns_mx_reserved0** 2 byte riservati</span><span class="sxs-lookup"><span data-stu-id="6e992-319">**nx_dns_mx_reserved0** Reserved 2 bytes</span></span>
- <span data-ttu-id="6e992-320">**nx_dns_mx_hostname_ptr** Puntatore al nome host del server di posta elettronica di Exchange Server 4 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-320">**nx_dns_mx_hostname_ptr** Pointer to mail exchange server host name 4 bytes</span></span>

<span data-ttu-id="6e992-321">Di seguito è riportato un buffer contenente quattro record MX.</span><span class="sxs-lookup"><span data-stu-id="6e992-321">A buffer containing four MX records is shown below.</span></span> <span data-ttu-id="6e992-322">Ogni record contiene i dati a lunghezza fissa dall'elenco precedente.</span><span class="sxs-lookup"><span data-stu-id="6e992-322">Each record contains the fixed length data from the list above.</span></span> <span data-ttu-id="6e992-323">Il puntatore al nome host di Exchange Server di posta elettronica punta al nome host corrispondente nella parte inferiore del buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-323">The pointer to the mail exchange server host name points to the corresponding host name at the bottom of the buffer.</span></span>

![Buffer contenente quattro record MX](media/image6.png)

<span data-ttu-id="6e992-325">Se l'input *record_buffer* non può contenere tutti i dati MX nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-325">If the input *record_buffer* cannot hold all the MX data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="6e992-326">Con il numero di record MX restituiti in \**record_count,* l'applicazione può analizzare i parametri MX, incluso il nome host della posta elettronica di ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="6e992-326">With the number of MX records returned in \**record_count,* the application can parse the MX parameters, including the mail host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-327">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-327">Input Parameters</span></span>

- <span data-ttu-id="6e992-328">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-328">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-329">**HOST_NAME** Puntatore al nome host per cui ottenere i dati MX</span><span class="sxs-lookup"><span data-stu-id="6e992-329">**host_name** Pointer to host name to obtain MX data for</span></span>
- <span data-ttu-id="6e992-330">**record_buffer** Puntatore alla posizione in cui estrarre i dati MX</span><span class="sxs-lookup"><span data-stu-id="6e992-330">**record_buffer** Pointer to location to extract MX data into</span></span>
- <span data-ttu-id="6e992-331">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati MX</span><span class="sxs-lookup"><span data-stu-id="6e992-331">**buffer_size** Size of buffer to hold MX data</span></span>
- <span data-ttu-id="6e992-332">**record_count** Puntatore al numero di record MX recuperati</span><span class="sxs-lookup"><span data-stu-id="6e992-332">**record_count** Pointer to the number of MX records retrieved</span></span>
- <span data-ttu-id="6e992-333">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-333">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-334">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-334">Return Values</span></span>

- <span data-ttu-id="6e992-335">**NX_SUCCESS** (0x00) ha ottenuto i dati MX</span><span class="sxs-lookup"><span data-stu-id="6e992-335">**NX_SUCCESS** (0x00) Successfully obtained MX data</span></span>
- <span data-ttu-id="6e992-336">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-336">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-337">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-337">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-338">NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido</span><span class="sxs-lookup"><span data-stu-id="6e992-338">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="6e992-339">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-339">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-340">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-340">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-341">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-341">Allowed From</span></span>

<span data-ttu-id="6e992-342">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-342">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-343">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-343">Example</span></span>
```C
#define MAX_RECORD_COUNT 10

ULONG  record_buffer[50];
UINT   record_count;  
NX_DNS_MX_ENTRY  *nx_dns_mx_entry_ptr[MAX_RECORD_COUNT];        

/* Request the mail exchange data for the specified host. */
status =  nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)" www.my_example.com ", 
                                          record_buffer, sizeof(record_buffer),   
                                          &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
       
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and MX
   data is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test MX: ");
    printf("record_count = %d \n", record_count);      


    /* Get the mail exchange. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)
               (record_buffer + i * sizeof(NX_DNS_MX_ENTRY));   

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,                   
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);

        printf("preference = %d \n ", 
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);

        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", 
                    nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
}


[Output]

-----------------------------------------------------
Test MX: record_count = 5 
record 0: IP address: 192.2.2.10
preference = 40 
hostname = alt3.aspmx.l.www.my_example.com
record 1: IP address: 192.2.2.11
preference = 50 
hostname = alt4.aspmx.l.www.my_example.com
record 2: IP address: 192.2.2.12
preference = 10 
hostname = aspmx.l.www.my_example.com
record 3: IP address: 192.2.2.13
preference = 20 
hostname = alt1.aspmx.l.www.my_example.com
record 4: IP address: 192.2.2.14
preference = 30 
hostname = alt2.aspmx.l.www.my_example.com
```

## <a name="nx_dns_domain_service_get"></a><span data-ttu-id="6e992-344">nx_dns_domain_service_get</span><span class="sxs-lookup"><span data-stu-id="6e992-344">nx_dns_domain_service_get</span></span>

<span data-ttu-id="6e992-345">Cerca i servizi forniti dal nome host di input</span><span class="sxs-lookup"><span data-stu-id="6e992-345">Look up the service(s) provided by the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-346">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-346">Prototype</span></span>
```C
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-347">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-347">Description</span></span>

<span data-ttu-id="6e992-348">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo SRV con il nome di dominio specificato per cercare i servizi e il relativo numero di porta associato al dominio specificato.</span><span class="sxs-lookup"><span data-stu-id="6e992-348">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SRV with the specified domain name to look up the service(s) and their port number associated with the specified domain.</span></span> <span data-ttu-id="6e992-349">Il client DNS copia i record SRV restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-349">The DNS Client copies the SRV record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-350">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-350">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="6e992-351">Nel client DNS di NetX Duo, il tipo di record del servizio, NX_DNS_SRV_ voce, viene salvato come sei parametri, per un totale di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="6e992-351">In NetX Duo DNS Client, the service record type, NX_DNS_SRV_ ENTRY, is saved as six parameters, totaling 16 bytes.</span></span> <span data-ttu-id="6e992-352">Ciò consente di archiviare i dati SRV a lunghezza variabile in modo efficiente in termini di memoria:</span><span class="sxs-lookup"><span data-stu-id="6e992-352">This enables variable length SRV data to be stored in a memory efficient manner:</span></span>

- <span data-ttu-id="6e992-353">**Indirizzo IPv4 del Server** nx_dns_srv_ipv4_address 4 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-353">**Server IPv4 address** nx_dns_srv_ipv4_address 4 bytes</span></span>
- <span data-ttu-id="6e992-354">**Priorità Server** nx_dns_srv_priority 2 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-354">**Server priority** nx_dns_srv_priority 2 bytes</span></span>
- <span data-ttu-id="6e992-355">**Peso Server** nx_dns_srv_weight 2 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-355">**Server weight** nx_dns_srv_weight 2 bytes</span></span>
- <span data-ttu-id="6e992-356">**Numero di porta del servizio** nx_dns_srv_port_number 2 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-356">**Service port number** nx_dns_srv_port_number 2 bytes</span></span>
- <span data-ttu-id="6e992-357">**Riservato per l'allineamento a 4 byte** nx_dns_srv_reserved0 2 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-357">**Reserved for 4-byte alignment** nx_dns_srv_reserved0 2 bytes</span></span>
- <span data-ttu-id="6e992-358">**Puntatore al nome host del server** \* nx_dns_srv_hostname_ptr 4 byte</span><span class="sxs-lookup"><span data-stu-id="6e992-358">**Pointer to server host name** \*nx_dns_srv_hostname_ptr 4 bytes</span></span>

<span data-ttu-id="6e992-359">Nel buffer fornito sono archiviati quattro record SRV.</span><span class="sxs-lookup"><span data-stu-id="6e992-359">Four SRV records are stored in the supplied buffer.</span></span> <span data-ttu-id="6e992-360">Ogni record di NX_DNS_SRV_ENTRY contiene un puntatore, *nx_dns_srv_hostname_ptr*, che punta alla stringa del nome host corrispondente nella parte inferiore del buffer di record:</span><span class="sxs-lookup"><span data-stu-id="6e992-360">Each NX_DNS_SRV_ENTRY record contains a pointer, *nx_dns_srv_hostname_ptr*, that points to the corresponding host name string in the bottom of the record buffer:</span></span>

![Quattro record SRV](media/image7.png)

<span data-ttu-id="6e992-362">Se l'input *record_buffer* non è in grado di contenere tutti i dati SRV nella risposta del server, il *record_buffer* include tutti i record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-362">If the input *record_buffer* cannot hold all the SRV data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="6e992-363">Con il numero di record SRV restituiti in \**record_count,* l'applicazione può analizzare i parametri SRV, incluso il nome host del server di ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="6e992-363">With the number of SRV records returned in \**record_count,* the application can parse the SRV parameters, including the server host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-364">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-364">Input Parameters</span></span>

- <span data-ttu-id="6e992-365">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-365">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-366">**HOST_NAME** Puntatore al nome host per il quale ottenere i dati SRV</span><span class="sxs-lookup"><span data-stu-id="6e992-366">**host_name** Pointer to host name to obtain SRV data for</span></span>
- <span data-ttu-id="6e992-367">**record_buffer** Puntatore alla posizione in cui estrarre i dati SRV</span><span class="sxs-lookup"><span data-stu-id="6e992-367">**record_buffer** Pointer to location to extract SRV data into</span></span>
- <span data-ttu-id="6e992-368">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati SRV</span><span class="sxs-lookup"><span data-stu-id="6e992-368">**buffer_size** Size of buffer to hold SRV data</span></span>
- <span data-ttu-id="6e992-369">**record_count** Puntatore al numero di record SRV recuperati</span><span class="sxs-lookup"><span data-stu-id="6e992-369">**record_count** Pointer to the number of SRV records retrieved</span></span>
- <span data-ttu-id="6e992-370">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-370">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-371">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-371">Return Values</span></span>

- <span data-ttu-id="6e992-372">**NX_SUCCESS** (0x00) ha ottenuto i dati SRV</span><span class="sxs-lookup"><span data-stu-id="6e992-372">**NX_SUCCESS** (0x00) Successfully obtained SRV data</span></span>
- <span data-ttu-id="6e992-373">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-373">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-374">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-374">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-375">Il parametro NX_DNS_PARAM_ERROR (0xA8) non è valido per il puntatore.</span><span class="sxs-lookup"><span data-stu-id="6e992-375">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer parameter.</span></span>
- <span data-ttu-id="6e992-376">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-376">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-377">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-377">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-378">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-378">Allowed From</span></span>

<span data-ttu-id="6e992-379">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-379">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-380">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-380">Example</span></span>
```C
#define MAX_RECORD_COUNT  10

UCHAR  record_buffer[50];
UINT   record_count;          
NX_DNS_SRV_ENTRY *nx_dns_srv_entry_ptr[MAX_RECORD_COUNT];

/* Request the service(s) provided by the specified host. */
status =  nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                                    record_buffer, sizeof(record_buffer), 
                                    &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SRV data
       is returned in record_buffer. */

        printf("------------------------------------------------------\n");
        printf("Test SRV: ");
        printf("record_count = %d \n", record_count);      

           
        /* Get the location of services. */
        for(i =0; i< record_count; i++)
        {
            nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)
                                    (record_buffer + i * sizeof(NX_DNS_SRV_ENTRY)); 

            printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 24,
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 16 & 0xFF,                   
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 8 & 0xFF,
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address & 0xFF);

           printf("port number = %d\n", 
                   nx_dns_srv_entry_ptr[i] -> nx_dns_srv_port_number );
           printf("priority = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_priority );
           printf("weight = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_weight );

           if(nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr)
           {
                printf("hostname = %s\n", 
                        nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr);
            }
           else
                printf("hostname is not set\n");
        }
}

[Output]
----------------------------------------------------
Test SRV: record_count = 3 
record 0: IP address: 192.2.2.10
port number = 5222
priority = 20
weight = 0
hostname = alt4.xmpp.l.www.my_example.com
record 1: IP address: 192.2.2.11
port number = 5222
priority = 5
weight = 0
hostname = xmpp.l.www.my_example.com
record 2: IP address: 192.2.2.12
port number = 5222
priority = 20
weight = 0
hostname = alt1.xmpp.l.www.my_example.com
```

## <a name="nx_dns_get_serverlist_size"></a><span data-ttu-id="6e992-381">nx_dns_get_serverlist_size</span><span class="sxs-lookup"><span data-stu-id="6e992-381">nx_dns_get_serverlist_size</span></span>

<span data-ttu-id="6e992-382">Restituisce le dimensioni dell'elenco di server del client DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-382">Return the size of the DNS Client’s Server list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-383">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-383">Prototype</span></span>
```C
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```
### <a name="description"></a><span data-ttu-id="6e992-384">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-384">Description</span></span>

<span data-ttu-id="6e992-385">Questo servizio restituisce il numero di server DNS validi (sia IPv4 che IPv6) nell'elenco client.</span><span class="sxs-lookup"><span data-stu-id="6e992-385">This service returns the number of valid DNS Servers (both IPv4 and IPv6) in the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-386">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-386">Input Parameters</span></span>

- <span data-ttu-id="6e992-387">**dns_ptr** Puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-387">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="6e992-388">**dimensioni** Restituisce il numero di server nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="6e992-388">**size** Returns the number of servers in the list</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-389">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-389">Return Values</span></span>

- <span data-ttu-id="6e992-390">Dimensioni elenco server DNS **NX_SUCCESS** (0x00) restituite correttamente</span><span class="sxs-lookup"><span data-stu-id="6e992-390">**NX_SUCCESS** (0x00) DNS Server list size successfully returned</span></span>
- <span data-ttu-id="6e992-391">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-391">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="6e992-392">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-392">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-393">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-393">Allowed From</span></span>

<span data-ttu-id="6e992-394">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-394">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-395">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-395">Example</span></span>
```C
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list. */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned. */
```

## <a name="nx_dns_info_by_name_get"></a><span data-ttu-id="6e992-396">nx_dns_info_by_name_get</span><span class="sxs-lookup"><span data-stu-id="6e992-396">nx_dns_info_by_name_get</span></span>

<span data-ttu-id="6e992-397">Restituire l'indirizzo IP e la porta del server DNS in base al nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-397">Return ip address and port of DNS server by host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-398">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-398">Prototype</span></span>
```C
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-399">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-399">Description</span></span>

<span data-ttu-id="6e992-400">Questo servizio restituisce l'indirizzo IP e la porta del server (record di servizio) in base al nome host di input da parte della query DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-400">This service returns the Server IP and port (service record) based on the input host name by DNS query.</span></span> <span data-ttu-id="6e992-401">Se non viene trovato un record del servizio, questa routine restituisce un indirizzo IP zero nel puntatore dell'indirizzo di input e un ritorno di stato di errore diverso da zero per segnalare un errore.</span><span class="sxs-lookup"><span data-stu-id="6e992-401">If a service record is not found, this routine returns a zero IP address in the input address pointer and a non-zero error status return to signal an error.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-402">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-402">Input Parameters</span></span>

- <span data-ttu-id="6e992-403">**dns_ptr** Puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-403">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="6e992-404">**HOST_NAME** Puntatore al buffer dei nomi host</span><span class="sxs-lookup"><span data-stu-id="6e992-404">**host_name** Pointer to host name buffer</span></span>
- <span data-ttu-id="6e992-405">**host_address_ptr** Puntatore all'indirizzo da restituire</span><span class="sxs-lookup"><span data-stu-id="6e992-405">**host_address_ptr** Pointer to address to return</span></span>
- <span data-ttu-id="6e992-406">**host_port_ptr** Puntatore alla porta da restituire</span><span class="sxs-lookup"><span data-stu-id="6e992-406">**host_port_ptr** Pointer to port to return</span></span>
- <span data-ttu-id="6e992-407">**WAIT_OPTION** Opzione wait per la risposta DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-407">**wait_option** Wait option for the DNS response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-408">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-408">Return Values</span></span>

- <span data-ttu-id="6e992-409">Record del server DNS **NX_SUCCESS** (0x00) restituito correttamente</span><span class="sxs-lookup"><span data-stu-id="6e992-409">**NX_SUCCESS** (0x00) DNS Server record successfully returned</span></span>
- <span data-ttu-id="6e992-410">**NX_DNS_NO_SERVER** (0XA1) nessun server DNS registrato con il client per l'invio di query sul nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-410">**NX_DNS_NO_SERVER** (0xA1) No DNS Server registered with Client to send query on hostname</span></span>
- <span data-ttu-id="6e992-411">La query DNS di **NX_DNS_QUERY_FAILED** (0xA3) non è riuscita. Nessuna risposta da alcun server DNS nell'elenco client o nessun record del servizio disponibile per il nome host di input.</span><span class="sxs-lookup"><span data-stu-id="6e992-411">**NX_DNS_QUERY_FAILED** (0xA3) DNS query failed; no response from any DNS servers in Client list or no service record is available for the input hostname.</span></span>
- <span data-ttu-id="6e992-412">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-412">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-413">NX_CALLER_ERROR (0x11) chiamante non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-413">NX_CALLER_ERROR (0x11) Invalid caller</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-414">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-414">Allowed From</span></span>

<span data-ttu-id="6e992-415">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-415">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-416">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-416">Example</span></span>
```C
ULONG ip_address
USHORT port;

/* Attempt to resolve the IP address and ports for this host name. */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned. */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a><span data-ttu-id="6e992-417">nx_dns_ipv4_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="6e992-417">nx_dns_ipv4_address_by_name_get</span></span>

<span data-ttu-id="6e992-418">Cercare l'indirizzo IPv4 per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="6e992-418">Look up the IPv4 address for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-419">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-419">Prototype</span></span>
```C
UINT nx_ dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                      UCHAR *host_name_ptr, VOID *buffer, 
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-420">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-420">Description</span></span>

<span data-ttu-id="6e992-421">Questo servizio invia una query di tipo A con il nome host specificato per ottenere gli indirizzi IP per il nome host di input.</span><span class="sxs-lookup"><span data-stu-id="6e992-421">This service sends a query of Type A with the specified host name to obtain the IP addresses for the input host name.</span></span> <span data-ttu-id="6e992-422">Il client DNS copia l'indirizzo IPv4 dai record A restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-422">The DNS Client copies the IPv4 address from the A record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

> [!NOTE]
> <span data-ttu-id="6e992-423">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-423">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="6e992-424">Più indirizzi IPv4 vengono archiviati nel buffer allineato a 4 byte, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6e992-424">Multiple IPv4 addresses are stored in the 4-byte aligned buffer as shown below:</span></span>

![buffer allineato a 4 byte a più indirizzi](media/image8.png)

<span data-ttu-id="6e992-426">Se il buffer fornito non è in grado di memorizzare tutti i dati degli indirizzi IP, i record A rimanenti non vengono archiviati in *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="6e992-426">If the supplied buffer cannot hold all the IP address data, the remaining A records are not stored in *record_buffer*.</span></span> <span data-ttu-id="6e992-427">Ciò consente all'applicazione di recuperare uno, alcuni o tutti i dati degli indirizzi IP disponibili nella risposta del server.</span><span class="sxs-lookup"><span data-stu-id="6e992-427">This enables the application to retrieve one, some or all of the available IP address data in the server reply.</span></span>

<span data-ttu-id="6e992-428">Con il numero di record restituiti in \**record_count* l'applicazione può analizzare i dati dell'indirizzo IPv4 dall' *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="6e992-428">With the number of A records returned in \**record_count* the application can parse the IPv4 address data from the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-429">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-429">Input Parameters</span></span>

- <span data-ttu-id="6e992-430">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-430">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-431">**host_name_ptr** Puntatore al nome host per ottenere l'indirizzo IPv4</span><span class="sxs-lookup"><span data-stu-id="6e992-431">**host_name_ptr** Pointer to host name to obtain IPv4 address</span></span>
- <span data-ttu-id="6e992-432">**buffer** Puntatore alla posizione in cui estrarre i dati IPv4</span><span class="sxs-lookup"><span data-stu-id="6e992-432">**buffer** Pointer to location to extract IPv4 data into</span></span>
- <span data-ttu-id="6e992-433">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati IPv4</span><span class="sxs-lookup"><span data-stu-id="6e992-433">**buffer_size** Size of buffer to hold IPv4 data</span></span>
- <span data-ttu-id="6e992-434">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-434">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-435">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-435">Return Values</span></span>

- <span data-ttu-id="6e992-436">**NX_SUCCESS** (0x00) ha ottenuto i dati IPv4</span><span class="sxs-lookup"><span data-stu-id="6e992-436">**NX_SUCCESS** (0x00) Successfully obtained IPv4 data</span></span>
- <span data-ttu-id="6e992-437">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-437">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-438">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-438">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-439">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-439">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-440">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-440">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-441">Il parametro NX_DNS_PARAM_ERROR (0xA8) non è valido per il puntatore.</span><span class="sxs-lookup"><span data-stu-id="6e992-441">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-442">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-442">Allowed From</span></span>

<span data-ttu-id="6e992-443">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-444">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-444">Example</span></span>
```C
#define MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
ULONG           *ipv4_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host. */
status =  nx_dns_ipv4_address_by_name_get(&client_dns, 
                                          (UCHAR *)"www.my_example.com",  
                                           record_buffer,                  
                                           sizeof(record_buffer),&record_count,                
                                           500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
        else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed the IPv4
       address(es) is returned in record_buffer. */

          
            printf("------------------------------------------------------\n");
            printf("Test A: ");
            printf("record_count = %d \n", record_count);      


           /* Get the IPv4 addresses of host. */
           for(i =0; i< record_count; i++)
           {
                ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG)); 
                printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                    *ipv4_address_ptr[i] >> 24,
                    *ipv4_address_ptr[i] >> 16 & 0xFF,                   
                    *ipv4_address_ptr[i] >> 8 & 0xFF,
                    *ipv4_address_ptr[i] & 0xFF);
            }

}

[Output]

------------------------------------------------------
Test A: record_count = 5 
record 0: IP address: 192.2.2.10
record 1: IP address: 192.2.2.11
record 2: IP address: 192.2.2.12
record 3: IP address: 192.2.2.13
record 4: IP address: 192.2.2.14
```

## <a name="nxd_dns_ipv6_address_by_name_get"></a><span data-ttu-id="6e992-445">nxd_dns_ipv6_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="6e992-445">nxd_dns_ipv6_address_by_name_get</span></span>

<span data-ttu-id="6e992-446">Cercare l'indirizzo IPv6 per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="6e992-446">Look up the IPv6 address for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-447">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-447">Prototype</span></span>
```C
UINT nxd_ dns_ipv6_address_by_name_get(NX_DNS *dns_ptr, 
                                      UCHAR *host_name_ptr, VOID *buffer, 
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-448">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-448">Description</span></span>

<span data-ttu-id="6e992-449">Questo servizio invia una query di tipo AAAA con il nome di dominio specificato per ottenere gli indirizzi IP per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="6e992-449">This service sends a query of type AAAA with the specified domain name to obtain the IP addresses for the input domain name.</span></span> <span data-ttu-id="6e992-450">Il client DNS copia l'indirizzo IPv6 dai record AAAA restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-450">The DNS Client copies the IPv6 address from the AAAA record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-451">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-451">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="6e992-452">Il formato degli indirizzi IPv6 archiviati nel buffer allineato a 4 byte è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6e992-452">The format of IPv6 addresses stored in the 4-byte aligned buffer is shown below:</span></span>

![Buffer allineato a 4 byte in formato IPv6](media/image9.png)

<span data-ttu-id="6e992-454">Se l'input *record_buffer* non può contenere tutti i dati aaaa nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="6e992-454">If the input *record_buffer* cannot hold all the AAAA data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="6e992-455">Con il numero di record AAAA restituiti in \**record_count,* l'applicazione può analizzare gli indirizzi IPv6 da ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="6e992-455">With the number of AAAA records returned in \**record_count,* the application can parse the IPv6 addresses from each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-456">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-456">Input Parameters</span></span>

- <span data-ttu-id="6e992-457">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-457">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-458">**host_name_ptr** Puntatore al nome host per ottenere l'indirizzo IPv6</span><span class="sxs-lookup"><span data-stu-id="6e992-458">**host_name_ptr** Pointer to host name to obtain IPv6 address</span></span>
- <span data-ttu-id="6e992-459">**buffer** Puntatore alla posizione in cui estrarre i dati IPv6</span><span class="sxs-lookup"><span data-stu-id="6e992-459">**buffer** Pointer to location to extract IPv6 data into</span></span>
- <span data-ttu-id="6e992-460">**BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati IPv6</span><span class="sxs-lookup"><span data-stu-id="6e992-460">**buffer_size** Size of buffer to hold IPv6 data</span></span>
- <span data-ttu-id="6e992-461">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-461">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-462">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-462">Return Values</span></span>

- <span data-ttu-id="6e992-463">**NX_SUCCESS** (0x00) ha ottenuto correttamente i dati IPv6</span><span class="sxs-lookup"><span data-stu-id="6e992-463">**NX_SUCCESS** (0x00) Successfully obtained IPv6 data</span></span>
- <span data-ttu-id="6e992-464">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-464">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-465">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-465">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-466">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-466">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-467">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-467">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-468">Il parametro NX_DNS_PARAM_ERROR (0xA8) non è valido per il puntatore.</span><span class="sxs-lookup"><span data-stu-id="6e992-468">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-469">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-469">Allowed From</span></span>

<span data-ttu-id="6e992-470">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-470">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-471">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-471">Example</span></span>
```C
#define      MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
NXD_ADDRESS    *ipv6_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host. */
status =  nxd_dns_ipv6_address_by_name_get(&client_dns, 
                                           (UCHAR *)"www.my_example.com", 
                                           record__buffer,                  
                                           sizeof(record_buffer), 
                                           &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
        else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed the IPv6 
    address(es) is (are) returned in record_buffer. */
      
    printf("------------------------------------------------------\n");
    printf("Test AAAA: ");
    printf("record_count = %d \n", record_count);      

    /* Get the IPv6 addresses of host. */
    for(i =0; i< record_count; i++)
    {

        ipv6_address_ptr[i] = 
            (NX_DNS_IPV6_ADDRESS *)(record_buffer + i * sizeof(NX_DNS_IPV6_ADDRESS)); 
             
        printf("record %d: IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", i, 
                ipv6_address_ptr[i] -> ipv6_address[0]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[0]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[1]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[1]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[2]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[2]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[3]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[3]  & 0xFFFF);
            }
}


[Output]
------------------------------------------------------
Test AAAA: record_count = 1 
record 0: IP address: 2001:0db8:0000:f101: 0000: 0000: 0000:01003
```

## <a name="nx_dns_host_by_address_get"></a><span data-ttu-id="6e992-472">nx_dns_host_by_address_get</span><span class="sxs-lookup"><span data-stu-id="6e992-472">nx_dns_host_by_address_get</span></span>

<span data-ttu-id="6e992-473">Cerca un nome host da un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="6e992-473">Look up a host name from an IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-474">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-474">Prototype</span></span>
```C
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-475">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-475">Description</span></span>

<span data-ttu-id="6e992-476">Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS precedentemente specificati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e992-476">This service requests name resolution of the supplied IP address from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="6e992-477">In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*.</span><span class="sxs-lookup"><span data-stu-id="6e992-477">If successful, the NULL-terminated host name is returned in the string specified by *host_name_ptr*.</span></span> <span data-ttu-id="6e992-478">Si tratta di una funzione wrapper per il servizio *nxd_dns_host_by_address_get* e non accetta indirizzi IPv6.</span><span class="sxs-lookup"><span data-stu-id="6e992-478">This is a wrapper function for *nxd_dns_host_by_address_get* service and does not accept IPv6 addresses.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-479">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-479">Input Parameters</span></span>

- <span data-ttu-id="6e992-480">**dns_ptr** Puntatore a un'istanza DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-480">**dns_ptr** Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="6e992-481">**ip_address** Indirizzo IP da risolvere in un nome</span><span class="sxs-lookup"><span data-stu-id="6e992-481">**ip_address** IP address to resolve into a name</span></span>
- <span data-ttu-id="6e992-482">**host_name_ptr** Puntatore all'area di destinazione per il nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-482">**host_name_ptr** Pointer to destination area for host name</span></span>
- <span data-ttu-id="6e992-483">**max_host_name_size** Dimensioni dell'area di destinazione per il nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-483">**max_host_name_size** Size of destination area for host name</span></span>
- <span data-ttu-id="6e992-484">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa nei cicli del timer per una risposta del server DNS dopo ogni tentativo di query e query DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-484">**wait_option** Defines how long the service will wait in timer ticks for a DNS server response after each DNS query and query retry.</span></span> <span data-ttu-id="6e992-485">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6e992-485">The wait options are defined as follows:</span></span>

  <span data-ttu-id="6e992-486">valore di timeout (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6e992-486">timeout value (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>

  <span data-ttu-id="6e992-487">Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6e992-487">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

  <span data-ttu-id="6e992-488">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-488">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-489">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-489">Return Values</span></span>

- <span data-ttu-id="6e992-490">**NX_SUCCESS** (0x00) risoluzione DNS riuscita</span><span class="sxs-lookup"><span data-stu-id="6e992-490">**NX_SUCCESS** (0x00) Successful DNS resolution</span></span>  
- <span data-ttu-id="6e992-491">Timeout di **NX_DNS_TIMEOUT** (0xA2) durante il recupero del mutex DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-491">**NX_DNS_TIMEOUT** (0xA2) Timed out on obtaining DNS mutex</span></span>
- <span data-ttu-id="6e992-492">**NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-492">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="6e992-493">**NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query</span><span class="sxs-lookup"><span data-stu-id="6e992-493">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="6e992-494">Indirizzo di input null **NX_DNS_BAD_ADDRESS_ERROR** (0xa4)</span><span class="sxs-lookup"><span data-stu-id="6e992-494">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null input address</span></span>
- <span data-ttu-id="6e992-495">L'indice **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)</span><span class="sxs-lookup"><span data-stu-id="6e992-495">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="6e992-496">**NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-496">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="6e992-497">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-497">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-498">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-498">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="6e992-499">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-499">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-500">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-500">Allowed From</span></span>

<span data-ttu-id="6e992-501">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-501">Threads</span></span>

<span data-ttu-id="6e992-502">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="6e992-502">**Example**</span></span>
```C
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */
```

## <a name="nxd_dns_host_by_address_get"></a><span data-ttu-id="6e992-503">nxd_dns_host_by_address_get</span><span class="sxs-lookup"><span data-stu-id="6e992-503">nxd_dns_host_by_address_get</span></span>

<span data-ttu-id="6e992-504">Cercare un nome host dall'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="6e992-504">Look up a host name from the IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-505">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-505">Prototype</span></span>
```C
UINT nxd_dns_host_by_address_get(NX_DNS *dns_ptr, 
                                 NXD_ADDRESS ip_address, 
                                 ULONG *host_name_ptr, 
                                 ULONG max_host_name_size, 
                                 ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-506">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-506">Description</span></span>

<span data-ttu-id="6e992-507">Questo servizio richiede la risoluzione dei nomi dell'indirizzo IPv6 o IPv4 nell'argomento *ip_address* input da uno o più server DNS precedentemente specificati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e992-507">This service requests name resolution of the IPv6 or IPv4 address in the *ip_address* input argument from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="6e992-508">In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*.</span><span class="sxs-lookup"><span data-stu-id="6e992-508">If successful, the NULL-terminated host name is returned in the string specified by *host_name_ptr*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-509">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-509">Input Parameters</span></span>

- <span data-ttu-id="6e992-510">**dns_ptr** Puntatore a un'istanza DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-510">**dns_ptr** Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="6e992-511">**ip_address** Indirizzo IP da risolvere in un nome</span><span class="sxs-lookup"><span data-stu-id="6e992-511">**ip_address** IP address to resolve into a name</span></span>
- <span data-ttu-id="6e992-512">**host_name_ptr** Puntatore all'area di destinazione per il nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-512">**host_name_ptr** Pointer to destination area for host name</span></span>
- <span data-ttu-id="6e992-513">**max_host_name_size** Dimensioni dell'area di destinazione per il nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-513">**max_host_name_size** Size of destination area for host name</span></span>
- <span data-ttu-id="6e992-514">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa nei cicli del timer per una risposta del server DNS dopo ogni tentativo di query e query DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-514">**wait_option** Defines how long the service will wait in timer ticks for a DNS server response after each DNS query and query retry.</span></span> <span data-ttu-id="6e992-515">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6e992-515">The wait options are defined as follows:</span></span>

  <span data-ttu-id="6e992-516">valore di timeout (0x00000001 tramite 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6e992-516">timeout value (0x00000001 through 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>  

  <span data-ttu-id="6e992-517">Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6e992-517">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

  <span data-ttu-id="6e992-518">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-518">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-519">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-519">Return Values</span></span>

- <span data-ttu-id="6e992-520">**NX_SUCCESS** (0x00) risoluzione DNS riuscita</span><span class="sxs-lookup"><span data-stu-id="6e992-520">**NX_SUCCESS** (0x00) Successful DNS resolution</span></span>  
- <span data-ttu-id="6e992-521">Timeout di **NX_DNS_TIMEOUT** (0xA2) durante il recupero del mutex DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-521">**NX_DNS_TIMEOUT** (0xA2) Timed out on obtaining DNS mutex</span></span>
- <span data-ttu-id="6e992-522">**NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-522">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="6e992-523">**NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query</span><span class="sxs-lookup"><span data-stu-id="6e992-523">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="6e992-524">Indirizzo di input null **NX_DNS_BAD_ADDRESS_ERROR** (0xa4)</span><span class="sxs-lookup"><span data-stu-id="6e992-524">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null input address</span></span>
- <span data-ttu-id="6e992-525">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-525">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-526">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-526">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="6e992-527">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-527">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-528">NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-528">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-529">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-529">Allowed From</span></span>

<span data-ttu-id="6e992-530">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-530">Threads</span></span>

<span data-ttu-id="6e992-531">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="6e992-531">**Example**</span></span>
```C
UCHAR   resolved_name[200];
NXD_ADDRESS host_address;

host_address.nxd_ip_version = NX_IP_VERISON_V6;
host_address.nxd_ip_address.v6[0] = 0x20010db8;
host_address.nxd_ip_address.v6[1] = 0x0;
host_address.nxd_ip_address.v6[2] = 0xf101;
host_address.nxd_ip-address.v6[3] = 0x108;

/* Get the name associated with theinput host_address. */
status =  nxd_dns_host_by_address_get(&my_dns, &host_address,
                                      resolved_name, sizeof(resolved_name), 4000);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
     error_counter++;
}     
else     
{
     printf("------------------------------------------------------\n");
     printf("Test PTR: %s\n", record_buffer);
}

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable. */


[Output]

 ------------------------------------------------------
 Test PTR: my_example.net
```

## <a name="nx_dns_host_by_name_get"></a><span data-ttu-id="6e992-532">nx_dns_host_by_name_get</span><span class="sxs-lookup"><span data-stu-id="6e992-532">nx_dns_host_by_name_get</span></span>

<span data-ttu-id="6e992-533">Cercare un indirizzo IP dal nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-533">Look up an IP address from the host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-534">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-534">Prototype</span></span>
```C
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-535">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-535">Description</span></span>

<span data-ttu-id="6e992-536">Questo servizio richiede la risoluzione dei nomi del nome fornito da uno o più server DNS precedentemente specificati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e992-536">This service requests name resolution of the supplied name from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="6e992-537">In caso di esito positivo, l'indirizzo IP associato viene restituito nella destinazione a cui punta host_address_ptr.</span><span class="sxs-lookup"><span data-stu-id="6e992-537">If successful, the associated IP address is returned in the destination pointed to by host_address_ptr.</span></span> <span data-ttu-id="6e992-538">Si tratta di una funzione wrapper per il servizio *nxd_dns_host_by_name_get* ed è limitata all'input dell'indirizzo IPv4.</span><span class="sxs-lookup"><span data-stu-id="6e992-538">This is a wrapper function for the *nxd_dns_host_by_name_get* service, and is limited to IPv4 address input.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-539">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-539">Input Parameters</span></span>

- <span data-ttu-id="6e992-540">**dns_ptr** Puntatore a un'istanza DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-540">**dns_ptr** Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="6e992-541">**HOST_NAME** Puntatore al nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-541">**host_name** Pointer to host name</span></span>
- <span data-ttu-id="6e992-542">**host_address_ptr** Indirizzo IP del server DNS restituito</span><span class="sxs-lookup"><span data-stu-id="6e992-542">**host_address_ptr** DNS Server IP address returned</span></span>
- <span data-ttu-id="6e992-543">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-543">**wait_option** Defines how long the service will wait for the DNS resolution.</span></span> <span data-ttu-id="6e992-544">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6e992-544">The wait options are defined as follows:</span></span>

  <span data-ttu-id="6e992-545">valore di timeout (0x00000001 tramite 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6e992-545">timeout value (0x00000001 through 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>

  <span data-ttu-id="6e992-546">Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6e992-546">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

  <span data-ttu-id="6e992-547">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-547">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-548">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-548">Return Values</span></span>

- <span data-ttu-id="6e992-549">**NX_SUCCESS** (0x00) la risoluzione DNS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="6e992-549">**NX_SUCCESS** (0x00) Successful DNS resolution.</span></span>
- <span data-ttu-id="6e992-550">**NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-550">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="6e992-551">**NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query</span><span class="sxs-lookup"><span data-stu-id="6e992-551">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="6e992-552">NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-552">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="6e992-553">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-553">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="6e992-554">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-554">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-555">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-555">Allowed From</span></span>

<span data-ttu-id="6e992-556">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-556">Threads</span></span>

<span data-ttu-id="6e992-557">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="6e992-557">**Example**</span></span>
```C
ULONG host_address;

/* Get the IP address for the name “www.my_example.com”. */
   status =  nx_dns_host_by_name_get(&my_dns, “www.my_example.com”, &host_address, 4000);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{

    /* If status is NX_SUCCESS the IP address for “www.my_example.com” can be found 
        in the “ip_address” variable. */
        
    printf("------------------------------------------------------\n");
    printf("Test A: \n");
    printf("IP address: %d.%d.%d.%d\n",
    host_address >> 24,
    host_address >> 16 & 0xFF,                   
    host_address >> 8 & 0xFF,
    host_address & 0xFF);
}

[Output]
 ------------------------------------------------------
Test A: 
IP address: 192.2.2.10
```

## <a name="nxd_dns_host_by_name_get"></a><span data-ttu-id="6e992-558">nxd_dns_host_by_name_get</span><span class="sxs-lookup"><span data-stu-id="6e992-558">nxd_dns_host_by_name_get</span></span>

<span data-ttu-id="6e992-559">Ricerca di un indirizzo IP dal nome host</span><span class="sxs-lookup"><span data-stu-id="6e992-559">Lookup an IP address from the host name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-560">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-560">Prototype</span></span>
```C
UINT nxd_dns_host_by_name_get(NX_DNS *dns_ptr, ULONG *host_name, 
                              NXD_ADDRESS *host_address_ptr, 
                              ULONG wait_option, UINT lookup_type);
```

### <a name="description"></a><span data-ttu-id="6e992-561">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-561">Description</span></span>

<span data-ttu-id="6e992-562">Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS precedentemente specificati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e992-562">This service requests name resolution of the supplied IP address from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="6e992-563">In caso di esito positivo, l'indirizzo IP associato viene restituito in un NXD_ADDRESS a cui punta *host_address_ptr*.</span><span class="sxs-lookup"><span data-stu-id="6e992-563">If successful, the associated IP address is returned in an NXD_ADDRESS pointed to by *host_address_ptr*.</span></span> <span data-ttu-id="6e992-564">Se il chiamante imposta in modo specifico l'input lookup_type per NX_IP_VERSION_V6, il servizio invierà una query per un indirizzo IPv6 host (record AAAA).</span><span class="sxs-lookup"><span data-stu-id="6e992-564">If the caller specifically sets the lookup_type input to NX_IP_VERSION_V6, this service will send out query for a host IPv6 address (AAAA record).</span></span> <span data-ttu-id="6e992-565">Se il chiamante imposta in modo specifico l'input lookup_type per NX_IP_VERSION_V4, il servizio invierà una query per un indirizzo IPv4 host (record A).</span><span class="sxs-lookup"><span data-stu-id="6e992-565">If the caller specifically sets the lookup_type input to NX_IP_VERSION_V4, this service will send out query for a host IPv4 address (A record).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-566">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-566">Input Parameters</span></span>

- <span data-ttu-id="6e992-567">**dns_ptr** Puntatore a un'istanza del client DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-567">**dns_ptr** Pointer to previously created DNS Client instance.</span></span>
- <span data-ttu-id="6e992-568">**HOST_NAME** Puntatore al nome host per trovare un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="6e992-568">**host_name** Pointer to host name to find an IP address of</span></span>
- <span data-ttu-id="6e992-569">**host_address_ptr** Puntatore alla destinazione per NXD_ADDRESS contenente l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="6e992-569">**host_address_ptr** Pointer to destination for NXD_ADDRESS containing the IP address</span></span>
- <span data-ttu-id="6e992-570">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa nei cicli del timer per la risposta del server DNS per ogni trasmissione e ritrasmissione della query.</span><span class="sxs-lookup"><span data-stu-id="6e992-570">**wait_option** Defines how long the service will wait in timer ticks for the DNS Server response for each query transmission and retransmission.</span></span> <span data-ttu-id="6e992-571">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6e992-571">The wait options are defined as follows:</span></span>

  <span data-ttu-id="6e992-572">valore di timeout (0x00000001 tramite 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6e992-572">timeout value (0x00000001 through 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>  

  <span data-ttu-id="6e992-573">Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6e992-573">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS Server responds to the request.</span></span>

  <span data-ttu-id="6e992-574">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-574">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

- <span data-ttu-id="6e992-575">**lookup_type** Indica il tipo di ricerca (A vs AAAA).</span><span class="sxs-lookup"><span data-stu-id="6e992-575">**lookup_type** Indicate type of lookup (A vs AAAA).</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-576">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-576">Return Values</span></span>

- <span data-ttu-id="6e992-577">**NX_SUCCESS** (0x00) la risoluzione DNS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="6e992-577">**NX_SUCCESS** (0x00) Successful DNS resolution.</span></span>
- <span data-ttu-id="6e992-578">**NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-578">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="6e992-579">**NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query</span><span class="sxs-lookup"><span data-stu-id="6e992-579">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="6e992-580">Indirizzo di input null **NX_DNS_BAD_ADDRESS_ERROR** (0xa4)</span><span class="sxs-lookup"><span data-stu-id="6e992-580">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null input address</span></span>
- <span data-ttu-id="6e992-581">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-581">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-582">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-582">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="6e992-583">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-583">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-584">NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-584">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-585">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-585">Allowed From</span></span>

<span data-ttu-id="6e992-586">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-586">Threads</span></span>

<span data-ttu-id="6e992-587">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="6e992-587">**Example**</span></span>
```C
NXD_ADDRESS host_ipduo_address;

/* Create an AAAA query to obtain the IPv6 address for the host “www.my_example.com”. */
status =  nxd_dns_host_by_name_get(&my_dns, “www.my_example.com”, 
                                   &host_ipduo_address, 4000, 
                                   NX_IP_VERSION_V6);

if (status != NX_SUCCESS)
{
        error_counter++;
}
else
{
/* If status is NX_SUCCESS the IP address for “www.my_example.com” can be 
   found in the “ip_address” variable. */

    printf("------------------------------------------------------\n");
    printf("Test AAAA: \n");

    printf("IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", 
           host_ipduo_address.nxd_ip_address.v6[0]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[0]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[1]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[1]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[2]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[2]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[3]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[3]  & 0xFFFF);
}

[Output]

------------------------------------------------------
Test AAAA: 
IP address: 2607:f8b0:4007:800:0:0:0:1008
```

<span data-ttu-id="6e992-588">Un altro esempio di utilizzo di questo servizio ora, questa volta usando gli indirizzi IPv4 e i tipi di record, è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6e992-588">Another example of using this time service, this time using IPv4 addresses and A record types, is shown below:</span></span>
```C
/* Create a query to obtain the IPv4 address for the host “www.my_example.com”. */
status =  nxd_dns_host_by_name_get(&my_dns, “www.my_example.com”, &ip_address, 4000, 
                                   NX_IP_VERSION_V4);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{   
/* If status is NX_SUCCESS the IP address for “www.my_example.com” can be 
   found in the “ip_address” variable. */
  
     printf("------------------------------------------------------\n");
     printf("Test A: \n");
     printf("IP address: %d.%d.%d.%d\n",
            host_ipduo_address.nxd_ip_address.v4 >> 24,
            host_ipduo_address.nxd_ip_address.v4 >> 16 & 0xFF,                   
            host_ipduo_address.nxd_ip_address.v4 >> 8 & 0xFF,
            host_ipduo_address.nxd_ip_address.v4 & 0xFF);
 }

[Output]

------------------------------------------------------
Test A: 
IP address: 192.2.2.10
```

## <a name="nx_dns_host_text_get"></a><span data-ttu-id="6e992-589">nx_dns_host_text_get</span><span class="sxs-lookup"><span data-stu-id="6e992-589">nx_dns_host_text_get</span></span>

<span data-ttu-id="6e992-590">Cerca la stringa di testo per il nome di dominio di input</span><span class="sxs-lookup"><span data-stu-id="6e992-590">Look up the text string for the input domain name</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-591">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-591">Prototype</span></span>
```C
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6e992-592">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-592">Description</span></span>

<span data-ttu-id="6e992-593">Questo servizio invia una query di tipo TXT con il nome di dominio e il buffer specificati per ottenere i dati stringa arbitrari.</span><span class="sxs-lookup"><span data-stu-id="6e992-593">This service sends a query of type TXT with the specified domain name and buffer to obtain the arbitrary string data.</span></span>

<span data-ttu-id="6e992-594">Il client DNS copia la stringa di testo nel record TXT nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="6e992-594">The DNS Client copies the text string in the TXT record in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-595">Non è necessario che la record_buffer sia allineata a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="6e992-595">The record_buffer does not need to be 4-byte aligned to receive the data.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-596">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-596">Input Parameters</span></span>

- <span data-ttu-id="6e992-597">**dns_ptr** Puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-597">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="6e992-598">**HOST_NAME** Puntatore al nome dell'host in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="6e992-598">**host_name** Pointer to name of host to search on</span></span>
- <span data-ttu-id="6e992-599">**record_buffer** Puntatore alla posizione in cui estrarre i dati TXT</span><span class="sxs-lookup"><span data-stu-id="6e992-599">**record_buffer** Pointer to location to extract TXT data into</span></span>
- <span data-ttu-id="6e992-600">**BUFFER_SIZE** Dimensioni del buffer per memorizzare i dati TXT</span><span class="sxs-lookup"><span data-stu-id="6e992-600">**buffer_size** Size of buffer to hold TXT data</span></span>
- <span data-ttu-id="6e992-601">**WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-601">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-602">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-602">Return Values</span></span>

- <span data-ttu-id="6e992-603">Stringa TXT ottenuta **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="6e992-603">**NX_SUCCESS** (0x00) Successfully TXT string obtained</span></span>
- <span data-ttu-id="6e992-604">L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-604">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="6e992-605">**NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="6e992-605">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="6e992-606">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-606">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="6e992-607">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-607">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-608">NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-608">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-609">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-609">Allowed From</span></span>

<span data-ttu-id="6e992-610">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-610">Threads</span></span>

######   
<span data-ttu-id="6e992-611">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-611">Example</span></span>
```C
CHAR            record_buffer[50];

/* Request the text string for the specified host. */
status =  nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", 
                               record_buffer, 
                               sizeof(record_buffer), 500);


/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
     error_counter++;
}
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and the
       text string is returned in record_buffer. */
 
     printf("------------------------------------------------------\n");
     printf("Test TXT:\n %s\n", record_buffer);
} 


[Output]

------------------------------------------------------
Test TXT: 
v=spf1 include:_www.my_example.com ip4:192.2.2.10/31 ip4:192.2.2.11/31 ~all
```

## <a name="nx_dns_packet_pool_set"></a><span data-ttu-id="6e992-612">nx_dns_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="6e992-612">nx_dns_packet_pool_set</span></span>

<span data-ttu-id="6e992-613">Impostare il pool di pacchetti client DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-613">Set the DNS Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-614">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-614">Prototype</span></span>
```C
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="6e992-615">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-615">Description</span></span>

<span data-ttu-id="6e992-616">Questo servizio imposta un pool di pacchetti creato in precedenza come pool di pacchetti client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-616">This service sets a previously created packet pool as the DNS Client packet pool.</span></span> <span data-ttu-id="6e992-617">Il client DNS userà questo pool di pacchetti per inviare query DNS, quindi il payload del pacchetto non deve essere inferiore a NX_DNS_PACKET_PAYLOAD che include le intestazioni Ethernet, IP e UDP ed è definito in *nxd_dns. h.*</span><span class="sxs-lookup"><span data-stu-id="6e992-617">The DNS Client will use this packet pool to send DNS queries, so the packet payload should not be less than NX_DNS_PACKET_PAYLOAD which includes the Ethernet, IP and UDP headers and is defined in *nxd_dns.h.*</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-618">*W* Hen il client DNS viene eliminato, il pool di pacchetti non viene eliminato con esso ed è responsabilità dell'applicazione eliminare il pool di pacchetti quando non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="6e992-618">*W* hen the DNS Client is deleted, the packet pool is not deleted with it and it is the responsibility of the application to delete the packet pool when it no longer needs it.</span></span>
>
> <span data-ttu-id="6e992-619">Questo servizio è disponibile solo se l'opzione di configurazione NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definita in *nxd_dns. h*</span><span class="sxs-lookup"><span data-stu-id="6e992-619">This service is only available if the configuration option NX_DNS_CLIENT_USER_CREATE_PACKET_POOL is defined in *nxd_dns.h*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-620">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-620">Input Parameters</span></span>

- <span data-ttu-id="6e992-621">**dns_ptr** Puntatore a un'istanza del client DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6e992-621">**dns_ptr** Pointer to previously created DNS Client instance.</span></span>
- <span data-ttu-id="6e992-622">**pool_ptr** Puntatore al pool di pacchetti creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="6e992-622">**pool_ptr** Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-623">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-623">Return Values</span></span>

- <span data-ttu-id="6e992-624">**NX_SUCCESS** (0x00) completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6e992-624">**NX_SUCCESS** (0x00) Successful completion.</span></span>
- <span data-ttu-id="6e992-625">Client di **NX_NOT_ENABLED** (0x14) non configurato per questa opzione</span><span class="sxs-lookup"><span data-stu-id="6e992-625">**NX_NOT_ENABLED** (0x14) Client not configured for this option</span></span>
- <span data-ttu-id="6e992-626">NX_PTR_ERROR (0x07) un puntatore client IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-626">NX_PTR_ERROR (0x07) Invalid IP or DNS Client pointer.</span></span>
- <span data-ttu-id="6e992-627">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="6e992-627">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-628">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-628">Allowed From</span></span>

<span data-ttu-id="6e992-629">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-629">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-630">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-630">Example</span></span>
```C
NXD_DNS my_dns;
NX_PACKET_POOL client_pool;
NX_IP *ip_ptr;


/* Create the DNS Client. */
status =  nx_dns_create(&my_dns, ip_ptr, “My DNS Client”);

/* Create a packet pool for the DNS Client. */
status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                NX_DNS_PACKET_PAYLOAD, free_mem_pointer, 
                                NX_DNS_PACKET_POOL_SIZE);

/* Set the DNS Client packet pool. */
status =  nx_dns_packet_pool_set(&my_dns, &client_pool);

/* If status is NX_SUCCESS the DNS Client packet pool was successfully set. */
```

## <a name="nx_dns_server_add"></a><span data-ttu-id="6e992-631">nx_dns_server_add</span><span class="sxs-lookup"><span data-stu-id="6e992-631">nx_dns_server_add</span></span>

<span data-ttu-id="6e992-632">Aggiungi indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-632">Add DNS Server IP Address</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-633">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-633">Prototype</span></span>
```C
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a><span data-ttu-id="6e992-634">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-634">Description</span></span>

<span data-ttu-id="6e992-635">Questo servizio aggiunge un server DNS IPv4 all'elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="6e992-635">This service adds an IPv4 DNS Server to the server list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-636">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-636">Input Parameters</span></span>

- <span data-ttu-id="6e992-637">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-637">**dns_ptr** Pointer to DNS control block.</span></span>  
- <span data-ttu-id="6e992-638">**server_address** Indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-638">**server_address** IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-639">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-639">Return Values</span></span>

- <span data-ttu-id="6e992-640">Aggiunta del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="6e992-640">**NX_SUCCESS** (0x00) Server successfully added</span></span>
- <span data-ttu-id="6e992-641">**NX_DNS_DUPLICATE_ENTRY**</span><span class="sxs-lookup"><span data-stu-id="6e992-641">**NX_DNS_DUPLICATE_ENTRY**</span></span>  
<span data-ttu-id="6e992-642">**NX_NO_MORE_ENTRIES** (0x17) non sono più consentiti server DNS (elenco completo)</span><span class="sxs-lookup"><span data-stu-id="6e992-642">**NX_NO_MORE_ENTRIES** (0x17) No more DNS Servers Allowed (list is full)</span></span>
- <span data-ttu-id="6e992-643">**NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-643">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="6e992-644">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-644">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-645">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-645">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="6e992-646">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-646">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-647">Input dell'indirizzo del server NX_DNS_BAD_ADDRESS_ERROR (0xA4) null</span><span class="sxs-lookup"><span data-stu-id="6e992-647">NX_DNS_BAD_ADDRESS_ERROR (0xA4) Null server address input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-648">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-648">Allowed From</span></span>

<span data-ttu-id="6e992-649">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-649">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-650">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-650">Example</span></span>
```C
/* Add a DNS Server at IP address 202.2.2.13. */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added. */
```

## <a name="nxd_dns_server_add"></a><span data-ttu-id="6e992-651">nxd_dns_server_add</span><span class="sxs-lookup"><span data-stu-id="6e992-651">nxd_dns_server_add</span></span>

<span data-ttu-id="6e992-652">Aggiungere un server DNS all'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-652">Add DNS Server to the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-653">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-653">Prototype</span></span>
```C
UINT nxd_dns_server_add(NX_DNS *dns_ptr, NXD_ADDRESS *server_address);
```
### <a name="description"></a><span data-ttu-id="6e992-654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-654">Description</span></span>

<span data-ttu-id="6e992-655">Questo servizio aggiunge l'indirizzo IP di un server DNS all'elenco dei server client DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-655">This service adds the IP address of a DNS server to the DNS Client server list.</span></span> <span data-ttu-id="6e992-656">È possibile che il server_address sia un indirizzo IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="6e992-656">The server_address may be either an IPv4 or IPv6 address.</span></span> <span data-ttu-id="6e992-657">Se il client desidera essere in grado di accedere allo stesso server tramite l'indirizzo IPv4 o IPv6, deve aggiungere entrambi gli indirizzi IP come voci all'elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="6e992-657">If the Client wishes to be able to access the same server by either its IPv4 address or IPv6 address it should add both IP addresses as entries to the server list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-658">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-658">Input Parameters</span></span>

- <span data-ttu-id="6e992-659">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-659">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="6e992-660">**server_address** Puntatore al NXD_ADDRESS contenente l'indirizzo IP del server DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-660">**server_address** Pointer to the NXD_ADDRESS containing the server IP address of DNS Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-661">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-661">Return Values</span></span>

- <span data-ttu-id="6e992-662">Aggiunta del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="6e992-662">**NX_SUCCESS** (0x00) Server successfully added</span></span>
- <span data-ttu-id="6e992-663">**NX_DNS_DUPLICATE_ENTRY**</span><span class="sxs-lookup"><span data-stu-id="6e992-663">**NX_DNS_DUPLICATE_ENTRY**</span></span>  
<span data-ttu-id="6e992-664">**NX_NO_MORE_ENTRIES** (0x17) non sono più consentiti server DNS (elenco completo)</span><span class="sxs-lookup"><span data-stu-id="6e992-664">**NX_NO_MORE_ENTRIES** (0x17) No more DNS Servers allowed (list is full)</span></span> 
- <span data-ttu-id="6e992-665">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-665">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-666">**NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-666">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="6e992-667">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-667">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="6e992-668">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-668">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-669">Input dell'indirizzo del server NX_DNS_BAD_ADDRESS_ERROR (0xA4) null</span><span class="sxs-lookup"><span data-stu-id="6e992-669">NX_DNS_BAD_ADDRESS_ERROR (0xA4) Null server address input</span></span>
- <span data-ttu-id="6e992-670">L'indice NX_DNS_INVALID_ADDRESS_TYPE (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)</span><span class="sxs-lookup"><span data-stu-id="6e992-670">NX_DNS_INVALID_ADDRESS_TYPE (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-671">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-671">Allowed From</span></span>

<span data-ttu-id="6e992-672">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-672">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-673">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-673">Example</span></span>
```C
NXD_ADDRESS server_address;

server_address.nxd_ip_version = NX_IP_VERISON_V6;
server_address.nxd_ip_address.v6[0] = 0x20010db8;
server_address.nxd_ip_address.v6[1] = 0x0;
server_address.nxd_ip_address.v6[2] = 0xf101;
server_address.nxd_ip-address.v6[3] = 0x108;


/* Add a DNS Server with the IP address pointed to by the server_address input. */
status =  nxd_dns_server_add(&my_dns, &server_address);

/* If status is NX_SUCCESS a DNS Server was successfully added. */
```

## <a name="nx_dns_server_get"></a><span data-ttu-id="6e992-674">nx_dns_server_get</span><span class="sxs-lookup"><span data-stu-id="6e992-674">nx_dns_server_get</span></span>

<span data-ttu-id="6e992-675">Restituire un server DNS IPv4 dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-675">Return an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-676">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-676">Prototype</span></span>
```C
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                        ULONG *dns_server_address);
```

### <a name="description"></a><span data-ttu-id="6e992-677">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-677">Description</span></span>

<span data-ttu-id="6e992-678">Questo servizio restituisce l'indirizzo del server DNS IPv4 dall'elenco dei server in corrispondenza dell'indice specificato.</span><span class="sxs-lookup"><span data-stu-id="6e992-678">This service returns the IPv4 DNS Server address from the server list at the specified index.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-679">L'indice è in base zero.</span><span class="sxs-lookup"><span data-stu-id="6e992-679">The index is zero based.</span></span> <span data-ttu-id="6e992-680">Se l'indice di input supera le dimensioni dell'elenco dei client DNS, viene trovato un indirizzo IPv6 in corrispondenza dell'indice o viene trovato un indirizzo null in corrispondenza dell'indice specificato. viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="6e992-680">If the input index exceeds the size of the DNS Client list, an IPv6 address is found at that index or a null address is found at the specified index, an error is returned.</span></span> <span data-ttu-id="6e992-681">È possibile chiamare il servizio *nx_dns_get_serverlist_size* prima di ottenere il numero di server DNS nell'elenco client.</span><span class="sxs-lookup"><span data-stu-id="6e992-681">The *nx_dns_get_serverlist_size* service may be called first obtain the number of DNS servers in the Client list.</span></span>

<span data-ttu-id="6e992-682">Questo servizio supporta solo indirizzi IPv4.</span><span class="sxs-lookup"><span data-stu-id="6e992-682">This service does only supports IPv4 addresses.</span></span> <span data-ttu-id="6e992-683">Chiama il servizio *nxd_dns_server_get* che supporta gli indirizzi sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="6e992-683">It calls the *nxd_dns_server_get* service which supports both IPv4 and IPv6 addresses.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-684">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-684">Input Parameters</span></span>

- <span data-ttu-id="6e992-685">**dns_ptr** Puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-685">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="6e992-686">**Indice** di Indicizzare nell'elenco dei server del client DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-686">**index** Index into DNS Client’s list of servers</span></span>
- <span data-ttu-id="6e992-687">**dns_server_address** Puntatore all'indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-687">**dns_server_address** Pointer to IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-688">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-688">Return Values</span></span>

- <span data-ttu-id="6e992-689">Il server **NX_SUCCESS** (0x00) ha restituito un esito positivo</span><span class="sxs-lookup"><span data-stu-id="6e992-689">**NX_SUCCESS** (0x00) Successful server returned</span></span>
- <span data-ttu-id="6e992-690">**NX_DNS_SERVER_NOT_FOUND** (0xA9) punta a uno slot vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-690">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Index points to empty slot</span></span>
- <span data-ttu-id="6e992-691">L'indice **NX_DNS_BAD_ADDRESS_ERROR** (0xa4) fa riferimento a un indirizzo null</span><span class="sxs-lookup"><span data-stu-id="6e992-691">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Index points to Null address</span></span>
- <span data-ttu-id="6e992-692">L'indice **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)</span><span class="sxs-lookup"><span data-stu-id="6e992-692">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="6e992-693">**NX_DNS_PARAM_ERROR** (0xA8) non è un input non puntatore valido</span><span class="sxs-lookup"><span data-stu-id="6e992-693">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="6e992-694">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-694">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="6e992-695">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-695">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-696">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-696">Allowed From</span></span>

<span data-ttu-id="6e992-697">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-697">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-698">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-698">Example</span></span>
```C
ULONG my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list. */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned. */
```

## <a name="nxd_dns_server_get"></a><span data-ttu-id="6e992-699">nxd_dns_server_get</span><span class="sxs-lookup"><span data-stu-id="6e992-699">nxd_dns_server_get</span></span>

<span data-ttu-id="6e992-700">Restituire un server DNS dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-700">Return a DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-701">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-701">Prototype</span></span>
```C
UINT nxd_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                        NXD_ADDRESS *dns_server_address);
```

### <a name="description"></a><span data-ttu-id="6e992-702">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-702">Description</span></span>

<span data-ttu-id="6e992-703">Questo servizio restituisce l'indirizzo IP del server DNS dall'elenco dei server in corrispondenza dell'indice specificato.</span><span class="sxs-lookup"><span data-stu-id="6e992-703">This service returns the DNS Server IP address from the server list at the specified index.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e992-704">L'indice è in base zero.</span><span class="sxs-lookup"><span data-stu-id="6e992-704">The index is zero based.</span></span> <span data-ttu-id="6e992-705">Se l'indice di input supera la dimensione dell'elenco dei client DNS oppure viene trovato un indirizzo null in corrispondenza dell'indice specificato, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="6e992-705">If the input index exceeds the size of the DNS Client list, or a null address is found at the specified index, an error is returned.</span></span> <span data-ttu-id="6e992-706">Il servizio *nx_dns_get_serverlist_size* può essere chiamato per primo per ottenere il numero di server DNS nell'elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="6e992-706">The *nx_dns_get_serverlist_size* service may be called first to obtain the number of DNS servers in the server list.</span></span>

<span data-ttu-id="6e992-707">Questo servizio supporta gli indirizzi IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="6e992-707">This service supports IPv4 and IPv6 addresses.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-708">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-708">Input Parameters</span></span>

- <span data-ttu-id="6e992-709">**dns_ptr** Puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-709">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="6e992-710">**Indice** di Indicizzare nell'elenco dei server del client DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-710">**index** Index into DNS Client’s list of servers</span></span>
- <span data-ttu-id="6e992-711">**dns_server_address** Puntatore all'indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="6e992-711">**dns_server_address** Pointer to IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-712">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-712">Return Values</span></span>

- <span data-ttu-id="6e992-713">**NX_SUCCESS** (0x00) ha restituito l'indirizzo IP del server</span><span class="sxs-lookup"><span data-stu-id="6e992-713">**NX_SUCCESS** (0x00) Successfully returned server IP address</span></span>
- <span data-ttu-id="6e992-714">**NX_DNS_SERVER_NOT_FOUND** (0xA9) punta a uno slot vuoto</span><span class="sxs-lookup"><span data-stu-id="6e992-714">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Index points to empty slot</span></span>
- <span data-ttu-id="6e992-715">L'indice **NX_DNS_BAD_ADDRESS_ERROR** (0xa4) punta all'indirizzo del server null</span><span class="sxs-lookup"><span data-stu-id="6e992-715">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Index points to null server address</span></span>
- <span data-ttu-id="6e992-716">L'indice **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)</span><span class="sxs-lookup"><span data-stu-id="6e992-716">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="6e992-717">**NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6e992-717">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="6e992-718">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-718">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="6e992-719">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-719">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-720">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-720">Allowed From</span></span>

<span data-ttu-id="6e992-721">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-721">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-722">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-722">Example</span></span>
```C
NXD_ADDRESS my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list. */
status =  nxd_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned. */
```

## <a name="nx_dns_server_remove"></a><span data-ttu-id="6e992-723">nx_dns_server_remove</span><span class="sxs-lookup"><span data-stu-id="6e992-723">nx_dns_server_remove</span></span>

<span data-ttu-id="6e992-724">Rimuovere un server DNS IPv4 dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-724">Remove an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-725">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-725">Prototype</span></span>
```C
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a><span data-ttu-id="6e992-726">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-726">Description</span></span>

<span data-ttu-id="6e992-727">Questo servizio rimuove un server DNS IPv4 dall'elenco client.</span><span class="sxs-lookup"><span data-stu-id="6e992-727">This service removes an IPv4 DNS Server from the Client list.</span></span> <span data-ttu-id="6e992-728">Si tratta di una funzione wrapper per *nxd_dns_server_remove*.</span><span class="sxs-lookup"><span data-stu-id="6e992-728">It is a wrapper function for *nxd_dns_server_remove*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-729">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-729">Input Parameters</span></span>

- <span data-ttu-id="6e992-730">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-730">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="6e992-731">**server_address** Indirizzo IP del server DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-731">**server_address** IP address of DNS Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-732">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-732">Return Values</span></span>

- <span data-ttu-id="6e992-733">Il server DNS **NX_SUCCESS** (0x00) è stato rimosso</span><span class="sxs-lookup"><span data-stu-id="6e992-733">**NX_SUCCESS** (0x00) DNS Server successfully removed</span></span>
- <span data-ttu-id="6e992-734">Server **NX_DNS_SERVER_NOT_FOUND** (0xA9) non presente nell'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-734">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Server not in Client list</span></span>
- <span data-ttu-id="6e992-735">Input dell'indirizzo del server **NX_DNS_BAD_ADDRESS_ERROR** (0XA4) null</span><span class="sxs-lookup"><span data-stu-id="6e992-735">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null server address input</span></span>
- <span data-ttu-id="6e992-736">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-736">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-737">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-737">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="6e992-738">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-738">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-739">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-739">Allowed From</span></span>

<span data-ttu-id="6e992-740">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-740">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-741">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-741">Example</span></span>
```C
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nxd_dns_server_remove"></a><span data-ttu-id="6e992-742">nxd_dns_server_remove</span><span class="sxs-lookup"><span data-stu-id="6e992-742">nxd_dns_server_remove</span></span>

<span data-ttu-id="6e992-743">Rimuovere un server DNS dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-743">Remove a DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-744">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-744">Prototype</span></span>
```C
UINT nxd_dns_server_remove(NX_DNS *dns_ptr, NXD_ADDRESS *server_address);
```
### <a name="description"></a><span data-ttu-id="6e992-745">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-745">Description</span></span>

<span data-ttu-id="6e992-746">Questo servizio rimuove dall'elenco client un server DNS dell'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="6e992-746">This service removes a DNS Server of the specified IP address from the Client list.</span></span> <span data-ttu-id="6e992-747">L'indirizzo IP di input accetta indirizzi IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="6e992-747">The input IP address accepts both IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="6e992-748">Dopo la rimozione del server, i server rimanenti spostano verso il basso di un indice nell'elenco per riempire lo slot sgomberato.</span><span class="sxs-lookup"><span data-stu-id="6e992-748">After the server is removed, the remaining servers move down one index in the list to fill the vacated slot.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-749">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-749">Input Parameters</span></span>

- <span data-ttu-id="6e992-750">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-750">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="6e992-751">**server_address** Puntatore al server DNS NXD_ADDRESS dati che contengono l'indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="6e992-751">**server_address** Pointer to DNS Server NXD_ADDRESS data containing server IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-752">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-752">Return Values</span></span>

- <span data-ttu-id="6e992-753">Il server DNS **NX_SUCCESS** (0x00) è stato rimosso</span><span class="sxs-lookup"><span data-stu-id="6e992-753">**NX_SUCCESS** (0x00) DNS Server successfully removed</span></span>
- <span data-ttu-id="6e992-754">Server **NX_DNS_SERVER_NOT_FOUND** (0xA9) non presente nell'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-754">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Server not in Client list</span></span>
- <span data-ttu-id="6e992-755">Input dell'indirizzo del server **NX_DNS_BAD_ADDRESS_ERROR** (0XA4) null</span><span class="sxs-lookup"><span data-stu-id="6e992-755">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null server address input</span></span>
- <span data-ttu-id="6e992-756">**NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato</span><span class="sxs-lookup"><span data-stu-id="6e992-756">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="6e992-757">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-757">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="6e992-758">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-758">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="6e992-759">L'indice NX_DNS_INVALID_ADDRESS_TYPE (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)</span><span class="sxs-lookup"><span data-stu-id="6e992-759">NX_DNS_INVALID_ADDRESS_TYPE (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-760">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-760">Allowed From</span></span>

<span data-ttu-id="6e992-761">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-761">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-762">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-762">Example</span></span>
```C
NXD_ADDRESS server_address;

server_address.nxd_ip_version = NX_IP_VERISON_V6;
server_address.nxd_ip_address.v6[0] = 0x20010db8;
server_address.nxd_ip_address.v6[1] = 0x0;
server_address.nxd_ip_address.v6[2] = 0xf101;
server_address.nxd_ip-address.v6[3] = 0x108;


/* Remove the DNS Server at the specified IP address from the Client list. */
status =  nxd_dns_server_remove(&my_dns,&server_ADDRESS);

/* If status is NX_SUCCESS a DNS Server was successfully removed. */
```

## <a name="nx_dns_server_remove_all"></a><span data-ttu-id="6e992-763">nx_dns_server_remove_all</span><span class="sxs-lookup"><span data-stu-id="6e992-763">nx_dns_server_remove_all</span></span>

<span data-ttu-id="6e992-764">Rimuovere tutti i server DNS dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="6e992-764">Remove all DNS Servers from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="6e992-765">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6e992-765">Prototype</span></span>
```C
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```
### <a name="description"></a><span data-ttu-id="6e992-766">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e992-766">Description</span></span>

<span data-ttu-id="6e992-767">Questo servizio rimuove tutti i server DNS dall'elenco client.</span><span class="sxs-lookup"><span data-stu-id="6e992-767">This service removes all DNS Servers from the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6e992-768">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6e992-768">Input Parameters</span></span>

- <span data-ttu-id="6e992-769">**dns_ptr** Puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="6e992-769">**dns_ptr** Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="6e992-770">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6e992-770">Return Values</span></span>

- <span data-ttu-id="6e992-771">Server DNS **NX_SUCCESS** (0x00) rimossi correttamente</span><span class="sxs-lookup"><span data-stu-id="6e992-771">**NX_SUCCESS** (0x00) DNS Servers successfully removed</span></span>
- <span data-ttu-id="6e992-772">**NX_DNS_ERROR** (messaggi 0XA0) non è in grado di ottenere il mutex di protezione</span><span class="sxs-lookup"><span data-stu-id="6e992-772">**NX_DNS_ERROR** (0xA0) Unable to obtain protection mutex</span></span>
- <span data-ttu-id="6e992-773">NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="6e992-773">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="6e992-774">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6e992-774">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6e992-775">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6e992-775">Allowed From</span></span>

<span data-ttu-id="6e992-776">Thread</span><span class="sxs-lookup"><span data-stu-id="6e992-776">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6e992-777">Esempio</span><span class="sxs-lookup"><span data-stu-id="6e992-777">Example</span></span>
```C
/* Remove all DNS Servers from the Client list. */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed. */
```