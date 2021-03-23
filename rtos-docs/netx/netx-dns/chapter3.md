---
title: Capitolo 3-Descrizione dei servizi client DNS di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi DNS di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 18e059e79f9742eaaafffbf15b55b4b5063363f8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822655"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dns-client-services"></a><span data-ttu-id="a8c3e-103">Capitolo 3-Descrizione dei servizi client DNS di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="a8c3e-103">Chapter 3 - Description of Azure RTOS NetX DNS Client Services</span></span>

<span data-ttu-id="a8c3e-104">Questo capitolo contiene una descrizione di tutti i servizi DNS di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-104">This chapter contains a description of all Azure RTOS NetX DNS services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="a8c3e-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="a8c3e-106">**nx_dns_authority_zone_start_get**: *ricercare l'inizio di una zona di autorità associata al nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-106">**nx_dns_authority_zone_start_get**: *Look up the start of a zone of authority associated with the specified host name*</span></span>
- <span data-ttu-id="a8c3e-107">**nx_dns_cache_initialize**: *inizializzare una cache DNS.*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-107">**nx_dns_cache_initialize**: *Initialize a DNS Cache.*</span></span>
- <span data-ttu-id="a8c3e-108">**nx_dns_cache_notify_clear**: *cancellare la funzione di notifica della cache completa.*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-108">**nx_dns_cache_notify_clear**: *Clear the cache full notify function.*</span></span>
- <span data-ttu-id="a8c3e-109">**nx_dns_cache_notify_set**: *impostare la funzione di notifica completa della cache.*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-109">**nx_dns_cache_notify_set**: *Set the cache full notify function.*</span></span>
- <span data-ttu-id="a8c3e-110">**nx_dns_cname_get**: *cercare il nome di dominio canonico per l'alias del nome di dominio di input*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-110">**nx_dns_cname_get**: *Look up the canonical domain name for the input domain name alias*</span></span>
- <span data-ttu-id="a8c3e-111">**nx_dns_create**: *creare un'istanza del client DNS*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-111">**nx_dns_create**: *Create a DNS Client instance*</span></span>
- <span data-ttu-id="a8c3e-112">**nx_dns_delete**: *eliminare un'istanza del client DNS*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-112">**nx_dns_delete**: *Delete a DNS Client instance*</span></span>
- <span data-ttu-id="a8c3e-113">**nx_dns_domain_name_server_get**: *cercare i server dei nomi autorevoli per la zona del dominio di input*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-113">**nx_dns_domain_name_server_get**: *Look up the authoritative name servers for the input domain zone*</span></span>
- <span data-ttu-id="a8c3e-114">**nx_dns_domain_mail_exchange_get**: *cercare l'host Exchange associato al nome host specificato.*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-114">**nx_dns_domain_mail_exchange_get**: *Look up the mail exchange associated the specified host name.*</span></span>
- <span data-ttu-id="a8c3e-115">**nx_dns_domain_service_get**: *cercare i servizi associati al nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-115">**nx_dns_domain_service_get**: *Look up the service(s) associated with the specified host name*</span></span>
- <span data-ttu-id="a8c3e-116">**nx_dns_get_serverlist_size**: *restituisce le dimensioni dell'elenco di server client DNS*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-116">**nx_dns_get_serverlist_size**: *Return the size of the DNS Client server list*</span></span>
- <span data-ttu-id="a8c3e-117">**nx_dns_info_by_name_get**: *restituire l'indirizzo IP, eseguire query sulla porta sul nome host di input*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-117">**nx_dns_info_by_name_get**: *Return IP address, port querying on input host name*</span></span>
- <span data-ttu-id="a8c3e-118">**nx_dns_ipv4_address_by_name_get**: *ricerca dell'indirizzo IPv4 dal nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-118">**nx_dns_ipv4_address_by_name_get**: *Look up the IPv4 address from the specified host name*</span></span>
- <span data-ttu-id="a8c3e-119">**nx_dns_host_by_address_get**: *cercare un nome host da un indirizzo IP specificato*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-119">**nx_dns_host_by_address_get**: *Look up a host name from a specified IP address*</span></span>
- <span data-ttu-id="a8c3e-120">**nx_dns_host_by_name_get**: *ricerca dell'indirizzo IPv4 dal nome host specificato*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-120">**nx_dns_host_by_name_get**: *Look up the IPv4 address from the specified host name*</span></span>
- <span data-ttu-id="a8c3e-121">**nx_dns_host_text_get**: *cercare i dati di testo per il nome di dominio di input*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-121">**nx_dns_host_text_get**: *Look up the text data for the input domain name*</span></span>
- <span data-ttu-id="a8c3e-122">**nx_dns_packet_pool_set**: *impostare il pool di pacchetti client DNS*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-122">**nx_dns_packet_pool_set**: *Set the DNS Client packet pool*</span></span>
- <span data-ttu-id="a8c3e-123">**nx_dns_server_add**: *aggiungere un server DNS all'indirizzo specificato all'elenco client*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-123">**nx_dns_server_add**: *Add a DNS Server at the specified address to the Client list*</span></span>
- <span data-ttu-id="a8c3e-124">**nx_dns_server_get**: *restituisce il server DNS nell'elenco client*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-124">**nx_dns_server_get**: *Return the DNS Server in the Client list*</span></span>
- <span data-ttu-id="a8c3e-125">**nx_dns_server_remove**: *rimuovere un server DNS dall'elenco client*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-125">**nx_dns_server_remove**: *Remove a DNS Server from the Client list*</span></span>
- <span data-ttu-id="a8c3e-126">**nx_dns_server_remove_all**: *rimuovere tutti i server DNS dall'elenco client*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-126">**nx_dns_server_remove_all**: *Remove all DNS Servers from the Client list*</span></span>

## <a name="nx_dns_authority_zone_start_get"></a><span data-ttu-id="a8c3e-127">nx_dns_authority_zone_start_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-127">nx_dns_authority_zone_start_get</span></span>

<span data-ttu-id="a8c3e-128">Cercare l'inizio della zona di autorità per l'host di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-128">Look up the start of the zone of authority for the input host</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-129">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-129">Prototype</span></span>

```c
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);

```

### <a name="description"></a><span data-ttu-id="a8c3e-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-130">Description</span></span>

<span data-ttu-id="a8c3e-131">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo SOA con il nome di dominio specificato per ottenere l'inizio della zona di autorità per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-131">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SOA with the specified domain name to obtain the start of the zone of authority for the input domain name.</span></span> <span data-ttu-id="a8c3e-132">Il client DNS copia i record SOA restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-132">The DNS Client copies the SOA record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 
>[!NOTE]
> <span data-ttu-id="a8c3e-133">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-133">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="a8c3e-134">Nel client DNS NetX, il tipo di record SOA, NX_DNS_SOA_ENTRY, viene salvato come parametri di 7 4 byte, totale di 28 byte:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-134">In NetX DNS Client, the SOA record type, NX_DNS_SOA_ENTRY, is saved as seven 4 byte parameters, totaling 28 bytes:</span></span>

- <span data-ttu-id="a8c3e-135">**nx_dns_soa_host_mname_ptr**: puntatore a origine dati primaria per questa zona</span><span class="sxs-lookup"><span data-stu-id="a8c3e-135">**nx_dns_soa_host_mname_ptr**: Pointer to primary source of data for this zone</span></span>
- <span data-ttu-id="a8c3e-136">**nx_dns_soa_host_rname_ptr**: puntatore alla cassetta postale responsabile di questa zona</span><span class="sxs-lookup"><span data-stu-id="a8c3e-136">**nx_dns_soa_host_rname_ptr**: Pointer to mailbox responsible for this zone</span></span>
- <span data-ttu-id="a8c3e-137">**nx_dns_soa_serial**: numero di versione zona</span><span class="sxs-lookup"><span data-stu-id="a8c3e-137">**nx_dns_soa_serial**: Zone version number</span></span>
- <span data-ttu-id="a8c3e-138">**nx_dns_soa_refresh**: intervallo di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a8c3e-138">**nx_dns_soa_refresh**: Refresh interval</span></span>
- <span data-ttu-id="a8c3e-139">**nx_dns_soa_retry**: intervallo tra i tentativi di query SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-139">**nx_dns_soa_retry**: Interval between SOA query retries</span></span>
- <span data-ttu-id="a8c3e-140">**nx_dns_soa_expire**: durata dell'ora di scadenza di SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-140">**nx_dns_soa_expire**: Time duration when SOA expires</span></span>
- <span data-ttu-id="a8c3e-141">**nx_dns_soa_minmum**: campo TTL minimo nei messaggi di risposta DNS del nome host SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-141">**nx_dns_soa_minmum**: Minimum TTL field in SOA hostname DNS reply messages</span></span>

<span data-ttu-id="a8c3e-142">L'archiviazione di due record SOA è illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-142">The storage of a two SOA records is shown below.</span></span> <span data-ttu-id="a8c3e-143">I record SOA contenenti dati a lunghezza fissa vengono immessi a partire dall'inizio del buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-143">The SOA records containing fixed length data are entered starting at the top of the buffer.</span></span> <span data-ttu-id="a8c3e-144">I puntatori MNAME e RNAME puntano ai dati a lunghezza variabile (nomi host) archiviati nella parte inferiore del buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-144">The pointers MNAME and RNAME point to the variable length data (host names) which are stored at the bottom of the buffer.</span></span> <span data-ttu-id="a8c3e-145">Vengono immessi record SOA aggiuntivi dopo il primo record ("record SOA aggiuntivi...") e i dati a lunghezza variabile vengono archiviati sopra i dati a lunghezza variabile dell'ultima voce ("dati di lunghezza variabile SOA aggiuntivi"):</span><span class="sxs-lookup"><span data-stu-id="a8c3e-145">Additional SOA records are entered after the first record (“additional SOA records…”) and their variable length data is stored above the last entry’s variable length data (“additional SOA variable length data”):</span></span>

