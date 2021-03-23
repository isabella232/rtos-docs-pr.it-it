---
title: Capitolo 8-eventi di traccia di Azure RTO NetX
description: Questo capitolo contiene una descrizione degli eventi NetX di Azure RTO.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: ce355d86d7db0b7e259ae58e306d990277b77a8f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824257"
---
# <a name="chapter-8---azure-rtos-netx-trace-events"></a><span data-ttu-id="213c9-103">Capitolo 8-eventi di traccia di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="213c9-103">Chapter 8 - Azure RTOS NetX trace events</span></span>

<span data-ttu-id="213c9-104">Questo capitolo contiene una descrizione degli eventi NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="213c9-104">This chapter contains a description of the Azure RTOS NetX events.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="213c9-105">Elenco di eventi e icone</span><span class="sxs-lookup"><span data-stu-id="213c9-105">List of Events and Icons</span></span>

<span data-ttu-id="213c9-106">Di seguito è riportato un elenco di eventi NetX visualizzati da TraceX.</span><span class="sxs-lookup"><span data-stu-id="213c9-106">The following is a list of NetX events displayed by TraceX.</span></span>

| <span data-ttu-id="213c9-107">Icona</span><span class="sxs-lookup"><span data-stu-id="213c9-107">Icon</span></span>                                           | <span data-ttu-id="213c9-108">Significato</span><span class="sxs-lookup"><span data-stu-id="213c9-108">Meaning</span></span>                 |
| -------------------------------- | ------------------------------------- |
| ![Icona di ricezione di una richiesta R P interna](./media/user-guide/netx-events/image1.png)    | <span data-ttu-id="213c9-110">Ricezione richiesta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-110">Internal ARP Request Receive</span></span> |
| ![Icona di invio di una richiesta R P interna](./media/user-guide/netx-events/image2.png)    | <span data-ttu-id="213c9-112">Invio richiesta ARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-112">Internal ARP Request Send</span></span> |
| ![Icona di ricezione di risposta R P interna](./media/user-guide/netx-events/image3.png)    | <span data-ttu-id="213c9-114">Ricezione risposta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-114">Internal ARP Response Receive</span></span> |
| ![Icona di invio risposta R P interna](./media/user-guide/netx-events/image4.png)    | <span data-ttu-id="213c9-116">Invio risposta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-116">Internal ARP Response Send</span></span> |
| ![Icona di ricezione interno I C M P](./media/user-guide/netx-events/image5.png)    | <span data-ttu-id="213c9-118">Ricezione ICMP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-118">Internal ICMP Receive</span></span> |
| ![Icona di invio C M P interna](./media/user-guide/netx-events/image6.png)    | <span data-ttu-id="213c9-120">Invio ICMP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-120">Internal ICMP Send</span></span> |
| ![Icona di ricezione NetX I G M interna](./media/user-guide/netx-events/image7.png)    | <span data-ttu-id="213c9-122">Ricezione IGMP NetX interna</span><span class="sxs-lookup"><span data-stu-id="213c9-122">Internal NetX IGMP Receive</span></span> |
| ![Icona di ricezione I P interni](./media/user-guide/netx-events/image8.png)    | <span data-ttu-id="213c9-124">Ricezione IP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-124">Internal IP Receive</span></span> |
| ![Icona di invio di I P interni](./media/user-guide/netx-events/image9.png)    | <span data-ttu-id="213c9-126">Invio IP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-126">Internal IP Send</span></span> |
| ![Icona di ricezione dati T C P interna](./media/user-guide/netx-events/image10.png)    | <span data-ttu-id="213c9-128">Ricezione di dati TCP interni</span><span class="sxs-lookup"><span data-stu-id="213c9-128">Internal TCP Data Receive</span></span> |
| ![Icona di invio dati T C P interna](./media/user-guide/netx-events/image11.png)    | <span data-ttu-id="213c9-130">Trasmissione dati TCP interni</span><span class="sxs-lookup"><span data-stu-id="213c9-130">Internal TCP Data Send</span></span> |
| ![Icona di ricezione T C P interna](./media/user-guide/netx-events/image12.png)    | <span data-ttu-id="213c9-132">Ricezione dell'aletta TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-132">Internal TCP FIN Receive</span></span> |
| ![Icona di invio T C P F I N](./media/user-guide/netx-events/image13.png)    | <span data-ttu-id="213c9-134">Trasmissione aletta TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-134">Internal TCP FIN Send</span></span> |
| ![Icona di ricezione T C P R S interna](./media/user-guide/netx-events/image14.png)    | <span data-ttu-id="213c9-136">Ricezione RST TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-136">Internal TCP RST Receive</span></span> |
| ![Icona di invio T C P R S interna](./media/user-guide/netx-events/image15.png)    | <span data-ttu-id="213c9-138">Trasmissione RST TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-138">Internal TCP RST Send</span></span> |
| ![Icona di ricezione T C P S interna](./media/user-guide/netx-events/image16.png)    | <span data-ttu-id="213c9-140">Ricezione SYN TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-140">Internal TCP SYN Receive</span></span> |
| ![Icona di invio T C P S interna](./media/user-guide/netx-events/image17.png)    | <span data-ttu-id="213c9-142">Trasmissione SYN TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-142">Internal TCP SYN Send</span></span> |
| ![Icona di ricezione U D P interna](./media/user-guide/netx-events/image18.png)    | <span data-ttu-id="213c9-144">Ricezione UDP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-144">Internal UDP Receive</span></span> |
| ![Icona di invio di U D P interna](./media/user-guide/netx-events/image19.png)    | <span data-ttu-id="213c9-146">Invio UDP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-146">Internal UDP Send</span></span> |
| ![Icona di ricezione r P interna](./media/user-guide/netx-events/image20.png)    | <span data-ttu-id="213c9-148">Ricezione RARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-148">Internal RARP Receive</span></span> |
| ![Icona interna R A R P Send](./media/user-guide/netx-events/image21.png)    | <span data-ttu-id="213c9-150">Invio RARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-150">Internal RARP Send</span></span> |
| ![Icona di ripetizione dei tentativi interna di T C](./media/user-guide/netx-events/image22.png)    | <span data-ttu-id="213c9-152">Tentativo TCP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-152">Internal TCP Retry</span></span> |
| ![Icona di modifica dello stato T C P interno](./media/user-guide/netx-events/image23.png)    | <span data-ttu-id="213c9-154">Modifica dello stato TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-154">Internal TCP State Change</span></span> |
| ![Icona di invio pacchetti driver I/O interno](./media/user-guide/netx-events/image24.png)    | <span data-ttu-id="213c9-156">Invio di pacchetti di driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="213c9-156">Internal I/O Driver Packet Send</span></span> |
| ![icon](./media/user-guide/netx-events/image25.png)    | <span data-ttu-id="213c9-158">Inizializzazione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-158">Internal I/O Driver Initialize</span></span> |
| ![Icona di inizializzazione del driver I/O interno](./media/user-guide/netx-events/image26.png)    | <span data-ttu-id="213c9-160">Abilitazione collegamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-160">Internal I/O Driver Link Enable</span></span> |
| ![Icona di disabilitazione collegamento driver I/O interno](./media/user-guide/netx-events/image27.png)    | <span data-ttu-id="213c9-162">Disabilitazione collegamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-162">Internal I/O Driver Link Disable</span></span> |
| ![Icona trasmissione pacchetti I/O interno](./media/user-guide/netx-events/image28.png)    | <span data-ttu-id="213c9-164">Trasmissione di pacchetti di driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="213c9-164">Internal I/O Driver Packet Broadcast</span></span> |
| ![Icona di trasmissione ARP driver I/O interno](./media/user-guide/netx-events/image29.png)    | <span data-ttu-id="213c9-166">Invio ARP driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-166">Internal I/O Driver ARP Send</span></span> |
| ![Icona di invio risposta ARP driver I/O interno](./media/user-guide/netx-events/image30.png)    | <span data-ttu-id="213c9-168">Invio risposta ARP driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-168">Internal I/O Driver ARP Response Send</span></span> |
| ![Icona di invio RARP driver I/O interno](./media/user-guide/netx-events/image31.png)    | <span data-ttu-id="213c9-170">Invio di un driver di I/O interno RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-170">Internal I/O Driver RARP Send</span></span> |
| ![Icona di join multicast driver I/O interno](./media/user-guide/netx-events/image32.png)    | <span data-ttu-id="213c9-172">Join multicast driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-172">Internal I/O Driver Multicast Join</span></span> |
| ![Icona di uscita multicast driver I/O interno](./media/user-guide/netx-events/image33.png)    | <span data-ttu-id="213c9-174">Uscita multicast driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-174">Internal I/O Driver Multicast Leave</span></span> |
| ![Icona di Ottieni stato driver I/O interno](./media/user-guide/netx-events/image34.png)    | <span data-ttu-id="213c9-176">Stato Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-176">Internal I/O Driver Get Status</span></span> |
| ![Icona di Ottieni velocità driver I/O interno](./media/user-guide/netx-events/image35.png)    | <span data-ttu-id="213c9-178">Velocità di ottenimento del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-178">Internal I/O Driver Get Speed</span></span> |
| ![Icona del tipo di driver di I/O interno Get duplex](./media/user-guide/netx-events/image36.png)    | <span data-ttu-id="213c9-180">Tipo duplex Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-180">Internal I/O Driver Get Duplex Type</span></span> |
| ![Icona per il conteggio degli errori di Get di driver I/O interno](./media/user-guide/netx-events/image37.png)    | <span data-ttu-id="213c9-182">Conteggio errori di Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-182">Internal I/O Driver Get Error Count</span></span> |
| ![Icona del conteggio RX del driver I/O interno](./media/user-guide/netx-events/image38.png)    | <span data-ttu-id="213c9-184">Conteggio RX del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-184">Internal I/O Driver Get RX Count</span></span> |
| ![Icona per il conteggio di un driver di I/O interno Get TX](./media/user-guide/netx-events/image39.png)    | <span data-ttu-id="213c9-186">Conteggio TX del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-186">Internal I/O Driver Get TX Count</span></span> |
| ![Icona per ottenere gli errori di allocazione del driver I/O interno](./media/user-guide/netx-events/image40.png)    | <span data-ttu-id="213c9-188">Errore di allocazione del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-188">Internal I/O Driver Get Allocation Errors</span></span> |
| ![Icona di annullamento inizializzazione del driver I/O interno](./media/user-guide/netx-events/image41.png)    | <span data-ttu-id="213c9-190">Annulla inizializzazione del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-190">Internal I/O Driver Un-initialize</span></span> |
| ![Icona di elaborazione posticipata del driver I/O interno](./media/user-guide/netx-events/image42.png)    | <span data-ttu-id="213c9-192">Elaborazione posticipata del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-192">Internal I/O Driver Deferred Processing</span></span> |
| ![Icona delle voci dinamiche di R P Invalidate](./media/user-guide/netx-events/image43.png)    | <span data-ttu-id="213c9-194">**Voci dinamiche ARP Invalidate** (*nx_arp_dynamic_entries_invalidate*)</span><span class="sxs-lookup"><span data-stu-id="213c9-194">**ARP Dynamic Entries Invalidate** (*nx_arp_dynamic_entries_invalidate*)</span></span> |
| ![Icona del set di voci dinamiche di R P](./media/user-guide/netx-events/image44.png)    | <span data-ttu-id="213c9-196">**Set di voci dinamiche ARP** (*nx_arp_dynamic_entry_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-196">**ARP Dynamic Entry Set** (*nx_arp_dynamic_entry_set*)</span></span> |
| ![Icona di abilitazione di R P](./media/user-guide/netx-events/image45.png)    | <span data-ttu-id="213c9-198">**Abilitazione ARP** (*nx_arp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-198">**ARP Enable** (*nx_arp_enable*)</span></span> |
| ![Icona di invio gratuito A R P](./media/user-guide/netx-events/image46.png)    | <span data-ttu-id="213c9-200">**Trasmissione gratuita ARP** (*nx_arp_gratuitous_send*)</span><span class="sxs-lookup"><span data-stu-id="213c9-200">**ARP Gratuitous Send** (*nx_arp_gratuitous_send*)</span></span> |
| ![Icona di ricerca indirizzo hardware R P](./media/user-guide/netx-events/image47.png)    | <span data-ttu-id="213c9-202">**Ricerca indirizzi hardware ARP** (*nx_arp_hardware_address_find*)</span><span class="sxs-lookup"><span data-stu-id="213c9-202">**ARP Hardware Address Find** (*nx_arp_hardware_address_find*)</span></span> |
| ![Icona di Get di informazioni R P](./media/user-guide/netx-events/image48.png)    | <span data-ttu-id="213c9-204">**Informazioni sul protocollo ARP Get** (*nx_arp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-204">**ARP Information Get** (*nx_arp_info_get*)</span></span> |
| ![Icona di ricerca di indirizzi IP R P](./media/user-guide/netx-events/image49.png)    | <span data-ttu-id="213c9-206">**Ricerca indirizzi IP ARP** (*nx_arp_ip_address_find*)</span><span class="sxs-lookup"><span data-stu-id="213c9-206">**ARP IP Address Find** (*nx_arp_ip_address_find*)</span></span> |
| ![Icona di creazione di una voce statica R P](./media/user-guide/netx-events/image50.png)    | <span data-ttu-id="213c9-208">**Creazione voce statica ARP** (*nx_arp_static_entry_create*)</span><span class="sxs-lookup"><span data-stu-id="213c9-208">**ARP Static Entry Create** (*nx_arp_static_entry_create*)</span></span> |
| ![Icona Elimina voci statiche R P](./media/user-guide/netx-events/image51.png)    | <span data-ttu-id="213c9-210">**Elimina voci statiche ARP** (*nx_arp_static_entries_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-210">**ARP Static Entries Delete** (*nx_arp_static_entries_delete*)</span></span> |
| ![Icona di eliminazione della voce statica di R P](./media/user-guide/netx-events/image52.png)    | <span data-ttu-id="213c9-212">**Eliminazione voce statica ARP** (*nx_arp_static_entry_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-212">**ARP Static Entry Delete** (*nx_arp_static_entry_delete*)</span></span> |
| ![Icona di eliminazione voce della cache Duo](./media/user-guide/netx-events/image53.png)    | <span data-ttu-id="213c9-214">**Eliminazione voce della cache Duo** (*nxd_nd_cache_entry_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-214">**Duo Cache Entry Delete** (*nxd_nd_cache_entry_delete*)</span></span> |
| ![Icona del set di voci della cache Duo](./media/user-guide/netx-events/image54.png)    | <span data-ttu-id="213c9-216">**Set di voci della cache Duo** (*nxd_nd_cache_entry_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-216">**Duo Cache Entry Set** (*nxd_nd_cache_entry_set*)</span></span> |
| ![Icona di invalidamento della cache Duo](./media/user-guide/netx-events/image55.png)    | <span data-ttu-id="213c9-218">**Invalidamento della cache Duo** (*nxd_nd_cache_invalidate*)</span><span class="sxs-lookup"><span data-stu-id="213c9-218">**Duo Cache Invalidate** (*nxd_nd_cache_invalidate*)</span></span> |
| ![Icona di ricerca dell'indirizzo del duo cache I P](./media/user-guide/netx-events/image56.png)    | <span data-ttu-id="213c9-220">**Ricerca indirizzo IP cache Duo** (*nxd_nd_cache_ip_address_find*)</span><span class="sxs-lookup"><span data-stu-id="213c9-220">**Duo Cache IP Address Find** (*nxd_nd_cache_ip_address_find*)</span></span> |
| ![Icona di abilitazione Duo I C M P](./media/user-guide/netx-events/image57.png)    | <span data-ttu-id="213c9-222">**Abilitazione ICMP Duo** (*nxd_icmp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-222">**Duo ICMP Enable** (*nxd_icmp_enable*)</span></span> |
| ![Icona di ping di duo I C M P I P v 6](./media/user-guide/netx-events/image58.png)    | <span data-ttu-id="213c9-224">**Ping IPv6 ICMP Duo** (*nxd_icmp_ping*)</span><span class="sxs-lookup"><span data-stu-id="213c9-224">**Duo ICMP IPv6 Ping** (*nxd_icmp_ping*)</span></span> |
| ![Icona trova dimensioni del payload massimo Duo I P](./media/user-guide/netx-events/image59.png)    | <span data-ttu-id="213c9-226">**Ricerca dimensioni massime payload IP Duo** (*nx_max_payload_size_find*)</span><span class="sxs-lookup"><span data-stu-id="213c9-226">**Duo IP Max Payload Size Find** (*nx_max_payload_size_find*)</span></span> |
| ![Icona di invio di pacchetti non elaborati Duo I P](./media/user-guide/netx-events/image60.png)    | <span data-ttu-id="213c9-228">**Trasmissione pacchetti non elaborati IP Duo** (*nxd_ip_raw_packet_send*)</span><span class="sxs-lookup"><span data-stu-id="213c9-228">**Duo IP Raw Packet Send** (*nxd_ip_raw_packet_send*)</span></span> |
| ![Icona di aggiunta del router predefinito Duo I P v 6](./media/user-guide/netx-events/image61.png)    | <span data-ttu-id="213c9-230">**Aggiunta del router predefinito IPv6 Duo** (*nxd_ipv6_default_router_add*)</span><span class="sxs-lookup"><span data-stu-id="213c9-230">**Duo IPv6 Default Router Add** (*nxd_ipv6_default_router_add*)</span></span> |
| ![Icona di eliminazione del router predefinito Duo I P v 6](./media/user-guide/netx-events/image62.png)    | <span data-ttu-id="213c9-232">**Eliminazione router default IPv6 Duo** (*nxd_ipv6_default_router_delete)*</span><span class="sxs-lookup"><span data-stu-id="213c9-232">**Duo IPv6 Default Router Delete** (*nxd_ipv6_default_router_delete)*</span></span> |
| ![Icona abilitazione Duo I P v 6](./media/user-guide/netx-events/image63.png)    | <span data-ttu-id="213c9-234">**Abilitazione IPv6 Duo** (*nxd_ipv6_enable)*</span><span class="sxs-lookup"><span data-stu-id="213c9-234">**Duo IPv6 Enable** (*nxd_ipv6_enable)*</span></span> |
| ![Icona Get indirizzo globale Duo I P v 6](./media/user-guide/netx-events/image64.png)    | <span data-ttu-id="213c9-236">**Indirizzo globale IPv6 Duo Get** (*nxd_ipv6_global_address_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-236">**Duo IPv6 Global Address Get** (*nxd_ipv6_global_address_get*)</span></span> |
| ![Icona del set di indirizzi globale Duo I P v 6](./media/user-guide/netx-events/image65.png)    | <span data-ttu-id="213c9-238">**Set di indirizzi globali IPv6 Duo** (*nxd_ipv6_global_address_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-238">**Duo IPv6 Global Address Set** (*nxd_ipv6_global_address_set*)</span></span> |
| ![Icona del processo padre di avvio Duo I P v 6](./media/user-guide/netx-events/image66.png)    | <span data-ttu-id="213c9-240">**Processo padre di avvio IPv6 Duo** (*nxd_ipv6_initiate_dad_process*)</span><span class="sxs-lookup"><span data-stu-id="213c9-240">**Duo IPv6 Initiate Dad Process** (*nxd_ipv6_initiate_dad_process*)</span></span> |
| ![Icona di Get dell'indirizzo dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image67.png)    | <span data-ttu-id="213c9-242">**Indirizzo di interfaccia IPv6 del duo Get** (*nxd_ipv6_interface_address_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-242">**Duo IPv6 Interface Address Get** (*nxd_ipv6_interface_address_get*)</span></span> |
| ![Icona set di indirizzi dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image68.png)    | <span data-ttu-id="213c9-244">**Set di indirizzi di interfaccia IPv6 Duo** (*nxd_ipv6_interface_address_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-244">**Duo IPv6 Interface Address Set** (*nxd_ipv6_interface_address_set*)</span></span> |
| ![Icona di Get dell'indirizzo locale del collegamento Duo I P v 6](./media/user-guide/netx-events/image69.png)    | <span data-ttu-id="213c9-246">**Indirizzo locale del collegamento IPv6 Duo Get** (*nxd_ipv6_linklocal_address_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-246">**Duo IPv6 Link Local Address Get** (*nxd_ipv6_linklocal_address_get*)</span></span> |
| ![Icona del set di indirizzi locali di collegamento I P v 6](./media/user-guide/netx-events/image70.png)    | <span data-ttu-id="213c9-248">**Set di indirizzi locali del collegamento IPv6 Duo** (*nxd_ipv6_linklocal_address_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-248">**Duo IPv6 Link Local Address Set** (*nxd_ipv6_linklocal_address_set*)</span></span> |
| ![Icona di invio di pacchetti non elaborati Duo I P v 6](./media/user-guide/netx-events/image71.png)    | <span data-ttu-id="213c9-250">**Trasmissione pacchetti non elaborati IPv6 Duo** (*nxd_ipv6_raw_packet_send)*</span><span class="sxs-lookup"><span data-stu-id="213c9-250">**Duo IPv6 Raw Packet Send** (*nxd_ipv6_raw_packet_send)*</span></span> |
| ![Icona Get per le informazioni su peer di Duo T C P](./media/user-guide/netx-events/image72.png)    | <span data-ttu-id="213c9-252">**Informazioni su peer socket TCP Duo Get** (*nxd_tcp_socket_peer_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-252">**Duo TCP Socket Peer Info Get** (*nxd_tcp_socket_peer_info_get*)</span></span> |
| ![Icona dell'interfaccia del set di socket T C P Duo](./media/user-guide/netx-events/image73.png)    | <span data-ttu-id="213c9-254">**Interfaccia del set di socket TCP Duo** (*nxd_tcp_socket_set_interface*)</span><span class="sxs-lookup"><span data-stu-id="213c9-254">**Duo TCP Socket Set Interface** (*nxd_tcp_socket_set_interface*)</span></span> |
| ![Icona di invio del socket Duo U D P](./media/user-guide/netx-events/image74.png)    | <span data-ttu-id="213c9-256">**Invio socket UDP Duo** (*nxd_udp_socket_send*)</span><span class="sxs-lookup"><span data-stu-id="213c9-256">**Duo UDP Socket Send** (*nxd_udp_socket_send*)</span></span> |
| ![Icona dell'interfaccia del set di socket U D P Duo](./media/user-guide/netx-events/image75.png)    | <span data-ttu-id="213c9-258">**Interfaccia del set di socket UDP Duo** (*nxd_udp_socket_set_interface*)</span><span class="sxs-lookup"><span data-stu-id="213c9-258">**Duo UDP Socket Set Interface** (*nxd_udp_socket_set_interface*)</span></span> |
| ![Icona estrazione origine Duo U D P](./media/user-guide/netx-events/image76.png)    | <span data-ttu-id="213c9-260">**Estrai origine UDP Duo** (*nxd_udp_source_extract*)</span><span class="sxs-lookup"><span data-stu-id="213c9-260">**Duo UDP Source Extract** (*nxd_udp_source_extract*)</span></span> |
| ![Icona di abilitazione I C M P](./media/user-guide/netx-events/image77.png)    | <span data-ttu-id="213c9-262">**Abilita ICMP** (*nx_icmp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-262">**ICMP Enable** (*nx_icmp_enable*)</span></span> |
| ![Icona di Get di informazioni C M P](./media/user-guide/netx-events/image78.png)    | <span data-ttu-id="213c9-264">**Informazioni sul protocollo ICMP Get** (*nx_icmp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-264">**ICMP Information Get** (*nx_icmp_info_get*)</span></span> |
| ![Icona ping I C M P](./media/user-guide/netx-events/image79.png)    | <span data-ttu-id="213c9-266">**Ping ICMP** (*nx_icmp_ping*)</span><span class="sxs-lookup"><span data-stu-id="213c9-266">**ICMP Ping** (*nx_icmp_ping*)</span></span> |
| ![Icona di abilitazione I G M P](./media/user-guide/netx-events/image80.png)    | <span data-ttu-id="213c9-268">**Abilitazione IGMP** (*nx_igmp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-268">**IGMP Enable** (*nx_igmp_enable*)</span></span> |
| ![Icona di informazioni Get di I G M P](./media/user-guide/netx-events/image81.png)    | <span data-ttu-id="213c9-270">**Informazioni IGMP Get** (*nx_igmp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-270">**IGMP Information Get** (*nx_igmp_info_get*)</span></span> |
| ![Icona di disabilitazione loopback di I G M P](./media/user-guide/netx-events/image82.png)    | <span data-ttu-id="213c9-272">**Disabilita loopback loopback** (*nx_igmp_loopback_disable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-272">**IGMP Loopback Disable** (*nx_igmp_loopback_disable*)</span></span> |
| ![Icona Abilita loopback I G M P](./media/user-guide/netx-events/image83.png)    | <span data-ttu-id="213c9-274">**Abilita loopback loopback** (*nx_igmp_loopback_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-274">**IGMP Loopback Enable** (*nx_igmp_loopback_enable*)</span></span> |
| ![Icona di join multicast I G M P](./media/user-guide/netx-events/image84.png)    | <span data-ttu-id="213c9-276">**Join multicast IGMP** (*nx_igmp_multicast_join*)</span><span class="sxs-lookup"><span data-stu-id="213c9-276">**IGMP Multicast Join** (*nx_igmp_multicast_join*)</span></span> |
| ![Icona di uscita multicast I G M P](./media/user-guide/netx-events/image85.png)    | <span data-ttu-id="213c9-278">**Uscita multicast IGMP** (*nx_igmp_multicast_leave*)</span><span class="sxs-lookup"><span data-stu-id="213c9-278">**IGMP Multicast Leave** (*nx_igmp_multicast_leave*)</span></span> |
| ![Icona di notifica della modifica dell'indirizzo I P](./media/user-guide/netx-events/image86.png)    | <span data-ttu-id="213c9-280">**Notifica di modifica dell'indirizzo IP** (*nx_ip_address_change_notify*)</span><span class="sxs-lookup"><span data-stu-id="213c9-280">**IP Address Change Notify** (*nx_ip_address_change_notify*)</span></span> |
| ![Icona Ottieni indirizzo I P](./media/user-guide/netx-events/image87.png)    | <span data-ttu-id="213c9-282">**Indirizzo IP Get** (*nx_ip_address_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-282">**IP Address Get** (*nx_ip_address_get*)</span></span> |
| ![Icona del set di indirizzi I P](./media/user-guide/netx-events/image88.png)    | <span data-ttu-id="213c9-284">**Set di indirizzi IP** (*nx_ip_address_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-284">**IP Address Set** (*nx_ip_address_set*)</span></span> |
| ![Icona di creazione P](./media/user-guide/netx-events/image89.png)    | <span data-ttu-id="213c9-286">**Creazione IP** (*nx_ip_create*)</span><span class="sxs-lookup"><span data-stu-id="213c9-286">**IP Create** (*nx_ip_create*)</span></span> |
| ![Icona di eliminazione I P](./media/user-guide/netx-events/image90.png)    | <span data-ttu-id="213c9-288">**Eliminazione IP** (*nx_ip_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-288">**IP Delete** (*nx_ip_delete*)</span></span> |
| ![Icona comando diretto driver I P](./media/user-guide/netx-events/image91.png)    | <span data-ttu-id="213c9-290">**Comando Direct driver IP** (*nx_ip_driver_direct_command*)</span><span class="sxs-lookup"><span data-stu-id="213c9-290">**IP Driver Direct Command** (*nx_ip_driver_direct_command*)</span></span> |
| ![Icona di disabilitazione dell'invio P](./media/user-guide/netx-events/image92.png)    | <span data-ttu-id="213c9-292">**Disabilitazione dell'invio IP** (*nx_ip_forwarding_disable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-292">**IP Forwarding Disable** (*nx_ip_forwarding_disable*)</span></span> |
| ![Icona Abilita l'invio P](./media/user-guide/netx-events/image93.png)    | <span data-ttu-id="213c9-294">**Abilitazione dell'invio IP** (*nx_ip_forwarding_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-294">**IP Forwarding Enable** (*nx_ip_forwarding_enable*)</span></span> |
| ![Icona di disabilitazione del frammento I P](./media/user-guide/netx-events/image94.png)    | <span data-ttu-id="213c9-296">**Disabilitazione frammenti IP** (*nx_ip_fragment_disable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-296">**IP Fragment Disable** (*nx_ip_fragment_disable*)</span></span> |
| ![Icona Abilita frammento I P](./media/user-guide/netx-events/image95.png)    | <span data-ttu-id="213c9-298">**Abilitazione frammenti IP** (*nx_ip_fragment_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-298">**IP Fragment Enable** (*nx_ip_fragment_enable*)</span></span>  |
| ![Icona del set di indirizzi del gateway I P](./media/user-guide/netx-events/image96.png)    | <span data-ttu-id="213c9-300">**Set di indirizzi IP gateway** (*nx_ip_gateway_address_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-300">**IP Gateway Address Set** (*nx_ip_gateway_address_set*)</span></span> |
| ![Icona di Get delle informazioni P](./media/user-guide/netx-events/image97.png)    | <span data-ttu-id="213c9-302">**Informazioni IP Get** (*nx_ip_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-302">**IP Information Get** (*nx_ip_info_get*)</span></span> |
| ![Icona di connessione interfaccia I P](./media/user-guide/netx-events/image98.png)    | <span data-ttu-id="213c9-304">**Connessione interfaccia IP** (*nx_ip_interface_attach*)</span><span class="sxs-lookup"><span data-stu-id="213c9-304">**IP Interface Attach** (*nx_ip_interface_attach*)</span></span> |
| ![Icona di informazioni di interfaccia I P Get](./media/user-guide/netx-events/image99.png)    | <span data-ttu-id="213c9-306">**Informazioni sull'interfaccia IP Get** (*nx_ip_interface_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-306">**IP Interface Info Get** (*nx_ip_interface_info_get*)</span></span> |
| ![Icona di disabilitazione pacchetti non elaborati](./media/user-guide/netx-events/image100.png)    | <span data-ttu-id="213c9-308">**Disabilitazione pacchetto non elaborato IP** (*nx_ip_raw_packet_disable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-308">**IP Raw Packet Disable** (*nx_ip_raw_packet_disable*)</span></span> |
| ![Icona di abilitazione di pacchetti non elaborati](./media/user-guide/netx-events/image101.png)    | <span data-ttu-id="213c9-310">**Abilitazione pacchetti non elaborati IP** (*nx_ip_raw_packet_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-310">**IP Raw Packet Enable** (*nx_ip_raw_packet_enable*)</span></span> |
| ![Icona di ricezione di pacchetti non elaborati](./media/user-guide/netx-events/image102.png)    | <span data-ttu-id="213c9-312">**Ricezione pacchetti non elaborati IP** (*nx_ip_raw_packet_receive*)</span><span class="sxs-lookup"><span data-stu-id="213c9-312">**IP Raw Packet Receive** (*nx_ip_raw_packet_receive*)</span></span> |
| ![Icona di invio di pacchetti non elaborati](./media/user-guide/netx-events/image103.png)    | <span data-ttu-id="213c9-314">**Invio pacchetti non elaborati IP** (*nx_ip_raw_packet_send*)</span><span class="sxs-lookup"><span data-stu-id="213c9-314">**IP Raw Packet Send** (*nx_ip_raw_packet_send*)</span></span> |
| ![Icona di aggiunta statica route I P](./media/user-guide/netx-events/image104.png)    | <span data-ttu-id="213c9-316">**Aggiunta route statica IP** (*nx_ip_static_route_add*)</span><span class="sxs-lookup"><span data-stu-id="213c9-316">**IP Static Route Add** (*nx_ip_static_route_add*)</span></span> |
| ![Icona di eliminazione route statica I P](./media/user-guide/netx-events/image105.png)    | <span data-ttu-id="213c9-318">**Eliminazione route statica IP** (*nx_ip_static_route_delete)*</span><span class="sxs-lookup"><span data-stu-id="213c9-318">**IP Static Route Delete** (*nx_ip_static_route_delete)*</span></span> |
| ![Icona di controllo stato I P](./media/user-guide/netx-events/image106.png)    | <span data-ttu-id="213c9-320">**Controllo stato IP** (*nx_ip_status_check*)</span><span class="sxs-lookup"><span data-stu-id="213c9-320">**IP Status Check** (*nx_ip_status_check*)</span></span>|
| ![Icona Enable i P S E C](./media/user-guide/netx-events/image107.png)    | <span data-ttu-id="213c9-322">**Abilita IPSec** (*nx_ipsec_enable)*</span><span class="sxs-lookup"><span data-stu-id="213c9-322">**IPSEC Enable** (*nx_ipsec_enable)*</span></span> |
| ![Icona di allocazione pacchetti](./media/user-guide/netx-events/image108.png)    | <span data-ttu-id="213c9-324">**Allocazione pacchetti** (*nx_packet_allocate*)</span><span class="sxs-lookup"><span data-stu-id="213c9-324">**Packet Allocate** (*nx_packet_allocate*)</span></span> |
| ![Icona copia pacchetti](./media/user-guide/netx-events/image109.png)    | <span data-ttu-id="213c9-326">**Copia di pacchetti** (*nx_packet_copy*)</span><span class="sxs-lookup"><span data-stu-id="213c9-326">**Packet Copy** (*nx_packet_copy*)</span></span> |
| ![Icona Accodamento dati pacchetto](./media/user-guide/netx-events/image110.png)    | <span data-ttu-id="213c9-328">**Accodamento dati pacchetto** (*nx_packet_data_append*)</span><span class="sxs-lookup"><span data-stu-id="213c9-328">**Packet Data Append** (*nx_packet_data_append*)</span></span> |
| ![Icona di offset estrazione dati pacchetto](./media/user-guide/netx-events/image111.png)    | <span data-ttu-id="213c9-330">**Offset estrazione dati pacchetto** (*nx_packet_data_extract_offset*)</span><span class="sxs-lookup"><span data-stu-id="213c9-330">**Packet Data Extract Offset** (*nx_packet_data_extract_offset*)</span></span> |
| ![Icona recupero dati pacchetto](./media/user-guide/netx-events/image112.png)    | <span data-ttu-id="213c9-332">**Recupero dati pacchetto** (*nx_packet_data_retrieve*)</span><span class="sxs-lookup"><span data-stu-id="213c9-332">**Packet Data Retrieve** (*nx_packet_data_retrieve*)</span></span> |
| ![Icona Ottieni lunghezza pacchetto](./media/user-guide/netx-events/image113.png)    | <span data-ttu-id="213c9-334">**Lunghezza pacchetto Get** (*nx_packet_length_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-334">**Packet Length Get** (*nx_packet_length_get*)</span></span> |
| ![Icona di creazione pool di pacchetti](./media/user-guide/netx-events/image114.png)    | <span data-ttu-id="213c9-336">**Creazione pool di pacchetti** (*nx_packet_pool_create*)</span><span class="sxs-lookup"><span data-stu-id="213c9-336">**Packet Pool Create** (*nx_packet_pool_create*)</span></span> |
| ![Icona di eliminazione del pool di pacchetti](./media/user-guide/netx-events/image115.png)    | <span data-ttu-id="213c9-338">**Eliminazione pool di pacchetti** (*nx_packet_pool_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-338">**Packet Pool Delete** (*nx_packet_pool_delete*)</span></span> |
| ![Icona Ottieni informazioni sul pool di pacchetti](./media/user-guide/netx-events/image116.png)    | <span data-ttu-id="213c9-340">**Informazioni sul pool di pacchetti Get** (*nx_packet_pool_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-340">**Packet Pool Information Get** (*nx_packet_pool_info_get*)</span></span> |
| ![Icona versione pacchetto](./media/user-guide/netx-events/image117.png)    | <span data-ttu-id="213c9-342">**Versione pacchetto** (*nx_packet_release*)</span><span class="sxs-lookup"><span data-stu-id="213c9-342">**Packet Release** (*nx_packet_release*)</span></span> |
| ![Icona della versione di trasmissione pacchetti](./media/user-guide/netx-events/image118.png)    | <span data-ttu-id="213c9-344">**Versione trasmissione pacchetti** (*nx_packet_transmit_release*)</span><span class="sxs-lookup"><span data-stu-id="213c9-344">**Packet Transmit Release** (*nx_packet_transmit_release*)</span></span> |
| ![Icona di disabilitazione r P](./media/user-guide/netx-events/image119.png)    | <span data-ttu-id="213c9-346">**Disabilitazione RARP** (*nx_rarp_disable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-346">**RARP Disable** (*nx_rarp_disable*)</span></span> |
| ![Icona di abilitazione r A r P](./media/user-guide/netx-events/image120.png)    | <span data-ttu-id="213c9-348">**Abilitazione di RARP** (*nx_rarp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-348">**RARP Enable** (*nx_rarp_enable*)</span></span> |
| ![Icona di r A r P Information Get](./media/user-guide/netx-events/image121.png)    | <span data-ttu-id="213c9-350">**Informazioni su RARP Get** (*nx_rarp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-350">**RARP Information Get** (*nx_rarp_info_get*)</span></span> |
| ![Icona Inizializzazione sistema](./media/user-guide/netx-events/image122.png)    | <span data-ttu-id="213c9-352">**Inizializzazione sistema** (*nx_system_initialize*)</span><span class="sxs-lookup"><span data-stu-id="213c9-352">**System Initialize** (*nx_system_initialize*)</span></span> |
| ![Icona di Binding socket client T C P](./media/user-guide/netx-events/image123.png)    | <span data-ttu-id="213c9-354">**Binding socket client TCP** (*nx_tcp_client_socket_bind*)</span><span class="sxs-lookup"><span data-stu-id="213c9-354">**TCP Client Socket Bind** (*nx_tcp_client_socket_bind*)</span></span> |
| ![Icona di connessione socket client T C P](./media/user-guide/netx-events/image124.png)    | <span data-ttu-id="213c9-356">**Connessione socket client TCP** (*nx_tcp_client_socket_connect*)</span><span class="sxs-lookup"><span data-stu-id="213c9-356">**TCP Client Socket Connect** (*nx_tcp_client_socket_connect*)</span></span> |
| ![Icona di Get della porta del socket client T C P](./media/user-guide/netx-events/image125.png)    | <span data-ttu-id="213c9-358">**Porta socket client TCP** (*nx_tcp_client_socket_port_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-358">**TCP Client Socket Port Get** (*nx_tcp_client_socket_port_get*)</span></span> |
| ![Icona di disassociazione socket client T C P](./media/user-guide/netx-events/image126.png)    | <span data-ttu-id="213c9-360">**Disassociazione socket client TCP** (*nx_tcp_client_socket_unbind*)</span><span class="sxs-lookup"><span data-stu-id="213c9-360">**TCP Client Socket Unbind** (*nx_tcp_client_socket_unbind*)</span></span> |
| ![Icona di abilitazione di T C P](./media/user-guide/netx-events/image127.png)    | <span data-ttu-id="213c9-362">**Abilitazione TCP** (*nx_tcp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-362">**TCP Enable** (*nx_tcp_enable*)</span></span> |
| ![Icona trova porta disponibile T C P](./media/user-guide/netx-events/image128.png)    | <span data-ttu-id="213c9-364">**Ricerca porta TCP gratuita** (*nx_tcp_free_port_find*)</span><span class="sxs-lookup"><span data-stu-id="213c9-364">**TCP Free Port Find** (*nx_tcp_free_port_find*)</span></span> |
| ![Icona di Get delle informazioni di T C P](./media/user-guide/netx-events/image129.png)    | <span data-ttu-id="213c9-366">**Informazioni sul protocollo TCP Get** (*nx_tcp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-366">**TCP Information Get** (*nx_tcp_info_get*)</span></span> |
| ![Icona di accettazione socket server T C P](./media/user-guide/netx-events/image130.png)    | <span data-ttu-id="213c9-368">**Accettazione socket server TCP** (*nx_tcp_server_socket_accept*)</span><span class="sxs-lookup"><span data-stu-id="213c9-368">**TCP Server Socket Accept** (*nx_tcp_server_socket_accept*)</span></span> |
| ![Icona ascolto Socket Server T C P](./media/user-guide/netx-events/image131.png)    | <span data-ttu-id="213c9-370">**Ascolto socket server TCP** (*nx_tcp_server_socket_listen*)</span><span class="sxs-lookup"><span data-stu-id="213c9-370">**TCP Server Socket Listen** (*nx_tcp_server_socket_listen*)</span></span> |
| ![Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image132.png)    | <span data-ttu-id="213c9-372">**Socket server TCP relisten** (*nx_tcp_server_socket_relisten*)</span><span class="sxs-lookup"><span data-stu-id="213c9-372">**TCP Server Socket Relisten** (*nx_tcp_server_socket_relisten*)</span></span> |
| ![Icona di unaccept socket server T C P](./media/user-guide/netx-events/image133.png)    | <span data-ttu-id="213c9-374">**Unaccept socket server TCP** (*nx_tcp_server_socket_unaccept*)</span><span class="sxs-lookup"><span data-stu-id="213c9-374">**TCP Server Socket Unaccept** (*nx_tcp_server_socket_unaccept*)</span></span> |
| ![Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image134.png)    | <span data-ttu-id="213c9-376">**Server socket TCP** non in elenco (*nx_tcp_server_socket_unlisten*)</span><span class="sxs-lookup"><span data-stu-id="213c9-376">**TCP Server Socket Unlisten** (*nx_tcp_server_socket_unlisten*)</span></span> |
| ![Icona di byte socket a T C P disponibile](./media/user-guide/netx-events/image135.png)    | <span data-ttu-id="213c9-378">**Byte socket TCP disponibili** (*nx_tcp_socket_bytes_available*)</span><span class="sxs-lookup"><span data-stu-id="213c9-378">**TCP Socket Bytes Available** (*nx_tcp_socket_bytes_available*)</span></span> |
| ![Icona di creazione socket T C P](./media/user-guide/netx-events/image136.png)    | <span data-ttu-id="213c9-380">**Creazione socket TCP** (*nx_tcp_socket_create*)</span><span class="sxs-lookup"><span data-stu-id="213c9-380">**TCP Socket Create** (*nx_tcp_socket_create*)</span></span> |
| ![Icona di eliminazione Socket T C P](./media/user-guide/netx-events/image137.png)    | <span data-ttu-id="213c9-382">**Elimina socket TCP** (*nx_tcp_socket_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-382">**TCP Socket Delete** (*nx_tcp_socket_delete*)</span></span> |
| ![Icona di disconnessione Socket T C P](./media/user-guide/netx-events/image138.png)    | <span data-ttu-id="213c9-384">**Disconnessione socket TCP** (*nx_tcp_socket_disconnect*)</span><span class="sxs-lookup"><span data-stu-id="213c9-384">**TCP Socket Disconnect** (*nx_tcp_socket_disconnect*)</span></span> |
| ![Icona di Get delle informazioni sul socket T C P](./media/user-guide/netx-events/image139.png)    | <span data-ttu-id="213c9-386">**Informazioni sul socket TCP Get** (*nx_tcp_socket_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-386">**TCP Socket Information Get** (*nx_tcp_socket_info_get*)</span></span> |
| ![Icona di Get MSS Socket T C P](./media/user-guide/netx-events/image140.png)    | <span data-ttu-id="213c9-388">**TCP socket MSS Get** (*nx_tcp_socket_mss_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-388">**TCP Socket MSS Get** (*nx_tcp_socket_mss_get*)</span></span> |
| ![Icona di Get del peer MSS di T C P](./media/user-guide/netx-events/image141.png)    | <span data-ttu-id="213c9-390">**Peer Get MSS socket TCP** (*nx_tcp_socket_mss_peer_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-390">**TCP Socket MSS Peer Get** (*nx_tcp_socket_mss_peer_get*)</span></span> |
| ![Icona set MSS Socket T C P](./media/user-guide/netx-events/image142.png)    | <span data-ttu-id="213c9-392">**Set MSS socket TCP** (*nx_tcp_socket_mss_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-392">**TCP Socket MSS Set** (*nx_tcp_socket_mss_set*)</span></span> |
| ![Icona di Get delle informazioni peer del socket T C P](./media/user-guide/netx-events/image143.png)    | <span data-ttu-id="213c9-394">**Get informazioni peer del socket TCP** (*nx_tcp_socket_peer_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-394">**TCP Socket Peer Info Get** (*nx_tcp_socket_peer_info_get*)</span></span> |
| ![Icona di ricezione Socket T C P](./media/user-guide/netx-events/image144.png)    | <span data-ttu-id="213c9-396">**Ricezione socket TCP** (*nx_tcp_socket_receive*)</span><span class="sxs-lookup"><span data-stu-id="213c9-396">**TCP Socket Receive** (*nx_tcp_socket_receive*)</span></span> |
| ![Icona di ricezione della notifica socket T C P](./media/user-guide/netx-events/image145.png)    | <span data-ttu-id="213c9-398">**Notifica ricezione socket TCP** (*nx_tcp_socket_receive_notify*)</span><span class="sxs-lookup"><span data-stu-id="213c9-398">**TCP Socket Receive Notify** (*nx_tcp_socket_receive_notify*)</span></span> |
| ![Icona di invio socket T C P](./media/user-guide/netx-events/image146.png)    | <span data-ttu-id="213c9-400">**Invio socket TCP** (*nx_tcp_socket_send*)</span><span class="sxs-lookup"><span data-stu-id="213c9-400">**TCP Socket Send** (*nx_tcp_socket_send*)</span></span> |
| ![Icona di attesa stato Socket T C P](./media/user-guide/netx-events/image147.png)    | <span data-ttu-id="213c9-402">**Attesa stato socket TCP** (*nx_tcp_socket_state_wait*)</span><span class="sxs-lookup"><span data-stu-id="213c9-402">**TCP Socket State Wait** (*nx_tcp_socket_state_wait*)</span></span> |
| ![Icona di configurazione di trasmissione Socket T C P](./media/user-guide/netx-events/image148.png)    | <span data-ttu-id="213c9-404">**Configurazione di trasmissione socket TCP** (*nx_tcp_socket_transmit_configure*)</span><span class="sxs-lookup"><span data-stu-id="213c9-404">**TCP Socket Transmit Configure** (*nx_tcp_socket_transmit_configure*)</span></span> |
| ![Icona del set di notifiche di aggiornamento della finestra socket di T C P](./media/user-guide/netx-events/image149.png)    | <span data-ttu-id="213c9-406">**Set Notify di aggiornamento finestra socket TCP** (*nx_tcp_socket_window_update_notify_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-406">**TCP Socket Window Update Notify Set** (*nx_tcp_socket_window_update_notify_set*)</span></span>  |
| ![Icona di abilitazione di U D P](./media/user-guide/netx-events/image150.png)    | <span data-ttu-id="213c9-408">**Abilita UDP** (*nx_udp_enable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-408">**UDP Enable** (*nx_udp_enable*)</span></span> |
| ![Icona trova porta gratuita U D P](./media/user-guide/netx-events/image151.png)    | <span data-ttu-id="213c9-410">**Ricerca porta gratuita UDP** (*nx_udp_free_port_find*)</span><span class="sxs-lookup"><span data-stu-id="213c9-410">**UDP Free Port Find** (*nx_udp_free_port_find*)</span></span> |
| ![Icona di Get delle informazioni di U D P](./media/user-guide/netx-events/image152.png)    | <span data-ttu-id="213c9-412">**Informazioni UDP Get** (*nx_udp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-412">**UDP Information Get** (*nx_udp_info_get*)</span></span> |
| ![Icona di Binding socket U D P](./media/user-guide/netx-events/image153.png)    | <span data-ttu-id="213c9-414">**Binding socket UDP** (*nx_udp_socket_bind*)</span><span class="sxs-lookup"><span data-stu-id="213c9-414">**UDP Socket Bind** (*nx_udp_socket_bind*)</span></span> |
| ![Icona di byte socket U D P disponibile](./media/user-guide/netx-events/image154.png)    | <span data-ttu-id="213c9-416">**Byte socket UDP disponibili** (*nx_udp_socket_bytes_available*)</span><span class="sxs-lookup"><span data-stu-id="213c9-416">**UDP Socket Bytes Available** (*nx_udp_socket_bytes_available*)</span></span> |
| ![Icona di disabilitazione checksum socket U D P](./media/user-guide/netx-events/image155.png)    | <span data-ttu-id="213c9-418">**Disabilita checksum socket UDP** (*nx_udp_socket_checksum_disable*)</span><span class="sxs-lookup"><span data-stu-id="213c9-418">**UDP Socket Checksum Disable** (*nx_udp_socket_checksum_disable*)</span></span> |
| ![Icona Abilita checksum socket U D P](./media/user-guide/netx-events/image156.png)    | <span data-ttu-id="213c9-420">**Enable UDP Socket checksum** *(nx_udp_socket_checksum_enable)*</span><span class="sxs-lookup"><span data-stu-id="213c9-420">**UDP Socket Checksum Enable** *(nx_udp_socket_checksum_enable)*</span></span> |
| ![Icona di creazione socket U D P](./media/user-guide/netx-events/image157.png)    | <span data-ttu-id="213c9-422">**Creazione socket UDP** (*nx_udp_socket_create*)</span><span class="sxs-lookup"><span data-stu-id="213c9-422">**UDP Socket Create** (*nx_udp_socket_create*)</span></span> |
| ![Icona di eliminazione socket U D P](./media/user-guide/netx-events/image158.png)    | <span data-ttu-id="213c9-424">**Elimina socket UDP** (*nx_udp_socket_delete*)</span><span class="sxs-lookup"><span data-stu-id="213c9-424">**UDP Socket Delete** (*nx_udp_socket_delete*)</span></span> |
| ![Icona di Get delle informazioni sul socket U D](./media/user-guide/netx-events/image159.png)    | <span data-ttu-id="213c9-426">**Informazioni sul socket UDP Get** (*nx_udp_socket_info_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-426">**UDP Socket Information Get** (*nx_udp_socket_info_get*)</span></span> |
| ![Icona del set di interfacce socket U D P](./media/user-guide/netx-events/image160.png)    | <span data-ttu-id="213c9-428">**Set di interfacce socket UDP** (*nx_udp_socket_interface_set*)</span><span class="sxs-lookup"><span data-stu-id="213c9-428">**UDP Socket Interface Set** (*nx_udp_socket_interface_set*)</span></span> |
| ![Icona di Get della porta socket U D P](./media/user-guide/netx-events/image161.png)    | <span data-ttu-id="213c9-430">**Porta del socket UDP Get** (*nx_udp_socket_port_get*)</span><span class="sxs-lookup"><span data-stu-id="213c9-430">**UDP Socket Port Get** (*nx_udp_socket_port_get*)</span></span> |
| ![Icona di ricezione socket U D P](./media/user-guide/netx-events/image162.png)    | <span data-ttu-id="213c9-432">**Ricezione socket UDP** (*nx_udp_socket_receive*)</span><span class="sxs-lookup"><span data-stu-id="213c9-432">**UDP Socket Receive** (*nx_udp_socket_receive*)</span></span> |
| ![Icona di ricezione della notifica socket U D P](./media/user-guide/netx-events/image163.png)    | <span data-ttu-id="213c9-434">**Notifica ricezione socket UDP** (*nx_udp_socket_receive_notify*)</span><span class="sxs-lookup"><span data-stu-id="213c9-434">**UDP Socket Receive Notify** (*nx_udp_socket_receive_notify*)</span></span> |
| ![Icona di invio socket U D P](./media/user-guide/netx-events/image164.png)    | <span data-ttu-id="213c9-436">**Invio socket UDP** (*nx_udp_socket_send*)</span><span class="sxs-lookup"><span data-stu-id="213c9-436">**UDP Socket Send** (*nx_udp_socket_send*)</span></span> |
| ![Icona di disassociazione socket U D P](./media/user-guide/netx-events/image165.png)    | <span data-ttu-id="213c9-438">**Disassociazione socket UDP** (*nx_udp_socket_unbind*)</span><span class="sxs-lookup"><span data-stu-id="213c9-438">**UDP Socket Unbind** (*nx_udp_socket_unbind*)</span></span> |
| ![Icona estrazione origine U D P](./media/user-guide/netx-events/image166.png)    | <span data-ttu-id="213c9-440">**Estrazione origine UDP** (*nx_udp_source_extract*)</span><span class="sxs-lookup"><span data-stu-id="213c9-440">**UDP Source Extract** (*nx_udp_source_extract*)</span></span> |

## <a name="event-descriptions"></a><span data-ttu-id="213c9-441">Descrizioni di eventi</span><span class="sxs-lookup"><span data-stu-id="213c9-441">Event Descriptions</span></span>

<span data-ttu-id="213c9-442">Nelle pagine seguenti vengono descritti gli eventi di traccia NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-442">The following pages describe the NetX Trace Events.</span></span>

### <a name="internal-arp-request-receive"></a><span data-ttu-id="213c9-443">Ricezione richiesta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-443">Internal ARP Request Receive</span></span> 

#### <a name="internal-arp-request-receive"></a><span data-ttu-id="213c9-444">Ricezione richiesta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-444">Internal ARP request receive</span></span>

<span data-ttu-id="213c9-445">**Icona** ![ di Icona di ricezione richiesta ARP interna](./media/user-guide/netx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-445">**Icon** ![Internal ARP request receive icon](./media/user-guide/netx-events/image1.png)</span></span>

<span data-ttu-id="213c9-446">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-446">**Description**</span></span>

<span data-ttu-id="213c9-447">Questo evento rappresenta un evento di ricezione della richiesta ARP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-447">This event represents an internal NetX ARP request receive event.</span></span>

<span data-ttu-id="213c9-448">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-448">**Information Fields**</span></span>

- <span data-ttu-id="213c9-449">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-449">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-450">Informazioni sul campo 2: indirizzo IP di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-450">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="213c9-451">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-451">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-452">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-452">Info Field 4: Not used</span></span>

### <a name="internal-arp-request-send"></a><span data-ttu-id="213c9-453">Invio richiesta ARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-453">Internal ARP Request Send</span></span> 

#### <a name="internal-arp-request-send"></a><span data-ttu-id="213c9-454">Invio richiesta ARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-454">Internal ARP request send</span></span>

<span data-ttu-id="213c9-455">**Icona** ![ di Icona di invio richiesta ARP interna](./media/user-guide/netx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-455">**Icon** ![Internal ARP request send icon](./media/user-guide/netx-events/image2.png)</span></span>

<span data-ttu-id="213c9-456">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-456">**Description**</span></span>

<span data-ttu-id="213c9-457">Questo evento rappresenta un evento di invio della richiesta ARP NetX interna.</span><span class="sxs-lookup"><span data-stu-id="213c9-457">This event represents an internal NetX ARP request send event.</span></span>

<span data-ttu-id="213c9-458">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-458">**Information Fields**</span></span>

- <span data-ttu-id="213c9-459">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-459">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-460">Informazioni sul campo 2: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-460">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="213c9-461">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-461">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-462">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-462">Info Field 4: Not used</span></span>

### <a name="internal-arp-response-receive"></a><span data-ttu-id="213c9-463">Ricezione risposta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-463">Internal ARP Response Receive</span></span> 

#### <a name="internal-arp-request-receive"></a><span data-ttu-id="213c9-464">Ricezione richiesta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-464">Internal ARP request receive</span></span>

<span data-ttu-id="213c9-465">**Icona** ![ di Icona di ricezione della richiesta ARP interna](./media/user-guide/netx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-465">**Icon** ![The Internal ARP request receive icon](./media/user-guide/netx-events/image3.png)</span></span>

<span data-ttu-id="213c9-466">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-466">**Description**</span></span>

<span data-ttu-id="213c9-467">Questo evento rappresenta un evento interno di ricezione della risposta ARP NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-467">This event represents an internal NetX ARP response receive event.</span></span>

<span data-ttu-id="213c9-468">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-468">**Information Fields**</span></span>

- <span data-ttu-id="213c9-469">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-469">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-470">Informazioni sul campo 2: indirizzo IP di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-470">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="213c9-471">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-471">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-472">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-472">Info Field 4: Not used</span></span>

### <a name="internal-arp-response-send"></a><span data-ttu-id="213c9-473">Invio risposta ARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-473">Internal ARP Response Send</span></span> 

#### <a name="internal-arp-request-send"></a><span data-ttu-id="213c9-474">Invio richiesta ARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-474">Internal ARP request send</span></span>

<span data-ttu-id="213c9-475">**Icona** ![ di Icona di invio della richiesta ARP interna](./media/user-guide/netx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-475">**Icon** ![The Internal ARP request send icon](./media/user-guide/netx-events/image4.png)</span></span>

<span data-ttu-id="213c9-476">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-476">**Description**</span></span>

<span data-ttu-id="213c9-477">Questo evento rappresenta un evento di invio risposta NetX interna.</span><span class="sxs-lookup"><span data-stu-id="213c9-477">This event represents an internal NetX response send event.</span></span>

<span data-ttu-id="213c9-478">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-478">**Information Fields**</span></span>

- <span data-ttu-id="213c9-479">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-479">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-480">Informazioni sul campo 2: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-480">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="213c9-481">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-481">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-482">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-482">Info Field 4: Not used</span></span>

### <a name="internal-icmp-receive"></a><span data-ttu-id="213c9-483">Ricezione ICMP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-483">Internal ICMP Receive</span></span> 

#### <a name="internal-icmp-receive"></a><span data-ttu-id="213c9-484">Ricezione ICMP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-484">Internal ICMP receive</span></span>

<span data-ttu-id="213c9-485">**Icona** ![ di Icona di ricezione interno I C M P](./media/user-guide/netx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-485">**Icon** ![Internal I C M P receive icon](./media/user-guide/netx-events/image5.png)</span></span>

<span data-ttu-id="213c9-486">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-486">**Description**</span></span>

<span data-ttu-id="213c9-487">Questo evento rappresenta un evento di ricezione ICMP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-487">This event represents an internal NetX ICMP receive event.</span></span>

<span data-ttu-id="213c9-488">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-488">**Information Fields**</span></span>

- <span data-ttu-id="213c9-489">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-489">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-490">Informazioni sul campo 2: indirizzo IP di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-490">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="213c9-491">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-491">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-492">Informazioni sul campo 4: Word 0 dell'intestazione ICMP</span><span class="sxs-lookup"><span data-stu-id="213c9-492">Info Field 4: Word 0 of ICMP header</span></span>

### <a name="internal-icmp-send"></a><span data-ttu-id="213c9-493">Invio ICMP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-493">Internal ICMP Send</span></span> 

#### <a name="internal-icmp-send"></a><span data-ttu-id="213c9-494">Invio ICMP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-494">Internal ICMP send</span></span>

<span data-ttu-id="213c9-495">**Icona** ![ di Icona di invio C M P interna](./media/user-guide/netx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-495">**Icon** ![Internal I C M P send icon](./media/user-guide/netx-events/image6.png)</span></span>

<span data-ttu-id="213c9-496">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-496">**Description**</span></span>

<span data-ttu-id="213c9-497">Questo evento rappresenta un evento di invio ICMP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-497">This event represents an internal NetX ICMP send event.</span></span>

<span data-ttu-id="213c9-498">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-498">**Information Fields**</span></span>

- <span data-ttu-id="213c9-499">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-499">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-500">Informazioni sul campo 2: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-500">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="213c9-501">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-501">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-502">Informazioni sul campo 4: Word 0 dell'intestazione ICMP</span><span class="sxs-lookup"><span data-stu-id="213c9-502">Info Field 4: Word 0 of ICMP header</span></span>

### <a name="internal-igmp-receive"></a><span data-ttu-id="213c9-503">Ricezione IGMP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-503">Internal IGMP Receive</span></span> 

#### <a name="internal-igmp-receive"></a><span data-ttu-id="213c9-504">Ricezione IGMP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-504">Internal IGMP receive</span></span>

<span data-ttu-id="213c9-505">**Icona** ![ di Icona di ricezione I G M interna](./media/user-guide/netx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-505">**Icon** ![Internal I G M P receive icon](./media/user-guide/netx-events/image7.png)</span></span>

<span data-ttu-id="213c9-506">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-506">**Description**</span></span>

<span data-ttu-id="213c9-507">Questo evento rappresenta un evento di ricezione IGMP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-507">This event represents an internal NetX IGMP receive event.</span></span>

<span data-ttu-id="213c9-508">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-508">**Information Fields**</span></span>

- <span data-ttu-id="213c9-509">Campo informazioni 1: puntatore IP</span><span class="sxs-lookup"><span data-stu-id="213c9-509">Info Field 1: IP Pointer</span></span>
- <span data-ttu-id="213c9-510">Informazioni sul campo 2: indirizzo IP di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-510">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="213c9-511">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-511">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-512">Informazioni sul campo 4: parola 0 dell'intestazione IGMP</span><span class="sxs-lookup"><span data-stu-id="213c9-512">Info Field 4: Word 0 of IGMP header</span></span>

### <a name="internal-ip-receive"></a><span data-ttu-id="213c9-513">Ricezione IP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-513">Internal IP Receive</span></span> 

#### <a name="internal-ip-receive"></a><span data-ttu-id="213c9-514">Ricezione IP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-514">Internal IP receive</span></span>

<span data-ttu-id="213c9-515">**Icona** ![ di Icona di ricezione I P interni](./media/user-guide/netx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-515">**Icon** ![Internal I P receive icon](./media/user-guide/netx-events/image8.png)</span></span>

<span data-ttu-id="213c9-516">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-516">**Description**</span></span>

<span data-ttu-id="213c9-517">Questo evento rappresenta un evento di ricezione IP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-517">This event represents an internal NetX IP receive event.</span></span>

<span data-ttu-id="213c9-518">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-518">**Information Fields**</span></span>

- <span data-ttu-id="213c9-519">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-519">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-520">Informazioni sul campo 2: indirizzo IP di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-520">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="213c9-521">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-521">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-522">Campo dati 4: lunghezza pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-522">Info Field 4: Packet length</span></span>

### <a name="internal-ip-send"></a><span data-ttu-id="213c9-523">Invio IP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-523">Internal IP Send</span></span>

#### <a name="internal-ip-send"></a><span data-ttu-id="213c9-524">Invio IP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-524">Internal IP send</span></span>

<span data-ttu-id="213c9-525">**Icona** ![ di Icona di invio di I P interni](./media/user-guide/netx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-525">**Icon** ![Internal I P send icon](./media/user-guide/netx-events/image9.png)</span></span>

<span data-ttu-id="213c9-526">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-526">**Description**</span></span>

<span data-ttu-id="213c9-527">Questo evento rappresenta un evento di invio IP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-527">This event represents an internal NetX IP send event.</span></span>

<span data-ttu-id="213c9-528">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-528">**Information Fields**</span></span>

- <span data-ttu-id="213c9-529">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-529">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-530">Informazioni sul campo 2: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-530">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="213c9-531">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-531">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-532">Campo dati 4: lunghezza pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-532">Info Field 4: Packet length</span></span>

### <a name="internal-tcp-data-receive"></a><span data-ttu-id="213c9-533">Ricezione di dati TCP interni</span><span class="sxs-lookup"><span data-stu-id="213c9-533">Internal TCP Data Receive</span></span> 

#### <a name="internal-tcp-data-receive"></a><span data-ttu-id="213c9-534">Ricezione di dati TCP interni</span><span class="sxs-lookup"><span data-stu-id="213c9-534">Internal TCP Data Receive</span></span>

<span data-ttu-id="213c9-535">**Icona** ![ di Icona di ricezione dati T C P interna](./media/user-guide/netx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-535">**Icon** ![Internal T C P data receive icon](./media/user-guide/netx-events/image10.png)</span></span>

<span data-ttu-id="213c9-536">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-536">**Description**</span></span>

<span data-ttu-id="213c9-537">Questo evento rappresenta un evento di ricezione dati TCP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-537">This event represents an internal NetX TCP data receive event.</span></span>

<span data-ttu-id="213c9-538">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-538">**Information Fields**</span></span>

- <span data-ttu-id="213c9-539">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-539">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-540">Informazioni sul campo 2: indirizzo IP di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-540">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="213c9-541">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-541">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-542">Campo dati 4: numero di sequenza di ricezione</span><span class="sxs-lookup"><span data-stu-id="213c9-542">Info Field 4: Receive sequence number</span></span>

### <a name="internal-tcp-data-send"></a><span data-ttu-id="213c9-543">Trasmissione dati TCP interni</span><span class="sxs-lookup"><span data-stu-id="213c9-543">Internal TCP data send</span></span> 

#### <a name="internal-tcp-data-send"></a><span data-ttu-id="213c9-544">Trasmissione dati TCP interni</span><span class="sxs-lookup"><span data-stu-id="213c9-544">Internal TCP Data Send</span></span>

<span data-ttu-id="213c9-545">**Icona** ![ di Icona di invio dati T C P interna](./media/user-guide/netx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-545">**Icon** ![Internal T C P data send icon](./media/user-guide/netx-events/image11.png)</span></span>

<span data-ttu-id="213c9-546">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-546">**Description**</span></span>

<span data-ttu-id="213c9-547">Questo evento rappresenta un evento di trasmissione dati TCP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-547">This event represents an internal NetX TCP data send event.</span></span>

<span data-ttu-id="213c9-548">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-548">**Information Fields**</span></span>

- <span data-ttu-id="213c9-549">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-549">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-550">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-550">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-551">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-551">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-552">Campo informazioni 4: numero di sequenza di trasmissione</span><span class="sxs-lookup"><span data-stu-id="213c9-552">Info Field 4: Transmit sequence number</span></span>

### <a name="internal-tcp-fin-receive"></a><span data-ttu-id="213c9-553">Ricezione dell'aletta TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-553">Internal TCP FIN Receive</span></span> 

#### <a name="internal-tcp-fin-receive"></a><span data-ttu-id="213c9-554">Ricezione dell'aletta TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-554">Internal TCP fin receive</span></span>

<span data-ttu-id="213c9-555">**Icona** ![ di Icona di ricezione T C P interna](./media/user-guide/netx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-555">**Icon** ![Internal T C P F I N receive icon](./media/user-guide/netx-events/image12.png)</span></span>

<span data-ttu-id="213c9-556">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-556">**Description**</span></span>

<span data-ttu-id="213c9-557">Questo evento rappresenta un evento interno di ricezione di NetX TCP.</span><span class="sxs-lookup"><span data-stu-id="213c9-557">This event represents an internal NetX TCP FIN receive event.</span></span>

<span data-ttu-id="213c9-558">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-558">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-559">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-559">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-560">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-560">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-561">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-561">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-562">Campo dati 4: numero di sequenza di ricezione</span><span class="sxs-lookup"><span data-stu-id="213c9-562">Info Field 4: Receive sequence number</span></span>

### <a name="internal-tcp-fin-send"></a><span data-ttu-id="213c9-563">Trasmissione aletta TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-563">Internal TCP FIN Send</span></span> 

#### <a name="internal-tcp-fin-send"></a><span data-ttu-id="213c9-564">Trasmissione aletta TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-564">Internal TCP fin send</span></span>

<span data-ttu-id="213c9-565">**Icona** ![ di Icona di invio T C P F I N](./media/user-guide/netx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-565">**Icon** ![Internal T C P F I N send icon](./media/user-guide/netx-events/image13.png)</span></span>

<span data-ttu-id="213c9-566">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-566">**Description**</span></span>

<span data-ttu-id="213c9-567">Questo evento rappresenta un evento NetX TCP aletta di invio interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-567">This event represents an internal NetX TCP FIN send event.</span></span>

<span data-ttu-id="213c9-568">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-568">**Information Fields**</span></span>

- <span data-ttu-id="213c9-569">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-569">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-570">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-570">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-571">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-571">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-572">Campo informazioni 4: numero di sequenza di trasmissione</span><span class="sxs-lookup"><span data-stu-id="213c9-572">Info Field 4:Transmit sequence number</span></span>

### <a name="internal-tcp-rst-receive"></a><span data-ttu-id="213c9-573">Ricezione RST TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-573">Internal TCP RST Receive</span></span> 

#### <a name="internal-tcp-rst-receive"></a><span data-ttu-id="213c9-574">Ricezione RST TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-574">Internal TCP RST receive</span></span>

<span data-ttu-id="213c9-575">**Icona** ![ di Icona di ricezione T C P R S interna](./media/user-guide/netx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-575">**Icon** ![Internal T C P R S T receive icon](./media/user-guide/netx-events/image14.png)</span></span>

<span data-ttu-id="213c9-576">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-576">**Description**</span></span>

<span data-ttu-id="213c9-577">Questo evento rappresenta un evento interno di ricezione della reimpostazione di NetX TCP.</span><span class="sxs-lookup"><span data-stu-id="213c9-577">This event represents an internal NetX TCP reset receive event.</span></span>

<span data-ttu-id="213c9-578">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-578">**Information Fields**</span></span>

- <span data-ttu-id="213c9-579">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-579">Info Field 1: Pointer to the IP instance.</span></span>
- <span data-ttu-id="213c9-580">Informazioni sul campo 2: puntatore al socket.</span><span class="sxs-lookup"><span data-stu-id="213c9-580">Info Field 2: Pointer to socket.</span></span>
- <span data-ttu-id="213c9-581">Informazioni sul campo 3: puntatore al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="213c9-581">Info Field 3: Pointer to packet.</span></span>
- <span data-ttu-id="213c9-582">Informazioni sul campo 4: numero di sequenza di ricezione.</span><span class="sxs-lookup"><span data-stu-id="213c9-582">Info Field 4: Receive sequence number.</span></span>

### <a name="internal-tcp-rst-send"></a><span data-ttu-id="213c9-583">Trasmissione RST TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-583">Internal TCP RST Send</span></span> 

#### <a name="internal-tcp-rst-send"></a><span data-ttu-id="213c9-584">Trasmissione RST TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-584">Internal TCP RST send</span></span>

<span data-ttu-id="213c9-585">**Icona** ![ di Icona di invio T C P R S interna](./media/user-guide/netx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-585">**Icon** ![Internal T C P R S T send icon](./media/user-guide/netx-events/image15.png)</span></span>

<span data-ttu-id="213c9-586">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-586">**Description**</span></span>

<span data-ttu-id="213c9-587">Questo evento rappresenta un evento di invio di reimpostazione TCP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-587">This event represents an internal NetX TCP reset send event.</span></span>

<span data-ttu-id="213c9-588">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-588">**Information Fields**</span></span>

- <span data-ttu-id="213c9-589">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-589">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-590">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-590">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-591">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-591">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-592">Campo informazioni 4: numero di sequenza di trasmissione</span><span class="sxs-lookup"><span data-stu-id="213c9-592">Info Field 4: Transmit sequence number</span></span>

### <a name="internal-tcp-syn-receive"></a><span data-ttu-id="213c9-593">Ricezione SYN TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-593">Internal TCP SYN Receive</span></span> 

#### <a name="internal-tcp-syn-receive"></a><span data-ttu-id="213c9-594">Ricezione SYN TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-594">Internal TCP SYN receive</span></span>

<span data-ttu-id="213c9-595">**Icona** ![ di Icona di ricezione T C P S interna](./media/user-guide/netx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-595">**Icon** ![Internal T C P S Y N receive icon](./media/user-guide/netx-events/image16.png)</span></span>

<span data-ttu-id="213c9-596">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-596">**Description**</span></span>

<span data-ttu-id="213c9-597">Questo evento rappresenta un evento NetX TCP SYN Receive interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-597">This event represents an internal NetX TCP SYN receive event.</span></span>

<span data-ttu-id="213c9-598">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-598">**Information Fields**</span></span>

- <span data-ttu-id="213c9-599">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-599">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-600">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-600">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-601">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-601">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-602">Campo dati 4: numero di sequenza di ricezione</span><span class="sxs-lookup"><span data-stu-id="213c9-602">Info Field 4: Receive sequence number</span></span>

### <a name="internal-tcp-syn-send"></a><span data-ttu-id="213c9-603">Trasmissione SYN TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-603">Internal TCP SYN Send</span></span> 

#### <a name="internal-tcp-syn-send"></a><span data-ttu-id="213c9-604">Trasmissione SYN TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-604">Internal TCP SYN send</span></span>

<span data-ttu-id="213c9-605">**Icona** ![ di Icona di invio T C P S interna](./media/user-guide/netx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-605">**Icon** ![Internal T C P S Y N send icon](./media/user-guide/netx-events/image17.png)</span></span>

<span data-ttu-id="213c9-606">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-606">**Description**</span></span>

<span data-ttu-id="213c9-607">Questo evento rappresenta un evento interno NetX TCP SYN Send.</span><span class="sxs-lookup"><span data-stu-id="213c9-607">This event represents an internal NetX TCP SYN send event.</span></span>

<span data-ttu-id="213c9-608">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="213c9-608">Information Fields</span></span> 

- <span data-ttu-id="213c9-609">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-609">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-610">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-610">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-611">Info Field 3: puntatore a Packet-Info Field 4: trasmissione numero di sequenza</span><span class="sxs-lookup"><span data-stu-id="213c9-611">Info Field 3: Pointer to packet -Info Field 4: Transmit sequence number</span></span>

### <a name="internal-udp-receive"></a><span data-ttu-id="213c9-612">Ricezione UDP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-612">Internal UDP Receive</span></span> 

#### <a name="internal-udp-receive"></a><span data-ttu-id="213c9-613">Ricezione UDP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-613">Internal UDP receive</span></span>

<span data-ttu-id="213c9-614">**Icona** ![ di Icona di ricezione U D P interna](./media/user-guide/netx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-614">**Icon** ![Internal U D P receive icon](./media/user-guide/netx-events/image18.png)</span></span>

<span data-ttu-id="213c9-615">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-615">**Description**</span></span>

<span data-ttu-id="213c9-616">Questo evento rappresenta un evento di ricezione UDP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-616">This event represents an internal NetX UDP receive event.</span></span>

<span data-ttu-id="213c9-617">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-617">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-618">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-618">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-619">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-619">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-620">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-620">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-621">Informazioni sul campo 4: Word 0 dell'intestazione UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-621">Info Field 4: Word 0 of UDP header</span></span>

### <a name="internal-udp-send"></a><span data-ttu-id="213c9-622">Invio UDP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-622">Internal UDP Send</span></span> 

#### <a name="internal-udp-send"></a><span data-ttu-id="213c9-623">Invio UDP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-623">Internal UDP send</span></span>

<span data-ttu-id="213c9-624">**Icona** ![ di Icona di invio di U D P interna](./media/user-guide/netx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-624">**Icon** ![Internal U D P send icon](./media/user-guide/netx-events/image19.png)</span></span>

<span data-ttu-id="213c9-625">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-625">**Description**</span></span>

<span data-ttu-id="213c9-626">Questo evento rappresenta un evento di trasmissione UDP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-626">This event represents an internal NetX UDP send event.</span></span>

<span data-ttu-id="213c9-627">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-627">**Information Fields**</span></span>

- <span data-ttu-id="213c9-628">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-628">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-629">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-629">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-630">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-630">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-631">Informazioni sul campo 4: Word 0 dell'intestazione UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-631">Info Field 4: Word 0 of UDP header</span></span>

### <a name="internal-rarp-receive"></a><span data-ttu-id="213c9-632">Ricezione RARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-632">Internal RARP Receive</span></span> 

#### <a name="internal-rarp-receive"></a><span data-ttu-id="213c9-633">Ricezione RARP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-633">Internal RARP receive</span></span> 

<span data-ttu-id="213c9-634">**Icona** ![ di Icona di ricezione r P interna](./media/user-guide/netx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-634">**Icon** ![Internal R A R P receive icon](./media/user-guide/netx-events/image20.png)</span></span>

<span data-ttu-id="213c9-635">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-635">**Description**</span></span>

<span data-ttu-id="213c9-636">Questo evento rappresenta un evento di ricezione RARP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-636">This event represents an internal NetX RARP receive event.</span></span>

<span data-ttu-id="213c9-637">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-637">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-638">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-638">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-639">Informazioni sul campo 2: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-639">Info Field 2: Target IP address</span></span>
- <span data-ttu-id="213c9-640">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-640">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-641">Campo informazioni 4: parola 1 dell'intestazione RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-641">Info Field 4: Word 1 of RARP header</span></span>

### <a name="internal-rarp-send"></a><span data-ttu-id="213c9-642">Invio RARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-642">Internal RARP Send</span></span> 

#### <a name="internal-rarp-send"></a><span data-ttu-id="213c9-643">Invio RARP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-643">Internal RARP send</span></span> 

<span data-ttu-id="213c9-644">**Icona** ![ di Icona interna R A R P Send](./media/user-guide/netx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-644">**Icon** ![Internal R A R P send icon](./media/user-guide/netx-events/image21.png)</span></span>

<span data-ttu-id="213c9-645">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-645">**Description**</span></span>

<span data-ttu-id="213c9-646">Questo evento rappresenta un evento di invio NetX RARP interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-646">This event represents an internal NetX RARP send event.</span></span>

<span data-ttu-id="213c9-647">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-647">**Information Fields**</span></span>

- <span data-ttu-id="213c9-648">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-648">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-649">Informazioni sul campo 2: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-649">Info Field 2: Target IP address</span></span>
- <span data-ttu-id="213c9-650">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-650">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-651">Campo informazioni 4: parola 1 dell'intestazione RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-651">Info Field 4: Word 1 of RARP header</span></span>

### <a name="internal-tcp-retry"></a><span data-ttu-id="213c9-652">Tentativo TCP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-652">Internal TCP Retry</span></span> 

#### <a name="internal-tcp-retry"></a><span data-ttu-id="213c9-653">Tentativo TCP interno</span><span class="sxs-lookup"><span data-stu-id="213c9-653">Internal TCP retry</span></span> 

<span data-ttu-id="213c9-654">**Icona** ![ di Icona di ripetizione dei tentativi interna di T C](./media/user-guide/netx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-654">**Icon** ![Internal T C P retry icon](./media/user-guide/netx-events/image22.png)</span></span>

<span data-ttu-id="213c9-655">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-655">**Description**</span></span>

<span data-ttu-id="213c9-656">Questo evento rappresenta un evento di ripetizione NetX TCP interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-656">This event represents an internal NetX TCP retry event.</span></span>

<span data-ttu-id="213c9-657">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-657">**Information Fields**</span></span>
- <span data-ttu-id="213c9-658">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-658">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-659">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-659">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-660">Informazioni sul campo 3: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-660">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="213c9-661">Campo informazioni 4: numero di tentativi</span><span class="sxs-lookup"><span data-stu-id="213c9-661">Info Field 4: Number of retries</span></span>

### <a name="internal-tcp-state-change"></a><span data-ttu-id="213c9-662">Modifica dello stato TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-662">Internal TCP State Change</span></span> 

#### <a name="internal-tcp-state-change"></a><span data-ttu-id="213c9-663">Modifica dello stato TCP interna</span><span class="sxs-lookup"><span data-stu-id="213c9-663">Internal TCP state change</span></span> 

<span data-ttu-id="213c9-664">**Icona** ![ di Icona di modifica dello stato T C P interno](./media/user-guide/netx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-664">**Icon** ![Internal T C P state change icon](./media/user-guide/netx-events/image23.png)</span></span>

<span data-ttu-id="213c9-665">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-665">**Description**</span></span>

<span data-ttu-id="213c9-666">Questo evento rappresenta un evento di modifica dello stato del socket TCP NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-666">This event represents an internal NetX TCP socket state change event.</span></span>

<span data-ttu-id="213c9-667">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-667">**Information Fields**</span></span>

- <span data-ttu-id="213c9-668">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-668">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-669">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-669">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-670">Informazioni sul campo 3: stato precedente</span><span class="sxs-lookup"><span data-stu-id="213c9-670">Info Field 3: Previous state</span></span>
- <span data-ttu-id="213c9-671">Campo informazioni 4: nuovo stato</span><span class="sxs-lookup"><span data-stu-id="213c9-671">Info Field 4: New state</span></span>

### <a name="internal-io-driver-packet-send"></a><span data-ttu-id="213c9-672">Invio di pacchetti di driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="213c9-672">Internal I/O Driver Packet Send</span></span> 

#### <a name="internal-io-driver-packet-send"></a><span data-ttu-id="213c9-673">Invio di pacchetti di driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="213c9-673">Internal I/O driver packet send</span></span>

<span data-ttu-id="213c9-674">**Icona** ![ di Icona di invio pacchetti driver I/O interno](./media/user-guide/netx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-674">**Icon** ![Internal I / O driver packet send icon](./media/user-guide/netx-events/image24.png)</span></span>

<span data-ttu-id="213c9-675">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-675">**Description**</span></span>

<span data-ttu-id="213c9-676">Questo evento rappresenta un evento di invio di pacchetti di driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-676">This event represents an internal NetX I/O driver packet send event.</span></span>

<span data-ttu-id="213c9-677">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-677">**Information Fields**</span></span>

- <span data-ttu-id="213c9-678">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-678">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-679">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-679">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-680">Informazioni sul campo 3: dimensioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-680">Info Field 3: Packet size</span></span>
- <span data-ttu-id="213c9-681">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-681">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-initialize"></a><span data-ttu-id="213c9-682">Inizializzazione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-682">Internal I/O Driver Initialize</span></span> 

#### <a name="internal-io-driver-initialize"></a><span data-ttu-id="213c9-683">Inizializzazione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-683">Internal I/O driver initialize</span></span>

<span data-ttu-id="213c9-684">**Icona** ![ di Icona di inizializzazione del driver I/O interno](./media/user-guide/netx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-684">**Icon** ![Internal I / O driver initialize icon](./media/user-guide/netx-events/image25.png)</span></span>

<span data-ttu-id="213c9-685">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-685">**Description**</span></span>

<span data-ttu-id="213c9-686">Questo evento rappresenta un evento di inizializzazione del driver I/O interno di NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-686">This event represents an internal NetX I/O driver initialize event.</span></span>

<span data-ttu-id="213c9-687">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-687">**Information Fields**</span></span>

- <span data-ttu-id="213c9-688">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-688">Info Field 1: Pointer to the IP instance.</span></span>
- <span data-ttu-id="213c9-689">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-689">Info Field 2: Not used.</span></span>
- <span data-ttu-id="213c9-690">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-690">Info Field 3: Not used.</span></span>
- <span data-ttu-id="213c9-691">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-691">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-link-enable"></a><span data-ttu-id="213c9-692">Abilitazione collegamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-692">Internal I/O Driver Link Enable</span></span> 

#### <a name="internal-io-driver-link-enable"></a><span data-ttu-id="213c9-693">Abilitazione collegamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-693">Internal I/O driver link enable</span></span>

<span data-ttu-id="213c9-694">**Icona** ![ di Icona Abilita collegamento driver I/O interno](./media/user-guide/netx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-694">**Icon** ![Internal I / O driver link enable icon](./media/user-guide/netx-events/image26.png)</span></span>

<span data-ttu-id="213c9-695">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-695">**Description**</span></span>

<span data-ttu-id="213c9-696">Questo evento rappresenta un evento di abilitazione del collegamento del driver I/O interno di NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-696">This event represents an internal NetX I/O driver link enable event.</span></span>

<span data-ttu-id="213c9-697">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-697">**Information Fields**</span></span>

- <span data-ttu-id="213c9-698">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-698">Info Field 1: Pointer to the IP instance.</span></span>
- <span data-ttu-id="213c9-699">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-699">Info Field 2: Not used.</span></span>
- <span data-ttu-id="213c9-700">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-700">Info Field 3: Not used.</span></span>
- <span data-ttu-id="213c9-701">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-701">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-link-disable"></a><span data-ttu-id="213c9-702">Disabilitazione collegamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-702">Internal I/O Driver Link Disable</span></span> 

#### <a name="internal-io-driver-link-disable"></a><span data-ttu-id="213c9-703">Disabilitazione collegamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-703">Internal I/O driver link disable</span></span>

<span data-ttu-id="213c9-704">**Icona** ![ di Icona di disabilitazione collegamento driver I/O interno](./media/user-guide/netx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-704">**Icon** ![Internal I / O driver link disable icon](./media/user-guide/netx-events/image27.png)</span></span>

<span data-ttu-id="213c9-705">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-705">**Description**</span></span>

<span data-ttu-id="213c9-706">Questo evento rappresenta un evento di disabilitazione del collegamento del driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-706">This event represents an internal NetX I/O driver link disable event.</span></span>

<span data-ttu-id="213c9-707">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-707">**Information Fields**</span></span>

- <span data-ttu-id="213c9-708">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-708">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-709">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-709">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-710">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-710">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-711">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-711">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-packet-broadcast"></a><span data-ttu-id="213c9-712">Trasmissione di pacchetti di driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="213c9-712">Internal I/O Driver Packet Broadcast</span></span> 

#### <a name="internal-io-driver-packet-broadcast"></a><span data-ttu-id="213c9-713">Trasmissione di pacchetti di driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="213c9-713">Internal I/O driver packet broadcast</span></span>

<span data-ttu-id="213c9-714">**Icona** ![ di Icona trasmissione pacchetti I/O interno](./media/user-guide/netx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-714">**Icon** ![Internal I / O driver packet broadcast icon](./media/user-guide/netx-events/image28.png)</span></span>

<span data-ttu-id="213c9-715">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-715">**Description**</span></span>

<span data-ttu-id="213c9-716">Questo evento rappresenta un evento interno di trasmissione pacchetti di driver I/O di NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-716">This event represents an internal NetX I/O driver packet broadcast event.</span></span>

<span data-ttu-id="213c9-717">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-717">**Information Fields**</span></span>

- <span data-ttu-id="213c9-718">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-718">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-719">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-719">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-720">Informazioni sul campo 3: dimensioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-720">Info Field 3: Packet size</span></span>
- <span data-ttu-id="213c9-721">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-721">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-arp-send"></a><span data-ttu-id="213c9-722">Invio ARP driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-722">Internal I/O Driver ARP Send</span></span> 

#### <a name="internal-io-driver-arp-send"></a><span data-ttu-id="213c9-723">Invio ARP driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-723">Internal I/O driver ARP send</span></span>

<span data-ttu-id="213c9-724">**Icona** ![ di Icona di trasmissione ARP driver I/O interno](./media/user-guide/netx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-724">**Icon** ![Internal I / O driver ARP send icon](./media/user-guide/netx-events/image29.png)</span></span>

<span data-ttu-id="213c9-725">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-725">**Description**</span></span>

<span data-ttu-id="213c9-726">Questo evento rappresenta un evento di invio ARP di un driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-726">This event represents an internal NetX I/O driver ARP send event.</span></span>

<span data-ttu-id="213c9-727">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-727">**Information Fields**</span></span>

- <span data-ttu-id="213c9-728">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-728">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-729">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-729">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-730">Informazioni sul campo 3: dimensioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-730">Info Field 3: Packet size</span></span>
- <span data-ttu-id="213c9-731">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-731">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-arp-response-send"></a><span data-ttu-id="213c9-732">Invio risposta ARP driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-732">Internal I/O Driver ARP Response Send</span></span> 

#### <a name="internal-io-driver-arp-response-send"></a><span data-ttu-id="213c9-733">Invio risposta ARP driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-733">Internal I/O driver ARP response send</span></span>

<span data-ttu-id="213c9-734">**Icona** ![ di Icona di invio risposta ARP driver I/O interno](./media/user-guide/netx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-734">**Icon** ![Internal I / O driver ARP response send icon](./media/user-guide/netx-events/image30.png)</span></span>

<span data-ttu-id="213c9-735">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-735">**Description**</span></span>

<span data-ttu-id="213c9-736">Questo evento rappresenta un evento di invio risposta ARP di un driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-736">This event represents an internal NetX I/O driver ARP response send event.</span></span>

<span data-ttu-id="213c9-737">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-737">**Information Fields**</span></span>

- <span data-ttu-id="213c9-738">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-738">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-739">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-739">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-740">Informazioni sul campo 3: dimensioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-740">Info Field 3: Packet size</span></span>
- <span data-ttu-id="213c9-741">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-741">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-rarp-send"></a><span data-ttu-id="213c9-742">Invio di un driver di I/O interno RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-742">Internal I/O Driver RARP Send</span></span> 

#### <a name="internal-io-driver-rarp-send"></a><span data-ttu-id="213c9-743">Invio di un driver di I/O interno RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-743">Internal I/O driver RARP send</span></span>

<span data-ttu-id="213c9-744">**Icona** ![ di Icona di invio RARP driver I/O interno](./media/user-guide/netx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-744">**Icon** ![Internal I / O driver RARP send icon](./media/user-guide/netx-events/image31.png)</span></span>

<span data-ttu-id="213c9-745">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-745">**Description**</span></span>

<span data-ttu-id="213c9-746">Questo evento rappresenta un evento di trasmissione RARP NetX I/O driver interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-746">This event represents an internal NetX I/O driver RARP send event.</span></span>

<span data-ttu-id="213c9-747">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-747">**Information Fields**</span></span>

- <span data-ttu-id="213c9-748">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-748">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-749">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-749">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-750">Informazioni sul campo 3: dimensioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-750">Info Field 3: Packet size</span></span>
- <span data-ttu-id="213c9-751">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-751">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-multicast-join"></a><span data-ttu-id="213c9-752">Join multicast driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-752">Internal I/O Driver Multicast Join</span></span> 

#### <a name="internal-io-driver-multicast-join"></a><span data-ttu-id="213c9-753">Join multicast driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-753">Internal I/O driver multicast join</span></span>

<span data-ttu-id="213c9-754">**Icona** ![ di Icona di join multicast driver I/O interno](./media/user-guide/netx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-754">**Icon** ![Internal I / O driver multicast join icon](./media/user-guide/netx-events/image32.png)</span></span>

<span data-ttu-id="213c9-755">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-755">**Description**</span></span>

<span data-ttu-id="213c9-756">Questo evento rappresenta un evento interno di join multicast driver I/O di NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-756">This event represents an internal NetX I/O driver multicast join event.</span></span>

<span data-ttu-id="213c9-757">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-757">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-758">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-758">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-759">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-759">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-760">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-760">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-761">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-761">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-multicast-leave"></a><span data-ttu-id="213c9-762">Uscita multicast driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-762">Internal I/O Driver Multicast Leave</span></span> 

#### <a name="internal-io-driver-multicast-leave"></a><span data-ttu-id="213c9-763">Uscita multicast driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-763">Internal I/O driver multicast leave</span></span>

<span data-ttu-id="213c9-764">**Icona** ![ di Icona di uscita multicast driver I/O interno](./media/user-guide/netx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-764">**Icon** ![Internal I / O driver multicast leave icon](./media/user-guide/netx-events/image33.png)</span></span>

<span data-ttu-id="213c9-765">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-765">**Description**</span></span>

<span data-ttu-id="213c9-766">Questo evento rappresenta un evento di uscita multicast del driver I/O interno di NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-766">This event represents an internal NetX I/O driver multicast leave event.</span></span>

<span data-ttu-id="213c9-767">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-767">**Information Fields**</span></span>

- <span data-ttu-id="213c9-768">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-768">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-769">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-769">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-770">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-770">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-771">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-771">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-status"></a><span data-ttu-id="213c9-772">Stato Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-772">Internal I/O Driver Get Status</span></span> 

#### <a name="internal-io-driver-get-status"></a><span data-ttu-id="213c9-773">Stato Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-773">Internal I/O driver get status</span></span>

<span data-ttu-id="213c9-774">**Icona** ![ di Icona di Ottieni stato driver I/O interno](./media/user-guide/netx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-774">**Icon** ![Internal I / O driver get status icon](./media/user-guide/netx-events/image34.png)</span></span>

<span data-ttu-id="213c9-775">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-775">**Description**</span></span>

<span data-ttu-id="213c9-776">Questo evento rappresenta un evento di stato Get driver I/O interno NetX.</span><span class="sxs-lookup"><span data-stu-id="213c9-776">This event represents an internal NetX I/O driver get status event.</span></span>

<span data-ttu-id="213c9-777">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-777">**Information Fields**</span></span>

- <span data-ttu-id="213c9-778">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-778">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-779">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-779">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-780">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-780">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-781">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-781">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-speed"></a><span data-ttu-id="213c9-782">Velocità di ottenimento del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-782">Internal I/O Driver Get Speed</span></span> 

#### <a name="internal-io-driver-get-speed"></a><span data-ttu-id="213c9-783">Velocità di ottenimento del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-783">Internal I/O driver get speed</span></span>

<span data-ttu-id="213c9-784">**Icona** ![ di Icona di Ottieni velocità driver I/O interno](./media/user-guide/netx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-784">**Icon** ![Internal I / O driver get speed icon](./media/user-guide/netx-events/image35.png)</span></span>

<span data-ttu-id="213c9-785">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-785">**Description**</span></span>

<span data-ttu-id="213c9-786">Questo evento rappresenta un evento di velocità di ottenimento di un driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-786">This event represents an internal NetX I/O driver get speed event.</span></span>

<span data-ttu-id="213c9-787">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-787">**Information Fields**</span></span>

- <span data-ttu-id="213c9-788">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-788">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-789">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-789">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-790">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-790">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-791">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-791">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-duplex-type"></a><span data-ttu-id="213c9-792">Tipo duplex Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-792">Internal I/O Driver Get Duplex Type</span></span> 

#### <a name="internal-io-driver-get-duplex-type"></a><span data-ttu-id="213c9-793">Tipo duplex Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-793">Internal I/O driver get duplex type</span></span>

<span data-ttu-id="213c9-794">**Icona** ![ di Icona del tipo di driver di I/O interno Get duplex](./media/user-guide/netx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-794">**Icon** ![Internal I / O driver get duplex type icon](./media/user-guide/netx-events/image36.png)</span></span>

<span data-ttu-id="213c9-795">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-795">**Description**</span></span>

<span data-ttu-id="213c9-796">Questo evento rappresenta un evento Internal NetX I/O driver Get duplex.</span><span class="sxs-lookup"><span data-stu-id="213c9-796">This event represents an internal NetX I/O driver get duplex type event.</span></span>

<span data-ttu-id="213c9-797">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-797">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-798">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-798">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-799">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-799">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-800">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-800">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-801">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-801">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-error-count"></a><span data-ttu-id="213c9-802">Conteggio errori di Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-802">Internal I/O Driver Get Error Count</span></span>

#### <a name="internal-io-driver-get-error-count"></a><span data-ttu-id="213c9-803">Conteggio errori di Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-803">Internal I/O driver get error count</span></span>

<span data-ttu-id="213c9-804">**Icona** ![ di Icona per il conteggio degli errori di Get di driver I/O interno](./media/user-guide/netx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-804">**Icon** ![Internal I / O driver get error count icon](./media/user-guide/netx-events/image37.png)</span></span>

<span data-ttu-id="213c9-805">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-805">**Description**</span></span>

<span data-ttu-id="213c9-806">Questo evento rappresenta un evento di conteggio degli errori di un driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-806">This event represents an internal NetX I/O driver get error count event.</span></span>

<span data-ttu-id="213c9-807">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-807">**Information Fields**</span></span>

- <span data-ttu-id="213c9-808">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-808">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-809">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-809">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-810">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-810">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-811">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-811">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-rx-count"></a><span data-ttu-id="213c9-812">Conteggio RX del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-812">Internal I/O Driver Get RX Count</span></span> 

#### <a name="internal-io-driver-get-rx-count"></a><span data-ttu-id="213c9-813">Conteggio RX del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-813">Internal I/O driver get RX count</span></span>

<span data-ttu-id="213c9-814">**Icona** ![ di Icona del conteggio RX del driver I/O interno](./media/user-guide/netx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-814">**Icon** ![Internal I / O driver get RX count icon](./media/user-guide/netx-events/image38.png)</span></span>

<span data-ttu-id="213c9-815">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-815">**Description**</span></span>

<span data-ttu-id="213c9-816">Questo evento rappresenta un evento di conteggio di un driver di I/O NetX interno Get RX.</span><span class="sxs-lookup"><span data-stu-id="213c9-816">This event represents an internal NetX I/O driver get RX count event.</span></span>

<span data-ttu-id="213c9-817">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-817">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-818">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-818">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-819">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-819">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-820">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-820">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-821">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-821">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-tx-count"></a><span data-ttu-id="213c9-822">Conteggio TX del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-822">Internal I/O Driver Get TX Count</span></span> 

#### <a name="internal-io-driver-get-tx-count"></a><span data-ttu-id="213c9-823">Conteggio TX del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-823">Internal I/O driver get TX count</span></span>

<span data-ttu-id="213c9-824">**Icona** ![ di Icona di conteggio del driver I/O interno get T X](./media/user-guide/netx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-824">**Icon** ![Internal I / O driver get T X count icon](./media/user-guide/netx-events/image39.png)</span></span>

<span data-ttu-id="213c9-825">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-825">**Description**</span></span>

<span data-ttu-id="213c9-826">Questo evento rappresenta un evento di conteggio di un driver di I/O NetX interno Get TX.</span><span class="sxs-lookup"><span data-stu-id="213c9-826">This event represents an internal NetX I/O driver get TX count event.</span></span>

<span data-ttu-id="213c9-827">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-827">**Information Fields**</span></span>

- <span data-ttu-id="213c9-828">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-828">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-829">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-829">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-830">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-830">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-831">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-831">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-allocation-errors"></a><span data-ttu-id="213c9-832">Errore di allocazione del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-832">Internal I/O Driver Get Allocation Errors</span></span> 

#### <a name="internal-io-driver-get-allocation-errors"></a><span data-ttu-id="213c9-833">Errore di allocazione del driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-833">Internal I/O driver get allocation errors</span></span>

<span data-ttu-id="213c9-834">**Icona** ![ di Icona per ottenere gli errori di allocazione del driver I/O interno](./media/user-guide/netx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-834">**Icon** ![Internal I / O driver get allocation errors icon](./media/user-guide/netx-events/image40.png)</span></span>

<span data-ttu-id="213c9-835">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-835">**Description**</span></span>

<span data-ttu-id="213c9-836">Questo evento rappresenta un evento di errore di allocazione di un driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-836">This event represents an internal NetX I/O driver get allocation errors event.</span></span>

<span data-ttu-id="213c9-837">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-837">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-838">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-838">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-839">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-839">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-840">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-840">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-841">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-841">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="213c9-842">Annulla inizializzazione del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-842">Internal I/O Driver Un-initialize</span></span> 

#### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="213c9-843">Annulla inizializzazione del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-843">Internal I/O driver un-initialize</span></span> 

<span data-ttu-id="213c9-844">**Icona** ![ di Icona di annullamento inizializzazione del driver I/O interno](./media/user-guide/netx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-844">**Icon** ![Internal I / O driver un-initialize icon](./media/user-guide/netx-events/image41.png)</span></span>

<span data-ttu-id="213c9-845">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-845">**Description**</span></span>

<span data-ttu-id="213c9-846">Questo evento rappresenta un evento di annullamento inizializzazione del driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-846">This event represents an internal NetX I/O driver un-initialize event.</span></span>

<span data-ttu-id="213c9-847">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-847">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-848">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-848">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-849">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-849">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-850">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-850">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-851">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-851">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-deferred-processing"></a><span data-ttu-id="213c9-852">Elaborazione posticipata del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-852">Internal I/O Driver Deferred Processing</span></span> 

#### <a name="internal-io-driver-deferred-processing"></a><span data-ttu-id="213c9-853">Elaborazione posticipata del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="213c9-853">Internal I/O driver deferred processing</span></span> 

<span data-ttu-id="213c9-854">**Icona** ![ di Icona di elaborazione posticipata del driver I/O interno](./media/user-guide/netx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-854">**Icon** ![Internal I / O driver deferred processing icon](./media/user-guide/netx-events/image42.png)</span></span>

<span data-ttu-id="213c9-855">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-855">**Description**</span></span>

<span data-ttu-id="213c9-856">Questo evento rappresenta un evento di elaborazione posticipato del driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="213c9-856">This event represents an internal NetX I/O driver deferred processing event.</span></span>

<span data-ttu-id="213c9-857">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-857">**Information Fields**</span></span>

- <span data-ttu-id="213c9-858">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-858">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-859">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-859">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-860">Informazioni sul campo 3: lunghezza del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-860">Info Field 3: Packet length</span></span>
- <span data-ttu-id="213c9-861">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-861">Info Field 4: Not used</span></span>

### <a name="arp-dynamic-entries-invalidate"></a><span data-ttu-id="213c9-862">Voci dinamiche ARP invalide</span><span class="sxs-lookup"><span data-stu-id="213c9-862">ARP Dynamic Entries Invalidate</span></span> 

#### <a name="nx_arp_dynamic_entries_invalidate"></a><span data-ttu-id="213c9-863">nx_arp_dynamic_entries_invalidate</span><span class="sxs-lookup"><span data-stu-id="213c9-863">nx_arp_dynamic_entries_invalidate</span></span>

<span data-ttu-id="213c9-864">**Icona** ![ di Icona delle voci dinamiche di R P Invalidate](./media/user-guide/netx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-864">**Icon** ![A R P Dynamic Entries Invalidate icon](./media/user-guide/netx-events/image43.png)</span></span>

<span data-ttu-id="213c9-865">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-865">**Description**</span></span>

<span data-ttu-id="213c9-866">Questo evento rappresenta l'invalidamento di tutte le intere ARP dinamiche tramite nx_arp_dynamic_entries_invalidate.</span><span class="sxs-lookup"><span data-stu-id="213c9-866">This event represents invalidating all dynamic ARP entires via nx_arp_dynamic_entries_invalidate.</span></span>

<span data-ttu-id="213c9-867">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-867">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-868">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-868">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-869">Campo informazioni 2: voci Invalidate</span><span class="sxs-lookup"><span data-stu-id="213c9-869">Info Field 2: Entries invalidated</span></span>
- <span data-ttu-id="213c9-870">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-870">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-871">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-871">Info Field 4: Not used</span></span>

### <a name="arp-dynamic-entry-set"></a><span data-ttu-id="213c9-872">Set di voci dinamiche ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-872">ARP Dynamic Entry Set</span></span> 

#### <a name="nx_arp_dynamic_entry_set"></a><span data-ttu-id="213c9-873">nx_arp_dynamic_entry_set</span><span class="sxs-lookup"><span data-stu-id="213c9-873">nx_arp_dynamic_entry_set</span></span>

<span data-ttu-id="213c9-874">**Icona** ![ di Icona del set di voci dinamiche di R P](./media/user-guide/netx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-874">**Icon** ![A R P Dynamic Entry Set icon](./media/user-guide/netx-events/image44.png)</span></span>

<span data-ttu-id="213c9-875">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-875">**Description**</span></span>

<span data-ttu-id="213c9-876">Questo evento rappresenta l'impostazione di una voce ARP dinamica tramite nx_arp_dynamic_entry_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-876">This event represents setting a dynamic ARP entry via nx_arp_dynamic_entry_set.</span></span>

<span data-ttu-id="213c9-877">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-877">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-878">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-878">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-879">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-879">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-880">Campo informazioni 3: indirizzo fisico (RSU)</span><span class="sxs-lookup"><span data-stu-id="213c9-880">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="213c9-881">Campo dati 4: indirizzo fisico (LSW)</span><span class="sxs-lookup"><span data-stu-id="213c9-881">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-enable"></a><span data-ttu-id="213c9-882">Abilitazione ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-882">ARP Enable</span></span> 

#### <a name="nx_arp_enable"></a><span data-ttu-id="213c9-883">nx_arp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-883">nx_arp_enable</span></span>

<span data-ttu-id="213c9-884">**Icona** ![ di Icona di abilitazione di R P](./media/user-guide/netx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-884">**Icon** ![A R P enable icon](./media/user-guide/netx-events/image45.png)</span></span>

<span data-ttu-id="213c9-885">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-885">**Description**</span></span>

<span data-ttu-id="213c9-886">Questo evento rappresenta l'abilitazione di ARP tramite nx_arp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-886">This event represents enabling ARP via nx_arp_enable.</span></span>

<span data-ttu-id="213c9-887">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-887">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-888">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-888">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-889">Informazioni sul campo 2: puntatore di memoria della cache ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-889">Info Field 2: ARP cache memory pointer</span></span>
- <span data-ttu-id="213c9-890">Informazioni sul campo 3: dimensioni della memoria della cache ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-890">Info Field 3: ARP cache memory size</span></span>
- <span data-ttu-id="213c9-891">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-891">Info Field 4: Not used</span></span>

### <a name="arp-gratuitous-send"></a><span data-ttu-id="213c9-892">Invio gratuito ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-892">ARP Gratuitous Send</span></span> 

#### <a name="nx_arp_gratuitous_send"></a><span data-ttu-id="213c9-893">nx_arp_gratuitous_send</span><span class="sxs-lookup"><span data-stu-id="213c9-893">nx_arp_gratuitous_send</span></span>

<span data-ttu-id="213c9-894">**Icona** ![ di Icona di invio gratuito A R P](./media/user-guide/netx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-894">**Icon** ![A R P gratuitous send icon](./media/user-guide/netx-events/image46.png)</span></span>

<span data-ttu-id="213c9-895">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-895">**Description**</span></span>

<span data-ttu-id="213c9-896">Questo evento rappresenta una trasmissione ARP gratuita tramite nx_arp_gratuitous_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-896">This event represents a gratuitous ARP send via nx_arp_gratuitous_send.</span></span>

<span data-ttu-id="213c9-897">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-897">**Information Fields**</span></span>

- <span data-ttu-id="213c9-898">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-898">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-899">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-899">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-900">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-900">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-901">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-901">Info Field 4: Not used</span></span>

### <a name="arp-hardware-address-find"></a><span data-ttu-id="213c9-902">Ricerca indirizzo hardware ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-902">ARP Hardware Address Find</span></span> 

#### <a name="nx_arp_hardware_address_find"></a><span data-ttu-id="213c9-903">nx_arp_hardware_address_find</span><span class="sxs-lookup"><span data-stu-id="213c9-903">nx_arp_hardware_address_find</span></span>

<span data-ttu-id="213c9-904">**Icona** ![ di Icona di ricerca indirizzo hardware R P](./media/user-guide/netx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-904">**Icon** ![A R P Hardware Address Find icon](./media/user-guide/netx-events/image47.png)</span></span>

<span data-ttu-id="213c9-905">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-905">**Description**</span></span>

<span data-ttu-id="213c9-906">Questo evento rappresenta la ricerca di un indirizzo fisico tramite nx_arp_hardware_address_find.</span><span class="sxs-lookup"><span data-stu-id="213c9-906">This event represents finding a physical address via nx_arp_hardware_address_find.</span></span>

<span data-ttu-id="213c9-907">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-907">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-908">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-908">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-909">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-909">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-910">Campo informazioni 3: indirizzo fisico (RSU)</span><span class="sxs-lookup"><span data-stu-id="213c9-910">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="213c9-911">Campo dati 4: indirizzo fisico (LSW)</span><span class="sxs-lookup"><span data-stu-id="213c9-911">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-information-get"></a><span data-ttu-id="213c9-912">Informazioni sul protocollo ARP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-912">ARP Information Get</span></span> 

#### <a name="nx_arp_info_get"></a><span data-ttu-id="213c9-913">nx_arp_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-913">nx_arp_info_get</span></span>

<span data-ttu-id="213c9-914">**Icona** ![ di Icona di R P informition Get](./media/user-guide/netx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-914">**Icon** ![A R P informition get icon](./media/user-guide/netx-events/image48.png)</span></span>

<span data-ttu-id="213c9-915">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-915">**Description**</span></span>

<span data-ttu-id="213c9-916">Questo evento rappresenta il recupero di informazioni tramite nx_arp_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-916">This event represents getting information via nx_arp_info_get.</span></span>

<span data-ttu-id="213c9-917">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-917">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-918">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-918">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-919">Campo informazioni 2: ARPs inviato</span><span class="sxs-lookup"><span data-stu-id="213c9-919">Info Field 2: ARPs sent</span></span>
- <span data-ttu-id="213c9-920">Informazioni sul campo 3: risposte ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-920">Info Field 3: ARP responses</span></span>
- <span data-ttu-id="213c9-921">Campo dati 4: ARPs ricevuto</span><span class="sxs-lookup"><span data-stu-id="213c9-921">Info Field 4: ARPs received</span></span>

### <a name="arp-ip-address-find"></a><span data-ttu-id="213c9-922">Ricerca di indirizzi IP ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-922">ARP IP Address Find</span></span> 

#### <a name="nx_arp_ip_address_find"></a><span data-ttu-id="213c9-923">nx_arp_ip_address_find</span><span class="sxs-lookup"><span data-stu-id="213c9-923">nx_arp_ip_address_find</span></span>

<span data-ttu-id="213c9-924">**Icona** ![ di Icona trova Indirizzo R P I P](./media/user-guide/netx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-924">**Icon** ![A R P I P address find icon](./media/user-guide/netx-events/image49.png)</span></span>

<span data-ttu-id="213c9-925">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-925">**Description**</span></span>

<span data-ttu-id="213c9-926">Questo evento rappresenta la ricerca di un indirizzo IP associato all'indirizzo fisico fornito tramite nx_arp_ip_address_find.</span><span class="sxs-lookup"><span data-stu-id="213c9-926">This event represents finding an IP address associated with the supplied physical address via nx_arp_ip_address_find.</span></span>

<span data-ttu-id="213c9-927">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-927">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-928">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-928">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-929">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-929">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-930">Campo informazioni 3: indirizzo fisico (RSU)</span><span class="sxs-lookup"><span data-stu-id="213c9-930">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="213c9-931">Campo dati 4: indirizzo fisico (LSW)</span><span class="sxs-lookup"><span data-stu-id="213c9-931">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-static-entry-create"></a><span data-ttu-id="213c9-932">Creazione voce statica ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-932">ARP Static Entry Create</span></span> 

#### <a name="nx_arp_static_entry_create"></a><span data-ttu-id="213c9-933">nx_arp_static_entry_create</span><span class="sxs-lookup"><span data-stu-id="213c9-933">nx_arp_static_entry_create</span></span>

<span data-ttu-id="213c9-934">**Icona** ![ di Icona di creazione di una voce statica R P](./media/user-guide/netx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-934">**Icon** ![A R P static entry create icon](./media/user-guide/netx-events/image50.png)</span></span>

<span data-ttu-id="213c9-935">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-935">**Description**</span></span>

<span data-ttu-id="213c9-936">Questo evento rappresenta la creazione di una voce ARP statica tramite nx_arp_static_entry_create.</span><span class="sxs-lookup"><span data-stu-id="213c9-936">This event represents creating a static ARP entry via nx_arp_static_entry_create.</span></span>

<span data-ttu-id="213c9-937">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-937">**Information Fields**</span></span>

- <span data-ttu-id="213c9-938">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-938">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-939">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-939">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-940">Campo informazioni 3: indirizzo fisico (RSU)</span><span class="sxs-lookup"><span data-stu-id="213c9-940">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="213c9-941">Campo dati 4: indirizzo fisico (LSW)</span><span class="sxs-lookup"><span data-stu-id="213c9-941">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-static-entries-delete"></a><span data-ttu-id="213c9-942">Elimina voci statiche ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-942">ARP Static Entries Delete</span></span> 

#### <a name="nx_arp_static_entries_delete"></a><span data-ttu-id="213c9-943">nx_arp_static_entries_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-943">nx_arp_static_entries_delete</span></span>

<span data-ttu-id="213c9-944">**Icona** ![ di Icona Elimina voci statiche R P](./media/user-guide/netx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-944">**Icon** ![A R P static entries delete icon](./media/user-guide/netx-events/image51.png)</span></span>

<span data-ttu-id="213c9-945">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-945">**Description**</span></span>

<span data-ttu-id="213c9-946">Questo evento rappresenta l'eliminazione di tutte le voci statiche ARP tramite nx_arp_static_entries_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-946">This event represents deleting all ARP static entries via nx_arp_static_entries_delete.</span></span>

<span data-ttu-id="213c9-947">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-947">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-948">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-948">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-949">Campo informazioni 2: voci eliminate</span><span class="sxs-lookup"><span data-stu-id="213c9-949">Info Field 2: Entries deleted</span></span>
- <span data-ttu-id="213c9-950">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-950">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-951">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-951">Info Field 4: Not used</span></span>

### <a name="arp-static-entry-delete"></a><span data-ttu-id="213c9-952">Eliminazione voce statica ARP</span><span class="sxs-lookup"><span data-stu-id="213c9-952">ARP Static Entry Delete</span></span> 

### <a name="nx_arp_static_entry_delete"></a><span data-ttu-id="213c9-953">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-953">nx_arp_static_entry_delete</span></span>

<span data-ttu-id="213c9-954">**Icona** ![ di Icona di eliminazione della voce statica di R P](./media/user-guide/netx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-954">**Icon** ![A R P static entry delete icon](./media/user-guide/netx-events/image52.png)</span></span>

<span data-ttu-id="213c9-955">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-955">**Description**</span></span>

<span data-ttu-id="213c9-956">Questo evento rappresenta l'eliminazione di una voce ARP statica tramite nx_arp_static_entry_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-956">This event represents deleting a static ARP entry via nx_arp_static_entry_delete.</span></span>

<span data-ttu-id="213c9-957">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-957">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-958">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-958">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-959">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-959">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-960">Campo informazioni 3: indirizzo fisico (RSU)</span><span class="sxs-lookup"><span data-stu-id="213c9-960">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="213c9-961">Campo dati 4: indirizzo fisico (LSW)</span><span class="sxs-lookup"><span data-stu-id="213c9-961">Info Field 4: Physical address (LSW)</span></span>

### <a name="duo-cache-entry-delete"></a><span data-ttu-id="213c9-962">Eliminazione voce della cache Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-962">Duo Cache Entry Delete</span></span> 

#### <a name="nxd_und_cache_entry_delete"></a><span data-ttu-id="213c9-963">nxd_und_cache_entry_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-963">nxd_und_cache_entry_delete</span></span>

<span data-ttu-id="213c9-964">**Icona** ![ di Icona di eliminazione voce della cache Duo](./media/user-guide/netx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-964">**Icon** ![Duo cache entry delete icon](./media/user-guide/netx-events/image53.png)</span></span>

<span data-ttu-id="213c9-965">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-965">**Description**</span></span>

<span data-ttu-id="213c9-966">Questo evento rappresenta l'eliminazione di una voce nella tabella della cache vicina tramite nx_udp_socket_create.</span><span class="sxs-lookup"><span data-stu-id="213c9-966">This event represents deleting an entry in the neighbor cache table via nx_udp_socket_create.</span></span>

<span data-ttu-id="213c9-967">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-967">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-968">Campo informazioni 1: quarto (meno significativo) parola dell'indirizzo locale del collegamento IPv6 da eliminare</span><span class="sxs-lookup"><span data-stu-id="213c9-968">Info Field 1: Fourth (least significant) word of the IPv6 link local address to delete</span></span>
- <span data-ttu-id="213c9-969">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-969">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-970">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-970">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-971">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-971">Info Field 4: Not used</span></span>

### <a name="duo-cache-entry-set"></a><span data-ttu-id="213c9-972">Set di voci della cache Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-972">Duo Cache Entry Set</span></span> 

#### <a name="nxd_nd_cache_entry_set"></a><span data-ttu-id="213c9-973">nxd_nd_cache_entry_set</span><span class="sxs-lookup"><span data-stu-id="213c9-973">nxd_nd_cache_entry_set</span></span>

<span data-ttu-id="213c9-974">**Icona** ![ di Icona del set di voci della cache Duo](./media/user-guide/netx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-974">**Icon** ![Duo cache entry set icon](./media/user-guide/netx-events/image54.png)</span></span>

<span data-ttu-id="213c9-975">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-975">**Description**</span></span>

<span data-ttu-id="213c9-976">Questo evento rappresenta la creazione di una voce della cache e l'aggiunta alla tabella della cache vicina tramite nxd_nd_cache_entry_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-976">This event represents creating a cache entry and adding to the neighbor cache table via nxd_nd_cache_entry_set.</span></span>

<span data-ttu-id="213c9-977">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-977">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-978">Campo informazioni 1: quarto (meno significativo) parola dell'indirizzo IPv6 da aggiungere</span><span class="sxs-lookup"><span data-stu-id="213c9-978">Info Field 1: Fourth (least significant) word of the IPv6 address to add</span></span>
- <span data-ttu-id="213c9-979">Informazioni sul campo 2: indirizzo fisico MSB</span><span class="sxs-lookup"><span data-stu-id="213c9-979">Info Field 2: Physical address msb</span></span>
- <span data-ttu-id="213c9-980">Informazioni sul campo 3: indirizzo fisico lsb</span><span class="sxs-lookup"><span data-stu-id="213c9-980">Info Field 3: Physical address lsb</span></span>
- <span data-ttu-id="213c9-981">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-981">Info Field 4: Not used</span></span>

### <a name="duo-cache-invalidate"></a><span data-ttu-id="213c9-982">Invalidamento della cache Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-982">Duo Cache Invalidate</span></span> 

#### <a name="nxd_nd_cache_invalidate"></a><span data-ttu-id="213c9-983">nxd_nd_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="213c9-983">nxd_nd_cache_invalidate</span></span>

<span data-ttu-id="213c9-984">**Icona** ![ di Icona di invalidamento della cache Duo](./media/user-guide/netx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-984">**Icon** ![Duo cache invalidate icon](./media/user-guide/netx-events/image55.png)</span></span>

<span data-ttu-id="213c9-985">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-985">**Description**</span></span>

<span data-ttu-id="213c9-986">Questo evento rappresenta l'invalidamento dell'intera tabella della cache vicina tramite nxd_nd_cache_invalidate.</span><span class="sxs-lookup"><span data-stu-id="213c9-986">This event represents invalidating the entire neighbor cache table via nxd_nd_cache_invalidate.</span></span>

<span data-ttu-id="213c9-987">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-987">**Information Fields**</span></span>

- <span data-ttu-id="213c9-988">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-988">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-989">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-989">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-990">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-990">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-991">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-991">Info Field 4: Not used</span></span>

### <a name="duo-cache-ip-address-find"></a><span data-ttu-id="213c9-992">Ricerca indirizzo IP cache Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-992">Duo Cache IP Address Find</span></span> 

#### <a name="nxd_nd_cache_ip_address_find"></a><span data-ttu-id="213c9-993">nxd_nd_cache_ip_address_find</span><span class="sxs-lookup"><span data-stu-id="213c9-993">nxd_nd_cache_ip_address_find</span></span>

<span data-ttu-id="213c9-994">**Icona** ![ di Icona di ricerca dell'indirizzo del duo cache I P](./media/user-guide/netx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-994">**Icon** ![Duo cache I P address find icon](./media/user-guide/netx-events/image56.png)</span></span>

<span data-ttu-id="213c9-995">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-995">**Description**</span></span>

<span data-ttu-id="213c9-996">Questo evento rappresenta il recupero di un indirizzo IP corrispondente all'indirizzo fisico fornito dalla tabella della cache tramite nxd_nd_cache_ip_address_find.</span><span class="sxs-lookup"><span data-stu-id="213c9-996">This event represents retrieving an IP address matching the supplied physical address from the cache table via nxd_nd_cache_ip_address_find.</span></span>

<span data-ttu-id="213c9-997">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-997">**Information Fields**</span></span>

- <span data-ttu-id="213c9-998">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-998">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-999">Campo Info 2: quarto (meno significativo) parola dell'indirizzo IPv6</span><span class="sxs-lookup"><span data-stu-id="213c9-999">Info Field 2: Fourth (least significant) word of the IPv6 address</span></span>
- <span data-ttu-id="213c9-1000">Informazioni sul campo 3: indirizzo fisico MSB</span><span class="sxs-lookup"><span data-stu-id="213c9-1000">Info Field 3: Physical address msb</span></span>
- <span data-ttu-id="213c9-1001">Informazioni sul campo 4: indirizzo fisico lsb</span><span class="sxs-lookup"><span data-stu-id="213c9-1001">Info Field 4: Physical address lsb</span></span>

### <a name="duo-icmp-enable"></a><span data-ttu-id="213c9-1002">Abilitazione ICMP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1002">Duo ICMP Enable</span></span> 

#### <a name="nxd_icmp_enable"></a><span data-ttu-id="213c9-1003">nxd_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1003">nxd_icmp_enable</span></span>

<span data-ttu-id="213c9-1004">**Icona** ![ di Icona di abilitazione Duo I C M P](./media/user-guide/netx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1004">**Icon** ![Duo I C M P enable icon](./media/user-guide/netx-events/image57.png)</span></span>

<span data-ttu-id="213c9-1005">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1005">**Description**</span></span>

<span data-ttu-id="213c9-1006">Questo evento rappresenta i servizi ICMPv4 e ICMPv6 abilitati nell'istanza IP specificata tramite nxd_icmp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1006">This event represents ICMPv4 and ICMPv6 services being enabled on the specified IP instance via nxd_icmp_enable.</span></span>

<span data-ttu-id="213c9-1007">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1007">**Information Fields**</span></span>
- <span data-ttu-id="213c9-1008">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1008">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1009">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1009">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1010">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1010">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1011">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1011">Info Field 4: Not used</span></span>

### <a name="duo-icmp-ping"></a><span data-ttu-id="213c9-1012">Ping ICMP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1012">Duo ICMP Ping</span></span> 

#### <a name="nxd_icmp_ping"></a><span data-ttu-id="213c9-1013">nxd_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="213c9-1013">nxd_icmp_ping</span></span>

<span data-ttu-id="213c9-1014">**Icona** ![ di Icona di ping di duo I C M P](./media/user-guide/netx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1014">**Icon** ![Duo I C M P ping icon](./media/user-guide/netx-events/image58.png)</span></span>

<span data-ttu-id="213c9-1015">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1015">**Description**</span></span>

<span data-ttu-id="213c9-1016">Questo evento rappresenta l'invio di un ping (richiesta echo) a un host IPv6 tramite nxd_icmp_ping.</span><span class="sxs-lookup"><span data-stu-id="213c9-1016">This event represents sending a ping (echo request) to an IPv6 host via nxd_icmp_ping.</span></span>

<span data-ttu-id="213c9-1017">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1017">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1018">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1018">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1019">Informazioni sul campo 2: indirizzo IPv6</span><span class="sxs-lookup"><span data-stu-id="213c9-1019">Info Field 2: IPv6 address</span></span>
- <span data-ttu-id="213c9-1020">Informazioni sul campo 3: puntatore ai dati echo</span><span class="sxs-lookup"><span data-stu-id="213c9-1020">Info Field 3: Pointer to echo data</span></span>
- <span data-ttu-id="213c9-1021">Informazioni sul campo 4: dimensioni dei dati echo</span><span class="sxs-lookup"><span data-stu-id="213c9-1021">Info Field 4: Size of echo data</span></span>

### <a name="duo-ip-max-payload-size-find"></a><span data-ttu-id="213c9-1022">Ricerca dimensioni massime payload IP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1022">Duo IP Max Payload Size Find</span></span> 

#### <a name="nxd_ip_max_payload_size"></a><span data-ttu-id="213c9-1023">nxd_ip_max_payload_size</span><span class="sxs-lookup"><span data-stu-id="213c9-1023">nxd_ip_max_payload_size</span></span>

<span data-ttu-id="213c9-1024">**Icona** ![ di Icona trova dimensioni del payload massimo Duo I P](./media/user-guide/netx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1024">**Icon** ![Duo I P max payload size find icon](./media/user-guide/netx-events/image59.png)</span></span>

<span data-ttu-id="213c9-1025">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1025">**Description**</span></span>

<span data-ttu-id="213c9-1026">Questo evento Calcola il payload massimo che il pacchetto specificato può eseguire senza richiedere la frammentazione.</span><span class="sxs-lookup"><span data-stu-id="213c9-1026">This event computes the max payload the specified packet can carry without requiring fragmentation.</span></span>

<span data-ttu-id="213c9-1027">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1027">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1028">Campo informazioni 1: puntatore socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1028">Info Field 1: Socket pointer</span></span>
- <span data-ttu-id="213c9-1029">Informazioni sul campo 2: indirizzo IP peer</span><span class="sxs-lookup"><span data-stu-id="213c9-1029">Info Field 2: Peer IP address</span></span>
- <span data-ttu-id="213c9-1030">Informazioni sul campo 3: campo informazioni porta peer 4: non utilizzato</span><span class="sxs-lookup"><span data-stu-id="213c9-1030">Info Field 3: Peer port Info Field 4: Not used</span></span>

### <a name="duo-ip-raw-packet-send"></a><span data-ttu-id="213c9-1031">Invio pacchetti non elaborati IP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1031">Duo IP Raw Packet Send</span></span> 

#### <a name="nxd_ip_max_packet_send"></a><span data-ttu-id="213c9-1032">nxd_ip_max_packet_send</span><span class="sxs-lookup"><span data-stu-id="213c9-1032">nxd_ip_max_packet_send</span></span>

<span data-ttu-id="213c9-1033">**Icona** ![ di Icona di invio di pacchetti non elaborati Duo I P](./media/user-guide/netx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1033">**Icon** ![Duo I P raw packet send icon](./media/user-guide/netx-events/image60.png)</span></span>

<span data-ttu-id="213c9-1034">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1034">**Description**</span></span>

<span data-ttu-id="213c9-1035">Questo evento rappresenta l'invio di un pacchetto IP non elaborato dall'interfaccia di rete specificata alla destinazione IP addressvia nxd_ip_raw_packet_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-1035">This event represents sending a raw IP packet out the specified network interface to the supplied IP destination addressvia nxd_ip_raw_packet_send.</span></span>

<span data-ttu-id="213c9-1036">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1036">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1037">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1037">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1038">Informazioni sul campo 2: puntatore al pacchetto da inviare</span><span class="sxs-lookup"><span data-stu-id="213c9-1038">Info Field 2: Pointer to packet to send</span></span>
- <span data-ttu-id="213c9-1039">Informazioni sul campo 3: puntatore all'indirizzo di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-1039">Info Field 3: Pointer to destination address</span></span>
- <span data-ttu-id="213c9-1040">Informazioni sul campo 4: protocollo Packet</span><span class="sxs-lookup"><span data-stu-id="213c9-1040">Info Field 4: Packet protocol</span></span>

### <a name="duo-ipv6-default-router-add"></a><span data-ttu-id="213c9-1041">Aggiunta router IPv6 predefinito Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1041">Duo IPv6 Default Router Add</span></span> 

#### <a name="nxd_ipv6_default_router_add"></a><span data-ttu-id="213c9-1042">nxd_ipv6_default_router_add</span><span class="sxs-lookup"><span data-stu-id="213c9-1042">nxd_ipv6_default_router_add</span></span>

<span data-ttu-id="213c9-1043">**Icona** ![ di Icona di aggiunta del router predefinito Duo I P v 6](./media/user-guide/netx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1043">**Icon** ![Duo I P v 6 default router add icon](./media/user-guide/netx-events/image61.png)</span></span>

<span data-ttu-id="213c9-1044">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1044">**Description**</span></span>

<span data-ttu-id="213c9-1045">Questo evento rappresenta l'aggiunta di un router predefinito alla tabella di routing IPv6 dell'istanza IP tramite nxd_ipv6_default_router_add.</span><span class="sxs-lookup"><span data-stu-id="213c9-1045">This event represents adding a default router to the IP instance's IPv6 routing table via nxd_ipv6_default_router_add.</span></span>

<span data-ttu-id="213c9-1046">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1046">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1047">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-1047">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="213c9-1048">Informazioni sul campo 2: indirizzo di rete di destinazione.</span><span class="sxs-lookup"><span data-stu-id="213c9-1048">Info Field 2: Destination Network address.</span></span>
- <span data-ttu-id="213c9-1049">Informazioni sul campo 3: informazioni sulla durata.</span><span class="sxs-lookup"><span data-stu-id="213c9-1049">Info Field 3: Life time information.</span></span>
- <span data-ttu-id="213c9-1050">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-1050">Info Field 4: Not used.</span></span>

### <a name="duo-ipv6-default-router-delete"></a><span data-ttu-id="213c9-1051">Eliminazione router default IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1051">Duo IPv6 Default Router Delete</span></span> 

#### <a name="nxd_ipv6_default_router_delete"></a><span data-ttu-id="213c9-1052">nxd_ipv6_default_router_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-1052">nxd_ipv6_default_router_delete</span></span>

<span data-ttu-id="213c9-1053">**Icona** ![ di Icona di eliminazione del router predefinito Duo I P v 6](./media/user-guide/netx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1053">**Icon** ![Duo I P v 6 default router delete icon](./media/user-guide/netx-events/image62.png)</span></span>

<span data-ttu-id="213c9-1054">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1054">**Description**</span></span>

<span data-ttu-id="213c9-1055">Questo evento rappresenta la rimozione di un router predefinito dalla tabella di routing IPv6 dell'istanza IP tramite nxd_ipv6_default_router_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-1055">This event represents removing a default router from the IP instance's IPv6 routing table via nxd_ipv6_default_router_delete.</span></span>

<span data-ttu-id="213c9-1056">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1056">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1057">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-1057">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="213c9-1058">Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo IPv6 del router predefinito.</span><span class="sxs-lookup"><span data-stu-id="213c9-1058">Info Field 2: Fourth word (least significant) of the default router IPv6 address.</span></span>
- <span data-ttu-id="213c9-1059">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-1059">Info Field 3: Not used.</span></span>
- <span data-ttu-id="213c9-1060">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="213c9-1060">Info Field 4: Not used.</span></span>

### <a name="duo-ipv6-enable"></a><span data-ttu-id="213c9-1061">Abilitazione IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1061">Duo IPv6 Enable</span></span> 

#### <a name="nxd_ipv6_enable"></a><span data-ttu-id="213c9-1062">nxd_ipv6_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1062">nxd_ipv6_enable</span></span>

<span data-ttu-id="213c9-1063">**Icona** ![ di Icona abilitazione Duo I P v 6](./media/user-guide/netx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1063">**Icon** ![Duo I P v 6 enable icon](./media/user-guide/netx-events/image63.png)</span></span>

<span data-ttu-id="213c9-1064">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1064">**Description**</span></span>

<span data-ttu-id="213c9-1065">Questo evento rappresenta l'abilitazione di servizi IPv6 sull'istanza IP fornita tramite nxd_ipv6_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1065">This event represents enabling IPv6 services on the supplied IP instance via nxd_ipv6_enable.</span></span>

<span data-ttu-id="213c9-1066">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1066">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1067">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1067">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1068">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1068">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1069">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1069">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1070">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1070">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-global-address-get"></a><span data-ttu-id="213c9-1071">Indirizzo globale IPv6 Duo Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1071">Duo IPv6 Global Address Get</span></span> 

#### <a name="nxd_ipv6_global_address_get"></a><span data-ttu-id="213c9-1072">nxd_ipv6_global_address_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1072">nxd_ipv6_global_address_get</span></span>

<span data-ttu-id="213c9-1073">**Icona** ![ di Icona Get indirizzo globale Duo I P v 6](./media/user-guide/netx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1073">**Icon** ![Duo I P v 6 global address get icon](./media/user-guide/netx-events/image64.png)</span></span>

<span data-ttu-id="213c9-1074">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1074">**Description**</span></span>

<span data-ttu-id="213c9-1075">Questo evento rappresenta il recupero dell'indirizzo IP globale (primario) nell'istanza IP situata in corrispondenza dell'indice 1 nella tabella dell'interfaccia dell'istanza IP tramite nxd_ipv6_global_address_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1075">This event represents retrieving the global (primary) IP address on the IP instance located at index 1 in the IP instance interface table via nxd_ipv6_global_address_get.</span></span>

<span data-ttu-id="213c9-1076">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1076">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1077">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-1077">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="213c9-1078">Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo globale</span><span class="sxs-lookup"><span data-stu-id="213c9-1078">Info Field 2: Fourth word (least significant) of the global address</span></span>
- <span data-ttu-id="213c9-1079">Informazioni sul campo 3: lunghezza del prefisso dell'indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="213c9-1079">Info Field 3: IPv6 address prefix length.</span></span>
- <span data-ttu-id="213c9-1080">Campo informazioni 4: indice nella tabella dell'interfaccia IP (1).</span><span class="sxs-lookup"><span data-stu-id="213c9-1080">Info Field 4: Index into IP interface table (1).</span></span>

### <a name="duo-ipv6-global-address-set"></a><span data-ttu-id="213c9-1081">Set di indirizzi globali IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1081">Duo IPv6 Global Address Set</span></span> 

#### <a name="nxd_ipv6_global_address_set"></a><span data-ttu-id="213c9-1082">nxd_ipv6_global_address_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1082">nxd_ipv6_global_address_set</span></span>

<span data-ttu-id="213c9-1083">**Icona** ![ di Icona del set di indirizzi globale Duo I P v 6](./media/user-guide/netx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1083">**Icon** ![Duo I P v 6 global address set icon](./media/user-guide/netx-events/image65.png)</span></span>

<span data-ttu-id="213c9-1084">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1084">**Description**</span></span>

<span data-ttu-id="213c9-1085">Questo evento rappresenta l'impostazione dell'indirizzo IP globale (primario) nell'istanza IP presente in corrispondenza dell'indice 1 nella tabella dell'interfaccia dell'istanza IP tramite nxd_ipv6_global_address_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1085">This event represents setting the global (primary) IP address on the IP instance located at index 1 in the IP instance interface table via nxd_ipv6_global_address_set.</span></span>

<span data-ttu-id="213c9-1086">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1086">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1087">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1087">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1088">Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo globale</span><span class="sxs-lookup"><span data-stu-id="213c9-1088">Info Field 2: Fourth word (least significant) of the global address</span></span>
- <span data-ttu-id="213c9-1089">Informazioni campo 3: lunghezza prefisso indirizzo IPv6</span><span class="sxs-lookup"><span data-stu-id="213c9-1089">Info Field 3: IPv6 address prefix length</span></span>
- <span data-ttu-id="213c9-1090">Campo informazioni 4: indice nella tabella dell'interfaccia IP (1)</span><span class="sxs-lookup"><span data-stu-id="213c9-1090">Info Field 4: Index into IP interface table (1)</span></span>

### <a name="duo-ipv6-initiate-dad-process"></a><span data-ttu-id="213c9-1091">Processo padre di avvio IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1091">Duo IPv6 Initiate Dad Process</span></span> 

#### <a name="nxd_ipv6_initiate_dad_process"></a><span data-ttu-id="213c9-1092">nxd_ipv6_initiate_dad_process</span><span class="sxs-lookup"><span data-stu-id="213c9-1092">nxd_ipv6_initiate_dad_process</span></span>

<span data-ttu-id="213c9-1093">**Icona** ![ di Icona del processo padre di avvio Duo I P v 6](./media/user-guide/netx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1093">**Icon** ![Duo I P v 6 initiate dad process icon](./media/user-guide/netx-events/image66.png)</span></span>

<span data-ttu-id="213c9-1094">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1094">**Description**</span></span>

<span data-ttu-id="213c9-1095">Questo evento rappresenta l'inizio del processo di rilevamento degli indirizzi duplicati (DAD) quando all'istanza IP viene assegnato un indirizzo di collegamento locale o di interfaccia IP tramite nxd_ipv6_initiate_dad_process.</span><span class="sxs-lookup"><span data-stu-id="213c9-1095">This event represents the start of the Duplicate Address Detection (DAD) process when the IP instance is assigned a link local or an IP interface address via nxd_ipv6_initiate_dad_process.</span></span>

<span data-ttu-id="213c9-1096">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1096">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1097">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1097">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1098">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1098">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1099">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1099">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1100">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1100">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-interface-address-get"></a><span data-ttu-id="213c9-1101">Indirizzo dell'interfaccia IPv6 Duo Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1101">Duo IPv6 Interface Address Get</span></span> 

#### <a name="nxd_ipv6_interface_address_get"></a><span data-ttu-id="213c9-1102">nxd_ipv6_interface_address_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1102">nxd_ipv6_interface_address_get</span></span>

<span data-ttu-id="213c9-1103">**Icona** ![ di Icona di Get dell'indirizzo dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1103">**Icon** ![Duo I P v 6 interface address get icon](./media/user-guide/netx-events/image67.png)</span></span>

<span data-ttu-id="213c9-1104">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1104">**Description**</span></span>

<span data-ttu-id="213c9-1105">Questo evento rappresenta il recupero dell'indirizzo IP e del prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'interfaccia dell'istanza IP tramite nxd_ipv6_interface_address_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1105">This event represents retrieving the IP address and prefix at the specified index into the IP instance interface address table via nxd_ipv6_interface_address_get.</span></span>

<span data-ttu-id="213c9-1106">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1106">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1107">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1107">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1108">Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo IPv6 da restituire</span><span class="sxs-lookup"><span data-stu-id="213c9-1108">Info Field 2: Fourth word (least significant) of the IPv6 address to return</span></span>
- <span data-ttu-id="213c9-1109">Informazioni sul campo 4: Indice dell'interfaccia nella tabella dell'interfaccia dell'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1109">Info Field 4: Index of interface into the IP instance interface table</span></span>

### <a name="duo-ipv6-interface-address-set"></a><span data-ttu-id="213c9-1110">Set di indirizzi dell'interfaccia IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1110">Duo IPv6 Interface Address Set</span></span> 

### <a name="nxd_ipv6_interface_address_set"></a><span data-ttu-id="213c9-1111">nxd_ipv6_interface_address_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1111">nxd_ipv6_interface_address_set</span></span>

<span data-ttu-id="213c9-1112">**Icona** ![ di Icona degli indirizzi dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1112">**Icon** ![Duo I P v 6 interface addresss et icon](./media/user-guide/netx-events/image68.png)</span></span>

<span data-ttu-id="213c9-1113">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1113">**Description**</span></span>

<span data-ttu-id="213c9-1114">Questo evento rappresenta l'impostazione dell'indirizzo IP e del prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'interfaccia dell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="213c9-1114">This event represents setting the IP address and prefix at the specified index into the IP instance interface address table.</span></span> <span data-ttu-id="213c9-1115">Non consentito in corrispondenza dell'indice zero (indirizzo locale collegamento) tramite nxd_ipv6_interface_address_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1115">Not permitted on index zero (link local address) via nxd_ipv6_interface_address_set.</span></span>

<span data-ttu-id="213c9-1116">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1116">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1117">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1117">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1118">Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo IPv6 da restituire</span><span class="sxs-lookup"><span data-stu-id="213c9-1118">Info Field 2: Fourth word (least significant) of the IPv6 address to return</span></span>
- <span data-ttu-id="213c9-1119">Informazioni sul campo 3: lunghezza del prefisso</span><span class="sxs-lookup"><span data-stu-id="213c9-1119">Info Field 3: Prefix length</span></span>
- <span data-ttu-id="213c9-1120">Informazioni sul campo 4: Indice dell'interfaccia nella tabella dell'interfaccia dell'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1120">Info Field 4: Index of interface into the IP instance interface table</span></span>

### <a name="duo-ipv6-link-local-address-get"></a><span data-ttu-id="213c9-1121">Indirizzo locale del collegamento IPv6 Duo Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1121">Duo IPv6 Link Local Address Get</span></span> 

#### <a name="nxd_ipv6_linklocal_address_get"></a><span data-ttu-id="213c9-1122">nxd_ipv6_linklocal_address_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1122">nxd_ipv6_linklocal_address_get</span></span>

<span data-ttu-id="213c9-1123">**Icona** ![ di Icona di Get dell'indirizzo locale del collegamento Duo I P v 6](./media/user-guide/netx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1123">**Icon** ![Duo I P v 6 link local address get icon](./media/user-guide/netx-events/image69.png)</span></span>

<span data-ttu-id="213c9-1124">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1124">**Description**</span></span>

<span data-ttu-id="213c9-1125">Questo evento rappresenta il recupero dell'indirizzo locale del collegamento dell'istanza IP specificata tramite nxd_ipv6_linklocal_address_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1125">This event represents retrieving the link local address of the specified IP instance via nxd_ipv6_linklocal_address_get.</span></span>

<span data-ttu-id="213c9-1126">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1126">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1127">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1127">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1128">Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo locale del collegamento IP V6</span><span class="sxs-lookup"><span data-stu-id="213c9-1128">Info Field 2: Fourth word (least significant) of the IP v6 link local address</span></span>
- <span data-ttu-id="213c9-1129">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1129">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1130">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1130">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-link-local-address-set"></a><span data-ttu-id="213c9-1131">Set di indirizzi locali collegamento IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1131">Duo IPv6 Link Local Address Set</span></span> 

#### <a name="nxd_ipv6_linklocal_address_set"></a><span data-ttu-id="213c9-1132">nxd_ipv6_linklocal_address_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1132">nxd_ipv6_linklocal_address_set</span></span>

<span data-ttu-id="213c9-1133">**Icona** ![ di Icona del set di indirizzi locali di collegamento I P v 6](./media/user-guide/netx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1133">**Icon** ![Duo I P v 6 link local address set icon](./media/user-guide/netx-events/image70.png)</span></span>

<span data-ttu-id="213c9-1134">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1134">**Description**</span></span>

<span data-ttu-id="213c9-1135">Questo evento rappresenta l'impostazione dell'indirizzo locale del collegamento dell'istanza IP tramite nxd_ipv6_linklocal_address_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1135">This event represents setting the link local address of the IP instance via nxd_ipv6_linklocal_address_set.</span></span>

<span data-ttu-id="213c9-1136">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1136">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1137">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1137">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1138">Informazioni sul campo 2: quarta (meno significativa) parola dell'indirizzo locale del collegamento IPv6</span><span class="sxs-lookup"><span data-stu-id="213c9-1138">Info Field 2: Fourth (least significant) word of the IPv6 link local address</span></span>
- <span data-ttu-id="213c9-1139">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1139">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1140">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1140">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-raw-packet-send"></a><span data-ttu-id="213c9-1141">Invio pacchetti non elaborati IPv6 Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1141">Duo IPv6 Raw Packet Send</span></span> 

#### <a name="nxd_ipv6_raw_packet_send"></a><span data-ttu-id="213c9-1142">nxd_ipv6_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="213c9-1142">nxd_ipv6_raw_packet_send</span></span>

<span data-ttu-id="213c9-1143">**Icona** ![ di Icona di invio di pacchetti non elaborati Duo I P v 6](./media/user-guide/netx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1143">**Icon** ![Duo I P v 6 raw packet send icon](./media/user-guide/netx-events/image71.png)</span></span>

<span data-ttu-id="213c9-1144">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1144">**Description**</span></span>

<span data-ttu-id="213c9-1145">Questo evento rappresenta l'invio di un pacchetto IP non elaborato tramite l'interfaccia IP primaria alla destinazione specificare tramite nxd_ip_raw_packet_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-1145">This event represents sending a raw IP packet through the primary IP interface to the speficied destination via nxd_ip_raw_packet_send.</span></span>

<span data-ttu-id="213c9-1146">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1146">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1147">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1147">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1148">Informazioni sul campo 2: puntatore al pacchetto da inviare</span><span class="sxs-lookup"><span data-stu-id="213c9-1148">Info Field 2: Pointer to packet to send</span></span>
- <span data-ttu-id="213c9-1149">Informazioni sul campo 3: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-1149">Info Field 3: Destination IP address</span></span>
- <span data-ttu-id="213c9-1150">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1150">Info Field 4: Not used</span></span>

### <a name="duo-tcp-socket-peer-info-get"></a><span data-ttu-id="213c9-1151">Informazioni Get peer socket TCP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1151">Duo TCP Socket Peer Info Get</span></span> 

#### <a name="nxd_tcp_socket_peer_info_get"></a><span data-ttu-id="213c9-1152">nxd_tcp_socket_peer_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1152">nxd_tcp_socket_peer_info_get</span></span>

<span data-ttu-id="213c9-1153">**Icona** ![ di Icona Get per le informazioni su peer di Duo T C P](./media/user-guide/netx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1153">**Icon** ![Duo T C P socket peer info get icon](./media/user-guide/netx-events/image72.png)</span></span>

<span data-ttu-id="213c9-1154">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1154">**Description**</span></span>

<span data-ttu-id="213c9-1155">Questo evento estrae i dati del mittente da un pacchetto TCP ricevuto sul socket specificato.</span><span class="sxs-lookup"><span data-stu-id="213c9-1155">This event extracts the sender data from a received TCP packet on the specified socket.</span></span> <span data-ttu-id="213c9-1156">Restituisce l'indirizzo IP e la porta del mittente.</span><span class="sxs-lookup"><span data-stu-id="213c9-1156">It returns the IP address and port of the sender.</span></span>

<span data-ttu-id="213c9-1157">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1157">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1158">Campo informazioni 1: puntatore socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1158">Info Field 1: Socket pointer</span></span>
- <span data-ttu-id="213c9-1159">Informazioni sul campo 2: indirizzo IP peer</span><span class="sxs-lookup"><span data-stu-id="213c9-1159">Info Field 2: Peer IP address</span></span>
- <span data-ttu-id="213c9-1160">Informazioni sul campo 3: porta peer</span><span class="sxs-lookup"><span data-stu-id="213c9-1160">Info Field 3: Peer port</span></span>
- <span data-ttu-id="213c9-1161">Info Field 4: il lease significativo 32 bit dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1161">Info Field 4: The lease significant 32-bit of the IP address</span></span>

### <a name="duo-tcp-socket-set-interface"></a><span data-ttu-id="213c9-1162">Interfaccia del set di socket TCP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1162">Duo TCP Socket Set Interface</span></span> 

#### <a name="nxd_tcp_socket_set_interface"></a><span data-ttu-id="213c9-1163">nxd_tcp_socket_set_interface</span><span class="sxs-lookup"><span data-stu-id="213c9-1163">nxd_tcp_socket_set_interface</span></span>

<span data-ttu-id="213c9-1164">**Icona** ![ di Icona dell'interfaccia del set di socket T C P Duo](./media/user-guide/netx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1164">**Icon** ![Duo T C P socket set interface icon](./media/user-guide/netx-events/image73.png)</span></span>

<span data-ttu-id="213c9-1165">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1165">**Description**</span></span>

<span data-ttu-id="213c9-1166">Questo evento rappresenta l'impostazione dell'interfaccia socket in uscita dopo che un client si connette con un server TCP nell'indirizzo IP del server specificato tramite nxd_tcp_client_socket_connect.</span><span class="sxs-lookup"><span data-stu-id="213c9-1166">This event represents setting the outgoing socket interface after a client connects with a TCP server on the specified server IP address via nxd_tcp_client_socket_connect.</span></span>

<span data-ttu-id="213c9-1167">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1167">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1168">Informazioni sul campo 1: puntatore al socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1168">Info Field 1: Pointer to TCP Socket</span></span>
- <span data-ttu-id="213c9-1169">Informazioni sul campo 2: ID interfaccia</span><span class="sxs-lookup"><span data-stu-id="213c9-1169">Info Field 2: Interface ID</span></span>
- <span data-ttu-id="213c9-1170">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1170">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1171">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1171">Info Field 4: Not used</span></span>

### <a name="duo-udp-socket-send"></a><span data-ttu-id="213c9-1172">Invio socket UDP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1172">Duo UDP Socket Send</span></span> 

#### <a name="nxd_udp_socket_send"></a><span data-ttu-id="213c9-1173">nxd_udp_socket_send</span><span class="sxs-lookup"><span data-stu-id="213c9-1173">nxd_udp_socket_send</span></span>

<span data-ttu-id="213c9-1174">**Icona** ![ di Icona di invio del socket Duo U D P](./media/user-guide/netx-events/image74.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1174">**Icon** ![Duo U D P socket send icon](./media/user-guide/netx-events/image74.png)</span></span>

<span data-ttu-id="213c9-1175">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1175">**Description**</span></span>

<span data-ttu-id="213c9-1176">Questo evento rappresenta l'invio di un pacchetto UDP tramite il socket specificato con l'indirizzo IP e la porta di input tramite nxd_udp_socket_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-1176">This event represents sending a UDP packet through the specified socket with the input IP address and port via nxd_udp_socket_send.</span></span>

<span data-ttu-id="213c9-1177">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1177">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1178">Informazioni sul campo 1: socket UDP puntatore</span><span class="sxs-lookup"><span data-stu-id="213c9-1178">Info Field 1: Pointer UDP Socket</span></span>
- <span data-ttu-id="213c9-1179">Informazioni sul campo 2: puntatore al pacchetto UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1179">Info Field 2: Pointer to UDP packet</span></span>
- <span data-ttu-id="213c9-1180">Informazioni sul campo 3: lunghezza del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1180">Info Field 3: Packet length</span></span>
- <span data-ttu-id="213c9-1181">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1181">Info Field 4: Not used</span></span>


### <a name="duo-udp-socket-set-interface"></a><span data-ttu-id="213c9-1182">Interfaccia del set di socket UDP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1182">Duo UDP Socket Set Interface</span></span> 

#### <a name="nxd_udp_socket_set_interface"></a><span data-ttu-id="213c9-1183">nxd_udp_socket_set_interface</span><span class="sxs-lookup"><span data-stu-id="213c9-1183">nxd_udp_socket_set_interface</span></span>

<span data-ttu-id="213c9-1184">**Icona** ![ di Icona dell'interfaccia del set di socket U D P Duo](./media/user-guide/netx-events/image75.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1184">**Icon** ![Duo U D P socket set interface icon](./media/user-guide/netx-events/image75.png)</span></span>

<span data-ttu-id="213c9-1185">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1185">**Description**</span></span>

<span data-ttu-id="213c9-1186">Questo evento rappresenta l'impostazione dell'interfaccia in uscita del socket UDP specificato sull'interfaccia corrispondente all'ID dell'interfaccia di input tramite nxd_udp_socket_set_interface.</span><span class="sxs-lookup"><span data-stu-id="213c9-1186">This event represents setting the specified UDP socket outgoing interface to the interface corresponding to the input interface ID via nxd_udp_socket_set_interface.</span></span>

<span data-ttu-id="213c9-1187">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1187">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1188">Informazioni sul campo 1: puntatore al socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1188">Info Field 1: Pointer to UDP Socket</span></span>
- <span data-ttu-id="213c9-1189">Informazioni sul campo 2: ID interfaccia</span><span class="sxs-lookup"><span data-stu-id="213c9-1189">Info Field 2: Interface ID</span></span>
- <span data-ttu-id="213c9-1190">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1190">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1191">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1191">Info Field 4: Not used</span></span>

### <a name="duo-udp-source-extract"></a><span data-ttu-id="213c9-1192">Estrazione origine UDP Duo</span><span class="sxs-lookup"><span data-stu-id="213c9-1192">Duo UDP Source Extract</span></span> 

#### <a name="nxd_udp_socket_extract"></a><span data-ttu-id="213c9-1193">nxd_udp_socket_extract</span><span class="sxs-lookup"><span data-stu-id="213c9-1193">nxd_udp_socket_extract</span></span>

<span data-ttu-id="213c9-1194">**Icona** ![ di Icona estrazione origine Duo U D P](./media/user-guide/netx-events/image76.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1194">**Icon** ![Duo U D P source extract icon](./media/user-guide/netx-events/image76.png)</span></span>

<span data-ttu-id="213c9-1195">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1195">**Description**</span></span>

<span data-ttu-id="213c9-1196">Questo evento rappresenta l'estrazione dell'indirizzo IP e della porta di origine di un pacchetto ricevuto (IPv4 o IPv6).</span><span class="sxs-lookup"><span data-stu-id="213c9-1196">This event represents extracting the IP address and source port of a received packet (either IPv4 or IPv6).</span></span> <span data-ttu-id="213c9-1197">Se IPv6, la quarta parola (meno significativa) dell'indirizzo IP viene restituita tramite nxd_udp_source_extract.</span><span class="sxs-lookup"><span data-stu-id="213c9-1197">If IPv6, the fourth word (least significant) of the IP address is returned via nxd_udp_source_extract.</span></span>

<span data-ttu-id="213c9-1198">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1198">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1199">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1199">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="213c9-1200">Informazioni sul campo 2: versione IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1200">Info Field 2: IP version</span></span>
- <span data-ttu-id="213c9-1201">Informazioni sul campo 3: indirizzo IP di origine (IPv4 o IPv6)</span><span class="sxs-lookup"><span data-stu-id="213c9-1201">Info Field 3: Source IP address (IPv4 or IPv6)</span></span>
- <span data-ttu-id="213c9-1202">Campo dati 4: porta di origine</span><span class="sxs-lookup"><span data-stu-id="213c9-1202">Info Field 4: Source port</span></span>

### <a name="icmp-enable"></a><span data-ttu-id="213c9-1203">Abilita ICMP</span><span class="sxs-lookup"><span data-stu-id="213c9-1203">ICMP Enable</span></span> 

#### <a name="nx_icmp_enable"></a><span data-ttu-id="213c9-1204">nx_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1204">nx_icmp_enable</span></span>

<span data-ttu-id="213c9-1205">**Icona** ![ di Icona di abilitazione I C M P](./media/user-guide/netx-events/image77.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1205">**Icon** ![I C M P enable icon](./media/user-guide/netx-events/image77.png)</span></span>

<span data-ttu-id="213c9-1206">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1206">**Description**</span></span>

<span data-ttu-id="213c9-1207">Questo evento rappresenta l'abilitazione di ICMP tramite nx_icmp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1207">This event represents enabling ICMP via nx_icmp_enable.</span></span>

<span data-ttu-id="213c9-1208">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1208">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1209">Info Field 1: puntatore all'istanza IP l;</span><span class="sxs-lookup"><span data-stu-id="213c9-1209">Info Field 1: Pointer to the IP instance l;</span></span>
- <span data-ttu-id="213c9-1210">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1210">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1211">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1211">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1212">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1212">Info Field 4: Not used</span></span>

### <a name="icmp-information-get"></a><span data-ttu-id="213c9-1213">Informazioni sul protocollo ICMP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1213">ICMP Information Get</span></span> 

#### <a name="nx_icmp_info_get"></a><span data-ttu-id="213c9-1214">nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1214">nx_icmp_info_get</span></span>

<span data-ttu-id="213c9-1215">**Icona** ![ di Icona di Get di informazioni C M P](./media/user-guide/netx-events/image78.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1215">**Icon** ![I C M P information get icon](./media/user-guide/netx-events/image78.png)</span></span>

<span data-ttu-id="213c9-1216">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1216">**Description**</span></span>

<span data-ttu-id="213c9-1217">Questo evento rappresenta il recupero di informazioni tramite nx_icmp_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1217">This event represents getting information via nx_icmp_info_get.</span></span>

<span data-ttu-id="213c9-1218">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1218">**Information Fields**</span></span>
- <span data-ttu-id="213c9-1219">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1219">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1220">Campo informazioni 2: ping inviati</span><span class="sxs-lookup"><span data-stu-id="213c9-1220">Info Field 2: Pings sent</span></span>
- <span data-ttu-id="213c9-1221">Informazioni sul campo 3: ping risposte</span><span class="sxs-lookup"><span data-stu-id="213c9-1221">Info Field 3: Ping responses</span></span>
- <span data-ttu-id="213c9-1222">Campo dati 4: ping ricevuti</span><span class="sxs-lookup"><span data-stu-id="213c9-1222">Info Field 4: Pings received</span></span>

### <a name="icmp-ping"></a><span data-ttu-id="213c9-1223">Ping ICMP</span><span class="sxs-lookup"><span data-stu-id="213c9-1223">ICMP Ping</span></span> 

#### <a name="nx_icmp_ping"></a><span data-ttu-id="213c9-1224">nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="213c9-1224">nx_icmp_ping</span></span>

<span data-ttu-id="213c9-1225">**Icona** ![ di Icona ping I C M P](./media/user-guide/netx-events/image79.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1225">**Icon** ![I C M P ping icon](./media/user-guide/netx-events/image79.png)</span></span>

<span data-ttu-id="213c9-1226">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1226">**Description**</span></span>

<span data-ttu-id="213c9-1227">Questo evento rappresenta il ping di un indirizzo IP di destinazione tramite nx_icmp_ping.</span><span class="sxs-lookup"><span data-stu-id="213c9-1227">This event represents pinging a target IP address via nx_icmp_ping.</span></span>

<span data-ttu-id="213c9-1228">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1228">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1229">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1229">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1230">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1230">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-1231">Informazioni sul campo 3: puntatore ai dati</span><span class="sxs-lookup"><span data-stu-id="213c9-1231">Info Field 3: Pointer to data</span></span>
- <span data-ttu-id="213c9-1232">Informazioni sul campo 4: dimensioni dei dati</span><span class="sxs-lookup"><span data-stu-id="213c9-1232">Info Field 4: Size of data</span></span>

### <a name="igmp-enable"></a><span data-ttu-id="213c9-1233">Abilitazione IGMP</span><span class="sxs-lookup"><span data-stu-id="213c9-1233">IGMP Enable</span></span> 

#### <a name="nx_icmp_enable"></a><span data-ttu-id="213c9-1234">nx_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1234">nx_icmp_enable</span></span>

<span data-ttu-id="213c9-1235">**Icona** ![ di Icona di abilitazione I G M P](./media/user-guide/netx-events/image80.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1235">**Icon** ![I G M P enable icon](./media/user-guide/netx-events/image80.png)</span></span>

<span data-ttu-id="213c9-1236">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1236">**Description**</span></span>

<span data-ttu-id="213c9-1237">Questo evento rappresenta l'abilitazione di IGMP tramite nx_igmp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1237">This event represents enabling IGMP via nx_igmp_enable.</span></span>

<span data-ttu-id="213c9-1238">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1238">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1239">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1239">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1240">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1240">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1241">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1241">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1242">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1242">Info Field 4: Not used</span></span>

### <a name="igmp-information-get"></a><span data-ttu-id="213c9-1243">Get informazioni IGMP</span><span class="sxs-lookup"><span data-stu-id="213c9-1243">IGMP Information Get</span></span> 

#### <a name="nx_icmp_info_get"></a><span data-ttu-id="213c9-1244">nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1244">nx_icmp_info_get</span></span>

<span data-ttu-id="213c9-1245">**Icona** ![ di Icona di informazioni Get di I G M P](./media/user-guide/netx-events/image81.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1245">**Icon** ![I G M P information get icon](./media/user-guide/netx-events/image81.png)</span></span>

<span data-ttu-id="213c9-1246">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1246">**Description**</span></span>

<span data-ttu-id="213c9-1247">Questo evento rappresenta il recupero di informazioni tramite nx_igmp_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1247">This event represents getting information via nx_igmp_info_get.</span></span>

<span data-ttu-id="213c9-1248">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1248">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1249">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1249">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1250">Campo informazioni 2: report inviati</span><span class="sxs-lookup"><span data-stu-id="213c9-1250">Info Field 2: Reports sent</span></span>
- <span data-ttu-id="213c9-1251">Campo informazioni 3: query ricevute</span><span class="sxs-lookup"><span data-stu-id="213c9-1251">Info Field 3: Queries received</span></span>
- <span data-ttu-id="213c9-1252">Campo informazioni 4: gruppi aggiunti</span><span class="sxs-lookup"><span data-stu-id="213c9-1252">Info Field 4: Groups joined</span></span>

### <a name="igmp-loopback-disable"></a><span data-ttu-id="213c9-1253">Disabilita loopback loopback</span><span class="sxs-lookup"><span data-stu-id="213c9-1253">IGMP Loopback Disable</span></span> 

#### <a name="nx_igmp_loopback_disable"></a><span data-ttu-id="213c9-1254">nx_igmp_loopback_disable</span><span class="sxs-lookup"><span data-stu-id="213c9-1254">nx_igmp_loopback_disable</span></span>

<span data-ttu-id="213c9-1255">**Icona** ![ di Icona di disabilitazione loopback di I G M P](./media/user-guide/netx-events/image82.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1255">**Icon** ![I G M P loopback disable icon](./media/user-guide/netx-events/image82.png)</span></span>

<span data-ttu-id="213c9-1256">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1256">**Description**</span></span>

<span data-ttu-id="213c9-1257">Questo evento rappresenta la disabilitazione del loopback IGMP tramite nx_igmp_loopback_disable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1257">This event represents disabling IGMP loopback via nx_igmp_loopback_disable.</span></span>

<span data-ttu-id="213c9-1258">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1258">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1259">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1259">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1260">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1260">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1261">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1261">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1262">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1262">Info Field 4: Not used</span></span>

### <a name="igmp-loopback-enable"></a><span data-ttu-id="213c9-1263">Abilita loopback loopback</span><span class="sxs-lookup"><span data-stu-id="213c9-1263">IGMP Loopback Enable</span></span> 

#### <a name="nx_igmp_loopback_enable"></a><span data-ttu-id="213c9-1264">nx_igmp_loopback_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1264">nx_igmp_loopback_enable</span></span>

<span data-ttu-id="213c9-1265">**Icona** ![ di Icona Abilita loopback I G M P](./media/user-guide/netx-events/image83.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1265">**Icon** ![I G M P loopback enable icon](./media/user-guide/netx-events/image83.png)</span></span>

<span data-ttu-id="213c9-1266">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1266">**Description**</span></span>

<span data-ttu-id="213c9-1267">Questo evento rappresenta l'abilitazione del loopback IGMP tramite nx_igmp_loopback_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1267">This event represents enabling IGMP loopback via nx_igmp_loopback_enable.</span></span>

<span data-ttu-id="213c9-1268">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1268">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1269">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1269">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1270">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1270">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1271">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1271">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1272">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1272">Info Field 4: Not used</span></span>

### <a name="igmp-multicast-join"></a><span data-ttu-id="213c9-1273">Join multicast IGMP</span><span class="sxs-lookup"><span data-stu-id="213c9-1273">IGMP Multicast Join</span></span> 

#### <a name="nx_igmp_multicast_join"></a><span data-ttu-id="213c9-1274">nx_igmp_multicast_join</span><span class="sxs-lookup"><span data-stu-id="213c9-1274">nx_igmp_multicast_join</span></span>

<span data-ttu-id="213c9-1275">**Icona** ![ di Icona di join multicast I G M P](./media/user-guide/netx-events/image84.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1275">**Icon** ![I G M P multicast join icon](./media/user-guide/netx-events/image84.png)</span></span>

<span data-ttu-id="213c9-1276">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1276">**Description**</span></span>

<span data-ttu-id="213c9-1277">Questo evento rappresenta l'Unione di un gruppo multicast tramite nx_igmp_multicast_join.</span><span class="sxs-lookup"><span data-stu-id="213c9-1277">This event represents joining a multicast group via nx_igmp_multicast_join.</span></span>

<span data-ttu-id="213c9-1278">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1278">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1279">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1279">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1280">Informazioni sul campo 2: indirizzo IP del gruppo</span><span class="sxs-lookup"><span data-stu-id="213c9-1280">Info Field 2: Group IP address</span></span>
- <span data-ttu-id="213c9-1281">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1281">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1282">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1282">Info Field 4: Not used</span></span>

### <a name="igmp-multicast-leave"></a><span data-ttu-id="213c9-1283">Uscita multicast IGMP</span><span class="sxs-lookup"><span data-stu-id="213c9-1283">IGMP Multicast Leave</span></span> 

#### <a name="nx_igmp_multicast_leave"></a><span data-ttu-id="213c9-1284">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="213c9-1284">nx_igmp_multicast_leave</span></span>

<span data-ttu-id="213c9-1285">**Icona** ![ di Icona di uscita multicast I G M P](./media/user-guide/netx-events/image85.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1285">**Icon** ![I G M P multicast leave icon](./media/user-guide/netx-events/image85.png)</span></span>

<span data-ttu-id="213c9-1286">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1286">**Description**</span></span>

<span data-ttu-id="213c9-1287">Questo evento rappresenta l'uscita da un gruppo multicast tramite nx_igmp_multicast_leave.</span><span class="sxs-lookup"><span data-stu-id="213c9-1287">This event represents leaving a multicast group via nx_igmp_multicast_leave.</span></span>

<span data-ttu-id="213c9-1288">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1288">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1289">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1289">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1290">Informazioni sul campo 2: indirizzo IP del gruppo</span><span class="sxs-lookup"><span data-stu-id="213c9-1290">Info Field 2: Group IP address</span></span>
- <span data-ttu-id="213c9-1291">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1291">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1292">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1292">Info Field 4: Not used</span></span>

### <a name="ip-address-change-notify"></a><span data-ttu-id="213c9-1293">Notifica di modifica degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1293">IP Address Change Notify</span></span> 

#### <a name="nx_ip_address_change_notify"></a><span data-ttu-id="213c9-1294">nx_ip_address_change_notify</span><span class="sxs-lookup"><span data-stu-id="213c9-1294">nx_ip_address_change_notify</span></span>

<span data-ttu-id="213c9-1295">**Icona** ![ di Icona di notifica della modifica dell'indirizzo I P](./media/user-guide/netx-events/image86.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1295">**Icon** ![I P address change notify icon](./media/user-guide/netx-events/image86.png)</span></span>

<span data-ttu-id="213c9-1296">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1296">**Description**</span></span>

<span data-ttu-id="213c9-1297">Questo evento rappresenta la registrazione per la notifica di modifica IP tramite nx_ip_address_change_notify.</span><span class="sxs-lookup"><span data-stu-id="213c9-1297">This event represents registering for IP change notification via nx_ip_address_change_notify.</span></span>

<span data-ttu-id="213c9-1298">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1298">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1299">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1299">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1300">Informazioni sul campo 2: puntatore alla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="213c9-1300">Info Field 2: Callback function pointer</span></span>
- <span data-ttu-id="213c9-1301">Campo informazioni 3: puntatore a informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="213c9-1301">Info Field 3: Additional information pointer</span></span>
- <span data-ttu-id="213c9-1302">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1302">Info Field 4: Not used</span></span>

### <a name="ip-address-get"></a><span data-ttu-id="213c9-1303">Indirizzo IP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1303">IP Address Get</span></span> 

#### <a name="nx_ip_address_get"></a><span data-ttu-id="213c9-1304">nx_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1304">nx_ip_address_get</span></span>

<span data-ttu-id="213c9-1305">**Icona** ![ di Icona Ottieni indirizzo I P](./media/user-guide/netx-events/image87.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1305">**Icon** ![I P address get icon](./media/user-guide/netx-events/image87.png)</span></span>

<span data-ttu-id="213c9-1306">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1306">**Description**</span></span>

<span data-ttu-id="213c9-1307">Questo evento rappresenta l'ottenimento dell'indirizzo IP tramite nx_ip_address_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1307">This event represents getting the IP address via nx_ip_address_get.</span></span>

<span data-ttu-id="213c9-1308">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1308">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1309">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1309">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1310">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1310">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-1311">Informazioni sul campo 3: Network mask</span><span class="sxs-lookup"><span data-stu-id="213c9-1311">Info Field 3: Network mask</span></span>
- <span data-ttu-id="213c9-1312">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1312">Info Field 4: Not used</span></span>

### <a name="ip-address-set"></a><span data-ttu-id="213c9-1313">Set di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1313">IP Address Set</span></span> 

#### <a name="nx_ip_address_set"></a><span data-ttu-id="213c9-1314">nx_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1314">nx_ip_address_set</span></span>

<span data-ttu-id="213c9-1315">**Icona** ![ di Icona del set di indirizzi I P](./media/user-guide/netx-events/image88.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1315">**Icon** ![I P address set icon](./media/user-guide/netx-events/image88.png)</span></span>

<span data-ttu-id="213c9-1316">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1316">**Description**</span></span>

<span data-ttu-id="213c9-1317">Questo evento rappresenta l'impostazione dell'indirizzo IP tramite nx_ip_address_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1317">This event represents setting the IP address via nx_ip_address_set.</span></span>

<span data-ttu-id="213c9-1318">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1318">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1319">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1319">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1320">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1320">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-1321">Informazioni sul campo 3: Network mask</span><span class="sxs-lookup"><span data-stu-id="213c9-1321">Info Field 3: Network mask</span></span>
- <span data-ttu-id="213c9-1322">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1322">Info Field 4: Not used</span></span>

### <a name="ip-create"></a><span data-ttu-id="213c9-1323">Creazione IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1323">IP Create</span></span> 

#### <a name="nx_ip_create"></a><span data-ttu-id="213c9-1324">nx_ip_create</span><span class="sxs-lookup"><span data-stu-id="213c9-1324">nx_ip_create</span></span>

<span data-ttu-id="213c9-1325">**Icona** ![ di Icona di creazione P](./media/user-guide/netx-events/image89.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1325">**Icon** ![I P create icon](./media/user-guide/netx-events/image89.png)</span></span>

<span data-ttu-id="213c9-1326">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1326">**Description**</span></span>

<span data-ttu-id="213c9-1327">Questo evento rappresenta la creazione di un'istanza IP tramite nx_ip_create.</span><span class="sxs-lookup"><span data-stu-id="213c9-1327">This event represents creating an IP instance via nx_ip_create.</span></span>

<span data-ttu-id="213c9-1328">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1328">**Information Fields**</span></span> 
- <span data-ttu-id="213c9-1329">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1329">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1330">Campo informazioni 2: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1330">Info Field 2: IP address</span></span>
- <span data-ttu-id="213c9-1331">Informazioni sul campo 3: Network mask</span><span class="sxs-lookup"><span data-stu-id="213c9-1331">Info Field 3: Network mask</span></span>
- <span data-ttu-id="213c9-1332">Informazioni sul campo 4: puntatore al pool di pacchetti predefinito</span><span class="sxs-lookup"><span data-stu-id="213c9-1332">Info Field 4: Default packet pool pointer</span></span>

### <a name="ip-delete"></a><span data-ttu-id="213c9-1333">Eliminazione IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1333">IP Delete</span></span> 

#### <a name="nx_ip_delete"></a><span data-ttu-id="213c9-1334">nx_ip_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-1334">nx_ip_delete</span></span>

<span data-ttu-id="213c9-1335">**Icona** ![ di Icona di eliminazione I P](./media/user-guide/netx-events/image90.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1335">**Icon** ![I P delete icon](./media/user-guide/netx-events/image90.png)</span></span>

<span data-ttu-id="213c9-1336">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1336">**Description**</span></span>

<span data-ttu-id="213c9-1337">Questo evento rappresenta l'eliminazione di un'istanza IP tramite nx_ip_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-1337">This event represents deleting an IP instance via nx_ip_delete.</span></span>

<span data-ttu-id="213c9-1338">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1338">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1339">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1339">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1340">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1340">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1341">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1341">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1342">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1342">Info Field 4: Not used</span></span>

### <a name="ip-driver-direct-command"></a><span data-ttu-id="213c9-1343">Comando Direct driver IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1343">IP Driver Direct Command</span></span> 

#### <a name="nx_ip_driver_direct_command"></a><span data-ttu-id="213c9-1344">nx_ip_driver_direct_command</span><span class="sxs-lookup"><span data-stu-id="213c9-1344">nx_ip_driver_direct_command</span></span>

<span data-ttu-id="213c9-1345">**Icona** ![ di Icona comando diretto driver I P](./media/user-guide/netx-events/image91.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1345">**Icon** ![I P driver direct command icon](./media/user-guide/netx-events/image91.png)</span></span>

<span data-ttu-id="213c9-1346">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1346">**Description**</span></span>

<span data-ttu-id="213c9-1347">Questo evento rappresenta un comando di driver I/O diretto tramite nx_ip_driver_direct_command.</span><span class="sxs-lookup"><span data-stu-id="213c9-1347">This event represents a direct I/O driver command via nx_ip_driver_direct_command.</span></span>

<span data-ttu-id="213c9-1348">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1348">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1349">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1349">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1350">Informazioni sul campo 2: comando driver</span><span class="sxs-lookup"><span data-stu-id="213c9-1350">Info Field 2: Driver command</span></span>
- <span data-ttu-id="213c9-1351">Informazioni campo 3: valore restituito</span><span class="sxs-lookup"><span data-stu-id="213c9-1351">Info Field 3: Return value</span></span>
- <span data-ttu-id="213c9-1352">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1352">Info Field 4: Not used</span></span>

### <a name="ip-forwarding-disable"></a><span data-ttu-id="213c9-1353">Disabilitazione dell'invio IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1353">IP Forwarding Disable</span></span> 

#### <a name="nx_ip_forwarding_disable"></a><span data-ttu-id="213c9-1354">nx_ip_forwarding_disable</span><span class="sxs-lookup"><span data-stu-id="213c9-1354">nx_ip_forwarding_disable</span></span>

<span data-ttu-id="213c9-1355">**Icona** ![ di Icona di disabilitazione dell'invio P](./media/user-guide/netx-events/image92.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1355">**Icon** ![I P forwarding disable icon](./media/user-guide/netx-events/image92.png)</span></span>

<span data-ttu-id="213c9-1356">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1356">**Description**</span></span>

<span data-ttu-id="213c9-1357">Questo evento rappresenta la disabilitazione dell'invio IP tramite nx_ip_forwarding_disable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1357">This event represents disabling IP forwarding via nx_ip_forwarding_disable.</span></span>

<span data-ttu-id="213c9-1358">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1358">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1359">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1359">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1360">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1360">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1361">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1361">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1362">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1362">Info Field 4: Not used</span></span>

### <a name="ip-forwarding-enable"></a><span data-ttu-id="213c9-1363">Abilitazione dell'invio IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1363">IP Forwarding Enable</span></span> 

#### <a name="nx_ip_forwarding_enable"></a><span data-ttu-id="213c9-1364">nx_ip_forwarding_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1364">nx_ip_forwarding_enable</span></span>

<span data-ttu-id="213c9-1365">**Icona** ![ di Icona Abilita l'invio P](./media/user-guide/netx-events/image93.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1365">**Icon** ![I P forwarding enable icon](./media/user-guide/netx-events/image93.png)</span></span>

<span data-ttu-id="213c9-1366">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1366">**Description**</span></span>

<span data-ttu-id="213c9-1367">Questo evento rappresenta l'abilitazione dell'invio IP tramite nx_ip_forwarding_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1367">This event represents enabling IP forwarding via nx_ip_forwarding_enable.</span></span>

<span data-ttu-id="213c9-1368">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1368">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1369">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1369">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1370">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1370">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1371">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1371">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1372">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1372">Info Field 4: Not used</span></span>

### <a name="ip-fragment-disable"></a><span data-ttu-id="213c9-1373">Disabilitazione frammenti IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1373">IP Fragment Disable</span></span> 

#### <a name="nx_ip_fragment_disable"></a><span data-ttu-id="213c9-1374">nx_ip_fragment_disable</span><span class="sxs-lookup"><span data-stu-id="213c9-1374">nx_ip_fragment_disable</span></span>

<span data-ttu-id="213c9-1375">**Icona** ![ di Icona di disabilitazione del frammento I P](./media/user-guide/netx-events/image94.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1375">**Icon** ![I P fragment disable icon](./media/user-guide/netx-events/image94.png)</span></span>

<span data-ttu-id="213c9-1376">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1376">**Description**</span></span>

<span data-ttu-id="213c9-1377">Questo evento rappresenta la disabilitazione della frammentazione IP tramite nx_ip_fragment_disable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1377">This event represents disabling IP fragmenting via nx_ip_fragment_disable.</span></span>

<span data-ttu-id="213c9-1378">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1378">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1379">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1379">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1380">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1380">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1381">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1381">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1382">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1382">Info Field 4: Not used</span></span>

### <a name="ip-fragment-enable"></a><span data-ttu-id="213c9-1383">Abilitazione frammenti IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1383">IP Fragment Enable</span></span> 

#### <a name="nx_ip_fragment_enable"></a><span data-ttu-id="213c9-1384">nx_ip_fragment_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1384">nx_ip_fragment_enable</span></span>

<span data-ttu-id="213c9-1385">**Icona** ![ di Icona Abilita frammento I P](./media/user-guide/netx-events/image95.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1385">**Icon** ![I P fragment enable icon](./media/user-guide/netx-events/image95.png)</span></span>

<span data-ttu-id="213c9-1386">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1386">**Description**</span></span>

<span data-ttu-id="213c9-1387">Questo evento rappresenta l'abilitazione della frammentazione IP tramite nx_ip_fragment_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1387">This event represents enabling IP fragmenting via nx_ip_fragment_enable.</span></span>

<span data-ttu-id="213c9-1388">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1388">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1389">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1389">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1390">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1390">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1391">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1391">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1392">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1392">Info Field 4: Not used</span></span>

### <a name="ip-gateway-address-set"></a><span data-ttu-id="213c9-1393">Set di indirizzi IP gateway</span><span class="sxs-lookup"><span data-stu-id="213c9-1393">IP Gateway Address Set</span></span> 

#### <a name="nx_ip_gateway_address_set"></a><span data-ttu-id="213c9-1394">nx_ip_gateway_address_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1394">nx_ip_gateway_address_set</span></span>

<span data-ttu-id="213c9-1395">**Icona** ![ di Icona del set di indirizzi del gateway I P](./media/user-guide/netx-events/image96.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1395">**Icon** ![I P gateway address set icon](./media/user-guide/netx-events/image96.png)</span></span>

<span data-ttu-id="213c9-1396">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1396">**Description**</span></span>

<span data-ttu-id="213c9-1397">Questo evento rappresenta l'impostazione dell'indirizzo IP del gateway tramite nx_ip_gateway_address_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1397">This event represents setting the gateway IP address via nx_ip_gateway_address_set.</span></span>

<span data-ttu-id="213c9-1398">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1398">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1399">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1399">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1400">Informazioni sul campo 2: indirizzo IP del gateway</span><span class="sxs-lookup"><span data-stu-id="213c9-1400">Info Field 2: Gateway IP address</span></span>
- <span data-ttu-id="213c9-1401">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1401">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1402">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1402">Info Field 4: Not used</span></span>

### <a name="ip-information-get"></a><span data-ttu-id="213c9-1403">Informazioni IP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1403">IP Information Get</span></span> 

#### <a name="nx_ip_info_get"></a><span data-ttu-id="213c9-1404">nx_ip_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1404">nx_ip_info_get</span></span>

<span data-ttu-id="213c9-1405">**Icona** ![ di Icona di Get delle informazioni P](./media/user-guide/netx-events/image97.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1405">**Icon** ![I P information get icon](./media/user-guide/netx-events/image97.png)</span></span>

<span data-ttu-id="213c9-1406">**Descrizione** di Questo evento rappresenta l'acquisizione di informazioni IP tramite nx_ip_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1406">**Description** This event represents getting IP information via nx_ip_info_get.</span></span>

<span data-ttu-id="213c9-1407">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1407">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1408">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1408">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1409">Campo informazioni 2: byte IP inviati</span><span class="sxs-lookup"><span data-stu-id="213c9-1409">Info Field 2: IP bytes sent</span></span>
- <span data-ttu-id="213c9-1410">Campo informazioni 3: byte IP ricevuti</span><span class="sxs-lookup"><span data-stu-id="213c9-1410">Info Field 3: IP bytes received</span></span>
- <span data-ttu-id="213c9-1411">Campo dati 4: pacchetti IP eliminati</span><span class="sxs-lookup"><span data-stu-id="213c9-1411">Info Field 4: IP packets dropped</span></span>

### <a name="ip-interface-attach"></a><span data-ttu-id="213c9-1412">Connessione interfaccia IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1412">IP Interface Attach</span></span> 

#### <a name="nx_interface_attach"></a><span data-ttu-id="213c9-1413">nx_interface_attach</span><span class="sxs-lookup"><span data-stu-id="213c9-1413">nx_interface_attach</span></span>

<span data-ttu-id="213c9-1414">**Icona** ![ di Icona di connessione Iterface P](./media/user-guide/netx-events/image98.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1414">**Icon** ![I P iterface attach icon](./media/user-guide/netx-events/image98.png)</span></span>

<span data-ttu-id="213c9-1415">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1415">**Description**</span></span>

<span data-ttu-id="213c9-1416">Questo evento rappresenta un'interfaccia di rete secondaria da collegare all'istanza IP tramite nx_ip_interface_attach.</span><span class="sxs-lookup"><span data-stu-id="213c9-1416">This event represents a secondary network interface being attached to the IP instance via nx_ip_interface_attach.</span></span>

<span data-ttu-id="213c9-1417">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1417">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1418">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1418">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1419">Informazioni sul campo 2: indirizzo IP dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="213c9-1419">Info Field 2: Interface IP Address</span></span>
- <span data-ttu-id="213c9-1420">Campo informazioni 3: indice nella tabella dell'interfaccia IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1420">Info Field 3: Index into IP interface table</span></span>
- <span data-ttu-id="213c9-1421">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1421">Info Field 4: Not used</span></span>

### <a name="ip-interface-info-get"></a><span data-ttu-id="213c9-1422">Informazioni sull'interfaccia IP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1422">IP Interface Info Get</span></span> 

#### <a name="nx_ip_interface_info_get"></a><span data-ttu-id="213c9-1423">nx_ip_interface_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1423">nx_ip_interface_info_get</span></span>

<span data-ttu-id="213c9-1424">**Icona** ![ di Icona di informazioni sull'interfaccia IP Get](./media/user-guide/netx-events/image99.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1424">**Icon** ![ IP interface info get icon](./media/user-guide/netx-events/image99.png)</span></span>

<span data-ttu-id="213c9-1425">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1425">**Description**</span></span>

<span data-ttu-id="213c9-1426">Questo evento rappresenta le informazioni recuperate dall'interfaccia di rete specificata tramite nx_ip_interface_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1426">This event represents information retrieved from the specified network interface via nx_ip_interface_info_get.</span></span>

<span data-ttu-id="213c9-1427">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1427">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1428">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1428">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1429">Informazioni sul campo 2: indirizzo IP dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="213c9-1429">Info Field 2: Interface IP address</span></span>
- <span data-ttu-id="213c9-1430">Informazioni sul campo 3: indirizzo MAC dell'interfaccia MSB</span><span class="sxs-lookup"><span data-stu-id="213c9-1430">Info Field 3: Interface MAC address msb</span></span>
- <span data-ttu-id="213c9-1431">Informazioni campo 4: indirizzo MAC interfaccia lsb</span><span class="sxs-lookup"><span data-stu-id="213c9-1431">Info Field 4: Interface MAC address lsb</span></span>

### <a name="ip-raw-packet-disable"></a><span data-ttu-id="213c9-1432">Disabilitazione pacchetto non elaborato IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1432">IP Raw Packet Disable</span></span> 

#### <a name="nx_ip_raw_packet_disable"></a><span data-ttu-id="213c9-1433">nx_ip_raw_packet_disable</span><span class="sxs-lookup"><span data-stu-id="213c9-1433">nx_ip_raw_packet_disable</span></span>

<span data-ttu-id="213c9-1434">**Icona** ![ di Icona di disabilitazione pacchetti non elaborati](./media/user-guide/netx-events/image100.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1434">**Icon** ![I P raw packet disable icon](./media/user-guide/netx-events/image100.png)</span></span>

<span data-ttu-id="213c9-1435">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1435">**Description**</span></span>

<span data-ttu-id="213c9-1436">Questo evento rappresenta la disabilitazione della comunicazione di pacchetti IP non elaborati tramite nx_ip_raw_packet_disable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1436">This event represents disabling raw IP packet communication via nx_ip_raw_packet_disable.</span></span>

<span data-ttu-id="213c9-1437">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1437">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1438">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1438">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1439">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1439">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1440">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1440">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1441">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1441">Info Field 4: Not used</span></span>

### <a name="ip-raw-packet-enable"></a><span data-ttu-id="213c9-1442">Abilitazione pacchetti non elaborati IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1442">IP Raw Packet Enable</span></span> 

#### <a name="nx_ip_raw_packet_enable"></a><span data-ttu-id="213c9-1443">nx_ip_raw_packet_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1443">nx_ip_raw_packet_enable</span></span>

<span data-ttu-id="213c9-1444">**Icona** ![ di Icona di abilitazione di pacchetti non elaborati](./media/user-guide/netx-events/image101.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1444">**Icon** ![I P raw packet enable icon](./media/user-guide/netx-events/image101.png)</span></span>

<span data-ttu-id="213c9-1445">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1445">**Description**</span></span>

<span data-ttu-id="213c9-1446">Questo evento rappresenta l'abilitazione della comunicazione di pacchetti IP non elaborati tramite nx_ip_raw_packet_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1446">This event represents enabling raw IP packet communication via nx_ip_raw_packet_enable.</span></span>

<span data-ttu-id="213c9-1447">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1447">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1448">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1448">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1449">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1449">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1450">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1450">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1451">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1451">Info Field 4: Not used</span></span>

### <a name="ip-raw-packet-receive"></a><span data-ttu-id="213c9-1452">Ricezione pacchetti non elaborati IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1452">IP Raw Packet Receive</span></span> 

#### <a name="nx_ip_raw_packet_receive"></a><span data-ttu-id="213c9-1453">nx_ip_raw_packet_receive</span><span class="sxs-lookup"><span data-stu-id="213c9-1453">nx_ip_raw_packet_receive</span></span>

<span data-ttu-id="213c9-1454">**Icona** ![ di Icona di ricezione di pacchetti non elaborati](./media/user-guide/netx-events/image102.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1454">**Icon** ![I P raw packet receive icon](./media/user-guide/netx-events/image102.png)</span></span>

<span data-ttu-id="213c9-1455">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1455">**Description**</span></span>

<span data-ttu-id="213c9-1456">Questo evento rappresenta la ricezione di un pacchetto IP non elaborato tramite nx_ip_raw_packet_receive.</span><span class="sxs-lookup"><span data-stu-id="213c9-1456">This event represents receiving a raw IP packet via nx_ip_raw_packet_receive.</span></span>

<span data-ttu-id="213c9-1457">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1457">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1458">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1458">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1459">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1459">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-1460">Informazioni sul campo 3: wait-opzione</span><span class="sxs-lookup"><span data-stu-id="213c9-1460">Info Field 3: Wait option</span></span>
- <span data-ttu-id="213c9-1461">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1461">Info Field 4: Not used</span></span>

### <a name="ip-raw-packet-send"></a><span data-ttu-id="213c9-1462">Invio pacchetti non elaborati IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1462">IP Raw Packet Send</span></span> 

#### <a name="nx_ip_raw_packet_send"></a><span data-ttu-id="213c9-1463">nx_ip_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="213c9-1463">nx_ip_raw_packet_send</span></span>

<span data-ttu-id="213c9-1464">**Icona** ![ di Icona di invio di pacchetti non elaborati](./media/user-guide/netx-events/image103.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1464">**Icon** ![I P raw packet send icon](./media/user-guide/netx-events/image103.png)</span></span>

<span data-ttu-id="213c9-1465">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1465">**Description**</span></span>

<span data-ttu-id="213c9-1466">Questo evento rappresenta l'invio di un pacchetto IP non elaborato tramite nx_ip_raw_packet_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-1466">This event represents sending a raw IP packet via nx_ip_raw_packet_send.</span></span>

<span data-ttu-id="213c9-1467">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1467">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1468">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1468">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1469">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1469">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-1470">Informazioni sul campo 3: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-1470">Info Field 3: Destination IP address</span></span>
- <span data-ttu-id="213c9-1471">Informazioni sul campo 4: tipo di servizio</span><span class="sxs-lookup"><span data-stu-id="213c9-1471">Info Field 4: Type of service</span></span>

### <a name="ip-static-route-add"></a><span data-ttu-id="213c9-1472">Aggiunta route statica IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1472">IP Static Route Add</span></span> 

#### <a name="nx_ip_static_route_add"></a><span data-ttu-id="213c9-1473">nx_ip_static_route_add</span><span class="sxs-lookup"><span data-stu-id="213c9-1473">nx_ip_static_route_add</span></span>

<span data-ttu-id="213c9-1474">**Icona** ![ di Icona di aggiunta statica route I P](./media/user-guide/netx-events/image104.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1474">**Icon** ![I P static route add icon](./media/user-guide/netx-events/image104.png)</span></span>

<span data-ttu-id="213c9-1475">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1475">**Description**</span></span>

<span data-ttu-id="213c9-1476">Questo evento rappresenta una route statica da aggiungere alla tabella di routing dell'istanza IP tramite nx_ip_static_route_add.</span><span class="sxs-lookup"><span data-stu-id="213c9-1476">This event represents a static route being added to the IP instance routing table via nx_ip_static_route_add.</span></span>

<span data-ttu-id="213c9-1477">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1477">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1478">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1478">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1479">Informazioni sul campo 2: indirizzo di rete</span><span class="sxs-lookup"><span data-stu-id="213c9-1479">Info Field 2: Network address</span></span>
- <span data-ttu-id="213c9-1480">Informazioni sul campo 3: Network mask</span><span class="sxs-lookup"><span data-stu-id="213c9-1480">Info Field 3: Network mask</span></span>
- <span data-ttu-id="213c9-1481">Campo informazioni 4: hop successivo</span><span class="sxs-lookup"><span data-stu-id="213c9-1481">Info Field 4: Next hop</span></span>

### <a name="ip-static-route-delete"></a><span data-ttu-id="213c9-1482">Eliminazione route statica IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1482">IP Static Route Delete</span></span> 

#### <a name="nx_ip_static_route_delete"></a><span data-ttu-id="213c9-1483">nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-1483">nx_ip_static_route_delete</span></span>

<span data-ttu-id="213c9-1484">**Icona** ![ di Icona di eliminazione statica di I P](./media/user-guide/netx-events/image105.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1484">**Icon** ![I P static rute delete icon](./media/user-guide/netx-events/image105.png)</span></span>

<span data-ttu-id="213c9-1485">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1485">**Description**</span></span>

<span data-ttu-id="213c9-1486">Questo evento rappresenta una route statica che viene rimossa dalla tabella di routing dell'istanza IP tramite nx_ip_static_route_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-1486">This event represents a static route being removed from the IP instance routing table via nx_ip_static_route_delete.</span></span>

<span data-ttu-id="213c9-1487">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1487">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1488">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1488">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1489">Informazioni sul campo 2: indirizzo di rete</span><span class="sxs-lookup"><span data-stu-id="213c9-1489">Info Field 2: Network address</span></span>
- <span data-ttu-id="213c9-1490">Informazioni sul campo 3: Network mask</span><span class="sxs-lookup"><span data-stu-id="213c9-1490">Info Field 3: Network mask</span></span>
- <span data-ttu-id="213c9-1491">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1491">Info Field 4: Not used</span></span>

### <a name="ip-status-check"></a><span data-ttu-id="213c9-1492">Verifica stato IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1492">IP Status Check</span></span> 

#### <a name="nx_ip_status_check"></a><span data-ttu-id="213c9-1493">nx_ip_status_check</span><span class="sxs-lookup"><span data-stu-id="213c9-1493">nx_ip_status_check</span></span>

<span data-ttu-id="213c9-1494">**Icona** ![ di Icona di controllo stato I P](./media/user-guide/netx-events/image106.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1494">**Icon** ![I P status check icon](./media/user-guide/netx-events/image106.png)</span></span>

<span data-ttu-id="213c9-1495">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1495">**Description**</span></span>

<span data-ttu-id="213c9-1496">Questo evento rappresenta il controllo dello stato IP tramite nx_ip_status_check.</span><span class="sxs-lookup"><span data-stu-id="213c9-1496">This event represents checking for an IP status via nx_ip_status_check.</span></span>

<span data-ttu-id="213c9-1497">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="213c9-1497">Information Fields</span></span> 

- <span data-ttu-id="213c9-1498">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1498">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="213c9-1499">Informazioni sul campo 2: stato richiesto</span><span class="sxs-lookup"><span data-stu-id="213c9-1499">Info Field 2: Requested status</span></span>
- <span data-ttu-id="213c9-1500">Campo informazioni 3: stato effettivo</span><span class="sxs-lookup"><span data-stu-id="213c9-1500">Info Field 3: Actual status</span></span>
- <span data-ttu-id="213c9-1501">Informazioni sul campo 4: Wait (opzione)</span><span class="sxs-lookup"><span data-stu-id="213c9-1501">Info Field 4: Wait option</span></span>

### <a name="ipsec-enable"></a><span data-ttu-id="213c9-1502">Abilita IPSEC</span><span class="sxs-lookup"><span data-stu-id="213c9-1502">IPSEC Enable</span></span> 

#### <a name="nx_ipsec_enable"></a><span data-ttu-id="213c9-1503">nx_ipsec_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1503">nx_ipsec_enable</span></span>

<span data-ttu-id="213c9-1504">**Icona** ![ di Icona Enable i P S E C](./media/user-guide/netx-events/image107.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1504">**Icon** ![I P S E C enable icon](./media/user-guide/netx-events/image107.png)</span></span>

<span data-ttu-id="213c9-1505">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1505">**Description**</span></span>

<span data-ttu-id="213c9-1506">Questo evento rappresenta l'abilitazione di servizi IPSec nell'istanza IP fornita tramite nx_ipsec_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1506">This event represents enabling IPSec services on the supplied IP instance via nx_ipsec_enable.</span></span>

<span data-ttu-id="213c9-1507">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1507">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1508">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1508">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1509">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1509">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1510">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1510">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1511">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1511">Info Field 4: Not used</span></span>

### <a name="packet-allocate"></a><span data-ttu-id="213c9-1512">Allocazione pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1512">Packet Allocate</span></span> 

#### <a name="nx_packet_allocate"></a><span data-ttu-id="213c9-1513">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="213c9-1513">nx_packet_allocate</span></span>

<span data-ttu-id="213c9-1514">**Icona** ![ di Icona di allocazione pacchetti](./media/user-guide/netx-events/image108.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1514">**Icon** ![Packet allocate icon](./media/user-guide/netx-events/image108.png)</span></span>

<span data-ttu-id="213c9-1515">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1515">**Description**</span></span>

<span data-ttu-id="213c9-1516">Questo evento rappresenta l'allocazione di un pacchetto tramite nx_packet_allocate.</span><span class="sxs-lookup"><span data-stu-id="213c9-1516">This event represents allocating a packet via nx_packet_allocate.</span></span>

<span data-ttu-id="213c9-1517">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1517">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1518">Informazioni sul campo 1: puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1518">Info Field 1: Pointer to the packet pool</span></span>
- <span data-ttu-id="213c9-1519">Informazioni sul campo 2: puntatore al pacchetto allocato</span><span class="sxs-lookup"><span data-stu-id="213c9-1519">Info Field 2: Pointer to packet allocated</span></span>
- <span data-ttu-id="213c9-1520">Campo informazioni 3: tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1520">Info Field 3: Packet type</span></span>
- <span data-ttu-id="213c9-1521">Campo dati 4: pacchetti disponibili</span><span class="sxs-lookup"><span data-stu-id="213c9-1521">Info Field 4: Available packets</span></span>

### <a name="packet-copy"></a><span data-ttu-id="213c9-1522">Copia pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1522">Packet Copy</span></span> 

#### <a name="nx_packet_copy"></a><span data-ttu-id="213c9-1523">nx_packet_copy</span><span class="sxs-lookup"><span data-stu-id="213c9-1523">nx_packet_copy</span></span>

<span data-ttu-id="213c9-1524">**Icona** ![ di Icona di CPY del pacchetto](./media/user-guide/netx-events/image109.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1524">**Icon** ![Packet cpy icon](./media/user-guide/netx-events/image109.png)</span></span>

<span data-ttu-id="213c9-1525">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1525">**Description**</span></span>

<span data-ttu-id="213c9-1526">Questo evento rappresenta la copia di un pacchetto tramite nx_packet_copy.</span><span class="sxs-lookup"><span data-stu-id="213c9-1526">This event represents copying a packet via nx_packet_copy.</span></span>

<span data-ttu-id="213c9-1527">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1527">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1528">Campo informazioni 2: nuovo puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1528">Info Field 2: New packet pointer</span></span>
- <span data-ttu-id="213c9-1529">Informazioni sul campo 3: puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1529">Info Field 3: Pointer to packet pool</span></span>
- <span data-ttu-id="213c9-1530">Informazioni sul campo 4: Wait (opzione)</span><span class="sxs-lookup"><span data-stu-id="213c9-1530">Info Field 4: Wait option</span></span>

### <a name="packet-data-append"></a><span data-ttu-id="213c9-1531">Accodamento dati pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1531">Packet Data Append</span></span> 

#### <a name="nx_packet_data_append"></a><span data-ttu-id="213c9-1532">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="213c9-1532">nx_packet_data_append</span></span>

<span data-ttu-id="213c9-1533">**Icona** ![ di Icona Accodamento dati pacchetto](./media/user-guide/netx-events/image110.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1533">**Icon** ![Packet data append icon](./media/user-guide/netx-events/image110.png)</span></span>

<span data-ttu-id="213c9-1534">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1534">**Description**</span></span>

<span data-ttu-id="213c9-1535">Questo evento rappresenta l'accodamento dei dati a un pacchetto tramite nx_packet_data_append.</span><span class="sxs-lookup"><span data-stu-id="213c9-1535">This event represents appending data to a packet via nx_packet_data_append.</span></span>

<span data-ttu-id="213c9-1536">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1536">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1537">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1537">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="213c9-1538">Informazioni sul campo 2: puntatore ai dati</span><span class="sxs-lookup"><span data-stu-id="213c9-1538">Info Field 2: Pointer to data</span></span>
- <span data-ttu-id="213c9-1539">Informazioni sul campo 3: dimensioni dei dati</span><span class="sxs-lookup"><span data-stu-id="213c9-1539">Info Field 3: Size of data</span></span>
- <span data-ttu-id="213c9-1540">Informazioni sul campo 4: puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1540">Info Field 4: Pointer to packet pool</span></span>

### <a name="packet-data-extract-offset"></a><span data-ttu-id="213c9-1541">Offset estrazione dati pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1541">Packet Data Extract Offset</span></span> 

#### <a name="nx_udp_source_extract_offset"></a><span data-ttu-id="213c9-1542">nx_udp_source_extract_offset</span><span class="sxs-lookup"><span data-stu-id="213c9-1542">nx_udp_source_extract_offset</span></span>

<span data-ttu-id="213c9-1543">**Icona** ![ di Icona di offset estrazione dati pacchetto](./media/user-guide/netx-events/image111.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1543">**Icon** ![Packet data extract offset icon](./media/user-guide/netx-events/image111.png)</span></span>

<span data-ttu-id="213c9-1544">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1544">**Description**</span></span>

<span data-ttu-id="213c9-1545">Questo evento rappresenta i dati dei pacchetti estratti in un buffer fornito da un pacchetto tramite nx_udp_source_extract_offset.</span><span class="sxs-lookup"><span data-stu-id="213c9-1545">This event represents packet data that is extracted into a supplied buffer from a packet via nx_udp_source_extract_offset.</span></span>

<span data-ttu-id="213c9-1546">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1546">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1547">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1547">Info Field 1: Pointer to packet</span></span>
- <span data-ttu-id="213c9-1548">Informazioni sul campo 2: dimensioni del buffer specificato</span><span class="sxs-lookup"><span data-stu-id="213c9-1548">Info Field 2: Size of specified buffer</span></span>
- <span data-ttu-id="213c9-1549">Campo informazioni 3: numero di byte copiati</span><span class="sxs-lookup"><span data-stu-id="213c9-1549">Info Field 3: Number of bytes copied</span></span>
- <span data-ttu-id="213c9-1550">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1550">Info Field 4: Not used</span></span>

### <a name="packet-data-retrieve"></a><span data-ttu-id="213c9-1551">Recupero dati pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1551">Packet Data Retrieve</span></span> 

#### <a name="nx_packet_data_retrieve"></a><span data-ttu-id="213c9-1552">nx_packet_data_retrieve</span><span class="sxs-lookup"><span data-stu-id="213c9-1552">nx_packet_data_retrieve</span></span>

<span data-ttu-id="213c9-1553">**Icona** ![ di Icona recupero dati pacchetto](./media/user-guide/netx-events/image112.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1553">**Icon** ![Packet data retrieve icon](./media/user-guide/netx-events/image112.png)</span></span>

<span data-ttu-id="213c9-1554">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1554">**Description**</span></span>

<span data-ttu-id="213c9-1555">Questo evento rappresenta il recupero di dati da un pacchetto tramite nx_packet_data_retrieve.</span><span class="sxs-lookup"><span data-stu-id="213c9-1555">This event represents retrieving data from a packet via nx_packet_data_retrieve.</span></span>

<span data-ttu-id="213c9-1556">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1556">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1557">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1557">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="213c9-1558">Informazioni sul campo 2: puntatore all'inizio del buffer</span><span class="sxs-lookup"><span data-stu-id="213c9-1558">Info Field 2: Pointer to start of buffer</span></span>
- <span data-ttu-id="213c9-1559">Campo info 3: byte copiati</span><span class="sxs-lookup"><span data-stu-id="213c9-1559">Info Field 3: Bytes copied</span></span>
- <span data-ttu-id="213c9-1560">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1560">Info Field 4: Not used</span></span>

### <a name="packet-length-get"></a><span data-ttu-id="213c9-1561">Lunghezza pacchetto Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1561">Packet Length Get</span></span> 

#### <a name="nx_packet_length_get"></a><span data-ttu-id="213c9-1562">nx_packet_length_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1562">nx_packet_length_get</span></span>

<span data-ttu-id="213c9-1563">**Icona** ![ di Icona Ottieni lunghezza pacchetto](./media/user-guide/netx-events/image113.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1563">**Icon** ![Packet length get icon](./media/user-guide/netx-events/image113.png)</span></span>

<span data-ttu-id="213c9-1564">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1564">**Description**</span></span>

<span data-ttu-id="213c9-1565">Questo evento rappresenta il recupero della lunghezza di un pacchetto tramite nx_packet_length_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1565">This event represents getting the length of a packet via nx_packet_length_get.</span></span>

<span data-ttu-id="213c9-1566">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1566">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1567">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1567">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="213c9-1568">Informazioni sul campo 2: lunghezza del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1568">Info Field 2: Packet length</span></span>
- <span data-ttu-id="213c9-1569">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1569">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1570">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1570">Info Field 4: Not used</span></span>

### <a name="packet-pool-create"></a><span data-ttu-id="213c9-1571">Creazione pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1571">Packet Pool Create</span></span> 

#### <a name="nx_packet_pool_create"></a><span data-ttu-id="213c9-1572">nx_packet_pool_create</span><span class="sxs-lookup"><span data-stu-id="213c9-1572">nx_packet_pool_create</span></span>

<span data-ttu-id="213c9-1573">**Icona** ![ di Icona di creazione pool di pacchetti](./media/user-guide/netx-events/image114.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1573">**Icon** ![Packet pool create icon](./media/user-guide/netx-events/image114.png)</span></span>

<span data-ttu-id="213c9-1574">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1574">**Description**</span></span>

<span data-ttu-id="213c9-1575">Questo evento rappresenta la creazione di un pool di pacchetti tramite nx_packet_pool_create.</span><span class="sxs-lookup"><span data-stu-id="213c9-1575">This event represents creating a packet pool via nx_packet_pool_create.</span></span>

<span data-ttu-id="213c9-1576">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1576">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1577">Informazioni sul campo 1: puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1577">Info Field 1: Pointer to the packet pool</span></span>
- <span data-ttu-id="213c9-1578">Informazioni sul campo 2: dimensioni del payload del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1578">Info Field 2: Packet payload size</span></span>
- <span data-ttu-id="213c9-1579">Informazioni sul campo 3: puntatore all'area di memoria del pool</span><span class="sxs-lookup"><span data-stu-id="213c9-1579">Info Field 3: Pointer to pool memory area</span></span>
- <span data-ttu-id="213c9-1580">Informazioni campo 4: dimensioni dell'area di memoria del pool</span><span class="sxs-lookup"><span data-stu-id="213c9-1580">Info Field 4: Size of pool memory area</span></span>

### <a name="packet-pool-delete"></a><span data-ttu-id="213c9-1581">Eliminazione pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1581">Packet Pool Delete</span></span> 

#### <a name="nx_packet_pool_delete"></a><span data-ttu-id="213c9-1582">nx_packet_pool_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-1582">nx_packet_pool_delete</span></span>

<span data-ttu-id="213c9-1583">**Icona** ![ di Icona di eliminazione del pool di pacchetti](./media/user-guide/netx-events/image115.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1583">**Icon** ![Packet pool delete icon](./media/user-guide/netx-events/image115.png)</span></span>

<span data-ttu-id="213c9-1584">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1584">**Description**</span></span>

<span data-ttu-id="213c9-1585">Questo evento rappresenta l'eliminazione di un pool di pacchetti tramite nx_packet_pool_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-1585">This event represents deleting a packet pool via nx_packet_pool_delete.</span></span>

<span data-ttu-id="213c9-1586">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1586">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1587">Informazioni sul campo 1: puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1587">Info Field 1: Pointer to the packet pool</span></span>
- <span data-ttu-id="213c9-1588">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1588">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1589">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1589">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1590">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1590">Info Field 4: Not used</span></span>

#### <a name="packet-pool-information-get"></a><span data-ttu-id="213c9-1591">Ottenere informazioni sul pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1591">Packet Pool Information Get</span></span> 

#### <a name="nx_packet_pool_info_get"></a><span data-ttu-id="213c9-1592">nx_packet_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1592">nx_packet_pool_info_get</span></span>

<span data-ttu-id="213c9-1593">**Icona** ![ di Icona Ottieni informazioni sul pool di pacchetti](./media/user-guide/netx-events/image116.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1593">**Icon** ![Packet pool information get icon](./media/user-guide/netx-events/image116.png)</span></span>

<span data-ttu-id="213c9-1594">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1594">**Description**</span></span>

<span data-ttu-id="213c9-1595">Questo evento rappresenta il recupero delle informazioni sul pool di pacchetti tramite nx_packet_pool_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1595">This event represents getting packet pool information via nx_packet_pool_info_get.</span></span>

<span data-ttu-id="213c9-1596">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1596">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1597">Informazioni sul campo 1: puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1597">Info Field 1: Pointer to packet pool</span></span>
- <span data-ttu-id="213c9-1598">Campo informazioni 2: totale pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1598">Info Field 2: Total packets</span></span>
- <span data-ttu-id="213c9-1599">Informazioni sul campo 3: pacchetti disponibili</span><span class="sxs-lookup"><span data-stu-id="213c9-1599">Info Field 3: Available packets</span></span>
- <span data-ttu-id="213c9-1600">Campo informazioni 4: richieste vuote</span><span class="sxs-lookup"><span data-stu-id="213c9-1600">Info Field 4: Empty requests</span></span>

### <a name="packet-release"></a><span data-ttu-id="213c9-1601">Versione pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1601">Packet Release</span></span> 

#### <a name="nx_packet_data_release"></a><span data-ttu-id="213c9-1602">nx_packet_data_release</span><span class="sxs-lookup"><span data-stu-id="213c9-1602">nx_packet_data_release</span></span>

<span data-ttu-id="213c9-1603">**Icona** ![ di Icona versione pacchetto](./media/user-guide/netx-events/image117.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1603">**Icon** ![Packet release icon](./media/user-guide/netx-events/image117.png)</span></span>

<span data-ttu-id="213c9-1604">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1604">**Description**</span></span>

<span data-ttu-id="213c9-1605">Questo evento rappresenta il rilascio di un pacchetto tramite nx_packet_release.</span><span class="sxs-lookup"><span data-stu-id="213c9-1605">This event represents releasing a packet via nx_packet_release.</span></span>

<span data-ttu-id="213c9-1606">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1606">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1607">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1607">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="213c9-1608">Informazioni sul campo 2: stato del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1608">Info Field 2: Packet status</span></span>
- <span data-ttu-id="213c9-1609">Informazioni sul campo 3: pacchetti disponibili</span><span class="sxs-lookup"><span data-stu-id="213c9-1609">Info Field 3: Available packets</span></span>
- <span data-ttu-id="213c9-1610">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1610">Info Field 4: Not used</span></span>

### <a name="packet-transmit-release"></a><span data-ttu-id="213c9-1611">Versione di trasmissione pacchetti</span><span class="sxs-lookup"><span data-stu-id="213c9-1611">Packet Transmit Release</span></span> 

#### <a name="nx_packet_transmit_release"></a><span data-ttu-id="213c9-1612">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="213c9-1612">nx_packet_transmit_release</span></span>

<span data-ttu-id="213c9-1613">**Icona** ![ di Icona della versione di trasmissione pacchetti](./media/user-guide/netx-events/image118.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1613">**Icon** ![Packet transmit release icon](./media/user-guide/netx-events/image118.png)</span></span>

<span data-ttu-id="213c9-1614">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1614">**Description**</span></span>

<span data-ttu-id="213c9-1615">Questo evento rappresenta il rilascio di un pacchetto di trasmissione tramite nx_packet_transmit_release.</span><span class="sxs-lookup"><span data-stu-id="213c9-1615">This event represents releasing a transmit packet via nx_packet_transmit_release.</span></span>

<span data-ttu-id="213c9-1616">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1616">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1617">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1617">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="213c9-1618">Informazioni sul campo 2: stato del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1618">Info Field 2: Packet status</span></span>
- <span data-ttu-id="213c9-1619">Informazioni sul campo 3: pacchetti disponibili</span><span class="sxs-lookup"><span data-stu-id="213c9-1619">Info Field 3: Available packets</span></span>
- <span data-ttu-id="213c9-1620">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1620">Info Field 4: Not used</span></span>

### <a name="rarp-disable"></a><span data-ttu-id="213c9-1621">Disabilitazione RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-1621">RARP Disable</span></span> 

#### <a name="nx_rarp_disable"></a><span data-ttu-id="213c9-1622">nx_rarp_disable</span><span class="sxs-lookup"><span data-stu-id="213c9-1622">nx_rarp_disable</span></span>

<span data-ttu-id="213c9-1623">**Icona** ![ di Icona di disabilitazione r P](./media/user-guide/netx-events/image119.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1623">**Icon** ![R A R P disable icon](./media/user-guide/netx-events/image119.png)</span></span>

<span data-ttu-id="213c9-1624">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1624">**Description**</span></span>

<span data-ttu-id="213c9-1625">Questo evento rappresenta la disabilitazione di RARP tramite nx_rarp_disable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1625">This event represents disabling RARP via nx_rarp_disable.</span></span>

<span data-ttu-id="213c9-1626">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1626">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1627">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1627">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1628">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1628">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1629">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1629">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1630">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1630">Info Field 4: Not used</span></span>

### <a name="rarp-enable"></a><span data-ttu-id="213c9-1631">Abilitazione di RARP</span><span class="sxs-lookup"><span data-stu-id="213c9-1631">RARP Enable</span></span> 

#### <a name="nx_rarp_enable"></a><span data-ttu-id="213c9-1632">nx_rarp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1632">nx_rarp_enable</span></span>

<span data-ttu-id="213c9-1633">**Icona** ![ di Icona di abilitazione r A r P](./media/user-guide/netx-events/image120.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1633">**Icon** ![R A R P enable icon](./media/user-guide/netx-events/image120.png)</span></span>

<span data-ttu-id="213c9-1634">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1634">**Description**</span></span>

<span data-ttu-id="213c9-1635">Questo evento rappresenta l'abilitazione di RARP tramite nx_rarp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1635">This event represents enabling RARP via nx_rarp_enable.</span></span>

<span data-ttu-id="213c9-1636">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1636">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1637">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1637">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1638">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1638">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1639">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1639">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1640">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1640">Info Field 4: Not used</span></span>

### <a name="rarp-information-get"></a><span data-ttu-id="213c9-1641">Informazioni su RARP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1641">RARP Information Get</span></span> 

#### <a name="nx_rarp_info_get"></a><span data-ttu-id="213c9-1642">nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1642">nx_rarp_info_get</span></span>

<span data-ttu-id="213c9-1643">**Icona** ![ di Icona di r A r P Information Get](./media/user-guide/netx-events/image121.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1643">**Icon** ![R A R P information get icon](./media/user-guide/netx-events/image121.png)</span></span>

<span data-ttu-id="213c9-1644">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1644">**Description**</span></span>

<span data-ttu-id="213c9-1645">Questo evento rappresenta l'acquisizione di informazioni RARP tramite nx_rarp_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1645">This event represents getting RARP information via nx_rarp_info_get.</span></span>

<span data-ttu-id="213c9-1646">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1646">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1647">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1647">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1648">Campo informazioni 2: richieste inviate</span><span class="sxs-lookup"><span data-stu-id="213c9-1648">Info Field 2: Requests sent</span></span>
- <span data-ttu-id="213c9-1649">Informazioni sul campo 3: risposte ricevute</span><span class="sxs-lookup"><span data-stu-id="213c9-1649">Info Field 3: Responses received</span></span>
- <span data-ttu-id="213c9-1650">Campo informazioni 4: risposte non valide</span><span class="sxs-lookup"><span data-stu-id="213c9-1650">Info Field 4: Invalid responses</span></span>

### <a name="system-initialize"></a><span data-ttu-id="213c9-1651">Inizializzazione sistema</span><span class="sxs-lookup"><span data-stu-id="213c9-1651">System Initialize</span></span> 

#### <a name="nx_system_initialize"></a><span data-ttu-id="213c9-1652">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="213c9-1652">nx_system_initialize</span></span>

<span data-ttu-id="213c9-1653">**Icona** ![ di Icona Inizializzazione sistema](./media/user-guide/netx-events/image122.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1653">**Icon** ![System initialize icon](./media/user-guide/netx-events/image122.png)</span></span>

<span data-ttu-id="213c9-1654">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1654">**Description**</span></span>

<span data-ttu-id="213c9-1655">Questo evento rappresenta l'inizializzazione di NetX tramite nx_system_initialize.</span><span class="sxs-lookup"><span data-stu-id="213c9-1655">This event represents initializing NetX via nx_system_initialize.</span></span>

<span data-ttu-id="213c9-1656">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1656">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1657">Campo informazioni 1: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1657">Info Field 1: Not used</span></span>
- <span data-ttu-id="213c9-1658">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1658">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1659">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1659">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1660">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1660">Info Field 4: Not used</span></span>

### <a name="tcp-client-socket-bind"></a><span data-ttu-id="213c9-1661">Binding socket client TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1661">TCP Client Socket Bind</span></span> 

#### <a name="nx_tcp_client_socket_bind"></a><span data-ttu-id="213c9-1662">nx_tcp_client_socket_bind</span><span class="sxs-lookup"><span data-stu-id="213c9-1662">nx_tcp_client_socket_bind</span></span>

<span data-ttu-id="213c9-1663">**Icona** ![ di Icona di Binding socket client T P](./media/user-guide/netx-events/image123.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1663">**Icon** ![T  P client socket bind icon](./media/user-guide/netx-events/image123.png)</span></span>

<span data-ttu-id="213c9-1664">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1664">**Description**</span></span>

<span data-ttu-id="213c9-1665">Questo evento rappresenta l'associazione di un socket client a una porta tramite nx_tcp_client_socket_bind.</span><span class="sxs-lookup"><span data-stu-id="213c9-1665">This event represents binding a client socket to a port via nx_tcp_client_socket_bind.</span></span>

<span data-ttu-id="213c9-1666">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1666">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1667">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1667">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1668">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1668">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1669">Informazioni sul campo 3: porta richiesta</span><span class="sxs-lookup"><span data-stu-id="213c9-1669">Info Field 3: Port requested</span></span>
- <span data-ttu-id="213c9-1670">Informazioni sul campo 4: Wait (opzione)</span><span class="sxs-lookup"><span data-stu-id="213c9-1670">Info Field 4: Wait option</span></span>

### <a name="tcp-client-socket-connect"></a><span data-ttu-id="213c9-1671">Connessione socket client TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1671">TCP Client Socket Connect</span></span> 

#### <a name="nx_tcp_client_socket_connect"></a><span data-ttu-id="213c9-1672">nx_tcp_client_socket_connect</span><span class="sxs-lookup"><span data-stu-id="213c9-1672">nx_tcp_client_socket_connect</span></span>

<span data-ttu-id="213c9-1673">**Icona** ![ di Icona di connessione socket client T C P](./media/user-guide/netx-events/image124.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1673">**Icon** ![T C P client socket connect icon](./media/user-guide/netx-events/image124.png)</span></span>

<span data-ttu-id="213c9-1674">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1674">**Description**</span></span>

<span data-ttu-id="213c9-1675">Questo evento rappresenta la creazione di una connessione socket client tramite nx_tcp_client_socket_connect.</span><span class="sxs-lookup"><span data-stu-id="213c9-1675">This event represents making a client socket connection via nx_tcp_client_socket_connect.</span></span>

<span data-ttu-id="213c9-1676">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1676">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1677">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1677">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1678">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1678">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1679">Campo info 3: indirizzo IP del server</span><span class="sxs-lookup"><span data-stu-id="213c9-1679">Info Field 3: Server IP address</span></span>
- <span data-ttu-id="213c9-1680">Campo informazioni 4: porta server richiesta</span><span class="sxs-lookup"><span data-stu-id="213c9-1680">Info Field 4: Server port requested</span></span>

### <a name="tcp-client-socket-port-get"></a><span data-ttu-id="213c9-1681">Porta socket client TCP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1681">TCP Client Socket Port Get</span></span> 

#### <a name="nx_tcp_client_socket_port_get"></a><span data-ttu-id="213c9-1682">nx_tcp_client_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1682">nx_tcp_client_socket_port_get</span></span>

<span data-ttu-id="213c9-1683">**Icona** ![ di Icona di Get della porta del socket client T C P](./media/user-guide/netx-events/image125.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1683">**Icon** ![T C P client socket port get icon](./media/user-guide/netx-events/image125.png)</span></span>

<span data-ttu-id="213c9-1684">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1684">**Description**</span></span>

<span data-ttu-id="213c9-1685">Questo evento rappresenta il recupero del numero di porta del socket client tramite nx_tcp_client_socket_port_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1685">This event represents getting the client socket port number via nx_tcp_client_socket_port_get.</span></span>

<span data-ttu-id="213c9-1686">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1686">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1687">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1687">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1688">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1688">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1689">Informazioni sul campo 3: numero di porta</span><span class="sxs-lookup"><span data-stu-id="213c9-1689">Info Field 3: Port number</span></span>
- <span data-ttu-id="213c9-1690">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1690">Info Field 4: Not used</span></span>

### <a name="tcp-client-socket-unbind"></a><span data-ttu-id="213c9-1691">Disassociazione socket client TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1691">TCP Client Socket Unbind</span></span> 

#### <a name="nx_tcp_client_socket_unbind"></a><span data-ttu-id="213c9-1692">nx_tcp_client_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="213c9-1692">nx_tcp_client_socket_unbind</span></span>

<span data-ttu-id="213c9-1693">**Icona** ![ di Icona di disassociazione socket client T C P](./media/user-guide/netx-events/image126.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1693">**Icon** ![T C P client socket unbind icon](./media/user-guide/netx-events/image126.png)</span></span>

<span data-ttu-id="213c9-1694">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1694">**Description**</span></span>

<span data-ttu-id="213c9-1695">Questo evento rappresenta l'annullamento dell'associazione della porta associata al socket tramite nx_tcp_client_socket_unbind.</span><span class="sxs-lookup"><span data-stu-id="213c9-1695">This event represents unbinding the port associated with the socket via nx_tcp_client_socket_unbind.</span></span>

<span data-ttu-id="213c9-1696">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1696">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1697">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1697">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1698">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1698">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1699">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1699">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1700">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1700">Info Field 4: Not used</span></span>

### <a name="tcp-enable"></a><span data-ttu-id="213c9-1701">Abilitazione TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1701">TCP Enable</span></span> 

#### <a name="nx_tcp_enable"></a><span data-ttu-id="213c9-1702">nx_tcp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1702">nx_tcp_enable</span></span>

<span data-ttu-id="213c9-1703">**Icona** ![ di Icona di abilitazione di T C P](./media/user-guide/netx-events/image127.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1703">**Icon** ![T C P enable icon](./media/user-guide/netx-events/image127.png)</span></span>

<span data-ttu-id="213c9-1704">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1704">**Description**</span></span>

<span data-ttu-id="213c9-1705">Questo evento rappresenta l'abilitazione di TCP tramite nx_tcp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1705">This event represents enabling TCP via nx_tcp_enable.</span></span>

<span data-ttu-id="213c9-1706">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1706">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1707">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1707">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1708">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1708">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1709">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1709">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1710">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1710">Info Field 4: Not used</span></span>

###  <a name="tcp-free-port-find-tcp-free-port-find"></a><span data-ttu-id="213c9-1711">Porta TCP gratuita-trova porta TCP gratuita</span><span class="sxs-lookup"><span data-stu-id="213c9-1711">TCP Free Port Find TCP Free Port Find</span></span> 

#### <a name="nx_tcp_free_port_find"></a><span data-ttu-id="213c9-1712">nx_tcp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="213c9-1712">nx_tcp_free_port_find</span></span>

<span data-ttu-id="213c9-1713">**Icona** ![ di Icona trova porta libera di T CP](./media/user-guide/netx-events/image128.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1713">**Icon** ![T  CP free port find icon](./media/user-guide/netx-events/image128.png)</span></span>

<span data-ttu-id="213c9-1714">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1714">**Description**</span></span>

<span data-ttu-id="213c9-1715">Questo evento rappresenta la ricerca di una porta TCP gratuita tramite nx_tcp_free_port_find.</span><span class="sxs-lookup"><span data-stu-id="213c9-1715">This event represents finding a free TCP port via nx_tcp_free_port_find.</span></span>

<span data-ttu-id="213c9-1716">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1716">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1717">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1717">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1718">Informazioni campo 2: avvio del numero di porta di ricerca</span><span class="sxs-lookup"><span data-stu-id="213c9-1718">Info Field 2: Starting search port number</span></span>
- <span data-ttu-id="213c9-1719">Campo informazioni 3: numero di porta disponibile</span><span class="sxs-lookup"><span data-stu-id="213c9-1719">Info Field 3: Free port number</span></span>
- <span data-ttu-id="213c9-1720">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1720">Info Field 4: Not used</span></span>

###  <a name="tcp-infomation-get"></a><span data-ttu-id="213c9-1721">TCP opuscolo Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1721">TCP Infomation Get</span></span> 

#### <a name="nx_tcp_info_get"></a><span data-ttu-id="213c9-1722">nx_tcp_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1722">nx_tcp_info_get</span></span>

<span data-ttu-id="213c9-1723">**Icona** ![ di Icona di Get delle informazioni di T C P](./media/user-guide/netx-events/image129.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1723">**Icon** ![T C P infomation get icon](./media/user-guide/netx-events/image129.png)</span></span>

<span data-ttu-id="213c9-1724">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1724">**Description**</span></span>

<span data-ttu-id="213c9-1725">Questo evento rappresenta il recupero delle informazioni TCP per l'istanza IP specificata tramite nx_tcp_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1725">This event represents retrieving TCP information for the specified IP instance via nx_tcp_info_get.</span></span>

<span data-ttu-id="213c9-1726">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1726">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1727">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1727">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1728">Campo informazioni 2: numero di byte inviati</span><span class="sxs-lookup"><span data-stu-id="213c9-1728">Info Field 2: Number of bytes sent</span></span>
- <span data-ttu-id="213c9-1729">Campo informazioni 3: numero di byte ricevuti</span><span class="sxs-lookup"><span data-stu-id="213c9-1729">Info Field 3: Number of bytes received</span></span>
- <span data-ttu-id="213c9-1730">Campo informazioni 4: numero di pacchetti non validi</span><span class="sxs-lookup"><span data-stu-id="213c9-1730">Info Field 4: Number of invalid packets</span></span>

###  <a name="tcp-server-socket-accept"></a><span data-ttu-id="213c9-1731">Accettazione socket server TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1731">TCP Server Socket Accept</span></span> 

#### <a name="nx_tcp_server_socket_accept"></a><span data-ttu-id="213c9-1732">nx_tcp_server_socket_accept</span><span class="sxs-lookup"><span data-stu-id="213c9-1732">nx_tcp_server_socket_accept</span></span>

<span data-ttu-id="213c9-1733">**Icona** ![ di Icona di accettazione socket server T C P](./media/user-guide/netx-events/image130.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1733">**Icon** ![T C P server socket accept icon](./media/user-guide/netx-events/image130.png)</span></span>

<span data-ttu-id="213c9-1734">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1734">**Description**</span></span>

<span data-ttu-id="213c9-1735">Questo evento rappresenta la configurazione del socket del server dopo la ricezione di una richiesta di connessione attiva tramite nx_tcp_server_socket_accept.</span><span class="sxs-lookup"><span data-stu-id="213c9-1735">This event represents setting up the server socket after an active connection request was received via nx_tcp_server_socket_accept.</span></span>

<span data-ttu-id="213c9-1736">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1736">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1737">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1737">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1738">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1738">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1739">Informazioni sul campo 3: wait-opzione</span><span class="sxs-lookup"><span data-stu-id="213c9-1739">Info Field 3: Wait option</span></span>
- <span data-ttu-id="213c9-1740">Informazioni sul campo 4: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1740">Info Field 4: Socket state</span></span>

###  <a name="tcp-server-socket-listen"></a><span data-ttu-id="213c9-1741">Ascolto socket server TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1741">TCP Server Socket Listen</span></span> 

#### <a name="nx_tcp_server_socket_listen"></a><span data-ttu-id="213c9-1742">nx_tcp_server_socket_listen</span><span class="sxs-lookup"><span data-stu-id="213c9-1742">nx_tcp_server_socket_listen</span></span>

<span data-ttu-id="213c9-1743">**Icona** ![ di Icona lsten socket server T C P](./media/user-guide/netx-events/image131.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1743">**Icon** ![T C P server socket lsten icon](./media/user-guide/netx-events/image131.png)</span></span>

<span data-ttu-id="213c9-1744">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1744">**Description**</span></span>

<span data-ttu-id="213c9-1745">Questo evento rappresenta la registrazione di una richiesta di ascolto e un socket server per la porta TCP specificata tramite nx_tcp_server_socket_listen.</span><span class="sxs-lookup"><span data-stu-id="213c9-1745">This event represents register a listen request and a server socket for the specified TCP port via nx_tcp_server_socket_listen.</span></span>

<span data-ttu-id="213c9-1746">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1746">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1747">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1747">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1748">Informazioni sul campo 2: numero di porta TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1748">Info Field 2: TCP port number</span></span>
- <span data-ttu-id="213c9-1749">Informazioni sul campo 3: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1749">Info Field 3: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1750">Campo dati 4: numero massimo di connessioni che possono essere accodate</span><span class="sxs-lookup"><span data-stu-id="213c9-1750">Info Field 4: Maximum number of connections that can be queued</span></span>

###  <a name="tcp-server-socket-relisten"></a><span data-ttu-id="213c9-1751">Socket server TCP rielenco</span><span class="sxs-lookup"><span data-stu-id="213c9-1751">TCP Server Socket Relisten</span></span> 

#### <a name="nx_tcp_server_socket_relisten"></a><span data-ttu-id="213c9-1752">nx_tcp_server_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="213c9-1752">nx_tcp_server_socket_relisten</span></span>

<span data-ttu-id="213c9-1753">**Icona** ![ di Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image132.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1753">**Icon** ![T C P server socket relisten icon](./media/user-guide/netx-events/image132.png)</span></span>

<span data-ttu-id="213c9-1754">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1754">**Description**</span></span>

<span data-ttu-id="213c9-1755">Questo evento rappresenta la registrazione di un altro socket server per una richiesta di ascolto esistente sulla porta TCP specificata tramite nx_tcp_server_socket_relisten.</span><span class="sxs-lookup"><span data-stu-id="213c9-1755">This event represents register another server socket for an existing listen request on the specified TCP port via nx_tcp_server_socket_relisten.</span></span>

<span data-ttu-id="213c9-1756">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1756">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1757">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1757">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1758">Informazioni sul campo 2: numero di porta TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1758">Info Field 2: TCP port number</span></span>
- <span data-ttu-id="213c9-1759">Informazioni sul campo 3: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1759">Info Field 3: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1760">Informazioni sul campo 4: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1760">Info Field 4: Socket state</span></span>

###  <a name="tcp-server-socket-unaccept"></a><span data-ttu-id="213c9-1761">Socket server TCP non accettato</span><span class="sxs-lookup"><span data-stu-id="213c9-1761">TCP Server Socket Unaccept</span></span> 

#### <a name="nx_tcp_server_socket_unaccept"></a><span data-ttu-id="213c9-1762">nx_tcp_server_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="213c9-1762">nx_tcp_server_socket_unaccept</span></span>

<span data-ttu-id="213c9-1763">**Icona** ![ di Icona di unaccept socket server T C P](./media/user-guide/netx-events/image133.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1763">**Icon** ![T C P server socket unaccept icon](./media/user-guide/netx-events/image133.png)</span></span>

<span data-ttu-id="213c9-1764">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1764">**Description**</span></span>

<span data-ttu-id="213c9-1765">Questo evento rappresenta la rimozione del socket del server dall'associazione alla porta che riceve una connessione passiva precedente tramite nx_tcp_server_socket_unaccept.</span><span class="sxs-lookup"><span data-stu-id="213c9-1765">This event represents removing the server socket from association with the port receiving an earlier passive connection via nx_tcp_server_socket_unaccept.</span></span>

<span data-ttu-id="213c9-1766">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1766">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1767">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1767">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1768">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1768">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1769">Informazioni sul campo 3: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1769">Info Field 3: Socket state</span></span>
- <span data-ttu-id="213c9-1770">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1770">Info Field 4: Not used</span></span>

###  <a name="tcp-server-socket-unlisten-tcp-server-socket-unlisten"></a><span data-ttu-id="213c9-1771">Il socket del server TCP non è in elenco</span><span class="sxs-lookup"><span data-stu-id="213c9-1771">TCP Server Socket Unlisten TCP Server Socket Unlisten</span></span> 

#### <a name="nx_tcp_server_socket_unlisten"></a><span data-ttu-id="213c9-1772">nx_tcp_server_socket_unlisten</span><span class="sxs-lookup"><span data-stu-id="213c9-1772">nx_tcp_server_socket_unlisten</span></span>

<span data-ttu-id="213c9-1773">**Icona** ![ di Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image134.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1773">**Icon** ![T C P server socket unlisten icon](./media/user-guide/netx-events/image134.png)</span></span>

<span data-ttu-id="213c9-1774">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1774">**Description**</span></span>

<span data-ttu-id="213c9-1775">Questo evento rappresenta la rimozione di una richiesta di ascolto precedente per la porta TCP specificata tramite nx_tcp_server_socket_unlisten.</span><span class="sxs-lookup"><span data-stu-id="213c9-1775">This event represents removing a previous listen request for the specified TCP port via nx_tcp_server_socket_unlisten.</span></span>

<span data-ttu-id="213c9-1776">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1776">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1777">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1777">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1778">Informazioni sul campo 2: numero di porta TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1778">Info Field 2: TCP port number</span></span>
- <span data-ttu-id="213c9-1779">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1779">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1780">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1780">Info Field 4: Not used</span></span>

### <a name="tcp-socket-bytes-available"></a><span data-ttu-id="213c9-1781">Byte socket TCP disponibili</span><span class="sxs-lookup"><span data-stu-id="213c9-1781">TCP Socket Bytes Available</span></span> 

#### <a name="nx_tcp_socket_bytes_available"></a><span data-ttu-id="213c9-1782">nx_tcp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="213c9-1782">nx_tcp_socket_bytes_available</span></span>

<span data-ttu-id="213c9-1783">**Icona** ![ di Icona di byte socket a T C P disponibile](./media/user-guide/netx-events/image135.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1783">**Icon** ![T C P socket bytes available icon](./media/user-guide/netx-events/image135.png)</span></span>

<span data-ttu-id="213c9-1784">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1784">**Description**</span></span>

<span data-ttu-id="213c9-1785">Questo evento rappresenta il numero di byte attualmente disponibili nel socket di ricezione TCP specificato tramite nx_tcp_socket_bytes_available.</span><span class="sxs-lookup"><span data-stu-id="213c9-1785">This event represents the number of bytes currently available on the specified TCP receiving socket via nx_tcp_socket_bytes_available.</span></span>

<span data-ttu-id="213c9-1786">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1786">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1787">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1787">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1788">Informazioni sul campo 2: puntatore al socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1788">Info Field 2: Pointer to TCP socket</span></span>
- <span data-ttu-id="213c9-1789">Campo info 3: byte ricevuti sul socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1789">Info Field 3: Bytes received on the socket</span></span>
- <span data-ttu-id="213c9-1790">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1790">Info Field 4: Not used</span></span>

### <a name="tcp-socket-create"></a><span data-ttu-id="213c9-1791">Creazione socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1791">TCP Socket Create</span></span> 

#### <a name="nx_tcp_socket_create"></a><span data-ttu-id="213c9-1792">nx_tcp_socket_create</span><span class="sxs-lookup"><span data-stu-id="213c9-1792">nx_tcp_socket_create</span></span>

<span data-ttu-id="213c9-1793">**Icona** ![ di Icona di creazione socket T C P](./media/user-guide/netx-events/image136.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1793">**Icon** ![T C P socket create icon](./media/user-guide/netx-events/image136.png)</span></span>

<span data-ttu-id="213c9-1794">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1794">**Description**</span></span>

<span data-ttu-id="213c9-1795">Questo evento rappresenta la creazione di un socket TCP tramite nx_tcp_socket_create.</span><span class="sxs-lookup"><span data-stu-id="213c9-1795">This event represents creating a TCP socket via nx_tcp_socket_create.</span></span>

<span data-ttu-id="213c9-1796">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1796">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1797">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1797">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1798">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1798">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1799">Informazioni sul campo 3: tipo di servizio</span><span class="sxs-lookup"><span data-stu-id="213c9-1799">Info Field 3: Type of service</span></span>
- <span data-ttu-id="213c9-1800">Informazioni sul campo 4: dimensioni della finestra di ricezione</span><span class="sxs-lookup"><span data-stu-id="213c9-1800">Info Field 4: Receive window size</span></span>

### <a name="tcp-socket-delete"></a><span data-ttu-id="213c9-1801">Eliminazione socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1801">TCP Socket Delete</span></span> 

#### <a name="nx_tcp_socket_delete"></a><span data-ttu-id="213c9-1802">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-1802">nx_tcp_socket_delete</span></span>

<span data-ttu-id="213c9-1803">**Icona** ![ di Icona di eliminazione Socket T C P](./media/user-guide/netx-events/image137.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1803">**Icon** ![T C P socket delete icon](./media/user-guide/netx-events/image137.png)</span></span>

<span data-ttu-id="213c9-1804">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1804">**Description**</span></span>

<span data-ttu-id="213c9-1805">Questo evento rappresenta l'eliminazione di un socket tramite nx_tcp_socket_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-1805">This event represents deleting a socket via nx_tcp_socket_delete.</span></span>

<span data-ttu-id="213c9-1806">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1806">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1807">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1807">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1808">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1808">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1809">Informazioni sul campo 3: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1809">Info Field 3: Socket state</span></span>
- <span data-ttu-id="213c9-1810">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1810">Info Field 4: Not used</span></span>

### <a name="tcp-socket-disconnect"></a><span data-ttu-id="213c9-1811">Connessione socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1811">TCP Socket Disconnect</span></span> 

#### <a name="nx_tcp_socket_disconnect"></a><span data-ttu-id="213c9-1812">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="213c9-1812">nx_tcp_socket_disconnect</span></span>

<span data-ttu-id="213c9-1813">**Icona** ![ di Icona di disconnessione Socket T C P](./media/user-guide/netx-events/image138.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1813">**Icon** ![T C P socket disconnect icon](./media/user-guide/netx-events/image138.png)</span></span>

<span data-ttu-id="213c9-1814">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1814">**Description**</span></span>

<span data-ttu-id="213c9-1815">Questo evento rappresenta la disconnessione di un socket tramite nx_tcp_socket_disconnect.</span><span class="sxs-lookup"><span data-stu-id="213c9-1815">This event represents disconnecting a socket via nx_tcp_socket_disconnect.</span></span>

<span data-ttu-id="213c9-1816">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1816">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1817">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1817">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1818">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1818">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1819">Informazioni sul campo 3: wait-opzione</span><span class="sxs-lookup"><span data-stu-id="213c9-1819">Info Field 3: Wait option</span></span>
- <span data-ttu-id="213c9-1820">Informazioni sul campo 4: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1820">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-information-get"></a><span data-ttu-id="213c9-1821">Informazioni sul socket TCP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1821">TCP Socket Information Get</span></span> 

#### <a name="nx_tcp_socket_info_get"></a><span data-ttu-id="213c9-1822">nx_tcp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1822">nx_tcp_socket_info_get</span></span>

<span data-ttu-id="213c9-1823">**Icona** ![ di Icona di Get delle informazioni sul socket T C P](./media/user-guide/netx-events/image139.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1823">**Icon** ![T C P socket information get icon](./media/user-guide/netx-events/image139.png)</span></span>

<span data-ttu-id="213c9-1824">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1824">**Description**</span></span>

<span data-ttu-id="213c9-1825">Questo evento rappresenta il recupero di informazioni su un socket tramite nx_tcp_socket_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1825">This event represents getting information about a socket via nx_tcp_socket_info_get.</span></span>

<span data-ttu-id="213c9-1826">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1826">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1827">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1827">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1828">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1828">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1829">Campo info 3: byte inviati tramite questo socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1829">Info Field 3: Bytes sent through this socket</span></span>
- <span data-ttu-id="213c9-1830">Campo dati 4: byte ricevuti tramite questo socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1830">Info Field 4: Bytes received through this socket</span></span>

### <a name="tcp-socket-mss-get"></a><span data-ttu-id="213c9-1831">Socket TCP MSS Get</span><span class="sxs-lookup"><span data-stu-id="213c9-1831">TCP Socket MSS Get</span></span> 

#### <a name="nx_tcp_socket_mss_get"></a><span data-ttu-id="213c9-1832">nx_tcp_socket_mss_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1832">nx_tcp_socket_mss_get</span></span>

<span data-ttu-id="213c9-1833">**Icona** ![ di Icona di Get del socket T C P s](./media/user-guide/netx-events/image140.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1833">**Icon** ![T C P socket M S S get icon](./media/user-guide/netx-events/image140.png)</span></span>

<span data-ttu-id="213c9-1834">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1834">**Description**</span></span>

<span data-ttu-id="213c9-1835">Questo evento rappresenta il recupero della MSS del socket tramite nx_tcp_socket_mss_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1835">This event represents getting the socket's MSS via nx_tcp_socket_mss_get.</span></span>

<span data-ttu-id="213c9-1836">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1836">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1837">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1837">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1838">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1838">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1839">Informazioni campo 3: dimensioni massime segmento (MSS)</span><span class="sxs-lookup"><span data-stu-id="213c9-1839">Info Field 3: Maximum Segment Size (MSS)</span></span>
- <span data-ttu-id="213c9-1840">Informazioni sul campo 4: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1840">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-mss-peer-get"></a><span data-ttu-id="213c9-1841">Peer Get MSS socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1841">TCP Socket MSS Peer Get</span></span> 

#### <a name="nx_tcp_socket_mss_peer_get"></a><span data-ttu-id="213c9-1842">nx_tcp_socket_mss_peer_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1842">nx_tcp_socket_mss_peer_get</span></span>

<span data-ttu-id="213c9-1843">**Icona** ![ di Icona di peer Get di T C P Socket M S](./media/user-guide/netx-events/image141.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1843">**Icon** ![T C P socket M S S peer get icon](./media/user-guide/netx-events/image141.png)</span></span>

<span data-ttu-id="213c9-1844">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1844">**Description**</span></span>

<span data-ttu-id="213c9-1845">Questo evento rappresenta il recupero del valore MSS del peer del socket tramite nx_tcp_socket_mss_peer_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1845">This event represents getting the MSS value of the socket's peer via nx_tcp_socket_mss_peer_get.</span></span>

<span data-ttu-id="213c9-1846">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1846">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1847">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1847">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1848">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1848">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1849">Informazioni sul campo 3: MSS del peer</span><span class="sxs-lookup"><span data-stu-id="213c9-1849">Info Field 3: Peer's MSS</span></span>
- <span data-ttu-id="213c9-1850">Informazioni sul campo 4: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1850">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-mss-set"></a><span data-ttu-id="213c9-1851">Set MSS socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1851">TCP Socket MSS Set</span></span> 

#### <a name="nx_tcp_socket_mss_set"></a><span data-ttu-id="213c9-1852">nx_tcp_socket_mss_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1852">nx_tcp_socket_mss_set</span></span>

<span data-ttu-id="213c9-1853">**Icona** ![ di Icona set di socket M S T s](./media/user-guide/netx-events/image142.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1853">**Icon** ![T C P socket M S S set icon](./media/user-guide/netx-events/image142.png)</span></span>

<span data-ttu-id="213c9-1854">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1854">**Description**</span></span>

<span data-ttu-id="213c9-1855">Questo evento rappresenta l'impostazione di un MSS del socket tramite nx_tcp_socket_mss_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1855">This event represents setting a socket's MSS via nx_tcp_socket_mss_set.</span></span>

<span data-ttu-id="213c9-1856">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1856">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1857">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1857">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1858">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1858">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1859">Campo informazioni 3: MSS</span><span class="sxs-lookup"><span data-stu-id="213c9-1859">Info Field 3: MSS</span></span>
- <span data-ttu-id="213c9-1860">Informazioni sul campo 4: stato socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1860">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-peer-info-get"></a><span data-ttu-id="213c9-1861">Get informazioni peer socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1861">TCP Socket Peer Info Get</span></span> 

#### <a name="nx_tcp_socket_peer_info_get"></a><span data-ttu-id="213c9-1862">nx_tcp_socket_peer_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1862">nx_tcp_socket_peer_info_get</span></span>

<span data-ttu-id="213c9-1863">**Icona** ![ di Icona di Get delle informazioni peer del socket T C P](./media/user-guide/netx-events/image143.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1863">**Icon** ![T C P socket peer info get icon](./media/user-guide/netx-events/image143.png)</span></span>

<span data-ttu-id="213c9-1864">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1864">**Description**</span></span>

<span data-ttu-id="213c9-1865">Questo evento rappresenta le informazioni recuperate dal socket TCP per quanto concerne il peer, ad esempio >connessione host, l'indirizzo IP e la porta tramite nx_tcp_socket_peer_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1865">This event represents information retrieved from the TCP socket regarding the peer (e.g. >connecting host) IP address and port via nx_tcp_socket_peer_info_get.</span></span>

<span data-ttu-id="213c9-1866">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1866">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1867">Informazioni sul campo 1: puntatore al socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1867">Info Field 1: Pointer to TCP socket</span></span>
- <span data-ttu-id="213c9-1868">Informazioni sul campo 2: indirizzo IP peer</span><span class="sxs-lookup"><span data-stu-id="213c9-1868">Info Field 2: Peer IP address</span></span>
- <span data-ttu-id="213c9-1869">Informazioni sul campo 3: numero di porta peer</span><span class="sxs-lookup"><span data-stu-id="213c9-1869">Info Field 3: Peer port number</span></span>
- <span data-ttu-id="213c9-1870">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1870">Info Field 4: Not used</span></span>

### <a name="tcp-socket-receive"></a><span data-ttu-id="213c9-1871">Ricezione socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1871">TCP Socket Receive</span></span> 

#### <a name="nx_tcp_socket_receive"></a><span data-ttu-id="213c9-1872">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="213c9-1872">nx_tcp_socket_receive</span></span>

<span data-ttu-id="213c9-1873">**Icona** ![ di Icona di ricezione Socket T C P](./media/user-guide/netx-events/image144.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1873">**Icon** ![T C P socket receive icon](./media/user-guide/netx-events/image144.png)</span></span>

<span data-ttu-id="213c9-1874">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1874">**Description**</span></span>

<span data-ttu-id="213c9-1875">Questo evento rappresenta la ricezione di dati da un socket tramite nx_tcp_socket_receive.</span><span class="sxs-lookup"><span data-stu-id="213c9-1875">This event represents receiving data from a socket via nx_tcp_socket_receive.</span></span>

<span data-ttu-id="213c9-1876">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1876">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1877">Informazioni sul campo 1: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1877">Info Field 1: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1878">Informazioni sul campo 2: puntatore al pacchetto ricevuto</span><span class="sxs-lookup"><span data-stu-id="213c9-1878">Info Field 2: Pointer to received packet</span></span>
- <span data-ttu-id="213c9-1879">Informazioni campo 3: lunghezza pacchetto ricevuta</span><span class="sxs-lookup"><span data-stu-id="213c9-1879">Info Field 3: Received packet length</span></span>
- <span data-ttu-id="213c9-1880">Campo dati 4: numero di sequenza di ricezione</span><span class="sxs-lookup"><span data-stu-id="213c9-1880">Info Field 4: Receive sequence number</span></span>

### <a name="tcp-socket-receive-notify"></a><span data-ttu-id="213c9-1881">Ricezione notifica socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1881">TCP Socket Receive Notify</span></span> 

#### <a name="nx_tcp_socket_receive_notify"></a><span data-ttu-id="213c9-1882">nx_tcp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="213c9-1882">nx_tcp_socket_receive_notify</span></span>

<span data-ttu-id="213c9-1883">**Icona** ![ di Icona di ricezione della notifica socket T C P](./media/user-guide/netx-events/image145.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1883">**Icon** ![T C P socket receive notify icon](./media/user-guide/netx-events/image145.png)</span></span>

<span data-ttu-id="213c9-1884">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1884">**Description**</span></span>

<span data-ttu-id="213c9-1885">Questo evento rappresenta la registrazione di un callback di notifica di ricezione per un socket tramite nx_tcp_socket_receive_notify.</span><span class="sxs-lookup"><span data-stu-id="213c9-1885">This event represents registering a receive notify callback for a socket via nx_tcp_socket_receive_notify.</span></span>

<span data-ttu-id="213c9-1886">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1886">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1887">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1887">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1888">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1888">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1889">Informazioni sul campo 3: puntatore a Receive Notify info callback campo 4: non utilizzato</span><span class="sxs-lookup"><span data-stu-id="213c9-1889">Info Field 3: Pointer to receive notify callback Info Field 4: Not used</span></span>

### <a name="tcp-socket-send"></a><span data-ttu-id="213c9-1890">Invio socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1890">TCP Socket Send</span></span> 

#### <a name="nx_tcp_socket_send"></a><span data-ttu-id="213c9-1891">nx_tcp_socket_send</span><span class="sxs-lookup"><span data-stu-id="213c9-1891">nx_tcp_socket_send</span></span>

<span data-ttu-id="213c9-1892">**Icona** ![ di Icona di invio socket T C P](./media/user-guide/netx-events/image146.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1892">**Icon** ![T C P socket send icon](./media/user-guide/netx-events/image146.png)</span></span>

<span data-ttu-id="213c9-1893">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1893">**Description**</span></span>

<span data-ttu-id="213c9-1894">Questo evento rappresenta l'invio di dati in un socket tramite nx_tcp_socket_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-1894">This event represents sending data on a socket via nx_tcp_socket_send.</span></span>

<span data-ttu-id="213c9-1895">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1895">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1896">Informazioni sul campo 1: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1896">Info Field 1: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1897">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1897">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-1898">Informazioni sul campo 3: lunghezza del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-1898">Info Field 3: Length of packet</span></span>
- <span data-ttu-id="213c9-1899">Campo informazioni 4: numero di sequenza di trasmissione</span><span class="sxs-lookup"><span data-stu-id="213c9-1899">Info Field 4: Transmit sequence number</span></span>

### <a name="tcp-socket-state-wait"></a><span data-ttu-id="213c9-1900">Attesa stato socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1900">TCP Socket State Wait</span></span> 

#### <a name="nx_tcp_socket_state_wait"></a><span data-ttu-id="213c9-1901">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="213c9-1901">nx_tcp_socket_state_wait</span></span>

<span data-ttu-id="213c9-1902">**Icona** ![ di Icona di attesa stato Socket T C P](./media/user-guide/netx-events/image147.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1902">**Icon** ![T C P socket state wait icon](./media/user-guide/netx-events/image147.png)</span></span>

<span data-ttu-id="213c9-1903">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1903">**Description**</span></span>

<span data-ttu-id="213c9-1904">Questo evento rappresenta l'attesa di un socket per l'immissione di un determinato stato tramite nx_tcp_socket_state_wait.</span><span class="sxs-lookup"><span data-stu-id="213c9-1904">This event represents waiting for a socket to enter a particular state via nx_tcp_socket_state_wait.</span></span>

<span data-ttu-id="213c9-1905">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1905">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1906">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1906">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1907">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1907">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1908">Informazioni sul campo 3: stato socket desiderato</span><span class="sxs-lookup"><span data-stu-id="213c9-1908">Info Field 3: Desired socket state</span></span>
- <span data-ttu-id="213c9-1909">Informazioni sul campo 4: stato del socket precedente</span><span class="sxs-lookup"><span data-stu-id="213c9-1909">Info Field 4: Previous socket state</span></span>

### <a name="tcp-socket-transmit-configure"></a><span data-ttu-id="213c9-1910">Configurazione trasmissione socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1910">TCP Socket Transmit Configure</span></span> 

#### <a name="nx_tcp_socket_transmit_configure"></a><span data-ttu-id="213c9-1911">nx_tcp_socket_transmit_configure</span><span class="sxs-lookup"><span data-stu-id="213c9-1911">nx_tcp_socket_transmit_configure</span></span>

<span data-ttu-id="213c9-1912">**Icona** ![ di Icona di configurazione di trasmissione Socket T C P](./media/user-guide/netx-events/image148.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1912">**Icon** ![T C P socket transmit configure icon](./media/user-guide/netx-events/image148.png)</span></span>

<span data-ttu-id="213c9-1913">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1913">**Description**</span></span>

<span data-ttu-id="213c9-1914">Questo evento rappresenta la configurazione delle opzioni di trasmissione per un socket tramite nx_tcp_socket_transmit_configure.</span><span class="sxs-lookup"><span data-stu-id="213c9-1914">This event represents configuring the transmit options for a socket via nx_tcp_socket_transmit_configure.</span></span>

<span data-ttu-id="213c9-1915">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1915">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1916">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1916">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1917">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1917">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1918">Informazioni sul campo 3: profondità della coda di trasmissione</span><span class="sxs-lookup"><span data-stu-id="213c9-1918">Info Field 3: Transmit queue depth</span></span>
- <span data-ttu-id="213c9-1919">Informazioni campo 4: valore di timeout</span><span class="sxs-lookup"><span data-stu-id="213c9-1919">Info Field 4: Timeout value</span></span>

### <a name="tcp-socket-window-update-notify-set"></a><span data-ttu-id="213c9-1920">Set di notifiche aggiornamento finestra socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1920">TCP Socket Window Update Notify Set</span></span> 

#### <a name="nx_tcp_window_update_notify_set"></a><span data-ttu-id="213c9-1921">nx_tcp_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="213c9-1921">nx_tcp_window_update_notify_set</span></span>

<span data-ttu-id="213c9-1922">**Icona** ![ di Icona del set di notifiche di aggiornamento della finestra socket di T C P](./media/user-guide/netx-events/image149.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1922">**Icon** ![T C P socket window update notify set icon](./media/user-guide/netx-events/image149.png)</span></span>

<span data-ttu-id="213c9-1923">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1923">**Description**</span></span>

<span data-ttu-id="213c9-1924">Questo evento rappresenta un socket TCP che riceve la notifica di un aumento nella finestra di ricezione dell'host remoto tramite nx_tcp_window_update_notify_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-1924">This event represents a TCP socket receiving notification of an increase in the remote host receive window via nx_tcp_window_update_notify_set.</span></span>

<span data-ttu-id="213c9-1925">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1925">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1926">Informazioni sul campo 1: puntatore al socket TCP</span><span class="sxs-lookup"><span data-stu-id="213c9-1926">Info Field 1: Pointer to TCP socket</span></span>
- <span data-ttu-id="213c9-1927">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1927">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1928">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1928">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1929">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1929">Info Field 4: Not used</span></span>

### <a name="udp-enable"></a><span data-ttu-id="213c9-1930">Abilita UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1930">UDP Enable</span></span> 

#### <a name="nx_udp_enable"></a><span data-ttu-id="213c9-1931">nx_udp_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1931">nx_udp_enable</span></span>

<span data-ttu-id="213c9-1932">**Icona** ![ di Icona di abilitazione di U D P](./media/user-guide/netx-events/image150.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1932">**Icon** ![U D P enable icon](./media/user-guide/netx-events/image150.png)</span></span>

<span data-ttu-id="213c9-1933">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1933">**Description**</span></span>

<span data-ttu-id="213c9-1934">Questo evento rappresenta l'abilitazione di UDP tramite nx_udp_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1934">This event represents enabling UDP via nx_udp_enable.</span></span>

<span data-ttu-id="213c9-1935">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1935">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1936">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1936">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1937">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1937">Info Field 2: Not used</span></span>
- <span data-ttu-id="213c9-1938">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1938">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1939">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1939">Info Field 4: Not used</span></span>

### <a name="udp-free-port-find"></a><span data-ttu-id="213c9-1940">Ricerca porta gratuita UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1940">UDP Free Port Find</span></span> 

#### <a name="nx_udp_free_port_find"></a><span data-ttu-id="213c9-1941">nx_udp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="213c9-1941">nx_udp_free_port_find</span></span>

<span data-ttu-id="213c9-1942">**Icona** ![ di Icona trova porta gratuita U D P](./media/user-guide/netx-events/image151.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1942">**Icon** ![U D P free port find icon](./media/user-guide/netx-events/image151.png)</span></span>

<span data-ttu-id="213c9-1943">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1943">**Description**</span></span>

<span data-ttu-id="213c9-1944">Questo evento rappresenta la ricerca di una porta UDP gratuita tramite nx_udp_free_port_find.</span><span class="sxs-lookup"><span data-stu-id="213c9-1944">This event represents finding a free UDP port via nx_udp_free_port_find.</span></span>

<span data-ttu-id="213c9-1945">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1945">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1946">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1946">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1947">Informazioni sul campo 2: avvio della porta da cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="213c9-1947">Info Field 2: Starting port to search from</span></span>
- <span data-ttu-id="213c9-1948">Informazioni sul campo 3: porta gratuita</span><span class="sxs-lookup"><span data-stu-id="213c9-1948">Info Field 3: Free port</span></span>
- <span data-ttu-id="213c9-1949">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1949">Info Field 4: Not used</span></span>

### <a name="udp-information-get"></a><span data-ttu-id="213c9-1950">Get informazioni UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1950">UDP Information Get</span></span> 

#### <a name="nx_udp_info_get"></a><span data-ttu-id="213c9-1951">nx_udp_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-1951">nx_udp_info_get</span></span>

<span data-ttu-id="213c9-1952">**Icona** ![ di Icona di Get delle informazioni di U D P](./media/user-guide/netx-events/image152.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1952">**Icon** ![U D P information get icon](./media/user-guide/netx-events/image152.png)</span></span>

<span data-ttu-id="213c9-1953">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1953">**Description**</span></span>

<span data-ttu-id="213c9-1954">Questo evento rappresenta il recupero di informazioni tramite nx_udp_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-1954">This event represents getting information via nx_udp_info_get.</span></span>

<span data-ttu-id="213c9-1955">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1955">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1956">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1956">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1957">Campo informazioni 2: byte UDP inviati</span><span class="sxs-lookup"><span data-stu-id="213c9-1957">Info Field 2: UDP bytes sent</span></span>
- <span data-ttu-id="213c9-1958">Campo informazioni 3: byte UDP ricevuti</span><span class="sxs-lookup"><span data-stu-id="213c9-1958">Info Field 3: UDP bytes received</span></span>
- <span data-ttu-id="213c9-1959">Campo dati 4: pacchetti non validi</span><span class="sxs-lookup"><span data-stu-id="213c9-1959">Info Field 4: Invalid packets</span></span>

### <a name="udp-socket-bind"></a><span data-ttu-id="213c9-1960">Binding socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1960">UDP Socket Bind</span></span> 

#### <a name="nx_udp_socket_bind"></a><span data-ttu-id="213c9-1961">nx_udp_socket_bind</span><span class="sxs-lookup"><span data-stu-id="213c9-1961">nx_udp_socket_bind</span></span>

<span data-ttu-id="213c9-1962">**Icona** ![ di Icona di Binding socket U D P](./media/user-guide/netx-events/image153.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1962">**Icon** ![U D P socket bind icon](./media/user-guide/netx-events/image153.png)</span></span>

<span data-ttu-id="213c9-1963">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1963">**Description**</span></span>

<span data-ttu-id="213c9-1964">Questo evento rappresenta l'associazione di un socket UDP a una porta tramite nx_udp_socket_bind.</span><span class="sxs-lookup"><span data-stu-id="213c9-1964">This event represents binding a UDP socket to a port via nx_udp_socket_bind.</span></span>

<span data-ttu-id="213c9-1965">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1965">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1966">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1966">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1967">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1967">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1968">Informazioni sul campo 3: numero di porta</span><span class="sxs-lookup"><span data-stu-id="213c9-1968">Info Field 3: Port number</span></span>
- <span data-ttu-id="213c9-1969">Informazioni sul campo 4: Wait (opzione)</span><span class="sxs-lookup"><span data-stu-id="213c9-1969">Info Field 4: Wait option</span></span>

### <a name="udp-socket-bytes-available"></a><span data-ttu-id="213c9-1970">Byte socket UDP disponibili</span><span class="sxs-lookup"><span data-stu-id="213c9-1970">UDP Socket Bytes Available</span></span> 

#### <a name="nx_udp_socket_bytes_available"></a><span data-ttu-id="213c9-1971">nx_udp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="213c9-1971">nx_udp_socket_bytes_available</span></span>

<span data-ttu-id="213c9-1972">**Icona** ![ di Icona di byte socket U D P disponibile](./media/user-guide/netx-events/image154.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1972">**Icon** ![U D P socket bytes available icon](./media/user-guide/netx-events/image154.png)</span></span>

<span data-ttu-id="213c9-1973">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1973">**Description**</span></span>

<span data-ttu-id="213c9-1974">Questo evento rappresenta il numero corrente di byte ricevuti sul socket UDP tramite nx_udp_socket_bytes_available.</span><span class="sxs-lookup"><span data-stu-id="213c9-1974">This event represents the current number of bytes received on the UDP socket via nx_udp_socket_bytes_available.</span></span>

<span data-ttu-id="213c9-1975">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1975">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1976">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1976">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1977">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1977">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1978">Campo info 3: byte ricevuti sul socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1978">Info Field 3: Bytes received on socket</span></span>
- <span data-ttu-id="213c9-1979">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1979">Info Field 4: Not used</span></span>

### <a name="udp-socket-checksum-disable"></a><span data-ttu-id="213c9-1980">Disabilita checksum socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1980">UDP Socket Checksum Disable</span></span> 

#### <a name="nx_udp_socket_checksum_disable"></a><span data-ttu-id="213c9-1981">nx_udp_socket_checksum_disable</span><span class="sxs-lookup"><span data-stu-id="213c9-1981">nx_udp_socket_checksum_disable</span></span>

<span data-ttu-id="213c9-1982">**Icona** ![ di Icona di disabilitazione checksum socket U D P](./media/user-guide/netx-events/image155.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1982">**Icon** ![U D P socket checksum disable icon](./media/user-guide/netx-events/image155.png)</span></span>

<span data-ttu-id="213c9-1983">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1983">**Description**</span></span>

<span data-ttu-id="213c9-1984">Questo evento rappresenta la disabilitazione del checksum per i dati in un socket UDP tramite nx_udp_socket_checksum_disable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1984">This event represents disabling the checksum for data on a UDP socket via nx_udp_socket_checksum_disable.</span></span>

<span data-ttu-id="213c9-1985">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1985">**Information Fields**</span></span> 

- <span data-ttu-id="213c9-1986">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1986">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1987">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1987">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1988">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1988">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1989">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1989">Info Field 4: Not used</span></span>

### <a name="udp-socket-checksum-enable"></a><span data-ttu-id="213c9-1990">Abilita checksum socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-1990">UDP Socket Checksum Enable</span></span> 

#### <a name="nx_udp_socket_checksum_enable"></a><span data-ttu-id="213c9-1991">nx_udp_socket_checksum_enable</span><span class="sxs-lookup"><span data-stu-id="213c9-1991">nx_udp_socket_checksum_enable</span></span>

<span data-ttu-id="213c9-1992">**Icona** ![ di Icona Abilita checksum socket U D P](./media/user-guide/netx-events/image156.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-1992">**Icon** ![U D P socket checksum enable icon](./media/user-guide/netx-events/image156.png)</span></span>

<span data-ttu-id="213c9-1993">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-1993">**Description**</span></span>

<span data-ttu-id="213c9-1994">Questo evento rappresenta l'abilitazione dell'elaborazione di checksum su un socket tramite nx_udp_socket_checksum_enable.</span><span class="sxs-lookup"><span data-stu-id="213c9-1994">This event represents enabling checksum processing on a socket via nx_udp_socket_checksum_enable.</span></span>

<span data-ttu-id="213c9-1995">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-1995">**Information Fields**</span></span>

- <span data-ttu-id="213c9-1996">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-1996">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-1997">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-1997">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-1998">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1998">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-1999">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-1999">Info Field 4: Not used</span></span>

### <a name="udp-socket-create"></a><span data-ttu-id="213c9-2000">Creazione socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2000">UDP Socket Create</span></span> 

#### <a name="nx_udp_socket_create"></a><span data-ttu-id="213c9-2001">nx_udp_socket_create</span><span class="sxs-lookup"><span data-stu-id="213c9-2001">nx_udp_socket_create</span></span>

<span data-ttu-id="213c9-2002">**Icona** ![ di Icona di creazione socket U D P](./media/user-guide/netx-events/image157.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2002">**Icon** ![U D P socket create icon](./media/user-guide/netx-events/image157.png)</span></span>

<span data-ttu-id="213c9-2003">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2003">**Description**</span></span>

<span data-ttu-id="213c9-2004">Questo evento rappresenta la creazione di un socket UDP tramite nx_udp_socket_create.</span><span class="sxs-lookup"><span data-stu-id="213c9-2004">This event represents creating a UDP socket via nx_udp_socket_create.</span></span>

<span data-ttu-id="213c9-2005">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2005">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2006">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2006">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2007">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2007">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-2008">Informazioni sul campo 3: tipo di servizio</span><span class="sxs-lookup"><span data-stu-id="213c9-2008">Info Field 3: Type of service</span></span>
- <span data-ttu-id="213c9-2009">Campo informazioni 4: coda di ricezione massima</span><span class="sxs-lookup"><span data-stu-id="213c9-2009">Info Field 4: Maximum receive queue</span></span>

### <a name="udp-socket-delete-event"></a><span data-ttu-id="213c9-2010">Evento di eliminazione socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2010">UDP Socket Delete Event</span></span> 

#### <a name="nx_udp_socket_delete-event"></a><span data-ttu-id="213c9-2011">evento nx_udp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="213c9-2011">nx_udp_socket_delete event</span></span>

<span data-ttu-id="213c9-2012">**Icona** ![ di Icona dell'evento di eliminazione socket U D P](./media/user-guide/netx-events/image158.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2012">**Icon** ![U D P socket delete event icon](./media/user-guide/netx-events/image158.png)</span></span>

<span data-ttu-id="213c9-2013">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2013">**Description**</span></span>

<span data-ttu-id="213c9-2014">Questo evento rappresenta l'eliminazione di un socket UDP tramite nx_udp_socket_delete.</span><span class="sxs-lookup"><span data-stu-id="213c9-2014">This event represents deleting a UDP socket via nx_udp_socket_delete.</span></span>

<span data-ttu-id="213c9-2015">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2015">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2016">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2016">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2017">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2017">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-2018">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2018">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-2019">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2019">Info Field 4: Not used</span></span>

### <a name="udp-socket-information-get-event"></a><span data-ttu-id="213c9-2020">Evento di Get delle informazioni sul socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2020">UDP Socket Information Get Event</span></span> 

#### <a name="nx_udp_socket_info_get-event"></a><span data-ttu-id="213c9-2021">evento nx_udp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="213c9-2021">nx_udp_socket_info_get event</span></span>

<span data-ttu-id="213c9-2022">**Icona** ![ di Icona dell'evento Get delle informazioni sul socket U D P](./media/user-guide/netx-events/image159.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2022">**Icon** ![U D P socket information get event icon](./media/user-guide/netx-events/image159.png)</span></span>

<span data-ttu-id="213c9-2023">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2023">**Description**</span></span>

<span data-ttu-id="213c9-2024">Questo evento rappresenta il recupero di informazioni su un socket UDP tramite nx_udp_socket_info_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-2024">This event represents getting information about a UDP socket via nx_udp_socket_info_get.</span></span>

<span data-ttu-id="213c9-2025">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2025">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2026">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2026">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2027">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2027">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-2028">Campo info 3: byte inviati tramite socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2028">Info Field 3: Bytes sent through socket</span></span>
- <span data-ttu-id="213c9-2029">Campo dati 4: byte ricevuti tramite socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2029">Info Field 4: Bytes received through socket</span></span>

### <a name="udp-socket-interface-set"></a><span data-ttu-id="213c9-2030">Set di interfacce socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2030">UDP Socket Interface Set</span></span> 

#### <a name="nx_udp_socket_interface_set-event"></a><span data-ttu-id="213c9-2031">evento nx_udp_socket_interface_set</span><span class="sxs-lookup"><span data-stu-id="213c9-2031">nx_udp_socket_interface_set event</span></span>

<span data-ttu-id="213c9-2032">**Icona** ![ di Icona del set di interfacce socket U D P](./media/user-guide/netx-events/image160.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2032">**Icon** ![U D P socket interface set icon](./media/user-guide/netx-events/image160.png)</span></span>

<span data-ttu-id="213c9-2033">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2033">**Description**</span></span>

<span data-ttu-id="213c9-2034">Questo evento rappresenta l'impostazione dell'interfaccia in uscita del socket UDP specificato con l'interfaccia specificata tramite nx_udp_socket_interface_set.</span><span class="sxs-lookup"><span data-stu-id="213c9-2034">This event represents setting the outgoing interface of the specified UDP socket with the specified interface via nx_udp_socket_interface_set.</span></span>

<span data-ttu-id="213c9-2035">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2035">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2036">Informazioni sul campo 1: puntatore al socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2036">Info Field 1: Pointer to UDP socket</span></span>
- <span data-ttu-id="213c9-2037">Campo informazioni 2: indice corrispondente all'interfaccia per il socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2037">Info Field 2: Index corresponding to the interface for the socket</span></span>
- <span data-ttu-id="213c9-2038">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2038">Info Field 3: Not used</span></span>
- <span data-ttu-id="213c9-2039">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2039">Info Field 4: Not used</span></span>

### <a name="udp-socket-port-get"></a><span data-ttu-id="213c9-2040">Porta socket UDP Get</span><span class="sxs-lookup"><span data-stu-id="213c9-2040">UDP Socket Port Get</span></span> 

#### <a name="nx_udp_socket_port_get"></a><span data-ttu-id="213c9-2041">nx_udp_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="213c9-2041">nx_udp_socket_port_get</span></span>

<span data-ttu-id="213c9-2042">**Icona** ![ di Icona di Get della porta socket U D P](./media/user-guide/netx-events/image161.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2042">**Icon** ![U D P socket port get icon](./media/user-guide/netx-events/image161.png)</span></span>

<span data-ttu-id="213c9-2043">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2043">**Description**</span></span>

<span data-ttu-id="213c9-2044">Questo evento rappresenta il recupero della porta UDP a cui è associato il socket UDP specificato tramite nx_udp_socket_port_get.</span><span class="sxs-lookup"><span data-stu-id="213c9-2044">This event represents retrieving the UDP port the specified UDP socket is bound to via nx_udp_socket_port_get.</span></span>

<span data-ttu-id="213c9-2045">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2045">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2046">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2046">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2047">Informazioni sul campo 2: puntatore al socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2047">Info Field 2: Pointer to UDP socket</span></span>
- <span data-ttu-id="213c9-2048">Informazioni sul campo 3: numero di porta</span><span class="sxs-lookup"><span data-stu-id="213c9-2048">Info Field 3: Port number</span></span>
- <span data-ttu-id="213c9-2049">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2049">Info Field 4: Not used</span></span>

### <a name="udp-socket-receive"></a><span data-ttu-id="213c9-2050">Ricezione socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2050">UDP Socket Receive</span></span> 

#### <a name="nx_udp_socket_receive"></a><span data-ttu-id="213c9-2051">nx_udp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="213c9-2051">nx_udp_socket_receive</span></span>

<span data-ttu-id="213c9-2052">**Icona** ![ di Icona di ricezione socket U D P](./media/user-guide/netx-events/image162.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2052">**Icon** ![U D P socket receive icon](./media/user-guide/netx-events/image162.png)</span></span>

<span data-ttu-id="213c9-2053">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2053">**Description**</span></span>

<span data-ttu-id="213c9-2054">Questo evento rappresenta la ricezione di dati sul socket UDP specificato tramite nx_udp_socket_receive.</span><span class="sxs-lookup"><span data-stu-id="213c9-2054">This event represents receiving data on the specified UDP socket via nx_udp_socket_receive.</span></span>

<span data-ttu-id="213c9-2055">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2055">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2056">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2056">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2057">Informazioni sul campo 2: puntatore al socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2057">Info Field 2: Pointer to UDP socket</span></span>
- <span data-ttu-id="213c9-2058">Informazioni sul campo 3: puntatore al pacchetto ricevuto</span><span class="sxs-lookup"><span data-stu-id="213c9-2058">Info Field 3: Pointer to received packet</span></span>
- <span data-ttu-id="213c9-2059">Informazioni sul campo 4: dimensioni del pacchetto ricevute</span><span class="sxs-lookup"><span data-stu-id="213c9-2059">Info Field 4: Received packet size</span></span>

### <a name="udp-socket-receive-notify"></a><span data-ttu-id="213c9-2060">Ricezione notifica socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2060">UDP Socket Receive Notify</span></span> 

#### <a name="nx_udp_socket_receive_notify"></a><span data-ttu-id="213c9-2061">nx_udp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="213c9-2061">nx_udp_socket_receive_notify</span></span>

<span data-ttu-id="213c9-2062">**Icona** ![ di Descrizione icona di ricezione di un socket U D P ](./media/user-guide/netx-events/image163.png) </span><span class="sxs-lookup"><span data-stu-id="213c9-2062">**Icon** ![U D P socket receive notify icon](./media/user-guide/netx-events/image163.png)s **Description**</span></span>

<span data-ttu-id="213c9-2063">Questo evento rappresenta la registrazione di un callback di notifica di ricezione tramite nx_udp_socket_receive_notify.</span><span class="sxs-lookup"><span data-stu-id="213c9-2063">This event represents registering a receive notify callback via nx_udp_socket_receive_notify.</span></span>

<span data-ttu-id="213c9-2064">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2064">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2065">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2065">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2066">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2066">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-2067">Informazioni sul campo 3: puntatore a Receive Notify Function info Field 4: not used</span><span class="sxs-lookup"><span data-stu-id="213c9-2067">Info Field 3: Pointer to receive notify function Info Field 4: Not used</span></span>

### <a name="udp-socket-send"></a><span data-ttu-id="213c9-2068">Invio socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2068">UDP Socket Send</span></span> 

#### <a name="nx_udp_socket_send"></a><span data-ttu-id="213c9-2069">nx_udp_socket_send</span><span class="sxs-lookup"><span data-stu-id="213c9-2069">nx_udp_socket_send</span></span>

<span data-ttu-id="213c9-2070">**Icona** ![ di Icona di invio socket U D P](./media/user-guide/netx-events/image164.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2070">**Icon** ![U D P socket send icon](./media/user-guide/netx-events/image164.png)</span></span>

<span data-ttu-id="213c9-2071">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2071">**Description**</span></span>

<span data-ttu-id="213c9-2072">Questo evento rappresenta l'invio di dati tramite un socket UDP tramite nx_udp_socket_send.</span><span class="sxs-lookup"><span data-stu-id="213c9-2072">This event represents sending data through a UDP socket via nx_udp_socket_send.</span></span>

<span data-ttu-id="213c9-2073">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2073">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2074">Informazioni sul campo 1: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2074">Info Field 1: Pointer to socket</span></span>
- <span data-ttu-id="213c9-2075">Informazioni sul campo 2: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-2075">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="213c9-2076">Informazioni sul campo 3: lunghezza del pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-2076">Info Field 3: Packet length</span></span>
- <span data-ttu-id="213c9-2077">Campo dati 4: indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="213c9-2077">Info Field 4: Destination IP address</span></span>

### <a name="udp-socket-unbind"></a><span data-ttu-id="213c9-2078">Disassociazione socket UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2078">UDP Socket Unbind</span></span> 

#### <a name="nx_udp_socket_unbind"></a><span data-ttu-id="213c9-2079">nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="213c9-2079">nx_udp_socket_unbind</span></span>

<span data-ttu-id="213c9-2080">**Icona** ![ di Icona di disassociazione socket U D P](./media/user-guide/netx-events/image165.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2080">**Icon** ![U D P socket unbind icon](./media/user-guide/netx-events/image165.png)</span></span>

<span data-ttu-id="213c9-2081">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2081">**Description**</span></span>

<span data-ttu-id="213c9-2082">Questo evento rappresenta l'annullamento dell'associazione di una porta UDP con un socket tramite nx_udp_socket_unbind.</span><span class="sxs-lookup"><span data-stu-id="213c9-2082">This event represents unbinding a UDP port with a socket via nx_udp_socket_unbind.</span></span>

<span data-ttu-id="213c9-2083">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2083">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2084">Informazioni sul campo 1: puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="213c9-2084">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="213c9-2085">Informazioni sul campo 2: puntatore al socket</span><span class="sxs-lookup"><span data-stu-id="213c9-2085">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="213c9-2086">Informazioni sul campo 3: numero di porta</span><span class="sxs-lookup"><span data-stu-id="213c9-2086">Info Field 3: Port number</span></span>
- <span data-ttu-id="213c9-2087">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2087">Info Field 4: Not used</span></span>

### <a name="udp-source-extract"></a><span data-ttu-id="213c9-2088">Estrazione origine UDP</span><span class="sxs-lookup"><span data-stu-id="213c9-2088">UDP Source Extract</span></span> 

#### <a name="nx_udp_socket_create"></a><span data-ttu-id="213c9-2089">nx_udp_socket_create</span><span class="sxs-lookup"><span data-stu-id="213c9-2089">nx_udp_socket_create</span></span>

<span data-ttu-id="213c9-2090">**Icona** ![ di Icona estrazione origine U D P](./media/user-guide/netx-events/image166.png)</span><span class="sxs-lookup"><span data-stu-id="213c9-2090">**Icon** ![U D P source extract icon](./media/user-guide/netx-events/image166.png)</span></span>

<span data-ttu-id="213c9-2091">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="213c9-2091">**Description**</span></span>

<span data-ttu-id="213c9-2092">Questo evento rappresenta il recupero dell'indirizzo IP e del numero di porta di un pacchetto UDP ricevuto tramite nx_udp_source_extract.</span><span class="sxs-lookup"><span data-stu-id="213c9-2092">This event represents getting the IP address and port number of a received UDP packet via nx_udp_source_extract.</span></span>

<span data-ttu-id="213c9-2093">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="213c9-2093">**Information Fields**</span></span>

- <span data-ttu-id="213c9-2094">Informazioni sul campo 1: puntatore al pacchetto</span><span class="sxs-lookup"><span data-stu-id="213c9-2094">Info Field 1: Pointer to packet</span></span>
- <span data-ttu-id="213c9-2095">Campo informazioni 2: indirizzo IP del mittente</span><span class="sxs-lookup"><span data-stu-id="213c9-2095">Info Field 2: Sender's IP address</span></span>
- <span data-ttu-id="213c9-2096">Informazioni campo 3: numero di porta del mittente</span><span class="sxs-lookup"><span data-stu-id="213c9-2096">Info Field 3: Sender's port number</span></span>
- <span data-ttu-id="213c9-2097">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="213c9-2097">Info Field 4: Not used</span></span>