![Diagramma che rappresenta l'archiviazione di un record a due O](media/image2.png)

<span data-ttu-id="a8c3e-147">Se l'input *record_buffer* non può contenere tutti i dati SOA nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-147">If the input *record_buffer* cannot hold all the SOA data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="a8c3e-148">Con il numero di record SOA restituiti in \**record_count,* l'applicazione può analizzare i dati da *record_buffer* ed estrarre l'inizio delle stringhe del nome host dell'autorità di zona.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-148">With the number of SOA records returned in \**record_count,* the application can parse the data from *record_buffer* and extract the start of zone authority host name strings.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-149">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-149">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-150">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-150">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-151">**HOST_NAME**: puntatore al nome host per cui ottenere i dati SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-151">**host_name**: Pointer to host name to obtain SOA data for</span></span>
- <span data-ttu-id="a8c3e-152">**record_buffer**: puntatore alla posizione in cui estrarre i dati SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-152">**record_buffer**: Pointer to location to extract SOA data into</span></span>
- <span data-ttu-id="a8c3e-153">**BUFFER_SIZE**: dimensioni del buffer per il mantenimento dei dati SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-153">**buffer_size**: Size of buffer to hold SOA data</span></span>
- <span data-ttu-id="a8c3e-154">**record_count**: puntatore al numero di record SOA recuperati</span><span class="sxs-lookup"><span data-stu-id="a8c3e-154">**record_count**: Pointer to the number of SOA records retrieved</span></span>
- <span data-ttu-id="a8c3e-155">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-155">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-156">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-156">Return Values</span></span>

- <span data-ttu-id="a8c3e-157">**NX_SUCCESS**: (0x00) ha ottenuto i dati SOA</span><span class="sxs-lookup"><span data-stu-id="a8c3e-157">**NX_SUCCESS**: (0x00) Successfully obtained SOA data</span></span>
- <span data-ttu-id="a8c3e-158">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-158">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-159">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-159">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-160">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-160">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-161">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-161">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="a8c3e-162">NX_DNS_PARAM_ERROR: (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-162">NX_DNS_PARAM_ERROR: (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-163">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-163">Allowed From</span></span>

<span data-ttu-id="a8c3e-164">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-164">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-165">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-165">Example</span></span>
```c
UCHAR                  record_buffer[50];
UINT                   record_count;   
NX_DNS_SOA_ENTRY       *nx_dns_soa_entry_ptr;

/* Request the start of authority zone(s) for the specified host.  */
status =  nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com",
                                          record _buffer, sizeof(record_buffer), 
                                          &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else 
{
/* If status is NX_SUCCESS a DNS query was successfully completed and SOA data is returned in soa_buffer.  */

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

```

```Output
Test SOA:
serial = 2012111212
refresh = 7200
retry = 1800
expire = 1209600
minmum = 300
host mname = ns1.www.my_example.com
host rname = dns-admin.www.my_example.com
```


## <a name="nx_dns_cache_initialize"></a><span data-ttu-id="a8c3e-166">nx_dns_cache_initialize</span><span class="sxs-lookup"><span data-stu-id="a8c3e-166">nx_dns_cache_initialize</span></span>

<span data-ttu-id="a8c3e-167">Inizializzare la cache DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-167">Initialize the DNS Cache</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-168">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-168">Prototype</span></span>

```c
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                             VOID *cache_ptr, UINT cache_size);

```
### <a name="description"></a><span data-ttu-id="a8c3e-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-169">Description</span></span>

<span data-ttu-id="a8c3e-170">Questo servizio crea e Inizializza una cache DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-170">This service creates and initializes a DNS Cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-171">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-171">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-172">**dns_ptr**: puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-172">**dns_ptr**: Pointer to DNS control block.</span></span>
- <span data-ttu-id="a8c3e-173">**cache_ptr**: puntatore alla cache DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-173">**cache_ptr**: Pointer to DNS Cache.</span></span>
- <span data-ttu-id="a8c3e-174">**cache_size**: dimensioni della cache DNS, in byte.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-174">**cache_size**: Size of DNS Cache, in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-175">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-175">Return Values</span></span>

- <span data-ttu-id="a8c3e-176">**NX_SUCCESS**: (0x00) cache DNS inizializzata correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-176">**NX_SUCCESS**: (0x00) DNS Cache successfully initialized</span></span>
- <span data-ttu-id="a8c3e-177">NX_DNS_ERROR: la cache (messaggi 0XA0) non è allineata a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-177">NX_DNS_ERROR: (0xA0) Cache is not 4-byte aligned.</span></span>
- <span data-ttu-id="a8c3e-178">NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-178">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="a8c3e-179">NX_PTR_ERROR: (0x07) puntatore DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-179">NX_PTR_ERROR: (0x07) Invalid DNS pointer.</span></span>
- <span data-ttu-id="a8c3e-180">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-180">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-181">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-181">Allowed From</span></span>

<span data-ttu-id="a8c3e-182">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-182">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-183">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-183">Example</span></span>
```c
UCHAR          dns_cache [2048]; 

/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, dns_cache, 2048);
/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a><span data-ttu-id="a8c3e-184">nx_dns_cache_notify_clear</span><span class="sxs-lookup"><span data-stu-id="a8c3e-184">nx_dns_cache_notify_clear</span></span>

<span data-ttu-id="a8c3e-185">Cancella la funzione di notifica completa della cache DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-185">Clear the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-186">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-186">Prototype</span></span>

```c
UINT     nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```
### <a name="description"></a><span data-ttu-id="a8c3e-187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-187">Description</span></span>

<span data-ttu-id="a8c3e-188">Questo servizio Cancella la funzione di notifica completa della cache.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-188">This service clears the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-189">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-189">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-190">**dns_ptr**: puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-190">**dns_ptr**: Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-191">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-191">Return Values</span></span>

- <span data-ttu-id="a8c3e-192">**NX_SUCCESS**: (0x00) la notifica della cache DNS è stata impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-192">**NX_SUCCESS**: (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="a8c3e-193">NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-193">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="a8c3e-194">NX_PTR_ERROR: (0x07) puntatore DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-194">NX_PTR_ERROR: (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-195">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-195">Allowed From</span></span>

<span data-ttu-id="a8c3e-196">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-197">Example</span></span>

```c
/* Clear the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a><span data-ttu-id="a8c3e-198">nx_dns_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8c3e-198">nx_dns_cache_notify_set</span></span>

<span data-ttu-id="a8c3e-199">Impostare la funzione di notifica completa della cache DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-199">Set the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-200">Prototype</span></span>

```c
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr, VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a><span data-ttu-id="a8c3e-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-201">Description</span></span>

<span data-ttu-id="a8c3e-202">Questo servizio imposta la funzione di notifica completa della cache.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-202">This service sets the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-203">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-203">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-204">**dns_ptr**: puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-204">**dns_ptr**: Pointer to DNS control block.</span></span>
- <span data-ttu-id="a8c3e-205">**cache_full_notify_cb**: funzione di callback da richiamare quando la cache diventa piena.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-205">**cache_full_notify_cb**: The callback function to be invoked when cache become full.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-206">Return Values</span></span>

- <span data-ttu-id="a8c3e-207">**NX_SUCCESS**: (0x00) la notifica della cache DNS è stata impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-207">**NX_SUCCESS**: (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="a8c3e-208">NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-208">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="a8c3e-209">NX_PTR_ERROR: (0x07) puntatore DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-209">NX_PTR_ERROR: (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-210">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-210">Allowed From</span></span>

<span data-ttu-id="a8c3e-211">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-211">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-212">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-212">Example</span></span>

```c
/* Set the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set.  */
 
```

## <a name="nx_dns_cname_get"></a><span data-ttu-id="a8c3e-213">nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-213">nx_dns_cname_get</span></span>

<span data-ttu-id="a8c3e-214">Cercare il nome canonico per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-214">Look up the canonical name for the input hostname</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-215">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-215">Prototype</span></span>
```c
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                      UCHAR *record_buffer, UINT buffer_size, 
                      ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-216">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-216">Description</span></span>

<span data-ttu-id="a8c3e-217">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES viene definito in *nx_dns. h*, questo servizio invia una query di tipo CNAME con il nome di dominio specificato per ottenere il nome di dominio canonico.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-217">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined in *nx_dns.h*, this service sends a query of type CNAME with the specified domain name to obtain the canonical domain name.</span></span> <span data-ttu-id="a8c3e-218">Il client DNS copia la stringa CNAME restituita nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-218">The DNS Client copies the CNAME string returned in the DNS Server response into the *record_buffer* memory location.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-219">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-219">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-220">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-220">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-221">**HOST_NAME**: puntatore al nome host per il quale ottenere i dati CNAME</span><span class="sxs-lookup"><span data-stu-id="a8c3e-221">**host_name**: Pointer to host name to obtain CNAME data for</span></span>
- <span data-ttu-id="a8c3e-222">**record_buffer**: puntatore alla posizione in cui estrarre i dati CNAME</span><span class="sxs-lookup"><span data-stu-id="a8c3e-222">**record_buffer**: Pointer to location to extract CNAME data into</span></span>
- <span data-ttu-id="a8c3e-223">**BUFFER_SIZE**: dimensioni del buffer per il mantenimento dei dati CNAME</span><span class="sxs-lookup"><span data-stu-id="a8c3e-223">**buffer_size**: Size of buffer to hold CNAME data</span></span>
- <span data-ttu-id="a8c3e-224">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-224">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-225">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-225">Return Values</span></span>

- <span data-ttu-id="a8c3e-226">**NX_SUCCESS**: (0x00) ha ottenuto i dati CNAME</span><span class="sxs-lookup"><span data-stu-id="a8c3e-226">**NX_SUCCESS**: (0x00) Successfully obtained CNAME data</span></span>
- <span data-ttu-id="a8c3e-227">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-227">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-228">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-228">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-229">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-229">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-230">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-230">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="a8c3e-231">NX_DNS_PARAM_ERROR: (0xA8) input non valido non puntatore</span><span class="sxs-lookup"><span data-stu-id="a8c3e-231">NX_DNS_PARAM_ERROR: (0xA8) Invalid non-pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-232">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-232">Allowed From</span></span>

<span data-ttu-id="a8c3e-233">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-233">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-234">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-234">Example</span></span>

```c
CHAR            record _buffer[50];

/* Request the canonical name for the specified host.  */
status =  nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                            record_buffer, sizeof(record_buffer), 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and the canonical host name is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test CNAME: %s\n", record_buffer);
} 
```

```Output
Test CNAME: **my_example**.com
```

## <a name="nx_dns_create"></a><span data-ttu-id="a8c3e-235">nx_dns_create</span><span class="sxs-lookup"><span data-stu-id="a8c3e-235">nx_dns_create</span></span>

<span data-ttu-id="a8c3e-236">Creare un'istanza del client DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-236">Create a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-237">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-237">Prototype</span></span>

```c
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```

### <a name="description"></a><span data-ttu-id="a8c3e-238">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-238">Description</span></span>

<span data-ttu-id="a8c3e-239">Questo servizio crea un'istanza del client DNS per l'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-239">This service creates a DNS Client instance for the previously created IP instance.</span></span>

>[!NOTE]
><span data-ttu-id="a8c3e-240">L'applicazione deve garantire che il payload dei pacchetti del pool di pacchetti utilizzato dal client DNS sia sufficientemente grande per il numero massimo di messaggi DNS a 512 byte, più le intestazioni UDP, IP e Ethernet.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-240">The application must ensure that the packet payload of the packet pool used by the DNS Client is large enough for the maximum 512 byte DNS message, plus UDP, IP and Ethernet headers.</span></span> <span data-ttu-id="a8c3e-241">Se il client DNS crea il proprio pool di pacchetti, viene definito da NX_DNS_PACKET_POOL_SIZE e NX_DNS_PACKET_PAYLOAD.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-241">If the DNS Client creates its own packet pool, this is defined by NX_DNS_PACKET_POOL_SIZE and NX_DNS_PACKET_PAYLOAD.</span></span> <span data-ttu-id="a8c3e-242">Se l'applicazione client DNS preferisce fornire un pool di pacchetti creato in precedenza, il payload per il client DNS IPv4 deve essere di 512 byte per il DNS massimo più 20 byte per l'intestazione IP, 8 byte per l'intestazione UDP e 14 byte per l'intestazione Ethernet.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-242">If the DNS Client application prefers to supply a previously created packet pool, the payload for IPv4 DNS Client should be 512 bytes for the maximum DNS plus 20 bytes for the IP header, 8 bytes for the UDP header and 14 bytes for the Ethernet header.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-243">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-243">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-244">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-244">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-245">**ip_ptr**: puntatore all'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-245">**ip_ptr**: Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="a8c3e-246">**Domain_name**: puntatore al nome di dominio per l'istanza DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-246">**domain_name**: Pointer to domain name for DNS instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-247">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-247">Return Values</span></span>

- <span data-ttu-id="a8c3e-248">**NX_SUCCESS**: (0x00) creazione DNS riuscita</span><span class="sxs-lookup"><span data-stu-id="a8c3e-248">**NX_SUCCESS**: (0x00) Successful DNS create</span></span>
- <span data-ttu-id="a8c3e-249">**NX_DNS_ERROR**: (messaggi 0XA0) errore di creazione DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-249">**NX_DNS_ERROR**: (0xA0) DNS create error</span></span>
- <span data-ttu-id="a8c3e-250">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-250">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-251">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-251">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-252">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-252">Allowed From</span></span>

<span data-ttu-id="a8c3e-253">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-253">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-254">Example</span></span>

```c
/* Create a DNS Client instance.  */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created.  */
```
## <a name="nx_dns_delete"></a><span data-ttu-id="a8c3e-255">nx_dns_delete</span><span class="sxs-lookup"><span data-stu-id="a8c3e-255">nx_dns_delete</span></span>

<span data-ttu-id="a8c3e-256">Eliminare un'istanza del client DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-256">Delete a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-257">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-257">Prototype</span></span>

```c
UINT     nx_dns_delete(NX_DNS *dns_ptr);
```

### <a name="description"></a><span data-ttu-id="a8c3e-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-258">Description</span></span>

<span data-ttu-id="a8c3e-259">Questo servizio Elimina un'istanza del client DNS creata in precedenza e libera le risorse.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-259">This service deletes a previously created DNS Client instance and frees up its resources.</span></span> 
>[!NOTE]
> <span data-ttu-id="a8c3e-260">Se **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** è definito e al client DNS è stato assegnato un pool di pacchetti definito dall'utente, spetta all'applicazione eliminare il pool di pacchetti client DNS se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-260">If **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** is defined and the DNS Client was assigned a user defined packet pool, it is up to the application to delete the DNS Client packet pool if it no longer needs it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-261">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-261">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-262">**dns_ptr**: puntatore all'istanza del **client** DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-262">**dns_ptr**: Pointer to previously created DNS **Client** instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-263">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-263">Return Values</span></span>

- <span data-ttu-id="a8c3e-264">**NX_SUCCESS**: (0x00) l'eliminazione del client DNS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-264">**NX_SUCCESS**: (0x00) Successful DNS Client delete.</span></span>
- <span data-ttu-id="a8c3e-265">NX_PTR_ERROR: (0x07) puntatore client IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-265">NX_PTR_ERROR: (0x07) Invalid IP or DNS Client pointer.</span></span>
- <span data-ttu-id="a8c3e-266">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-266">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-267">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-267">Allowed From</span></span>

<span data-ttu-id="a8c3e-268">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-268">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-269">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-269">Example</span></span>

```c
/* Delete a DNS Client instance.  */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted.  */
```
## <a name="nx_dns_domain_name_server_get"></a><span data-ttu-id="a8c3e-270">nx_dns_domain_name_server_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-270">nx_dns_domain_name_server_get</span></span>

<span data-ttu-id="a8c3e-271">Cercare i server dei nomi autorevoli per la zona del dominio di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-271">Look up the authoritative name servers for the input domain zone</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-272">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-272">Prototype</span></span>

```c
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-273">Description</span></span>

<span data-ttu-id="a8c3e-274">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo NS con il nome di dominio specificato per ottenere i server dei nomi per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-274">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type NS with the specified domain name to obtain the name servers for the input domain name.</span></span> <span data-ttu-id="a8c3e-275">Il client DNS copia i record NS restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-275">The DNS Client copies the NS record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="a8c3e-276">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-276">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="a8c3e-277">Nel client DNS di NetX il tipo di dati NS, NX_DNS_NS_ENTRY, viene salvato come parametri a 2 4 byte:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-277">In NetX DNS Client the NS data type, NX_DNS_NS_ENTRY, is saved as two 4-byte parameters:</span></span>

- <span data-ttu-id="a8c3e-278">**nx_dns_ns_ipv4_address**: indirizzo IPv4 del server dei nomi</span><span class="sxs-lookup"><span data-stu-id="a8c3e-278">**nx_dns_ns_ipv4_address**: Name server’s IPv4 address</span></span>
- <span data-ttu-id="a8c3e-279">**nx_dns_ns_hostname_ptr**: puntatore al nome host del server dei nomi</span><span class="sxs-lookup"><span data-stu-id="a8c3e-279">**nx_dns_ns_hostname_ptr**: Pointer to the name server’s hostname</span></span>

<span data-ttu-id="a8c3e-280">Il buffer riportato di seguito contiene quattro record NX_DNS_NS_ENTRY.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-280">The buffer shown below contains four NX_DNS_NS_ENTRY records.</span></span> <span data-ttu-id="a8c3e-281">Il puntatore alla stringa del nome host in ogni voce punta alla stringa del nome host corrispondente nella metà inferiore del buffer:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-281">The pointer to host name string in each entry points to the corresponding host name string in the bottom half of the buffer:</span></span>

![Diagramma del buffer che contiene quattro N record di immissione n s n s.](media/image3.png)

<span data-ttu-id="a8c3e-283">Se il *record_buffer* di input non può contenere tutti i dati NS nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-283">If the input *record_buffer* cannot hold all the NS data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="a8c3e-284">Con il numero di record NS restituiti in \**record_count,* l'applicazione può analizzare l'indirizzo IP e il nome host di ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-284">With the number of NS records returned in \**record_count,* the application can parse the IP address and host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-285">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-285">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-286">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-286">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-287">**HOST_NAME**: puntatore al nome host per cui ottenere i dati NS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-287">**host_name**: Pointer to host name to obtain NS data for</span></span>
- <span data-ttu-id="a8c3e-288">**record_buffer**: puntatore alla posizione in cui estrarre i dati NS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-288">**record_buffer**: Pointer to location to extract NS data into</span></span>
- <span data-ttu-id="a8c3e-289">**BUFFER_SIZE**: dimensioni del buffer per il mantenimento dei dati NS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-289">**buffer_size**: Size of buffer to hold NS data</span></span>
- <span data-ttu-id="a8c3e-290">**record_count**: puntatore al numero di record NS recuperati</span><span class="sxs-lookup"><span data-stu-id="a8c3e-290">**record_count**: Pointer to the number of NS records retrieved</span></span>
- <span data-ttu-id="a8c3e-291">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-291">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-292">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-292">Return Values</span></span>

- <span data-ttu-id="a8c3e-293">**NX_SUCCESS**: (0x00) ha ottenuto i dati NS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-293">**NX_SUCCESS**: (0x00) Successfully obtained NS data</span></span>
- <span data-ttu-id="a8c3e-294">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-294">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-295">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-295">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-296">NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-296">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="a8c3e-297">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-297">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-298">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-298">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-299">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-299">Allowed From</span></span>

<span data-ttu-id="a8c3e-300">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-300">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-301">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-301">Example</span></span>
```c
#define RECORD_COUNT        10

ULONG                      record_buffer[50];
UINT                       record_count;          
NX_DNS_NS_ENTRY            *nx_dns_ns_entry_ptr[RECORD_COUNT];

/* Request the name server(s) for the specified host.  */
status =  nx_dns_domain_name_server_get(&client_dns, (UCHAR *)" www.my_example.com ",  
                                        record_buffer, sizeof(record_buffer),  
                                        &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and NS data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test NS: ");
    printf("record_count = %d \n", record_count);      

    /* Get the name server.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)(record_buffer + i * sizeof(NX_DNS_NS_ENTRY)); 

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
```

```Output
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

## <a name="nx_dns_domain_mail_exchange_get"></a><span data-ttu-id="a8c3e-302">nx_dns_domain_mail_exchange_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-302">nx_dns_domain_mail_exchange_get</span></span>

<span data-ttu-id="a8c3e-303">Cerca lo scambio di posta/i per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-303">Look up the mail exchange(s) for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-304">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-304">Prototype</span></span>
```c
UINT     nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                        VOID *record_buffer,                                        
                                        UINT buffer_size, 
                                        UINT *record_count, 
                                        ULONG wait_option);

```

### <a name="description"></a><span data-ttu-id="a8c3e-305">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-305">Description</span></span>

<span data-ttu-id="a8c3e-306">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo MX con il nome di dominio specificato per ottenere lo scambio di posta elettronica per il nome di dominio di input.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-306">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type MX with the specified domain name to obtain the mail exchange for the input domain name.</span></span> <span data-ttu-id="a8c3e-307">Il client DNS copia i record MX restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-307">The DNS Client copies the MX record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

>[!NOTE]
><span data-ttu-id="a8c3e-308">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-308">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="a8c3e-309">Nel client DNS NetX, il tipo di record di scambio di posta elettronica, NX_DNS_MAIL_EXCHANGE_ENTRY, viene salvato come quattro parametri, per un totale di 12 byte:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-309">In NetX DNS Client, the mail exchange record type, NX_DNS_MAIL_EXCHANGE_ENTRY, is saved as four parameters, totaling 12 bytes:</span></span>

- <span data-ttu-id="a8c3e-310">**nx_dns_mx_ipv4_address**: indirizzo IPv4 di Exchange per posta elettronica 4 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-310">**nx_dns_mx_ipv4_address**: Mail exchange IPv4 address 4 bytes</span></span>
- <span data-ttu-id="a8c3e-311">**nx_dns_mx_preference**: preferenza 2 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-311">**nx_dns_mx_preference**: Preference 2 bytes</span></span>
- <span data-ttu-id="a8c3e-312">**nx_dns_mx_reserved0**: riservato 2 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-312">**nx_dns_mx_reserved0**: Reserved 2 bytes</span></span>
- <span data-ttu-id="a8c3e-313">**nx_dns_mx_hostname_ptr**: puntatore al nome host del server di posta elettronica di Exchange Server 4 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-313">**nx_dns_mx_hostname_ptr**: Pointer to mail exchange server host name 4 bytes</span></span>

<span data-ttu-id="a8c3e-314">Di seguito è riportato un buffer contenente quattro record MX.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-314">A buffer containing four MX records is shown below.</span></span> <span data-ttu-id="a8c3e-315">Ogni record contiene i dati a lunghezza fissa dall'elenco precedente.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-315">Each record contains the fixed length data from the list above.</span></span> <span data-ttu-id="a8c3e-316">Il puntatore al nome host di Exchange Server di posta elettronica punta al nome host corrispondente nella parte inferiore del buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-316">The pointer to the mail exchange server host name points to the corresponding host name at the bottom of the buffer.</span></span>

![Diagramma che mostra il buffer contenente quattro record M X.](media/image4.png)

<span data-ttu-id="a8c3e-318">Se l'input *record_buffer* non può contenere tutti i dati MX nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-318">If the input *record_buffer* cannot hold all the MX data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="a8c3e-319">Con il numero di record MX restituiti in \**record_count,* l'applicazione può analizzare i parametri MX, incluso il nome host della posta elettronica di ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-319">With the number of MX records returned in \**record_count,* the application can parse the MX parameters, including the mail host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-320">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-320">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-321">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-321">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-322">**HOST_NAME**: puntatore al nome host per cui ottenere i dati MX</span><span class="sxs-lookup"><span data-stu-id="a8c3e-322">**host_name**: Pointer to host name to obtain MX data for</span></span>
- <span data-ttu-id="a8c3e-323">**record_buffer**: puntatore alla posizione in cui estrarre i dati MX</span><span class="sxs-lookup"><span data-stu-id="a8c3e-323">**record_buffer**: Pointer to location to extract MX data into</span></span>
- <span data-ttu-id="a8c3e-324">**BUFFER_SIZE**: dimensioni del buffer per il mantenimento dei dati MX</span><span class="sxs-lookup"><span data-stu-id="a8c3e-324">**buffer_size**: Size of buffer to hold MX data</span></span>
- <span data-ttu-id="a8c3e-325">**record_count**: puntatore al numero di record MX recuperati</span><span class="sxs-lookup"><span data-stu-id="a8c3e-325">**record_count**: Pointer to the number of MX records retrieved</span></span>
- <span data-ttu-id="a8c3e-326">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-326">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-327">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-327">Return Values</span></span>

- <span data-ttu-id="a8c3e-328">**NX_SUCCESS**: (0x00) ha ottenuto i dati MX</span><span class="sxs-lookup"><span data-stu-id="a8c3e-328">**NX_SUCCESS**: (0x00) Successfully obtained MX data</span></span>
- <span data-ttu-id="a8c3e-329">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-329">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-330">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-330">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-331">NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-331">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="a8c3e-332">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-332">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-333">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-333">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-334">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-334">Allowed From</span></span>

<span data-ttu-id="a8c3e-335">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-335">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-336">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-336">Example</span></span>
```c
#define           MAX_RECORD_COUNT 10

ULONG             record_buffer[50];
UINT              record_count;  
NX_DNS_MX_ENTRY  *nx_dns_mx_entry_ptr[MAX_RECORD_COUNT];        

/* Request the mail exchange data for the specified host.  */
status =  nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)" www.my_example.com ", 
                                          record_buffer, sizeof(record_buffer),   
                                          &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
       
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and MX data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test MX: ");
    printf("record_count = %d \n", record_count);      


    /* Get the mail exchange.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)(record_buffer + i * sizeof(NX_DNS_MX_ENTRY));   

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,                   
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);

        printf("preference = %d \n ", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);

        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
    }
}
```

```Output
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


## <a name="nx_dns_domain_service_get"></a><span data-ttu-id="a8c3e-337">nx_dns_domain_service_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-337">nx_dns_domain_service_get</span></span>

<span data-ttu-id="a8c3e-338">Cerca i servizi forniti dal nome host di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-338">Look up the service(s) provided by the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-339">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-339">Prototype</span></span>

```c
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-340">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-340">Description</span></span>

<span data-ttu-id="a8c3e-341">Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo SRV con il nome di dominio specificato per cercare i servizi e il relativo numero di porta associato al dominio specificato.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-341">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SRV with the specified domain name to look up the service(s) and their port number associated with the specified domain.</span></span> <span data-ttu-id="a8c3e-342">Il client DNS copia i record SRV restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-342">The DNS Client copies the SRV record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="a8c3e-343">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-343">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="a8c3e-344">Nel client DNS NetX, il tipo di record del servizio, NX_DNS_SRV_ voce, viene salvato come sei parametri, per un totale di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-344">In NetX DNS Client, the service record type, NX_DNS_SRV_ ENTRY, is saved as six parameters, totaling 16 bytes.</span></span> <span data-ttu-id="a8c3e-345">Ciò consente di archiviare i dati SRV a lunghezza variabile in modo efficiente in termini di memoria:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-345">This enables variable length SRV data to be stored in a memory efficient manner:</span></span>

- <span data-ttu-id="a8c3e-346">**Indirizzo IPv4 del server**: nx_dns_srv_ipv4_address 4 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-346">**Server IPv4 address**: nx_dns_srv_ipv4_address 4 bytes</span></span>
- <span data-ttu-id="a8c3e-347">**Priorità server**: nx_dns_srv_priority 2 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-347">**Server priority**: nx_dns_srv_priority 2 bytes</span></span>
- <span data-ttu-id="a8c3e-348">**Peso server**: nx_dns_srv_weight 2 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-348">**Server weight**: nx_dns_srv_weight 2 bytes</span></span>
- <span data-ttu-id="a8c3e-349">**Numero di porta del servizio**: nx_dns_srv_port_number 2 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-349">**Service port number**: nx_dns_srv_port_number 2 bytes</span></span>
- <span data-ttu-id="a8c3e-350">**Riservato per l'allineamento a 4 byte**: nx_dns_srv_reserved0 2 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-350">**Reserved for 4-byte alignment**: nx_dns_srv_reserved0 2 bytes</span></span>
- <span data-ttu-id="a8c3e-351">**Puntatore al nome host del server**: \* nx_dns_srv_hostname_ptr 4 byte</span><span class="sxs-lookup"><span data-stu-id="a8c3e-351">**Pointer to server host name**: \*nx_dns_srv_hostname_ptr 4 bytes</span></span>

<span data-ttu-id="a8c3e-352">Nel buffer fornito sono archiviati quattro record SRV.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-352">Four SRV records are stored in the supplied buffer.</span></span> <span data-ttu-id="a8c3e-353">Ogni record di NX_DNS_SRV_ENTRY contiene un puntatore, *nx_dns_srv_hostname_ptr*, che punta alla stringa del nome host corrispondente nella parte inferiore del buffer di record:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-353">Each NX_DNS_SRV_ENTRY record contains a pointer, *nx_dns_srv_hostname_ptr*, that points to the corresponding host name string in the bottom of the record buffer:</span></span>

![Diagramma di quattro record S R V archiviati nel buffer fornito.](media/image5.png)

<span data-ttu-id="a8c3e-355">Se l'input *record_buffer* non è in grado di contenere tutti i dati SRV nella risposta del server, il *record_buffer* include tutti i record che si adattano e restituisce il numero di record nel buffer.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-355">If the input *record_buffer* cannot hold all the SRV data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="a8c3e-356">Con il numero di record SRV restituiti in \**record_count,* l'applicazione può analizzare i parametri SRV, incluso il nome host del server di ogni record nel *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-356">With the number of SRV records returned in \**record_count,* the application can parse the SRV parameters, including the server host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-357">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-357">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-358">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-358">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-359">**HOST_NAME**: puntatore al nome host per il quale ottenere i dati SRV</span><span class="sxs-lookup"><span data-stu-id="a8c3e-359">**host_name**: Pointer to host name to obtain SRV data for</span></span>
- <span data-ttu-id="a8c3e-360">**record_buffer**: puntatore alla posizione in cui estrarre i dati SRV</span><span class="sxs-lookup"><span data-stu-id="a8c3e-360">**record_buffer**: Pointer to location to extract SRV data into</span></span>
- <span data-ttu-id="a8c3e-361">**BUFFER_SIZE**: dimensioni del buffer per il mantenimento dei dati SRV</span><span class="sxs-lookup"><span data-stu-id="a8c3e-361">**buffer_size**: Size of buffer to hold SRV data</span></span>
- <span data-ttu-id="a8c3e-362">**record_count**: puntatore al numero di record SRV recuperati</span><span class="sxs-lookup"><span data-stu-id="a8c3e-362">**record_count**: Pointer to the number of SRV records retrieved</span></span>
- <span data-ttu-id="a8c3e-363">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-363">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-364">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-364">Return Values</span></span>

- <span data-ttu-id="a8c3e-365">**NX_SUCCESS**: (0x00) ha ottenuto i dati SRV</span><span class="sxs-lookup"><span data-stu-id="a8c3e-365">**NX_SUCCESS**: (0x00) Successfully obtained SRV data</span></span>
- <span data-ttu-id="a8c3e-366">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-366">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-367">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-367">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-368">NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-368">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="a8c3e-369">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-369">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-370">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-370">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-371">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-371">Allowed From</span></span>

<span data-ttu-id="a8c3e-372">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-372">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-373">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-373">Example</span></span>

```c
#define MAX_RECORD_COUNT  10

UCHAR                  record_buffer[50];
UINT                   record_count;
NX_DNS_SRV_ENTRY       *nx_dns_srv_entry_ptr[MAX_RECORD_COUNT];

/* Request the service(s) provided by the specified host.  */
status =  nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                    record_buffer, sizeof(record_buffer), 
                                    &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SRV data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test SRV: ");
    printf("record_count = %d \n", record_count);      

       
    /* Get the location of services.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)(record_buffer + i * sizeof(NX_DNS_SRV_ENTRY)); 

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
```

```Output
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

## <a name="nx_dns_get_serverlist_size"></a><span data-ttu-id="a8c3e-374">nx_dns_get_serverlist_size</span><span class="sxs-lookup"><span data-stu-id="a8c3e-374">nx_dns_get_serverlist_size</span></span>

<span data-ttu-id="a8c3e-375">Restituisce le dimensioni dell'elenco di server del client DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-375">Return the size of the DNS Client’s Server list</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-376">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-376">Prototype</span></span>

```c
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```

### <a name="description"></a><span data-ttu-id="a8c3e-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-377">Description</span></span>

<span data-ttu-id="a8c3e-378">Questo servizio restituisce il numero di server DNS validi nell'elenco client.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-378">This service returns the number of valid DNS Servers in the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-379">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-379">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-380">**dns_ptr**: puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-380">**dns_ptr**: Pointer to DNS control block</span></span>  
- <span data-ttu-id="a8c3e-381">**size**: restituisce il numero di server nell'elenco</span><span class="sxs-lookup"><span data-stu-id="a8c3e-381">**size**: Returns the number of servers in the list</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-382">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-382">Return Values</span></span>

- <span data-ttu-id="a8c3e-383">**NX_SUCCESS**: (0x00) dimensioni elenco server DNS restituite correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-383">**NX_SUCCESS**: (0x00) DNS Server list size successfully returned</span></span>
- <span data-ttu-id="a8c3e-384">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-384">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="a8c3e-385">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-385">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-386">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-386">Allowed From</span></span>

<span data-ttu-id="a8c3e-387">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-387">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-388">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-388">Example</span></span>

```c
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list.  */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned.  */
```

## <a name="nx_dns_info_by_name_get"></a><span data-ttu-id="a8c3e-389">nx_dns_info_by_name_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-389">nx_dns_info_by_name_get</span></span>

<span data-ttu-id="a8c3e-390">Restituire l'indirizzo IP e la porta del server DNS in base al nome host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-390">Return ip address and port of DNS server by host name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-391">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-391">Prototype</span></span>

```c
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-392">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-392">Description</span></span>

<span data-ttu-id="a8c3e-393">Questo servizio restituisce l'indirizzo IP e la porta del server (record di servizio) in base al nome host di input da parte della query DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-393">This service returns the Server IP and port (service record) based on the input host name by DNS query.</span></span> <span data-ttu-id="a8c3e-394">Se non viene trovato un record del servizio, questa routine restituisce un indirizzo IP zero nel puntatore dell'indirizzo di input e un ritorno di stato di errore diverso da zero per segnalare un errore.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-394">If a service record is not found, this routine returns a zero IP address in the input address pointer and a non-zero error status return to signal an error.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-395">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-395">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-396">**dns_ptr**: puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-396">**dns_ptr**: Pointer to DNS control block</span></span>  
- <span data-ttu-id="a8c3e-397">**HOST_NAME**: puntatore al buffer dei nomi host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-397">**host_name**: Pointer to host name buffer</span></span>
- <span data-ttu-id="a8c3e-398">**host_address_ptr**: puntatore all'indirizzo da restituire</span><span class="sxs-lookup"><span data-stu-id="a8c3e-398">**host_address_ptr**: Pointer to address to return</span></span>
- <span data-ttu-id="a8c3e-399">**host_port_ptr**: puntatore alla porta per restituire Wait_option opzione wait per la risposta DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-399">**host_port_ptr**: Pointer to port to return wait_option Wait option for the DNS response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-400">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-400">Return Values</span></span>

- <span data-ttu-id="a8c3e-401">**NX_SUCCESS**: (0x00) il record del server DNS è stato restituito</span><span class="sxs-lookup"><span data-stu-id="a8c3e-401">**NX_SUCCESS**: (0x00) DNS Server record successfully returned</span></span>
- <span data-ttu-id="a8c3e-402">**NX_DNS_NO_SERVER**: (0XA1) nessun server DNS registrato con il client per l'invio della query sul nome host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-402">**NX_DNS_NO_SERVER**: (0xA1) No DNS Server registered with Client to send query on hostname</span></span>
- <span data-ttu-id="a8c3e-403">**NX_DNS_QUERY_FAILED**: (0xA3) la query DNS non è riuscita. Nessuna risposta da alcun server DNS nell'elenco client o nessun record del servizio disponibile per il nome host di input.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-403">**NX_DNS_QUERY_FAILED**: (0xA3) DNS query failed; no response from any DNS servers in Client list or no service record is available for the input hostname.</span></span>
- <span data-ttu-id="a8c3e-404">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-404">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-405">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-405">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-406">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-406">Allowed From</span></span>

<span data-ttu-id="a8c3e-407">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-407">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-408">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-408">Example</span></span>
```c
ULONG         ip_address;
USHORT         port;

/* Attempt to resolve the IP address and ports for this host name.  */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned.  */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a><span data-ttu-id="a8c3e-409">nx_dns_ipv4_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-409">nx_dns_ipv4_address_by_name_get</span></span>

<span data-ttu-id="a8c3e-410">Cercare l'indirizzo IPv4 per il nome host di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-410">Look up the IPv4 address for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-411">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-411">Prototype</span></span>

```c
UINT nx_dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                       UCHAR *host_name_ptr, VOID *buffer, 
                                       UINT buffer_size, 
                                       UINT *record_count,
                                       ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-412">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-412">Description</span></span>

<span data-ttu-id="a8c3e-413">Questo servizio invia una query di tipo A con il nome host specificato per ottenere gli indirizzi IP per il nome host di input.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-413">This service sends a query of Type A with the specified host name to obtain the IP addresses for the input host name.</span></span> <span data-ttu-id="a8c3e-414">Il client DNS copia l'indirizzo IPv4 dai record A restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-414">The DNS Client copies the IPv4 address from the A record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="a8c3e-415">Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-415">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="a8c3e-416">Più indirizzi IPv4 vengono archiviati nel buffer allineato a 4 byte, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-416">Multiple IPv4 addresses are stored in the 4-byte aligned buffer as shown below:</span></span>

![Diagramma di più indirizzi I P v 4 archiviati nel buffer allineato a 4 byte.](media/image6.png)

<span data-ttu-id="a8c3e-418">Se il buffer fornito non è in grado di memorizzare tutti i dati degli indirizzi IP, i record A rimanenti non vengono archiviati in *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-418">If the supplied buffer cannot hold all the IP address data, the remaining A records are not stored in *record_buffer*.</span></span> <span data-ttu-id="a8c3e-419">Ciò consente all'applicazione di recuperare uno, alcuni o tutti i dati degli indirizzi IP disponibili nella risposta del server.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-419">This enables the application to retrieve one, some or all of the available IP address data in the server reply.</span></span>

<span data-ttu-id="a8c3e-420">Con il numero di record restituiti in \**record_count* l'applicazione può analizzare i dati dell'indirizzo IPv4 dall' *record_buffer*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-420">With the number of A records returned in \**record_count* the application can parse the IPv4 address data from the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-421">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-421">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-422">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-422">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-423">**host_name_ptr**: puntatore al nome host per ottenere il puntatore del buffer di indirizzi IPv4 al percorso in cui estrarre i dati IPv4</span><span class="sxs-lookup"><span data-stu-id="a8c3e-423">**host_name_ptr**: Pointer to host name to obtain IPv4 address buffer Pointer to location to extract IPv4 data into</span></span>
- <span data-ttu-id="a8c3e-424">**BUFFER_SIZE**: dimensioni del buffer per il mantenimento dei dati IPv4</span><span class="sxs-lookup"><span data-stu-id="a8c3e-424">**buffer_size**: Size of buffer to hold IPv4 data</span></span>
- <span data-ttu-id="a8c3e-425">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-425">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-426">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-426">Return Values</span></span>

- <span data-ttu-id="a8c3e-427">**NX_SUCCESS**: (0x00) ha ottenuto i dati IPv4</span><span class="sxs-lookup"><span data-stu-id="a8c3e-427">**NX_SUCCESS**: (0x00) Successfully obtained IPv4 data</span></span>
- <span data-ttu-id="a8c3e-428">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-428">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-429">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-429">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-430">NX_DNS_PARAM_ERROR: (0xA8) parametro di input non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-430">NX_DNS_PARAM_ERROR: (0xA8) Invalid input parameter.</span></span>
- <span data-ttu-id="a8c3e-431">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-431">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="a8c3e-432">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-432">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-433">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-433">Allowed From</span></span>

<span data-ttu-id="a8c3e-434">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-434">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-435">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-435">Example</span></span>

```c
#define MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
ULONG           *ipv4_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host.  */
status =  nx_dns_ipv4_address_by_name_get(&client_dns, 
                                          (UCHAR *)"www.my_example.com",  
                                           record_buffer,                  
                                           sizeof(record_buffer),&record_count,                
                                           500);

        /* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed the IPv4 address(es) is returned in record_buffer.  */
    printf("------------------------------------------------------\n");
    printf("Test A: ");
    printf("record_count = %d \n", record_count);      


    /* Get the IPv4 addresses of host.  */
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
```

```Output
------------------------------------------------------
Test A: record_count = 5 
record 0: IP address: 192.2.2.10
record 1: IP address: 192.2.2.11
record 2: IP address: 192.2.2.12
record 3: IP address: 192.2.2.13
record 4: IP address: 192.2.2.14
```

## <a name="nx_dns_host_by_address_get"></a><span data-ttu-id="a8c3e-436">nx_dns_host_by_address_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-436">nx_dns_host_by_address_get</span></span>

<span data-ttu-id="a8c3e-437">Cerca un nome host da un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="a8c3e-437">Look up a host name from an IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-438">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-438">Prototype</span></span>

```c
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-439">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-439">Description</span></span>

<span data-ttu-id="a8c3e-440">Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS precedentemente specificati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-440">This service requests name resolution of the supplied IP address from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="a8c3e-441">In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-441">If successful, the NULL-terminated host name is returned in the string specified by *host_name_ptr*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-442">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-442">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-443">**dns_ptr**: puntatore all'istanza DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-443">**dns_ptr**: Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="a8c3e-444">**ip_address**: indirizzo IP da risolvere in un nome</span><span class="sxs-lookup"><span data-stu-id="a8c3e-444">**ip_address**: IP address to resolve into a name</span></span>
- <span data-ttu-id="a8c3e-445">**host_name_ptr**: puntatore all'area di destinazione per il nome host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-445">**host_name_ptr**: Pointer to destination area for host name</span></span>
- <span data-ttu-id="a8c3e-446">**max_host_name_size**: dimensioni dell'area di destinazione per il nome host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-446">**max_host_name_size**: Size of destination area for host name</span></span>
- <span data-ttu-id="a8c3e-447">**WAIT_OPTION**: definisce il tempo di attesa del servizio nei cicli del timer per una risposta del server DNS dopo ogni query DNS e ripetizione delle query. le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-447">**wait_option**: Defines how long the service will wait in timer ticks for a DNS server response after each DNS query and query retry The wait options are defined as follows:</span></span>
    - <span data-ttu-id="a8c3e-448">**valore di timeout**: (0x00000001-0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-448">**timeout value**: (0x00000001-0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>
    - <span data-ttu-id="a8c3e-449">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server DNS non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-449">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-450">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-450">Return Values</span></span>

- <span data-ttu-id="a8c3e-451">**NX_SUCCESS**: (0x00) risoluzione DNS riuscita</span><span class="sxs-lookup"><span data-stu-id="a8c3e-451">**NX_SUCCESS**: (0x00) Successful DNS resolution</span></span>  
- <span data-ttu-id="a8c3e-452">**NX_DNS_TIMEOUT**: (0xA2) si è verificato un timeout durante il recupero del mutex DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-452">**NX_DNS_TIMEOUT**: (0xA2) Timed out on obtaining DNS mutex</span></span>
- <span data-ttu-id="a8c3e-453">**NX_DNS_NO_SERVER**: (0XA1) non è stato specificato alcun indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-453">**NX_DNS_NO_SERVER**: (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="a8c3e-454">**NX_DNS_QUERY_FAILED**: (0xA3) non ha ricevuto risposta alla query</span><span class="sxs-lookup"><span data-stu-id="a8c3e-454">**NX_DNS_QUERY_FAILED**: (0xA3) Received no response to query</span></span>
- <span data-ttu-id="a8c3e-455">**NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) indirizzo di input null</span><span class="sxs-lookup"><span data-stu-id="a8c3e-455">**NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Null input address</span></span>
- <span data-ttu-id="a8c3e-456">**NX_DNS_INVALID_ADDRESS_TYPE**: (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)</span><span class="sxs-lookup"><span data-stu-id="a8c3e-456">**NX_DNS_INVALID_ADDRESS_TYPE**: (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="a8c3e-457">**NX_DNS_PARAM_ERROR**: (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-457">**NX_DNS_PARAM_ERROR**: (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="a8c3e-458">NX_PTR_ERROR: (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-458">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="a8c3e-459">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-459">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-460">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-460">Allowed From</span></span>

<span data-ttu-id="a8c3e-461">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-461">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-462">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-462">Example</span></span>

```c
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */

```

## <a name="nx_dns_host_by_name_get"></a><span data-ttu-id="a8c3e-463">nx_dns_host_by_name_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-463">nx_dns_host_by_name_get</span></span>

<span data-ttu-id="a8c3e-464">Cercare un indirizzo IP dal nome host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-464">Look up an IP address from the host name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-465">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-465">Prototype</span></span>

```c
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-466">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-466">Description</span></span>

<span data-ttu-id="a8c3e-467">Questo servizio richiede la risoluzione dei nomi del nome fornito, a cui fa riferimento *HOST_NAME*, da uno o più server DNS precedentemente specificati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-467">This service requests name resolution of the supplied name, pointed to by *host_name*, from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="a8c3e-468">In caso di esito positivo, l'indirizzo IP associato viene restituito nella destinazione a cui punta *host_address_ptr*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-468">If successful, the associated IP address is returned in the destination pointed to by *host_address_ptr*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-469">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-469">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-470">**dns_ptr**: puntatore all'istanza DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-470">**dns_ptr**: Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="a8c3e-471">**HOST_NAME**: puntatore al nome host</span><span class="sxs-lookup"><span data-stu-id="a8c3e-471">**host_name**: Pointer to host name</span></span>
- <span data-ttu-id="a8c3e-472">**host_address_ptr**: puntatore all'indirizzo IP dell'host DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-472">**host_address_ptr**: Pointer to DNS host IP address</span></span>
- <span data-ttu-id="a8c3e-473">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-473">**wait_option**: Defines how long the service will wait for the DNS resolution.</span></span> <span data-ttu-id="a8c3e-474">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="a8c3e-474">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="a8c3e-475">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-475">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>
    - <span data-ttu-id="a8c3e-476">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server DNS non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-476">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-477">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-477">Return Values</span></span>

- <span data-ttu-id="a8c3e-478">**NX_SUCCESS**: (0x00) la risoluzione DNS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-478">**NX_SUCCESS**: (0x00) Successful DNS resolution.</span></span>
- <span data-ttu-id="a8c3e-479">**NX_DNS_NO_SERVER**: (0XA1) non è stato specificato alcun indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-479">**NX_DNS_NO_SERVER**: (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="a8c3e-480">**NX_DNS_QUERY_FAILED**: (0xA3) non ha ricevuto risposta alla query</span><span class="sxs-lookup"><span data-stu-id="a8c3e-480">**NX_DNS_QUERY_FAILED**: (0xA3) Received no response to query</span></span>
- <span data-ttu-id="a8c3e-481">NX_DNS_PARAM_ERROR: (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-481">NX_DNS_PARAM_ERROR: (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="a8c3e-482">NX_PTR_ERROR: (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-482">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="a8c3e-483">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-483">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-484">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-484">Allowed From</span></span>

<span data-ttu-id="a8c3e-485">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-485">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-486">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-486">Example</span></span>
```c
ULONG ip_address;

    /* Get the IP address for the name “www.my_example.com”.  */
    status =  nx_dns_host_by_name_get(&my_dns, “www.my_example.com”, &ip_address, 4000);

    /* Check for DNS query error.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else     
    {

    /* If status is NX_SUCCESS the IP address for “www.my_example.com” can be found in the “ip_address” variable.  */
        
        printf("------------------------------------------------------\n");
        printf("Test A: \n");
        printf("IP address: %d.%d.%d.%d\n",
                host_ip_address >> 24,
                host_ip_address >> 16 & 0xFF,                   
                host_ip_address >> 8 & 0xFF,
                host_ip_address & 0xFF);
    }
```

```Output
Test A: 
IP address: 192.2.2.10
```

## <a name="nx_dns_host_text_get"></a><span data-ttu-id="a8c3e-487">nx_dns_host_text_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-487">nx_dns_host_text_get</span></span>

<span data-ttu-id="a8c3e-488">Cerca la stringa di testo per il nome di dominio di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-488">Look up the text string for the input domain name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-489">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-489">Prototype</span></span>

```c
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a8c3e-490">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-490">Description</span></span>

<span data-ttu-id="a8c3e-491">Questo servizio invia una query di tipo TXT con il nome di dominio e il buffer specificati per ottenere i dati stringa arbitrari.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-491">This service sends a query of type TXT with the specified domain name and buffer to obtain the arbitrary string data.</span></span>

<span data-ttu-id="a8c3e-492">Il client DNS copia la stringa di testo nel record TXT nella risposta del server DNS nel percorso di memoria *record_buffer* .</span><span class="sxs-lookup"><span data-stu-id="a8c3e-492">The DNS Client copies the text string in the TXT record in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="a8c3e-493">Non è necessario che la *record_buffer* sia allineata a 4 byte per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-493">The *record_buffer* does not need to be 4-byte aligned to receive the data.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-494">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-494">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-495">**dns_ptr**: puntatore al client DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-495">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="a8c3e-496">**HOST_NAME**: puntatore al nome dell'host in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="a8c3e-496">**host_name**: Pointer to name of host to search on</span></span>
- <span data-ttu-id="a8c3e-497">**record_buffer**: puntatore alla posizione in cui estrarre i dati txt</span><span class="sxs-lookup"><span data-stu-id="a8c3e-497">**record_buffer**: Pointer to location to extract TXT data into</span></span>
- <span data-ttu-id="a8c3e-498">**BUFFER_SIZE**: dimensioni del buffer per memorizzare i dati txt</span><span class="sxs-lookup"><span data-stu-id="a8c3e-498">**buffer_size**: Size of buffer to hold TXT data</span></span>
- <span data-ttu-id="a8c3e-499">**WAIT_OPTION**: wait-opzione per ricevere la risposta del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-499">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-500">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-500">Return Values</span></span>

- <span data-ttu-id="a8c3e-501">**NX_SUCCESS**: (0x00) è stata ottenuta una stringa txt completata</span><span class="sxs-lookup"><span data-stu-id="a8c3e-501">**NX_SUCCESS**: (0x00) Successfully TXT string obtained</span></span>
- <span data-ttu-id="a8c3e-502">**NX_DNS_NO_SERVER**: l'elenco dei server client (0xA1) è vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-502">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="a8c3e-503">**NX_DNS_QUERY_FAILED**: (0XA3) non è stata ricevuta alcuna risposta DNS valida</span><span class="sxs-lookup"><span data-stu-id="a8c3e-503">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="a8c3e-504">NX_PTR_ERROR: (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-504">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="a8c3e-505">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-505">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="a8c3e-506">NX_DNS_PARAM_ERROR: (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-506">NX_DNS_PARAM_ERROR: (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-507">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-507">Allowed From</span></span>

<span data-ttu-id="a8c3e-508">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-508">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-509">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-509">Example</span></span>

```c
CHAR            record_buffer[50];

/* Request the text string for the specified host.  */
status =  nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                record_buffer, 
                                sizeof(record_buffer), 500);


/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
     error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and the text string is returned in record_buffer.  */
 
     printf("------------------------------------------------------\n");
     printf("Test TXT:\n %s\n", record_buffer);
} 
```

```Output
Test TXT: 
v=spf1 include:_www.my_example.com ip4:192.2.2.10/31 ip4:192.2.2.11/31 ~all
```

## <a name="nx_dns_packet_pool_set"></a><span data-ttu-id="a8c3e-510">nx_dns_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="a8c3e-510">nx_dns_packet_pool_set</span></span>

<span data-ttu-id="a8c3e-511">Impostare il pool di pacchetti client DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-511">Set the DNS Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-512">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-512">Prototype</span></span>

```c
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="a8c3e-513">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-513">Description</span></span>

<span data-ttu-id="a8c3e-514">Questo servizio imposta un pool di pacchetti creato in precedenza come pool di pacchetti **client** DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-514">This service sets a previously created packet pool as the DNS **Client** packet pool.</span></span> <span data-ttu-id="a8c3e-515">Il client DNS userà questo pool di pacchetti per inviare query DNS, quindi il payload del pacchetto non deve essere inferiore a NX_DNS_PACKET_PAYLOAD_UNALIGNED che include il frame Ethernet, le intestazioni IP e UDP ed è definito in *nx_dns. h*.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-515">The DNS Client will use this packet pool to send DNS queries, so the packet payload should not be less than NX_DNS_PACKET_PAYLOAD_UNALIGNED which includes the Ethernet frame, IP and UDP headers and is defined in *nx_dns.h*.</span></span>
 
>[!NOTE]
><span data-ttu-id="a8c3e-516">Quando il client DNS viene eliminato, il pool di pacchetti non viene eliminato con esso ed è responsabilità dell'applicazione eliminare il pool di pacchetti quando non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-516">When the DNS Client is deleted, the packet pool is not deleted with it and it is the responsibility of the application to delete the packet pool when it no longer needs it.</span></span>

>[!NOTE]
><span data-ttu-id="a8c3e-517">Questo servizio è disponibile solo se l'opzione di configurazione NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definita in *nx_dns. h*</span><span class="sxs-lookup"><span data-stu-id="a8c3e-517">This service is only available if the configuration option NX_DNS_CLIENT_USER_CREATE_PACKET_POOL is defined in *nx_dns.h*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-518">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-518">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-519">**dns_ptr**: puntatore all'istanza del **client** DNS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-519">**dns_ptr**: Pointer to previously created DNS **Client** instance.</span></span>
- <span data-ttu-id="a8c3e-520">**pool_ptr**: puntatore al pool di pacchetti creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="a8c3e-520">**pool_ptr**: Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-521">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-521">Return Values</span></span>

- <span data-ttu-id="a8c3e-522">**NX_SUCCESS**: (0x00) completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-522">**NX_SUCCESS**: (0x00) Successful completion.</span></span>
- <span data-ttu-id="a8c3e-523">**NX_NOT_ENABLED**: (0X14) client non configurato per questa opzione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-523">**NX_NOT_ENABLED**: (0x14) Client not configured for this option</span></span>
- <span data-ttu-id="a8c3e-524">NX_PTR_ERROR: (0x07) puntatore **client** IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-524">NX_PTR_ERROR: (0x07) Invalid IP or DNS **Client** pointer.</span></span>
- <span data-ttu-id="a8c3e-525">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-525">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-526">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-526">Allowed From</span></span>

<span data-ttu-id="a8c3e-527">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-527">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-528">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-528">Example</span></span>
```c
NX_DNS             my_dns;
NX_PACKET_POOL     client_pool;
NX_IP             *ip_ptr;


/* Create the DNS Client.  */
status =  nx_dns_create(&my_dns, ip_ptr, “My DNS Client”);

/* Create a packet pool for the DNS Client.  */
status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                 NX_DNS_PACKET_PAYLOAD, free_mem_pointer, 
                                 NX_DNS_PACKET_POOL_SIZE);

/* Set the DNS Client packet pool.  */
status =  nx_dns_packet_pool_set(&my_dns, &client_pool);

/* If status is NX_SUCCESS the DNS Client packet pool was successfully set.  */
```

## <a name="nx_dns_server_add"></a><span data-ttu-id="a8c3e-529">nx_dns_server_add</span><span class="sxs-lookup"><span data-stu-id="a8c3e-529">nx_dns_server_add</span></span>

<span data-ttu-id="a8c3e-530">Aggiungi indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-530">Add DNS Server IP Address</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-531">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-531">Prototype</span></span>

```c
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="a8c3e-532">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-532">Description</span></span>

<span data-ttu-id="a8c3e-533">Questo servizio aggiunge un server DNS IPv4 all'elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-533">This service adds an IPv4 DNS Server to the server list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-534">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-534">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-535">**dns_ptr**: puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-535">**dns_ptr**: Pointer to DNS control block.</span></span>  
- <span data-ttu-id="a8c3e-536">**server_address**: indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-536">**server_address**: IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-537">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-537">Return Values</span></span>

- <span data-ttu-id="a8c3e-538">**NX_SUCCESS**: (0x00) server aggiunto correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-538">**NX_SUCCESS**: (0x00) Server successfully added</span></span>
- <span data-ttu-id="a8c3e-539">**NX_DNS_DUPLICATE_ENTRY** o **NX_NO_MORE_ENTRIES**: (0x17) non sono più consentiti server DNS (elenco completo)</span><span class="sxs-lookup"><span data-stu-id="a8c3e-539">**NX_DNS_DUPLICATE_ENTRY** or **NX_NO_MORE_ENTRIES**: (0x17) No more DNS Servers Allowed (list is full)</span></span>
- <span data-ttu-id="a8c3e-540">**NX_DNS_PARAM_ERROR**: (0xA8) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-540">**NX_DNS_PARAM_ERROR**: (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="a8c3e-541">NX_PTR_ERROR: (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-541">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="a8c3e-542">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-542">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="a8c3e-543">NX_DNS_BAD_ADDRESS_ERROR: (0xA4) input dell'indirizzo del server null</span><span class="sxs-lookup"><span data-stu-id="a8c3e-543">NX_DNS_BAD_ADDRESS_ERROR: (0xA4) Null server address input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-544">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-544">Allowed From</span></span>

<span data-ttu-id="a8c3e-545">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-545">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-546">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-546">Example</span></span>

```c
/* Add a DNS Server at IP address 202.2.2.13.  */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added.  */
```

## <a name="nx_dns_server_get"></a><span data-ttu-id="a8c3e-547">nx_dns_server_get</span><span class="sxs-lookup"><span data-stu-id="a8c3e-547">nx_dns_server_get</span></span>

<span data-ttu-id="a8c3e-548">Restituire un server DNS IPv4 dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="a8c3e-548">Return an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-549">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-549">Prototype</span></span>

```c
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                       ULONG *dns_server_address);
```

### <a name="description"></a><span data-ttu-id="a8c3e-550">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-550">Description</span></span>

<span data-ttu-id="a8c3e-551">Questo servizio restituisce l'indirizzo del server DNS IPv4 dall'elenco dei server in corrispondenza dell'indice specificato.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-551">This service returns the IPv4 DNS Server address from the server list at the specified index.</span></span> <span data-ttu-id="a8c3e-552">Si noti che l'indice è in base zero.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-552">Note that the index is zero based.</span></span> <span data-ttu-id="a8c3e-553">Se l'indice di input supera le dimensioni dell'elenco client DNS, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-553">If the input index exceeds the size of the DNS Client list, an error is returned.</span></span> <span data-ttu-id="a8c3e-554">È possibile chiamare il servizio *nx_dns_get_serverlist_size* prima di ottenere il numero di server DNS nell'elenco client.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-554">The *nx_dns_get_serverlist_size* service may be called first obtain the number of DNS servers in the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-555">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-555">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-556">**dns_ptr**: puntatore al blocco di controllo DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-556">**dns_ptr**: Pointer to DNS control block</span></span>  
- <span data-ttu-id="a8c3e-557">**index**: indicizza nell'elenco dei server del client DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-557">**index**: Index into DNS Client’s list of servers</span></span>
- <span data-ttu-id="a8c3e-558">**dns_server_address**: puntatore all'indirizzo IP del server DNS</span><span class="sxs-lookup"><span data-stu-id="a8c3e-558">**dns_server_address**: Pointer to IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-559">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-559">Return Values</span></span>

- <span data-ttu-id="a8c3e-560">**NX_SUCCESS**: (0x00) il server restituito è riuscito</span><span class="sxs-lookup"><span data-stu-id="a8c3e-560">**NX_SUCCESS**: (0x00) Successful server returned</span></span>
- <span data-ttu-id="a8c3e-561">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) punta a uno slot vuoto</span><span class="sxs-lookup"><span data-stu-id="a8c3e-561">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) Index points to empty slot</span></span>
- <span data-ttu-id="a8c3e-562">**NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) l'indice punta a un indirizzo null</span><span class="sxs-lookup"><span data-stu-id="a8c3e-562">**NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Index points to Null address</span></span>
- <span data-ttu-id="a8c3e-563">**NX_DNS_PARAM_ERROR**: (0xA8) l'indice supera le dimensioni dell'elenco</span><span class="sxs-lookup"><span data-stu-id="a8c3e-563">**NX_DNS_PARAM_ERROR**: (0xA8) Index exceeds size of list</span></span>
- <span data-ttu-id="a8c3e-564">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-564">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="a8c3e-565">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-565">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-566">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-566">Allowed From</span></span>

<span data-ttu-id="a8c3e-567">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-568">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-568">Example</span></span>

```c
ULONG     my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list.  */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned.  */
```

## <a name="nx_dns_server_remove"></a><span data-ttu-id="a8c3e-569">nx_dns_server_remove</span><span class="sxs-lookup"><span data-stu-id="a8c3e-569">nx_dns_server_remove</span></span>

<span data-ttu-id="a8c3e-570">Rimuovere un server DNS IPv4 dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="a8c3e-570">Remove an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-571">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-571">Prototype</span></span>

```c
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="a8c3e-572">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-572">Description</span></span>

<span data-ttu-id="a8c3e-573">Questo servizio rimuove un server DNS IPv4 dall'elenco client.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-573">This service removes an IPv4 DNS Server from the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-574">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-574">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-575">**dns_ptr**: puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-575">**dns_ptr**: Pointer to DNS control block.</span></span>
- <span data-ttu-id="a8c3e-576">**server_address**: indirizzo IP del server DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-576">**server_address**: IP address of DNS Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-577">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-577">Return Values</span></span>

- <span data-ttu-id="a8c3e-578">**NX_SUCCESS**: (0x00) server DNS rimosso correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-578">**NX_SUCCESS**: (0x00) DNS Server successfully removed</span></span>
- <span data-ttu-id="a8c3e-579">**NX_DNS_SERVER_NOT_FOUND**: (0XA9) Server non presente nell'elenco client</span><span class="sxs-lookup"><span data-stu-id="a8c3e-579">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) Server not in Client list</span></span>
- <span data-ttu-id="a8c3e-580">**NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) input dell'indirizzo del server null</span><span class="sxs-lookup"><span data-stu-id="a8c3e-580">**NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Null server address input</span></span>
- <span data-ttu-id="a8c3e-581">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-581">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="a8c3e-582">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-582">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-583">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-583">Allowed From</span></span>

<span data-ttu-id="a8c3e-584">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-584">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-585">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-585">Example</span></span>

```c
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nx_dns_server_remove_all"></a><span data-ttu-id="a8c3e-586">nx_dns_server_remove_all</span><span class="sxs-lookup"><span data-stu-id="a8c3e-586">nx_dns_server_remove_all</span></span>

<span data-ttu-id="a8c3e-587">Rimuovere tutti i server DNS dall'elenco client</span><span class="sxs-lookup"><span data-stu-id="a8c3e-587">Remove all DNS Servers from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="a8c3e-588">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a8c3e-588">Prototype</span></span>

```c
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```

### <a name="description"></a><span data-ttu-id="a8c3e-589">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-589">Description</span></span>

<span data-ttu-id="a8c3e-590">Questo servizio rimuove tutti i server DNS dall'elenco client.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-590">This service removes all DNS Servers from the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8c3e-591">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a8c3e-591">Input Parameters</span></span>

- <span data-ttu-id="a8c3e-592">**dns_ptr**: puntatore al blocco di controllo DNS.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-592">**dns_ptr**: Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8c3e-593">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a8c3e-593">Return Values</span></span>

- <span data-ttu-id="a8c3e-594">**NX_SUCCESS**: (0x00) server DNS rimossi correttamente</span><span class="sxs-lookup"><span data-stu-id="a8c3e-594">**NX_SUCCESS**: (0x00) DNS Servers successfully removed</span></span>
- <span data-ttu-id="a8c3e-595">**NX_DNS_ERROR**: (messaggi 0XA0) non è possibile ottenere il mutex di protezione</span><span class="sxs-lookup"><span data-stu-id="a8c3e-595">**NX_DNS_ERROR**: (0xA0) Unable to obtain protection mutex</span></span>
- <span data-ttu-id="a8c3e-596">NX_PTR_ERROR: (0x07) puntatore IP o DNS non valido.</span><span class="sxs-lookup"><span data-stu-id="a8c3e-596">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="a8c3e-597">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="a8c3e-597">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8c3e-598">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a8c3e-598">Allowed From</span></span>

<span data-ttu-id="a8c3e-599">Thread</span><span class="sxs-lookup"><span data-stu-id="a8c3e-599">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8c3e-600">Esempio</span><span class="sxs-lookup"><span data-stu-id="a8c3e-600">Example</span></span>

```c

/* Remove all DNS Servers from the Client list.  */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed.  */
```