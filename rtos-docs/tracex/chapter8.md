---
title: Capitolo 8 - Azure RTOS di traccia NetX
description: Questo capitolo contiene una descrizione dei Azure RTOS NetX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: f785b421ffc6d588080eb45a50dad949daf1ca6a9bf36770110f0450cd465bf1
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116805300"
---
# <a name="chapter-8---azure-rtos-netx-trace-events"></a>Capitolo 8 - Azure RTOS di traccia NetX

Questo capitolo contiene una descrizione dei Azure RTOS NetX. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

Di seguito è riportato un elenco di eventi NetX visualizzati da TraceX.

| Icona                                           | Significato                 |
| -------------------------------- | ------------------------------------- |
| ![Icona interna R P Request Receive](./media/user-guide/netx-events/image1.png)    | Ricezione richiesta ARP interna |
| ![Icona interna R P Request Send](./media/user-guide/netx-events/image2.png)    | Invio di richieste ARP interne |
| ![Icona interna R P Response Receive](./media/user-guide/netx-events/image3.png)    | Ricezione della risposta ARP interna |
| ![Icona interna R P Response Send](./media/user-guide/netx-events/image4.png)    | Invio di risposta ARP interno |
| ![Icona di ricezione I C M P interna](./media/user-guide/netx-events/image5.png)    | Ricezione ICMP interna |
| ![Icona I C M P Send interna](./media/user-guide/netx-events/image6.png)    | Invio ICMP interno |
| ![Icona interna NetX I G M P Receive](./media/user-guide/netx-events/image7.png)    | Ricezione interna IGMP NetX |
| ![Icona I P Receive interno](./media/user-guide/netx-events/image8.png)    | Ricezione IP interna |
| ![Icona I P Send interno](./media/user-guide/netx-events/image9.png)    | Invio IP interno |
| ![Icona interna T C P Data Receive](./media/user-guide/netx-events/image10.png)    | Ricezione di dati TCP interni |
| ![Icona interna T C P Data Send](./media/user-guide/netx-events/image11.png)    | Invio di dati TCP interni |
| ![Icona interna T C P FIN Receive (Ricezione P FIN T C interna)](./media/user-guide/netx-events/image12.png)    | Ricezione FIN TCP interna |
| ![Icona interna T C P F I N Send](./media/user-guide/netx-events/image13.png)    | Invio INTERNO DELLA FIN TCP |
| ![Icona interna T C P R S T Receive](./media/user-guide/netx-events/image14.png)    | Ricezione RST TCP interna |
| ![Icona interna T C P R S T Send](./media/user-guide/netx-events/image15.png)    | Invio RST TCP interno |
| ![Icona interna T C P S Y N Receive](./media/user-guide/netx-events/image16.png)    | Ricezione SYN TCP interna |
| ![Icona interna T C P S Y N Send](./media/user-guide/netx-events/image17.png)    | Invio SYN TCP interno |
| ![Icona interna UD P Receive](./media/user-guide/netx-events/image18.png)    | Ricezione UDP interna |
| ![Icona interna UD P Send](./media/user-guide/netx-events/image19.png)    | Invio UDP interno |
| ![Icona interna R A R P Receive](./media/user-guide/netx-events/image20.png)    | Ricezione RARP interna |
| ![Icona interna R A R P Send](./media/user-guide/netx-events/image21.png)    | Invio RARP interno |
| ![Icona interna T C P Retry](./media/user-guide/netx-events/image22.png)    | Tentativi TCP interni |
| ![Icona di modifica dello stato di T C P interna](./media/user-guide/netx-events/image23.png)    | Modifica dello stato TCP interno |
| ![Icona di invio pacchetti del driver I/O interno](./media/user-guide/netx-events/image24.png)    | Invio di pacchetti del driver di I/O interno |
| ![icon](./media/user-guide/netx-events/image25.png)    | Inizializzazione del driver di I/O interno |
| ![Icona di inizializzazione del driver I/O interno](./media/user-guide/netx-events/image26.png)    | Abilitazione del collegamento del driver di I/O interno |
| ![Icona disabilitazione collegamento driver I/O interno](./media/user-guide/netx-events/image27.png)    | Disabilitazione del collegamento del driver di I/O interno |
| ![Icona di trasmissione pacchetti del driver I/O interno](./media/user-guide/netx-events/image28.png)    | Trasmissione pacchetti del driver di I/O interno |
| ![Icona di invio ARP del driver I/O interno](./media/user-guide/netx-events/image29.png)    | Invio ARP del driver di I/O interno |
| ![Icona di invio della risposta ARP del driver I/O interno](./media/user-guide/netx-events/image30.png)    | Invio della risposta ARP del driver di I/O interno |
| ![Icona di invio RARP del driver I/O interno](./media/user-guide/netx-events/image31.png)    | Invio RARP del driver di I/O interno |
| ![Icona aggiunta multicast del driver I/O interno](./media/user-guide/netx-events/image32.png)    | Aggiunta multicast del driver di I/O interno |
| ![Icona Disametto multicast del driver I/O interno](./media/user-guide/netx-events/image33.png)    | Lasciare multicast del driver di I/O interno |
| ![Icona Ottieni stato driver I/O interno](./media/user-guide/netx-events/image34.png)    | Stato di get del driver di I/O interno |
| ![Icona Del driver I/O interno Get Speed](./media/user-guide/netx-events/image35.png)    | Velocità get del driver di I/O interno |
| ![Icona del driver I/O interno Get Duplex Type](./media/user-guide/netx-events/image36.png)    | Tipo duplex del driver di I/O interno |
| ![Icona Ottieni conteggio errori driver I/O interno](./media/user-guide/netx-events/image37.png)    | Conteggio errori get driver I/O interno |
| ![Icona Ottieni conteggio RX del driver I/O interno](./media/user-guide/netx-events/image38.png)    | Conteggio RX del driver di I/O interno |
| ![Icona Ottieni conteggio TX driver I/O interno](./media/user-guide/netx-events/image39.png)    | Conteggio TX del driver di I/O interno |
| ![Icona Errori di allocazione del driver I/O interno](./media/user-guide/netx-events/image40.png)    | Errori di allocazione del driver di I/O interno |
| ![Icona di annullamento dell'inizializzazione del driver I/O interno](./media/user-guide/netx-events/image41.png)    | Annullamento dell'inizializzazione del driver di I/O interno |
| ![Icona di elaborazione posticipata del driver I/O interno](./media/user-guide/netx-events/image42.png)    | Elaborazione posticipata del driver di I/O interno |
| ![Icona Invalida voci dinamiche R P](./media/user-guide/netx-events/image43.png)    | **Le voci dinamiche ARP non sono valide** (*nx_arp_dynamic_entries_invalidate*) |
| ![Icona di R P Dynamic Entry Set](./media/user-guide/netx-events/image44.png)    | **Set di voci dinamiche ARP** (*nx_arp_dynamic_entry_set*) |
| ![Icona Abilitazione R P](./media/user-guide/netx-events/image45.png)    | **ARP Enable** (*nx_arp_enable*) |
| ![Icona R P Gratuitous Send](./media/user-guide/netx-events/image46.png)    | **Invio gratuito ARP** (*nx_arp_gratuitous_send*) |
| ![Icona di ricerca di un indirizzo hardware R P](./media/user-guide/netx-events/image47.png)    | **Ricerca di indirizzi hardware ARP** (*nx_arp_hardware_address_find*) |
| ![Icona R P Information Get](./media/user-guide/netx-events/image48.png)    | **ARP Information Get** (*nx_arp_info_get*) |
| ![Icona di ricerca di un indirizzo IP R P](./media/user-guide/netx-events/image49.png)    | **Ricerca di indirizzi IP ARP** (*nx_arp_ip_address_find*) |
| ![Icona di creazione di una voce statica R P](./media/user-guide/netx-events/image50.png)    | **Creazione di una voce statica ARP** (*nx_arp_static_entry_create*) |
| ![Icona R P Static Entries Delete (Elimina voci statiche R P)](./media/user-guide/netx-events/image51.png)    | **ARP Static Entries Delete** (*nx_arp_static_entries_delete*) |
| ![Icona di eliminazione di una voce statica R P](./media/user-guide/netx-events/image52.png)    | **ARP Static Entry Delete** (*nx_arp_static_entry_delete*) |
| ![Icona duo cache entry delete](./media/user-guide/netx-events/image53.png)    | **Duo Cache Entry Delete** (*nxd_nd_cache_entry_delete*) |
| ![Icona di Duo Cache Entry Set](./media/user-guide/netx-events/image54.png)    | **Duo Cache Entry Set** (*nxd_nd_cache_entry_set*) |
| ![Icona di Invalidazione di Duo Cache](./media/user-guide/netx-events/image55.png)    | **Invalidare Duo Cache** (*nxd_nd_cache_invalidate*) |
| ![Icona trova indirizzo I/O di Duo Cache](./media/user-guide/netx-events/image56.png)    | **Duo Cache IP Address Find** (*nxd_nd_cache_ip_address_find*) |
| ![Icona di abilitazione di Duo I C M P](./media/user-guide/netx-events/image57.png)    | **Duo ICMP Enable** (*nxd_icmp_enable*) |
| ![Icona ping Duo I C M P I P v 6](./media/user-guide/netx-events/image58.png)    | **Duo ICMP IPv6 Ping** (*nxd_icmp_ping*) |
| ![Icona trova dimensioni payload Duo I P Max](./media/user-guide/netx-events/image59.png)    | **Duo IP Max Payload Size Find** (*nx_max_payload_size_find*) |
| ![Icona di invio di pacchetti non elaborati duo IP](./media/user-guide/netx-events/image60.png)    | **Duo IP Raw Packet Send** (*nxd_ip_raw_packet_send*) |
| ![Icona di aggiunta router predefinito Duo I P v6](./media/user-guide/netx-events/image61.png)    | **Duo IPv6 Default Router Add** (*nxd_ipv6_default_router_add*) |
| ![Icona di eliminazione del router predefinito Duo I P v6](./media/user-guide/netx-events/image62.png)    | **Duo IPv6 Default Router Delete** (*nxd_ipv6_default_router_delete)* |
| ![Icona Di abilitazione di Duo I P v6](./media/user-guide/netx-events/image63.png)    | **Duo IPv6 Enable** *(nxd_ipv6_enable)* |
| ![Icona di Duo I P v 6 Global Address Get](./media/user-guide/netx-events/image64.png)    | **Duo IPv6 Global Address Get** (*nxd_ipv6_global_address_get*) |
| ![Icona di Duo I P v 6 Global Address Set](./media/user-guide/netx-events/image65.png)    | **Duo IPv6 Global Address Set** (*nxd_ipv6_global_address_set*) |
| ![Icona di avvio del processo di avvio di Duo I P 6](./media/user-guide/netx-events/image66.png)    | **Duo IPv6 Initiate Process** (*nxd_ipv6_initiate_dad_process*) |
| ![Icona di Duo I P v 6 Interface Address Get](./media/user-guide/netx-events/image67.png)    | **Duo IPv6 Interface Address Get** (*nxd_ipv6_interface_address_get*) |
| ![Icona del set di indirizzi dell'interfaccia Duo I P v6](./media/user-guide/netx-events/image68.png)    | **Duo IPv6 Interface Address Set** (*nxd_ipv6_interface_address_set*) |
| ![Icona di Duo I P v 6 Link Local Address Get](./media/user-guide/netx-events/image69.png)    | **Duo IPv6 Link Local Address Get** (*nxd_ipv6_linklocal_address_get*) |
| ![Icona di Duo I P v 6 Link Local Address Set](./media/user-guide/netx-events/image70.png)    | **Set di indirizzi locali del collegamento IPv6 Duo** (*nxd_ipv6_linklocal_address_set*) |
| ![Icona di invio di pacchetti non elaborati duo I P v6](./media/user-guide/netx-events/image71.png)    | **Duo IPv6 Raw Packet Send** (*nxd_ipv6_raw_packet_send)* |
| ![Icona Ottieni informazioni peer socket Duo T C](./media/user-guide/netx-events/image72.png)    | **Duo TCP Socket Peer Info Get** (*nxd_tcp_socket_peer_info_get*) |
| ![Icona dell'interfaccia del set di socket Duo T C](./media/user-guide/netx-events/image73.png)    | **Duo TCP Socket Set Interface** (*nxd_tcp_socket_set_interface*) |
| ![Icona di invio socket di Duo UD P](./media/user-guide/netx-events/image74.png)    | **Duo UDP Socket Send** (*nxd_udp_socket_send*) |
| ![Icona di Duo U D P Socket Set Interface](./media/user-guide/netx-events/image75.png)    | **Duo UDP Socket Set Interface** (*nxd_udp_socket_set_interface*) |
| ![Icona di estrazione origine di Duo UD P](./media/user-guide/netx-events/image76.png)    | **Duo UDP Source Extract** (*nxd_udp_source_extract*) |
| ![Icona I C M P Enable](./media/user-guide/netx-events/image77.png)    | **ICMP Enable** (*nx_icmp_enable*) |
| ![Icona I C M P Information Get](./media/user-guide/netx-events/image78.png)    | **ICMP Information Get** (*nx_icmp_info_get*) |
| ![Icona ping I C M P](./media/user-guide/netx-events/image79.png)    | **Ping ICMP** (*nx_icmp_ping*) |
| ![Icona abilita I G M P](./media/user-guide/netx-events/image80.png)    | **IGMP Enable** (*nx_igmp_enable*) |
| ![Icona I G M P Information Get](./media/user-guide/netx-events/image81.png)    | **IGMP Information Get** (*nx_igmp_info_get*) |
| ![Icona I G M P Loopback Disable](./media/user-guide/netx-events/image82.png)    | **IGMP Loopback Disable** (*nx_igmp_loopback_disable*) |
| ![Icona I G M P Loopback Enable](./media/user-guide/netx-events/image83.png)    | **IGMP Loopback Enable** (*nx_igmp_loopback_enable*) |
| ![Icona I G M P Join multicast](./media/user-guide/netx-events/image84.png)    | **Join multicast IGMP** (*nx_igmp_multicast_join*) |
| ![Icona I G M P Multicast Leave](./media/user-guide/netx-events/image85.png)    | **IGMP Multicast Leave** (*nx_igmp_multicast_leave*) |
| ![Icona I P Address Change Notify (Notifica modifica indirizzo IP)](./media/user-guide/netx-events/image86.png)    | **Notifica della modifica dell'indirizzo IP** (*nx_ip_address_change_notify*) |
| ![Icona I P Address Get](./media/user-guide/netx-events/image87.png)    | **Ip Address Get** (*nx_ip_address_get*) |
| ![Icona I P Address Set (Set di indirizzi IP)](./media/user-guide/netx-events/image88.png)    | **Set di indirizzi IP** (*nx_ip_address_set*) |
| ![Icona Crea](./media/user-guide/netx-events/image89.png)    | **Creazione IP** (*nx_ip_create*) |
| ![Icona I P Delete](./media/user-guide/netx-events/image90.png)    | **Eliminazione IP** (*nx_ip_delete*) |
| ![Icona I P Driver Direct Command](./media/user-guide/netx-events/image91.png)    | **Comando diretto del driver IP** (*nx_ip_driver_direct_command*) |
| ![Icona I P Forwarding Disable (Disabilita inoltro)](./media/user-guide/netx-events/image92.png)    | **Disabilitazione dell'inoltro IP** (*nx_ip_forwarding_disable*) |
| ![Icona I P Forwarding Enable (Abilita inoltro)](./media/user-guide/netx-events/image93.png)    | **Ip Forwarding Enable** (*nx_ip_forwarding_enable*) |
| ![Icona I P Fragment Disable (Disabilita frammento I/O)](./media/user-guide/netx-events/image94.png)    | **Disabilitazione frammento IP** (*nx_ip_fragment_disable*) |
| ![Icona I P Fragment Enable](./media/user-guide/netx-events/image95.png)    | **Abilitazione frammento IP** (*nx_ip_fragment_enable*)  |
| ![Icona I P Gateway Address Set](./media/user-guide/netx-events/image96.png)    | **Set di indirizzi del gateway IP** (*nx_ip_gateway_address_set*) |
| ![Icona I P Information Get](./media/user-guide/netx-events/image97.png)    | **Informazioni IP get** (*nx_ip_info_get*) |
| ![Icona I P Interface Attach](./media/user-guide/netx-events/image98.png)    | **Collegamento all'interfaccia IP** (*nx_ip_interface_attach*) |
| ![Icona I P Interface Info Get](./media/user-guide/netx-events/image99.png)    | **Informazioni sull'interfaccia IP Get** (*nx_ip_interface_info_get*) |
| ![Icona I P Raw Packet Disable](./media/user-guide/netx-events/image100.png)    | **Disabilitazione pacchetti non elaborati IP** (*nx_ip_raw_packet_disable*) |
| ![Icona I P Raw Packet Enable](./media/user-guide/netx-events/image101.png)    | **Ip Raw Packet Enable** (*nx_ip_raw_packet_enable*) |
| ![Icona I P Raw Packet Receive](./media/user-guide/netx-events/image102.png)    | **Ricezione di pacchetti non elaborati IP** (*nx_ip_raw_packet_receive*) |
| ![Icona I P Raw Packet Send](./media/user-guide/netx-events/image103.png)    | **Invio di pacchetti non elaborati IP** (*nx_ip_raw_packet_send*) |
| ![Icona Aggiungi route statica I P](./media/user-guide/netx-events/image104.png)    | **Aggiunta route statica IP** (*nx_ip_static_route_add*) |
| ![Icona I P Static Route Delete](./media/user-guide/netx-events/image105.png)    | **Eliminazione route statica IP** *(nx_ip_static_route_delete)* |
| ![Icona I P Status Check (Controllo stato I P)](./media/user-guide/netx-events/image106.png)    | **Controllo dello stato IP** (*nx_ip_status_check*)|
| ![Icona I P S E C Enable](./media/user-guide/netx-events/image107.png)    | **Abilita IPSEC** *(nx_ipsec_enable)* |
| ![Icona Disallocazione pacchetti](./media/user-guide/netx-events/image108.png)    | **Allocazione pacchetti** (*nx_packet_allocate*) |
| ![Icona Copia pacchetto](./media/user-guide/netx-events/image109.png)    | **Copia pacchetti** (*nx_packet_copy*) |
| ![Icona Di accodamento dati pacchetto](./media/user-guide/netx-events/image110.png)    | **Packet Data Append** (*nx_packet_data_append*) |
| ![Icona Offset estrazione dati pacchetto](./media/user-guide/netx-events/image111.png)    | **Offset estrazione dati** pacchetto (*nx_packet_data_extract_offset*) |
| ![Icona Recupera dati pacchetto](./media/user-guide/netx-events/image112.png)    | **Recupero dei dati dei** pacchetti (*nx_packet_data_retrieve*) |
| ![Icona Get della lunghezza del pacchetto](./media/user-guide/netx-events/image113.png)    | **Packet Length Get** (*nx_packet_length_get*) |
| ![Icona Crea pool di pacchetti](./media/user-guide/netx-events/image114.png)    | **Creazione pool di pacchetti** (*nx_packet_pool_create*) |
| ![Icona Eliminazione pool di pacchetti](./media/user-guide/netx-events/image115.png)    | **Eliminazione pool di** pacchetti (*nx_packet_pool_delete*) |
| ![Icona Ottieni informazioni sul pool di pacchetti](./media/user-guide/netx-events/image116.png)    | **Packet Pool Information Get** (*nx_packet_pool_info_get*) |
| ![Icona Versione pacchetto](./media/user-guide/netx-events/image117.png)    | **Versione pacchetto** (*nx_packet_release*) |
| ![Icona della versione di trasmissione pacchetti](./media/user-guide/netx-events/image118.png)    | **Versione di trasmissione pacchetti** (*nx_packet_transmit_release*) |
| ![Icona R A R P Disable](./media/user-guide/netx-events/image119.png)    | **RARP Disable** (*nx_rarp_disable*) |
| ![Icona R A R P Enable](./media/user-guide/netx-events/image120.png)    | **RARP Enable** (*nx_rarp_enable*) |
| ![Icona R A R P Information Get](./media/user-guide/netx-events/image121.png)    | **RARP Information Get** (*nx_rarp_info_get*) |
| ![Icona Inizializzazione sistema](./media/user-guide/netx-events/image122.png)    | **Inizializzazione sistema** (*nx_system_initialize*) |
| ![Icona T C P Client Socket Bind](./media/user-guide/netx-events/image123.png)    | **Tcp Client Socket Bind** (*nx_tcp_client_socket_bind*) |
| ![Icona del socket client T C P Connessione'icona](./media/user-guide/netx-events/image124.png)    | **Socket client TCP Connessione** (*nx_tcp_client_socket_connect*) |
| ![Icona T C P Client Socket Port Get](./media/user-guide/netx-events/image125.png)    | **Tcp Client Socket Port Get** (*nx_tcp_client_socket_port_get*) |
| ![Icona T C P Client Socket Unbind](./media/user-guide/netx-events/image126.png)    | **Tcp Client Socket Unbind** (*nx_tcp_client_socket_unbind*) |
| ![Icona T C P Enable (Abilita T C P)](./media/user-guide/netx-events/image127.png)    | **Tcp Enable** (*nx_tcp_enable*) |
| ![Icona T C P Free Port Find](./media/user-guide/netx-events/image128.png)    | **Tcp Free Port Find** (*nx_tcp_free_port_find*) |
| ![Icona T C P Information Get](./media/user-guide/netx-events/image129.png)    | **TCP Information Get** (*nx_tcp_info_get*) |
| ![Icona T C P Server Socket Accept](./media/user-guide/netx-events/image130.png)    | **Tcp Server Socket Accept** (*nx_tcp_server_socket_accept*) |
| ![Icona T C P Server Socket Listen](./media/user-guide/netx-events/image131.png)    | **Ascolto socket server TCP** (*nx_tcp_server_socket_listen*) |
| ![Icona T C P Server Socket Relisten](./media/user-guide/netx-events/image132.png)    | **Rielenza socket** del server TCP (*nx_tcp_server_socket_relisten*) |
| ![Icona T C P Server Socket Unaccept](./media/user-guide/netx-events/image133.png)    | **Tcp Server Socket Unaccept** (*nx_tcp_server_socket_unaccept*) |
| ![Icona T C P Server Socket Unlisten](./media/user-guide/netx-events/image134.png)    | **Tcp Server Socket Unlisten** (*nx_tcp_server_socket_unlisten*) |
| ![Icona Byte socket T C P disponibili](./media/user-guide/netx-events/image135.png)    | **Byte socket TCP disponibili** (*nx_tcp_socket_bytes_available*) |
| ![Icona T C P Socket Create](./media/user-guide/netx-events/image136.png)    | **Tcp Socket Create** (*nx_tcp_socket_create*) |
| ![Icona T C P Socket Delete](./media/user-guide/netx-events/image137.png)    | **Eliminazione socket TCP** (*nx_tcp_socket_delete*) |
| ![Icona T C P Socket Disconnect](./media/user-guide/netx-events/image138.png)    | **Disconnessione socket TCP** (*nx_tcp_socket_disconnect*) |
| ![Icona T C P Socket Information Get](./media/user-guide/netx-events/image139.png)    | **Tcp Socket Information Get** (*nx_tcp_socket_info_get*) |
| ![Icona T C P Socket MSS Get](./media/user-guide/netx-events/image140.png)    | **TCP Socket MSS Get** (*nx_tcp_socket_mss_get*) |
| ![Icona T C P Socket MSS Peer Get](./media/user-guide/netx-events/image141.png)    | **TCP Socket MSS Peer Get** (*nx_tcp_socket_mss_peer_get*) |
| ![Icona T C P Socket MSS Set](./media/user-guide/netx-events/image142.png)    | **TCP Socket MSS Set** (*nx_tcp_socket_mss_set*) |
| ![Icona T C P Socket Peer Info Get](./media/user-guide/netx-events/image143.png)    | **Tcp Socket Peer Info Get** (*nx_tcp_socket_peer_info_get*) |
| ![Icona T C P Socket Receive](./media/user-guide/netx-events/image144.png)    | **Ricezione socket TCP** (*nx_tcp_socket_receive*) |
| ![Icona T C P Socket Receive Notify](./media/user-guide/netx-events/image145.png)    | **Notifica ricezione socket TCP** (*nx_tcp_socket_receive_notify*) |
| ![Icona T C P Socket Send](./media/user-guide/netx-events/image146.png)    | **TCP Socket Send** (*nx_tcp_socket_send*) |
| ![Icona T C P Socket State Wait](./media/user-guide/netx-events/image147.png)    | **Attesa dello stato del socket TCP** (*nx_tcp_socket_state_wait*) |
| ![Icona di configurazione T C P Socket Transmit Configure](./media/user-guide/netx-events/image148.png)    | **Tcp Socket Transmit Configure** (*nx_tcp_socket_transmit_configure*) |
| ![Icona T C P Socket Window Update Notify Set](./media/user-guide/netx-events/image149.png)    | **Tcp Socket Window Update Notify Set** (*nx_tcp_socket_window_update_notify_set*)  |
| ![Icona U D P Enable](./media/user-guide/netx-events/image150.png)    | **Udp Enable** (*nx_udp_enable*) |
| ![Icona U D P Free Port Find](./media/user-guide/netx-events/image151.png)    | **Ricerca porte gratuite UDP** (*nx_udp_free_port_find*) |
| ![Icona U D P Information Get](./media/user-guide/netx-events/image152.png)    | **Udp Information Get** (*nx_udp_info_get*) |
| ![Icona UD P Socket Bind](./media/user-guide/netx-events/image153.png)    | **Binding socket UDP** (*nx_udp_socket_bind*) |
| ![Icona Byte socket U D P disponibili](./media/user-guide/netx-events/image154.png)    | **Byte socket UDP disponibili** (*nx_udp_socket_bytes_available*) |
| ![Icona disabilitazione checksum del socket U D P](./media/user-guide/netx-events/image155.png)    | **Udp Socket Checksum Disable** (*nx_udp_socket_checksum_disable*) |
| ![Icona U D P Socket Checksum Enable](./media/user-guide/netx-events/image156.png)    | **Udp Socket Checksum Enable** *(nx_udp_socket_checksum_enable)* |
| ![Icona UD P Socket Create](./media/user-guide/netx-events/image157.png)    | **Creazione socket UDP** (*nx_udp_socket_create*) |
| ![Icona U D P Socket Delete](./media/user-guide/netx-events/image158.png)    | **Eliminazione socket UDP** (*nx_udp_socket_delete*) |
| ![Icona U D Socket Information Get](./media/user-guide/netx-events/image159.png)    | **Udp Socket Information Get** (*nx_udp_socket_info_get*) |
| ![Icona del set di interfacce U D P Socket](./media/user-guide/netx-events/image160.png)    | **Set di interfacce socket UDP** (*nx_udp_socket_interface_set*) |
| ![Icona U D P Socket Port Get](./media/user-guide/netx-events/image161.png)    | **Udp Socket Port Get** (*nx_udp_socket_port_get*) |
| ![Icona ricezione socket U D P](./media/user-guide/netx-events/image162.png)    | **Ricezione socket UDP** (*nx_udp_socket_receive*) |
| ![Icona UD P Socket Receive Notify](./media/user-guide/netx-events/image163.png)    | **Udp Socket Receive Notify** (*nx_udp_socket_receive_notify*) |
| ![Icona U D P Socket Send](./media/user-guide/netx-events/image164.png)    | **Udp Socket Send** (*nx_udp_socket_send*) |
| ![Icona U D P Socket Unbind](./media/user-guide/netx-events/image165.png)    | **Unbind del socket UDP** (*nx_udp_socket_unbind*) |
| ![Icona UD P Source Extract](./media/user-guide/netx-events/image166.png)    | **Estrazione origine UDP** (*nx_udp_source_extract*) |

## <a name="event-descriptions"></a>Descrizioni di eventi

Le pagine seguenti descrivono gli eventi di traccia NetX.

### <a name="internal-arp-request-receive"></a>Ricezione richiesta ARP interna 

#### <a name="internal-arp-request-receive"></a>Ricezione richiesta ARP interna

**Icona** ![ Icona di ricezione della richiesta ARP interna](./media/user-guide/netx-events/image1.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione della richiesta ARP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Info 2: Indirizzo IP di origine
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-arp-request-send"></a>Invio di richieste ARP interne 

#### <a name="internal-arp-request-send"></a>Invio di richieste ARP interne

**Icona** ![ Icona di invio della richiesta ARP interna](./media/user-guide/netx-events/image2.png)

**Descrizione**

Questo evento rappresenta un evento di invio di richieste ARP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP di destinazione
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-arp-response-receive"></a>Ricezione della risposta ARP interna 

#### <a name="internal-arp-request-receive"></a>Ricezione richiesta ARP interna

**Icona** ![ Icona di ricezione della richiesta ARP interna](./media/user-guide/netx-events/image3.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione della risposta NetX ARP interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Info 2: Indirizzo IP di origine
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-arp-response-send"></a>Invio di risposta ARP interno 

#### <a name="internal-arp-request-send"></a>Invio di richieste ARP interne

**Icona** ![ Icona di invio della richiesta ARP interna](./media/user-guide/netx-events/image4.png)

**Descrizione**

Questo evento rappresenta un evento di invio della risposta NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP di destinazione
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-icmp-receive"></a>Ricezione ICMP interna 

#### <a name="internal-icmp-receive"></a>Ricezione ICMP interna

**Icona** ![ Icona di ricezione I C M P interna](./media/user-guide/netx-events/image5.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione ICMP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Info 2: Indirizzo IP di origine
- Campo informazioni 3: Puntatore al pacchetto
- Info Field 4: Word 0 of ICMP header (Campo informazioni 4: Word 0 dell'intestazione ICMP)

### <a name="internal-icmp-send"></a>Invio ICMP interno 

#### <a name="internal-icmp-send"></a>Invio ICMP interno

**Icona** ![ Icona di invio I C M P interno](./media/user-guide/netx-events/image6.png)

**Descrizione**

Questo evento rappresenta un evento di invio ICMP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP di destinazione
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Parola 0 dell'intestazione ICMP

### <a name="internal-igmp-receive"></a>Ricezione IGMP interna 

#### <a name="internal-igmp-receive"></a>Ricezione IGMP interna

**Icona** ![ Icona di ricezione IG M P interna](./media/user-guide/netx-events/image7.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione IGMP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore IP
- Campo informazioni 2: Indirizzo IP di origine
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Parola 0 dell'intestazione IGMP

### <a name="internal-ip-receive"></a>Ricezione IP interna 

#### <a name="internal-ip-receive"></a>Ricezione IP interna

**Icona** ![ Icona di ricezione indirizzo I/O interno](./media/user-guide/netx-events/image8.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione IP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP di origine
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Lunghezza pacchetto

### <a name="internal-ip-send"></a>Invio IP interno

#### <a name="internal-ip-send"></a>Invio IP interno

**Icona** ![ Icona I/O interno](./media/user-guide/netx-events/image9.png)

**Descrizione**

Questo evento rappresenta un evento di invio IP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP di destinazione
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Lunghezza pacchetto

### <a name="internal-tcp-data-receive"></a>Ricezione di dati TCP interni 

#### <a name="internal-tcp-data-receive"></a>Ricezione di dati TCP interni

**Icona** ![ Icona di ricezione dei dati T C P interna](./media/user-guide/netx-events/image10.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione dati TCP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP di origine
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Numero di sequenza di ricezione

### <a name="internal-tcp-data-send"></a>Invio di dati TCP interni 

#### <a name="internal-tcp-data-send"></a>Invio dati TCP interno

**Icona** ![ Icona di invio dei dati T C P interna](./media/user-guide/netx-events/image11.png)

**Descrizione**

Questo evento rappresenta un evento di invio dati TCP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Trasmettere il numero di sequenza

### <a name="internal-tcp-fin-receive"></a>Ricezione TCP FIN interna 

#### <a name="internal-tcp-fin-receive"></a>Ricezione interna TCP fin

**Icona** ![ Icona di ricezione interna di T C P F I N](./media/user-guide/netx-events/image12.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione NETX TCP FIN interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Numero di sequenza di ricezione

### <a name="internal-tcp-fin-send"></a>Invio TCP FIN interno 

#### <a name="internal-tcp-fin-send"></a>Tcp fin send interno

**Icona** ![ Icona di invio interna di T C P F I N](./media/user-guide/netx-events/image13.png)

**Descrizione**

Questo evento rappresenta un evento di invio NETX TCP FIN interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Trasmettere il numero di sequenza

### <a name="internal-tcp-rst-receive"></a>Ricezione RST TCP interna 

#### <a name="internal-tcp-rst-receive"></a>Ricezione RST TCP interna

**Icona** ![ Icona di ricezione T C R S T interna](./media/user-guide/netx-events/image14.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione di reimpostazione TCP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Campo informazioni 2: puntatore al socket.
- Campo informazioni 3: puntatore al pacchetto.
- Campo informazioni 4: numero di sequenza di ricezione.

### <a name="internal-tcp-rst-send"></a>Invio RST TCP interno 

#### <a name="internal-tcp-rst-send"></a>Invio RST TCP interno

**Icona** ![ Icona di invio T C R S T interna](./media/user-guide/netx-events/image15.png)

**Descrizione**

Questo evento rappresenta un evento di invio di reimpostazione TCP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Trasmettere il numero di sequenza

### <a name="internal-tcp-syn-receive"></a>Ricezione SYN TCP interna 

#### <a name="internal-tcp-syn-receive"></a>Ricezione SYN TCP interna

**Icona** ![ Icona di ricezione T C S Y N interna](./media/user-guide/netx-events/image16.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione NETX TCP SYN interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Numero di sequenza di ricezione

### <a name="internal-tcp-syn-send"></a>Invio SYN TCP interno 

#### <a name="internal-tcp-syn-send"></a>Invio SYN TCP interno

**Icona** ![ Icona interna T C P S Y N send](./media/user-guide/netx-events/image17.png)

**Descrizione**

Questo evento rappresenta un evento di invio NETX TCP SYN interno.

Campi di informazioni 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto -Info Campo 4: Trasmettere il numero di sequenza

### <a name="internal-udp-receive"></a>Ricezione UDP interna 

#### <a name="internal-udp-receive"></a>Ricezione UDP interna

**Icona** ![ Icona di ricezione UD P interna](./media/user-guide/netx-events/image18.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione UDP NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Info Field 4: Word 0 of UDP header (Campo informazioni 4: Word 0 dell'intestazione UDP)

### <a name="internal-udp-send"></a>Invio UDP interno 

#### <a name="internal-udp-send"></a>Invio UDP interno

**Icona** ![ Icona di invio UD P interna](./media/user-guide/netx-events/image19.png)

**Descrizione**

Questo evento rappresenta un evento di invio UDP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Info Field 4: Word 0 of UDP header (Campo informazioni 4: Word 0 dell'intestazione UDP)

### <a name="internal-rarp-receive"></a>Ricezione RARP interna 

#### <a name="internal-rarp-receive"></a>Ricezione RARP interna 

**Icona** ![ Icona di ricezione R A R P interna](./media/user-guide/netx-events/image20.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione RARP NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP di destinazione
- Campo informazioni 3: Puntatore al pacchetto
- Info Field 4: Word 1 of RARP header (Campo informazioni 4: Word 1 dell'intestazione RARP)

### <a name="internal-rarp-send"></a>Invio RARP interno 

#### <a name="internal-rarp-send"></a>Invio RARP interno 

**Icona** ![ Icona di invio R A R P interna](./media/user-guide/netx-events/image21.png)

**Descrizione**

Questo evento rappresenta un evento di invio RARP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP di destinazione
- Campo informazioni 3: Puntatore al pacchetto
- Info Field 4: Word 1 of RARP header (Campo informazioni 4: Word 1 dell'intestazione RARP)

### <a name="internal-tcp-retry"></a>Tentativi TCP interni 

#### <a name="internal-tcp-retry"></a>Nuovo tentativo TCP interno 

**Icona** ![ Icona di ripetizione dei tentativi T C P interna](./media/user-guide/netx-events/image22.png)

**Descrizione**

Questo evento rappresenta un evento di ripetizione dei tentativi TCP NetX interno.

**Campi di informazioni**
- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore al pacchetto
- Campo informazioni 4: Numero di tentativi

### <a name="internal-tcp-state-change"></a>Modifica dello stato TCP interno 

#### <a name="internal-tcp-state-change"></a>Modifica dello stato TCP interno 

**Icona** ![ Icona di modifica dello stato di T C P interno](./media/user-guide/netx-events/image23.png)

**Descrizione**

Questo evento rappresenta un evento di modifica dello stato del socket TCP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Stato precedente
- Campo informazioni 4: Nuovo stato

### <a name="internal-io-driver-packet-send"></a>Invio di pacchetti del driver di I/O interno 

#### <a name="internal-io-driver-packet-send"></a>Invio di pacchetti del driver di I/O interno

**Icona** ![ Icona di invio pacchetti del driver I/O interno](./media/user-guide/netx-events/image24.png)

**Descrizione**

Questo evento rappresenta un evento interno di invio di pacchetti del driver di I/O NetX.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Dimensioni pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-initialize"></a>Inizializzazione del driver di I/O interno 

#### <a name="internal-io-driver-initialize"></a>Inizializzazione del driver di I/O interno

**Icona** ![ Icona di inizializzazione del driver I/O interno](./media/user-guide/netx-events/image25.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="internal-io-driver-link-enable"></a>Abilitazione del collegamento del driver di I/O interno 

#### <a name="internal-io-driver-link-enable"></a>Abilitazione del collegamento del driver di I/O interno

**Icona** ![ Icona di abilitazione del collegamento del driver I/O interno](./media/user-guide/netx-events/image26.png)

**Descrizione**

Questo evento rappresenta un evento di abilitazione del collegamento di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-link-disable"></a>Disabilitazione del collegamento del driver di I/O interno 

#### <a name="internal-io-driver-link-disable"></a>Disabilitazione del collegamento del driver di I/O interno

**Icona** ![ Icona di disabilitazione del collegamento del driver I/O interno](./media/user-guide/netx-events/image27.png)

**Descrizione**

Questo evento rappresenta un evento di disabilitazione del collegamento del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-packet-broadcast"></a>Trasmissione pacchetti del driver di I/O interno 

#### <a name="internal-io-driver-packet-broadcast"></a>Trasmissione dei pacchetti del driver di I/O interno

**Icona** ![ Icona di trasmissione pacchetti del driver I/O interno](./media/user-guide/netx-events/image28.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione di pacchetti del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Dimensioni pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-arp-send"></a>Invio ARP del driver di I/O interno 

#### <a name="internal-io-driver-arp-send"></a>Invio ARP del driver di I/O interno

**Icona** ![ Icona di invio ARP del driver I/O interno](./media/user-guide/netx-events/image29.png)

**Descrizione**

Questo evento rappresenta un evento di invio ARP del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Dimensioni pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-arp-response-send"></a>Invio della risposta ARP del driver di I/O interno 

#### <a name="internal-io-driver-arp-response-send"></a>Invio della risposta ARP del driver di I/O interno

**Icona** ![ Icona di invio della risposta ARP del driver I/O interno](./media/user-guide/netx-events/image30.png)

**Descrizione**

Questo evento rappresenta un evento di invio della risposta ARP del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Dimensioni pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-rarp-send"></a>Driver di I/O interno RARP Send 

#### <a name="internal-io-driver-rarp-send"></a>Invio RARP del driver di I/O interno

**Icona** ![ Icona di invio RARP del driver I/O interno](./media/user-guide/netx-events/image31.png)

**Descrizione**

Questo evento rappresenta un evento di invio RARP del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Dimensioni pacchetto
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-multicast-join"></a>Join multicast del driver di I/O interno 

#### <a name="internal-io-driver-multicast-join"></a>Join multicast del driver di I/O interno

**Icona** ![ Icona di join multicast del driver I/O interno](./media/user-guide/netx-events/image32.png)

**Descrizione**

Questo evento rappresenta un evento di join multicast del driver di I/O NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-multicast-leave"></a>Lascia il multicast del driver di I/O interno 

#### <a name="internal-io-driver-multicast-leave"></a>Lascia il multicast del driver di I/O interno

**Icona** ![ Icona di uscire dal multicast del driver I/O interno](./media/user-guide/netx-events/image33.png)

**Descrizione**

Questo evento rappresenta un evento di lasciare multicast interno del driver di I/O NetX.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-status"></a>Stato get del driver di I/O interno 

#### <a name="internal-io-driver-get-status"></a>Ottenere lo stato del driver di I/O interno

**Icona** ![ Icona per ottenere lo stato del driver I/O interno](./media/user-guide/netx-events/image34.png)

**Descrizione**

Questo evento rappresenta un evento di stato get del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-speed"></a>Velocità di get del driver di I/O interno 

#### <a name="internal-io-driver-get-speed"></a>Velocità del driver di I/O interno

**Icona** ![ Icona per ottenere la velocità del driver I/O interno](./media/user-guide/netx-events/image35.png)

**Descrizione**

Questo evento rappresenta un evento di velocità get di un driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-duplex-type"></a>Tipo duplex get del driver di I/O interno 

#### <a name="internal-io-driver-get-duplex-type"></a>Tipo duplex del driver di I/O interno

**Icona** ![ Icona per ottenere il tipo duplex del driver I/O interno](./media/user-guide/netx-events/image36.png)

**Descrizione**

Questo evento rappresenta un evento di tipo duplex get del driver di I/O NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-error-count"></a>Conteggio errori get driver I/O interno

#### <a name="internal-io-driver-get-error-count"></a>Numero di errori restituiti dal driver di I/O interno

**Icona** ![ Icona di conteggio errori del driver I/O interno](./media/user-guide/netx-events/image37.png)

**Descrizione**

Questo evento rappresenta un evento di conteggio errori del driver I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-rx-count"></a>Numero RX del driver di I/O interno 

#### <a name="internal-io-driver-get-rx-count"></a>Il driver di I/O interno ottiene il conteggio RX

**Icona** ![ Icona di conteggio RX del driver I/O interno](./media/user-guide/netx-events/image38.png)

**Descrizione**

Questo evento rappresenta un evento di conteggio RX del driver I/O NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-tx-count"></a>Numero TX del driver di I/O interno 

#### <a name="internal-io-driver-get-tx-count"></a>Il driver di I/O interno ottiene il conteggio TX

**Icona** ![ Icona di conteggio T X del driver I/O interno](./media/user-guide/netx-events/image39.png)

**Descrizione**

Questo evento rappresenta un evento di conteggio TX del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-get-allocation-errors"></a>Errori di allocazione del driver di I/O interno 

#### <a name="internal-io-driver-get-allocation-errors"></a>Errori di allocazione del driver di I/O interno

**Icona** ![ Icona degli errori di allocazione del driver I/O interno](./media/user-guide/netx-events/image40.png)

**Descrizione**

Questo evento rappresenta un evento interno degli errori di allocazione del driver di I/O NetX.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-un-initialize"></a>Inizializzazione del driver di I/O interno 

#### <a name="internal-io-driver-un-initialize"></a>Annullamento dell'inizializzazione del driver di I/O interno 

**Icona** ![ Icona di annullamento dell'inizializzazione del driver I/O interno](./media/user-guide/netx-events/image41.png)

**Descrizione**

Questo evento rappresenta un evento di annullamento dell'inizializzazione di un driver di I/O NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="internal-io-driver-deferred-processing"></a>Elaborazione posticipata del driver di I/O interno 

#### <a name="internal-io-driver-deferred-processing"></a>Elaborazione posticipata del driver di I/O interno 

**Icona** ![ Icona di elaborazione posticipata del driver I/O interno](./media/user-guide/netx-events/image42.png)

**Descrizione**

Questo evento rappresenta un evento di elaborazione posticipata del driver di I/O NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Lunghezza pacchetto
- Campo informazioni 4: Non usato

### <a name="arp-dynamic-entries-invalidate"></a>Le voci dinamiche ARP non sono valide 

#### <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate

**Icona** ![ Icona A R P Dynamic Entries Invalidate (Invalida voci dinamiche R P)](./media/user-guide/netx-events/image43.png)

**Descrizione**

Questo evento rappresenta l'invalidazione di tutti gli interi ARP dinamici tramite nx_arp_dynamic_entries_invalidate.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Voci invalidate
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="arp-dynamic-entry-set"></a>Set di voci dinamiche ARP 

#### <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set

**Icona** ![ Icona di R P Dynamic Entry Set](./media/user-guide/netx-events/image44.png)

**Descrizione**

Questo evento rappresenta l'impostazione di una voce ARP dinamica tramite nx_arp_dynamic_entry_set.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP
- Campo informazioni 3: Indirizzo fisico (MSW)
- Campo informazioni 4: Indirizzo fisico (LSW)

### <a name="arp-enable"></a>ARP Enable 

#### <a name="nx_arp_enable"></a>nx_arp_enable

**Icona** ![ Icona di abilitazione di R P](./media/user-guide/netx-events/image45.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di ARP tramite nx_arp_enable.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore alla memoria della cache ARP
- Campo informazioni 3: Dimensioni memoria cache ARP
- Campo informazioni 4: Non usato

### <a name="arp-gratuitous-send"></a>Invio gratuito ARP 

#### <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send

**Icona** ![ Icona di invio gratuito di R P](./media/user-guide/netx-events/image46.png)

**Descrizione**

Questo evento rappresenta un invio gratuito di ARP tramite nx_arp_gratuitous_send.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="arp-hardware-address-find"></a>Ricerca di indirizzi hardware ARP 

#### <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find

**Icona** ![ Icona di ricerca di un indirizzo hardware R P](./media/user-guide/netx-events/image47.png)

**Descrizione**

Questo evento rappresenta la ricerca di un indirizzo fisico tramite nx_arp_hardware_address_find.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP
- Campo informazioni 3: Indirizzo fisico (MSW)
- Campo informazioni 4: Indirizzo fisico (LSW)

### <a name="arp-information-get"></a>Ottenere informazioni ARP 

#### <a name="nx_arp_info_get"></a>nx_arp_info_get

**Icona** ![ Icona di R P informition get](./media/user-guide/netx-events/image48.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_arp_info_get.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: ARP inviati
- Campo informazioni 3: Risposte ARP
- Info Field 4: ARP received

### <a name="arp-ip-address-find"></a>Ricerca di indirizzi IP ARP 

#### <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find

**Icona** ![ Icona di ricerca di un indirizzo I/O R](./media/user-guide/netx-events/image49.png)

**Descrizione**

Questo evento rappresenta la ricerca di un indirizzo IP associato all'indirizzo fisico fornito tramite nx_arp_ip_address_find.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP
- Campo informazioni 3: Indirizzo fisico (MSW)
- Campo informazioni 4: Indirizzo fisico (LSW)

### <a name="arp-static-entry-create"></a>Creazione di una voce statica ARP 

#### <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create

**Icona** ![ Icona di creazione di una voce statica R P](./media/user-guide/netx-events/image50.png)

**Descrizione**

Questo evento rappresenta la creazione di una voce ARP statica tramite nx_arp_static_entry_create.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP
- Campo informazioni 3: Indirizzo fisico (MSW)
- Campo informazioni 4: Indirizzo fisico (LSW)

### <a name="arp-static-entries-delete"></a>Eliminazione di voci statiche ARP 

#### <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

**Icona** ![ Icona di eliminazione delle voci statiche di R P](./media/user-guide/netx-events/image51.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di tutte le voci statiche ARP tramite nx_arp_static_entries_delete.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Voci eliminate
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="arp-static-entry-delete"></a>Eliminazione voce statica ARP 

### <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete

**Icona** ![ Icona di eliminazione di una voce statica R P](./media/user-guide/netx-events/image52.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di una voce ARP statica tramite nx_arp_static_entry_delete.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo IP
- Campo informazioni 3: Indirizzo fisico (MSW)
- Campo informazioni 4: Indirizzo fisico (LSW)

### <a name="duo-cache-entry-delete"></a>Eliminazione voce cache Duo 

#### <a name="nxd_und_cache_entry_delete"></a>nxd_und_cache_entry_delete

**Icona** ![ Icona di eliminazione della voce della cache duo](./media/user-guide/netx-events/image53.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di una voce nella tabella della cache adiacente tramite nx_udp_socket_create.

**Campi di informazioni** 

- Campo informazioni 1: quarta parola (meno significativa) dell'indirizzo locale del collegamento IPv6 da eliminare
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-cache-entry-set"></a>Duo Cache Entry Set 

#### <a name="nxd_nd_cache_entry_set"></a>nxd_nd_cache_entry_set

**Icona** ![ Icona del set di voci della cache Duo](./media/user-guide/netx-events/image54.png)

**Descrizione**

Questo evento rappresenta la creazione di una voce della cache e l'aggiunta alla tabella della cache adiacente tramite nxd_nd_cache_entry_set.

**Campi di informazioni** 

- Campo informazioni 1: quarta parola (meno significativa) dell'indirizzo IPv6 da aggiungere
- Campo informazioni 2: indirizzo fisico msb
- Campo informazioni 3: Indirizzo fisico lsb
- Campo informazioni 4: Non usato

### <a name="duo-cache-invalidate"></a>Invalidazione di Duo Cache 

#### <a name="nxd_nd_cache_invalidate"></a>nxd_nd_cache_invalidate

**Icona** ![ Icona invalida cache Duo](./media/user-guide/netx-events/image55.png)

**Descrizione**

Questo evento rappresenta l'invalidazione dell'intera tabella della cache adiacente tramite nxd_nd_cache_invalidate.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-cache-ip-address-find"></a>Ricerca dell'indirizzo IP di Duo Cache 

#### <a name="nxd_nd_cache_ip_address_find"></a>nxd_nd_cache_ip_address_find

**Icona** ![ Icona di ricerca dell'indirizzo IP di Duo Cache](./media/user-guide/netx-events/image56.png)

**Descrizione**

Questo evento rappresenta il recupero di un indirizzo IP corrispondente all'indirizzo fisico fornito dalla tabella della cache tramite nxd_nd_cache_ip_address_find.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo IPv6
- Campo informazioni 3: indirizzo fisico msb
- Campo informazioni 4: Indirizzo fisico lsb

### <a name="duo-icmp-enable"></a>Duo ICMP Enable 

#### <a name="nxd_icmp_enable"></a>nxd_icmp_enable

**Icona** ![ Icona di abilitazione di Duo I C M P](./media/user-guide/netx-events/image57.png)

**Descrizione**

Questo evento rappresenta i servizi ICMPv4 e ICMPv6 abilitati nell'istanza IP specificata tramite nxd_icmp_enable.

**Campi di informazioni**
- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-icmp-ping"></a>Duo ICMP Ping 

#### <a name="nxd_icmp_ping"></a>nxd_icmp_ping

**Icona** ![ Icona ping di Duo I C M P](./media/user-guide/netx-events/image58.png)

**Descrizione**

Questo evento rappresenta l'invio di un ping (richiesta echo) a un host IPv6 tramite nxd_icmp_ping.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: indirizzo IPv6
- Campo informazioni 3: Puntatore ai dati echo
- Campo informazioni 4: Dimensioni dei dati echo

### <a name="duo-ip-max-payload-size-find"></a>Ricerca delle dimensioni massime del payload di Duo IP 

#### <a name="nxd_ip_max_payload_size"></a>nxd_ip_max_payload_size

**Icona** ![ Icona di ricerca delle dimensioni massime del payload duo I P](./media/user-guide/netx-events/image59.png)

**Descrizione**

Questo evento calcola il payload massimo che il pacchetto specificato può contenere senza richiedere frammentazione.

**Campi di informazioni**

- Campo informazioni 1: Puntatore socket
- Campo informazioni 2: Indirizzo IP peer
- Campo informazioni 3: Campo informazioni porta peer 4: Non usato

### <a name="duo-ip-raw-packet-send"></a>Duo IP Raw Packet Send 

#### <a name="nxd_ip_max_packet_send"></a>nxd_ip_max_packet_send

**Icona** ![ Icona di invio di pacchetti non elaborati duo IP](./media/user-guide/netx-events/image60.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto IP non elaborato dall'interfaccia di rete specificata all'indirizzo IP di destinazione nxd_ip_raw_packet_send.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto da inviare
- Campo informazioni 3: Puntatore all'indirizzo di destinazione
- Campo informazioni 4: Protocollo di pacchetti

### <a name="duo-ipv6-default-router-add"></a>Aggiunta router predefinito Duo IPv6 

#### <a name="nxd_ipv6_default_router_add"></a>nxd_ipv6_default_router_add

**Icona** ![ Icona di aggiunta del router predefinito Duo I P v6](./media/user-guide/netx-events/image61.png)

**Descrizione**

Questo evento rappresenta l'aggiunta di un router predefinito alla tabella di routing IPv6 dell'istanza IP tramite nxd_ipv6_default_router_add.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Campo informazioni 2: indirizzo di rete di destinazione.
- Campo informazioni 3: informazioni sulla durata.
- Campo informazioni 4: Non usato.

### <a name="duo-ipv6-default-router-delete"></a>Duo IPv6 Default Router Delete 

#### <a name="nxd_ipv6_default_router_delete"></a>nxd_ipv6_default_router_delete

**Icona** ![ Icona di eliminazione del router predefinito Duo I P v6](./media/user-guide/netx-events/image62.png)

**Descrizione**

Questo evento rappresenta la rimozione di un router predefinito dalla tabella di routing IPv6 dell'istanza IP tramite nxd_ipv6_default_router_delete.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo IPv6 del router predefinito.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="duo-ipv6-enable"></a>Duo IPv6 Enable 

#### <a name="nxd_ipv6_enable"></a>nxd_ipv6_enable

**Icona** ![ Icona di abilitazione di Duo I P v6](./media/user-guide/netx-events/image63.png)

**Descrizione**

Questo evento rappresenta l'abilitazione dei servizi IPv6 nell'istanza IP fornita tramite nxd_ipv6_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-ipv6-global-address-get"></a>Duo IPv6 Global Address Get 

#### <a name="nxd_ipv6_global_address_get"></a>nxd_ipv6_global_address_get

**Icona** ![ Icona di ottenere l'indirizzo globale duo I P v6](./media/user-guide/netx-events/image64.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP globale (primario) nell'istanza IP in corrispondenza dell'indice 1 nella tabella dell'interfaccia dell'istanza IP tramite nxd_ipv6_global_address_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo globale
- Campo informazioni 3: lunghezza del prefisso dell'indirizzo IPv6.
- Campo informazioni 4: indice nella tabella dell'interfaccia IP (1).

### <a name="duo-ipv6-global-address-set"></a>Duo IPv6 Global Address Set 

#### <a name="nxd_ipv6_global_address_set"></a>nxd_ipv6_global_address_set

**Icona** ![ Icona del set di indirizzi globale Duo I P v6](./media/user-guide/netx-events/image65.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP globale (primario) nell'istanza IP in corrispondenza dell'indice 1 nella tabella dell'interfaccia dell'istanza IP tramite nxd_ipv6_global_address_set.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo globale
- Campo informazioni 3: Lunghezza prefisso indirizzo IPv6
- Campo informazioni 4: Indice nella tabella dell'interfaccia IP (1)

### <a name="duo-ipv6-initiate-dad-process"></a>Duo IPv6 Initiate Dad Process 

#### <a name="nxd_ipv6_initiate_dad_process"></a>nxd_ipv6_initiate_dad_process

**Icona** ![ Icona del processo di avvio di Duo I P v6](./media/user-guide/netx-events/image66.png)

**Descrizione**

Questo evento rappresenta l'inizio del processo DI RILEVAMENTO DI INDIRIZZI DUPLICATI quando all'istanza IP viene assegnato un collegamento locale o un indirizzo di interfaccia IP tramite nxd_ipv6_initiate_dad_process.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-ipv6-interface-address-get"></a>Ottenere l'indirizzo dell'interfaccia IPv6 Duo 

#### <a name="nxd_ipv6_interface_address_get"></a>nxd_ipv6_interface_address_get

**Icona** ![ Icona di ottenere l'indirizzo dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image67.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP e del prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'interfaccia dell'istanza IP tramite nxd_ipv6_interface_address_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo IPv6 da restituire
- Campo informazioni 4: indice dell'interfaccia nella tabella dell'interfaccia dell'istanza IP

### <a name="duo-ipv6-interface-address-set"></a>Set di indirizzi dell'interfaccia IPv6 Duo 

### <a name="nxd_ipv6_interface_address_set"></a>nxd_ipv6_interface_address_set

**Icona** ![ Icona degli indirizzi di interfaccia di Duo I P v 6 e](./media/user-guide/netx-events/image68.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP e del prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'interfaccia dell'istanza IP. Non consentito nell'indice zero (indirizzo locale di collegamento) tramite nxd_ipv6_interface_address_set.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo IPv6 da restituire
- Campo informazioni 3: Lunghezza del prefisso
- Campo informazioni 4: indice dell'interfaccia nella tabella dell'interfaccia dell'istanza IP

### <a name="duo-ipv6-link-local-address-get"></a>Duo IPv6 Link Local Address Get 

#### <a name="nxd_ipv6_linklocal_address_get"></a>nxd_ipv6_linklocal_address_get

**Icona** ![ Icona di ottenere l'indirizzo locale del collegamento Duo I P v 6](./media/user-guide/netx-events/image69.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo locale del collegamento dell'istanza IP specificata tramite nxd_ipv6_linklocal_address_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo locale del collegamento IP v6
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-ipv6-link-local-address-set"></a>Set di indirizzi locali del collegamento IPv6 Duo 

#### <a name="nxd_ipv6_linklocal_address_set"></a>nxd_ipv6_linklocal_address_set

**Icona** ![ Icona del set di indirizzi locali del collegamento Duo I P v 6](./media/user-guide/netx-events/image70.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo locale del collegamento dell'istanza IP tramite nxd_ipv6_linklocal_address_set.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo locale del collegamento IPv6
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-ipv6-raw-packet-send"></a>Duo IPv6 Raw Packet Send 

#### <a name="nxd_ipv6_raw_packet_send"></a>nxd_ipv6_raw_packet_send

**Icona** ![ Icona di invio di pacchetti non elaborati Duo I P v 6](./media/user-guide/netx-events/image71.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto IP non elaborato tramite l'interfaccia IP primaria alla destinazione speficied tramite nxd_ip_raw_packet_send.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto da inviare
- Campo Informazioni 3: Indirizzo IP di destinazione
- Campo informazioni 4: Non usato

### <a name="duo-tcp-socket-peer-info-get"></a>Ottenere le informazioni sul peer del socket TCP Duo 

#### <a name="nxd_tcp_socket_peer_info_get"></a>nxd_tcp_socket_peer_info_get

**Icona** ![ Icona di visualizzazione delle informazioni peer socket T C Duo](./media/user-guide/netx-events/image72.png)

**Descrizione**

Questo evento estrae i dati del mittente da un pacchetto TCP ricevuto nel socket specificato. Restituisce l'indirizzo IP e la porta del mittente.

**Campi di informazioni**

- Campo informazioni 1: Puntatore socket
- Campo Info 2: Indirizzo IP peer
- Campo informazioni 3: Porta peer
- Campo informazioni 4: lease significativo a 32 bit dell'indirizzo IP

### <a name="duo-tcp-socket-set-interface"></a>Interfaccia del set di socket TCP Duo 

#### <a name="nxd_tcp_socket_set_interface"></a>nxd_tcp_socket_set_interface

**Icona** ![ Icona dell'interfaccia del set di socket Duo T C](./media/user-guide/netx-events/image73.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'interfaccia socket in uscita dopo che un client si connette a un server TCP nell'indirizzo IP del server specificato tramite nxd_tcp_client_socket_connect.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore al socket TCP
- Campo informazioni 2: ID interfaccia
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-udp-socket-send"></a>Duo UDP Socket Send 

#### <a name="nxd_udp_socket_send"></a>nxd_udp_socket_send

**Icona** ![ Icona di invio socket di Duo U D P](./media/user-guide/netx-events/image74.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto UDP tramite il socket specificato con l'indirizzo IP di input e la porta tramite nxd_udp_socket_send.

**Campi di informazioni** 

- Campo informazioni 1: Socket UDP puntatore
- Campo informazioni 2: Puntatore al pacchetto UDP
- Campo informazioni 3: Lunghezza pacchetto
- Campo informazioni 4: Non usato


### <a name="duo-udp-socket-set-interface"></a>Interfaccia del set di socket UDP Duo 

#### <a name="nxd_udp_socket_set_interface"></a>nxd_udp_socket_set_interface

**Icona** ![ Icona dell'interfaccia del set di socket di Duo U D P](./media/user-guide/netx-events/image75.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'interfaccia in uscita del socket UDP specificata sull'interfaccia corrispondente all'ID dell'interfaccia di input tramite nxd_udp_socket_set_interface.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore al socket UDP
- Campo informazioni 2: ID interfaccia
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="duo-udp-source-extract"></a>Estrazione origine UDP Duo 

#### <a name="nxd_udp_socket_extract"></a>nxd_udp_socket_extract

**Icona** ![ Icona di estrazione dell'origine di Duo U D P](./media/user-guide/netx-events/image76.png)

**Descrizione**

Questo evento rappresenta l'estrazione dell'indirizzo IP e della porta di origine di un pacchetto ricevuto (IPv4 o IPv6). Se IPv6, la quarta parola (meno significativa) dell'indirizzo IP viene restituita tramite nxd_udp_source_extract.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pacchetto
- Campo informazioni 2: versione IP
- Campo Informazioni 3: Indirizzo IP di origine (IPv4 o IPv6)
- Campo informazioni 4: Porta di origine

### <a name="icmp-enable"></a>Abilitazione ICMP 

#### <a name="nx_icmp_enable"></a>nx_icmp_enable

**Icona** ![ Icona di abilitazione I C M P](./media/user-guide/netx-events/image77.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di ICMP tramite nx_icmp_enable.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP l;
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="icmp-information-get"></a>Ottenere informazioni ICMP 

#### <a name="nx_icmp_info_get"></a>nx_icmp_info_get

**Icona** ![ Icona I C M P information get](./media/user-guide/netx-events/image78.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_icmp_info_get.

**Campi di informazioni**
- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Ping inviati
- Campo informazioni 3: Risposte ping
- Campo informazioni 4: Ping ricevuti

### <a name="icmp-ping"></a>Ping ICMP 

#### <a name="nx_icmp_ping"></a>nx_icmp_ping

**Icona** ![ Icona ping I C M P](./media/user-guide/netx-events/image79.png)

**Descrizione**

Questo evento rappresenta il ping di un indirizzo IP di destinazione tramite nx_icmp_ping.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: Puntatore ai dati
- Campo informazioni 4: Dimensioni dei dati

### <a name="igmp-enable"></a>Abilitazione IGMP 

#### <a name="nx_icmp_enable"></a>nx_icmp_enable

**Icona** ![ Icona di abilitazione I G M P](./media/user-guide/netx-events/image80.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di IGMP tramite nx_igmp_enable.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="igmp-information-get"></a>Ottenere informazioni IGMP 

#### <a name="nx_icmp_info_get"></a>nx_icmp_info_get

**Icona** ![ Icona I G M P information get](./media/user-guide/netx-events/image81.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_igmp_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Report inviati
- Campo informazioni 3: Query ricevute
- Campo informazioni 4: Gruppi aggiunti

### <a name="igmp-loopback-disable"></a>Disabilitazione loopback IGMP 

#### <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable

**Icona** ![ Icona di disabilitazione del loopback I G M P](./media/user-guide/netx-events/image82.png)

**Descrizione**

Questo evento rappresenta la disabilitazione del loopback IGMP tramite nx_igmp_loopback_disable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="igmp-loopback-enable"></a>Abilitazione loopback IGMP 

#### <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable

**Icona** ![ Icona di abilitazione loopback I G M P](./media/user-guide/netx-events/image83.png)

**Descrizione**

Questo evento rappresenta l'abilitazione del loopback IGMP tramite nx_igmp_loopback_enable.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="igmp-multicast-join"></a>Aggiunta multicast IGMP 

#### <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join

**Icona** ![ Icona di aggiunta multicast I G M P](./media/user-guide/netx-events/image84.png)

**Descrizione**

Questo evento rappresenta l'aggiunta a un gruppo multicast tramite nx_igmp_multicast_join.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP del gruppo
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="igmp-multicast-leave"></a>IGMP Multicast Leave 

#### <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave

**Icona** ![ Icona di lasciare multicast I G M P](./media/user-guide/netx-events/image85.png)

**Descrizione**

Questo evento rappresenta l'uscita di un gruppo multicast tramite nx_igmp_multicast_leave.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP del gruppo
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-address-change-notify"></a>Notifica della modifica dell'indirizzo IP 

#### <a name="nx_ip_address_change_notify"></a>nx_ip_address_change_notify

**Icona** ![ Icona di notifica della modifica dell'indirizzo I P](./media/user-guide/netx-events/image86.png)

**Descrizione**

Questo evento rappresenta la registrazione per la notifica delle modifiche IP tramite nx_ip_address_change_notify.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore a funzione di callback
- Campo informazioni 3: Puntatore alle informazioni aggiuntive
- Campo informazioni 4: Non usato

### <a name="ip-address-get"></a>Ottenere l'indirizzo IP 

#### <a name="nx_ip_address_get"></a>nx_ip_address_get

**Icona** ![ Icona I P address get](./media/user-guide/netx-events/image87.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP tramite nx_ip_address_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: Network mask
- Campo informazioni 4: Non usato

### <a name="ip-address-set"></a>Set di indirizzi IP 

#### <a name="nx_ip_address_set"></a>nx_ip_address_set

**Icona** ![ Icona del set di indirizzi I P](./media/user-guide/netx-events/image88.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP tramite nx_ip_address_set.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: Network mask
- Campo informazioni 4: Non usato

### <a name="ip-create"></a>Creazione ip 

#### <a name="nx_ip_create"></a>nx_ip_create

**Icona** ![ Icona I P create](./media/user-guide/netx-events/image89.png)

**Descrizione**

Questo evento rappresenta la creazione di un'istanza IP tramite nx_ip_create.

**Campi di informazioni** 
- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: Network mask
- Campo informazioni 4: Puntatore del pool di pacchetti predefinito

### <a name="ip-delete"></a>Eliminazione IP 

#### <a name="nx_ip_delete"></a>nx_ip_delete

**Icona** ![ Icona I P delete](./media/user-guide/netx-events/image90.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un'istanza IP tramite nx_ip_delete.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-driver-direct-command"></a>Comando diretto del driver IP 

#### <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command

**Icona** ![ Icona del comando diretto del driver I P](./media/user-guide/netx-events/image91.png)

**Descrizione**

Questo evento rappresenta un comando diretto del driver di I/O tramite nx_ip_driver_direct_command.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: comando Driver
- Campo informazioni 3: valore restituito
- Campo informazioni 4: Non usato

### <a name="ip-forwarding-disable"></a>Disabilitazione inoltro IP 

#### <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable

**Icona** ![ Icona di disabilitazione dell'inoltro I P](./media/user-guide/netx-events/image92.png)

**Descrizione**

Questo evento rappresenta la disabilitazione dell'inoltro IP tramite nx_ip_forwarding_disable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-forwarding-enable"></a>Abilitazione dell'inoltro IP 

#### <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable

**Icona** ![ Icona di abilitazione dell'inoltro P](./media/user-guide/netx-events/image93.png)

**Descrizione**

Questo evento rappresenta l'abilitazione dell'inoltro IP tramite nx_ip_forwarding_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-fragment-disable"></a>Disabilitazione frammento IP 

#### <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable

**Icona** ![ Icona di disabilitazione del frammento I P](./media/user-guide/netx-events/image94.png)

**Descrizione**

Questo evento rappresenta la disabilitazione della frammentazione IP tramite nx_ip_fragment_disable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-fragment-enable"></a>Abilitazione frammento IP 

#### <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable

**Icona** ![ Icona di abilitazione frammento I P](./media/user-guide/netx-events/image95.png)

**Descrizione**

Questo evento rappresenta l'abilitazione della frammentazione IP tramite nx_ip_fragment_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-gateway-address-set"></a>Set di indirizzi del gateway IP 

#### <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set

**Icona** ![ Icona del set di indirizzi del gateway I P](./media/user-guide/netx-events/image96.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP del gateway tramite nx_ip_gateway_address_set.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP del gateway
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-information-get"></a>Ottenere informazioni IP 

#### <a name="nx_ip_info_get"></a>nx_ip_info_get

**Icona** ![ Icona I P information get](./media/user-guide/netx-events/image97.png)

**Descrizione** Questo evento rappresenta il recupero di informazioni IP tramite nx_ip_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: byte IP inviati
- Campo informazioni 3: Byte IP ricevuti
- Campo informazioni 4: Pacchetti IP eliminati

### <a name="ip-interface-attach"></a>Collegamento all'interfaccia IP 

#### <a name="nx_interface_attach"></a>nx_interface_attach

**Icona** ![ I P iterface attach icon (I P iterface attach icon)](./media/user-guide/netx-events/image98.png)

**Descrizione**

Questo evento rappresenta un'interfaccia di rete secondaria collegata all'istanza IP tramite nx_ip_interface_attach.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP dell'interfaccia
- Campo informazioni 3: Indice nella tabella dell'interfaccia IP
- Campo informazioni 4: Non usato

### <a name="ip-interface-info-get"></a>Ottenere informazioni sull'interfaccia IP 

#### <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get

**Icona** ![ Icona Ottieni informazioni sull'interfaccia IP](./media/user-guide/netx-events/image99.png)

**Descrizione**

Questo evento rappresenta le informazioni recuperate dall'interfaccia di rete specificata tramite nx_ip_interface_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo Informazioni 2: Indirizzo IP dell'interfaccia
- Campo informazioni 3: Indirizzo MAC dell'interfaccia msb
- Campo informazioni 4: Indirizzo MAC dell'interfaccia lsb

### <a name="ip-raw-packet-disable"></a>Disabilitazione pacchetto ip non elaborato 

#### <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable

**Icona** ![ Icona I P raw packet disable](./media/user-guide/netx-events/image100.png)

**Descrizione**

Questo evento rappresenta la disabilitazione della comunicazione di pacchetti IP non elaborati tramite nx_ip_raw_packet_disable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-raw-packet-enable"></a>Abilitazione pacchetti ip non elaborati 

#### <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable

**Icona** ![ Icona I P raw packet enable](./media/user-guide/netx-events/image101.png)

**Descrizione**

Questo evento rappresenta l'abilitazione della comunicazione di pacchetti IP non elaborati tramite nx_ip_raw_packet_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="ip-raw-packet-receive"></a>Ricezione di pacchetti non elaborati IP 

#### <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive

**Icona** ![ Icona I P raw packet receive](./media/user-guide/netx-events/image102.png)

**Descrizione**

Questo evento rappresenta la ricezione di un pacchetto IP non elaborato tramite nx_ip_raw_packet_receive.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: opzione di attesa
- Campo informazioni 4: Non usato

### <a name="ip-raw-packet-send"></a>Invio di pacchetti ip non elaborati 

#### <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send

**Icona** ![ Icona I P raw packet send](./media/user-guide/netx-events/image103.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto IP non elaborato tramite nx_ip_raw_packet_send.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al pacchetto
- Campo Informazioni 3: Indirizzo IP di destinazione
- Campo informazioni 4: Tipo di servizio

### <a name="ip-static-route-add"></a>Aggiunta route statica IP 

#### <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add

**Icona** ![ Icona I P static route add](./media/user-guide/netx-events/image104.png)

**Descrizione**

Questo evento rappresenta una route statica aggiunta alla tabella di routing dell'istanza IP tramite nx_ip_static_route_add.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo di rete
- Campo informazioni 3: Network mask
- Campo informazioni 4: Hop successivo

### <a name="ip-static-route-delete"></a>Eliminazione route statica IP 

#### <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete

**Icona** ![ Icona I P static rute delete](./media/user-guide/netx-events/image105.png)

**Descrizione**

Questo evento rappresenta una route statica rimossa dalla tabella di routing dell'istanza IP tramite nx_ip_static_route_delete.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Indirizzo di rete
- Campo informazioni 3: Network mask
- Campo informazioni 4: Non usato

### <a name="ip-status-check"></a>Controllo dello stato IP 

#### <a name="nx_ip_status_check"></a>nx_ip_status_check

**Icona** ![ Icona di controllo dello stato I P](./media/user-guide/netx-events/image106.png)

**Descrizione**

Questo evento rappresenta il controllo di uno stato IP tramite nx_ip_status_check.

Campi di informazioni 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Stato richiesto
- Campo informazioni 3: Stato effettivo
- Campo informazioni 4: Opzione di attesa

### <a name="ipsec-enable"></a>IPSEC Enable 

#### <a name="nx_ipsec_enable"></a>nx_ipsec_enable

**Icona** ![ Icona di abilitazione di I PS E C](./media/user-guide/netx-events/image107.png)

**Descrizione**

Questo evento rappresenta l'abilitazione dei servizi IPSec nell'istanza IP fornita tramite nx_ipsec_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="packet-allocate"></a>Allocazione pacchetti 

#### <a name="nx_packet_allocate"></a>nx_packet_allocate

**Icona** ![ Icona di allocazione pacchetti](./media/user-guide/netx-events/image108.png)

**Descrizione**

Questo evento rappresenta l'allocazione di un pacchetto tramite nx_packet_allocate.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al pool di pacchetti
- Campo informazioni 2: Puntatore al pacchetto allocato
- Campo informazioni 3: Tipo di pacchetto
- Campo informazioni 4: Pacchetti disponibili

### <a name="packet-copy"></a>Copia di pacchetti 

#### <a name="nx_packet_copy"></a>nx_packet_copy

**Icona** ![ Icona cpy del pacchetto](./media/user-guide/netx-events/image109.png)

**Descrizione**

Questo evento rappresenta la copia di un pacchetto tramite nx_packet_copy.

**Campi di informazioni**

- Campo informazioni 2: Nuovo puntatore al pacchetto
- Campo informazioni 3: Puntatore al pool di pacchetti
- Campo informazioni 4: Opzione di attesa

### <a name="packet-data-append"></a>Packet Data Append 

#### <a name="nx_packet_data_append"></a>nx_packet_data_append

**Icona** ![ Icona di accodamento dei dati dei pacchetti](./media/user-guide/netx-events/image110.png)

**Descrizione**

Questo evento rappresenta l'aggiunta di dati a un pacchetto tramite nx_packet_data_append.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pacchetto
- Campo informazioni 2: Puntatore ai dati
- Campo informazioni 3: Dimensioni dei dati
- Campo informazioni 4: Puntatore al pool di pacchetti

### <a name="packet-data-extract-offset"></a>Offset estrazione dati pacchetto 

#### <a name="nx_udp_source_extract_offset"></a>nx_udp_source_extract_offset

**Icona** ![ Icona dell'offset per l'estrazione dei dati dei pacchetti](./media/user-guide/netx-events/image111.png)

**Descrizione**

Questo evento rappresenta i dati del pacchetto estratti in un buffer fornito da un pacchetto tramite nx_udp_source_extract_offset.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al pacchetto
- Campo informazioni 2: dimensioni del buffer specificato
- Campo informazioni 3: numero di byte copiati
- Campo informazioni 4: Non usato

### <a name="packet-data-retrieve"></a>Recupero dei dati dei pacchetti 

#### <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve

**Icona** ![ Icona di recupero dei dati dei pacchetti](./media/user-guide/netx-events/image112.png)

**Descrizione**

Questo evento rappresenta il recupero di dati da un pacchetto tramite nx_packet_data_retrieve.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al pacchetto
- Campo informazioni 2: puntatore all'inizio del buffer
- Campo informazioni 3: Byte copiati
- Campo informazioni 4: Non usato

### <a name="packet-length-get"></a>Packet Length Get 

#### <a name="nx_packet_length_get"></a>nx_packet_length_get

**Icona** ![ Icona get della lunghezza del pacchetto](./media/user-guide/netx-events/image113.png)

**Descrizione**

Questo evento rappresenta il recupero della lunghezza di un pacchetto tramite nx_packet_length_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pacchetto
- Campo informazioni 2: Lunghezza pacchetto
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="packet-pool-create"></a>Creazione del pool di pacchetti 

#### <a name="nx_packet_pool_create"></a>nx_packet_pool_create

**Icona** ![ Icona di creazione del pool di pacchetti](./media/user-guide/netx-events/image114.png)

**Descrizione**

Questo evento rappresenta la creazione di un pool di pacchetti tramite nx_packet_pool_create.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore al pool di pacchetti
- Campo informazioni 2: Dimensioni del payload del pacchetto
- Campo informazioni 3: Puntatore all'area di memoria del pool
- Campo informazioni 4: Dimensioni dell'area di memoria del pool

### <a name="packet-pool-delete"></a>Eliminazione del pool di pacchetti 

#### <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete

**Icona** ![ Icona di eliminazione del pool di pacchetti](./media/user-guide/netx-events/image115.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un pool di pacchetti tramite nx_packet_pool_delete.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore al pool di pacchetti
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

#### <a name="packet-pool-information-get"></a>Ottenere informazioni sul pool di pacchetti 

#### <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get

**Icona** ![ Icona di acquisizione delle informazioni sul pool di pacchetti](./media/user-guide/netx-events/image116.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sul pool di pacchetti tramite nx_packet_pool_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al pool di pacchetti
- Campo informazioni 2: Totale pacchetti
- Campo informazioni 3: Pacchetti disponibili
- Campo informazioni 4: Richieste vuote

### <a name="packet-release"></a>Rilascio di pacchetti 

#### <a name="nx_packet_data_release"></a>nx_packet_data_release

**Icona** ![ Icona di rilascio del pacchetto](./media/user-guide/netx-events/image117.png)

**Descrizione**

Questo evento rappresenta il rilascio di un pacchetto tramite nx_packet_release.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pacchetto
- Campo informazioni 2: Stato del pacchetto
- Campo informazioni 3: Pacchetti disponibili
- Campo informazioni 4: Non usato

### <a name="packet-transmit-release"></a>Rilascio della trasmissione di pacchetti 

#### <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release

**Icona** ![ Icona di rilascio per la trasmissione di pacchetti](./media/user-guide/netx-events/image118.png)

**Descrizione**

Questo evento rappresenta il rilascio di un pacchetto di trasmissione tramite nx_packet_transmit_release.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pacchetto
- Campo informazioni 2: Stato del pacchetto
- Campo informazioni 3: Pacchetti disponibili
- Campo informazioni 4: Non usato

### <a name="rarp-disable"></a>RARP Disable 

#### <a name="nx_rarp_disable"></a>nx_rarp_disable

**Icona** ![ Icona di disabilitazione R A R P](./media/user-guide/netx-events/image119.png)

**Descrizione**

Questo evento rappresenta la disabilitazione di RARP tramite nx_rarp_disable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="rarp-enable"></a>RARP Enable 

#### <a name="nx_rarp_enable"></a>nx_rarp_enable

**Icona** ![ Icona di abilitazione R A R P](./media/user-guide/netx-events/image120.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di RARP tramite nx_rarp_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="rarp-information-get"></a>RARP Information Get 

#### <a name="nx_rarp_info_get"></a>nx_rarp_info_get

**Icona** ![ Icona R A R P information get (Ottieni informazioni R A R)](./media/user-guide/netx-events/image121.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni RARP tramite nx_rarp_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Richieste inviate
- Campo informazioni 3: Risposte ricevute
- Campo informazioni 4: Risposte non valide

### <a name="system-initialize"></a>Inizializzazione del sistema 

#### <a name="nx_system_initialize"></a>nx_system_initialize

**Icona** ![ Icona di inizializzazione del sistema](./media/user-guide/netx-events/image122.png)

**Descrizione**

Questo evento rappresenta l'inizializzazione di NetX tramite nx_system_initialize.

**Campi di informazioni**

- Campo informazioni 1: Non usato
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="tcp-client-socket-bind"></a>Associazione socket client TCP 

#### <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind

**Icona** ![ Icona di binding del socket client T P](./media/user-guide/netx-events/image123.png)

**Descrizione**

Questo evento rappresenta l'associazione di un socket client a una porta tramite nx_tcp_client_socket_bind.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Porta richiesta
- Campo informazioni 4: Opzione di attesa

### <a name="tcp-client-socket-connect"></a>Tcp Client Socket Connessione 

#### <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect

**Icona** ![ Icona di connessione del socket client T C P](./media/user-guide/netx-events/image124.png)

**Descrizione**

Questo evento rappresenta la creazione di una connessione socket client tramite nx_tcp_client_socket_connect.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Indirizzo IP del server
- Campo informazioni 4: Porta server richiesta

### <a name="tcp-client-socket-port-get"></a>TCP Client Socket Port Get 

#### <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get

**Icona** ![ T C P client socket port get icon](./media/user-guide/netx-events/image125.png)

**Descrizione**

Questo evento rappresenta il recupero del numero di porta del socket client tramite nx_tcp_client_socket_port_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Numero di porta
- Campo informazioni 4: Non usato

### <a name="tcp-client-socket-unbind"></a>TCP Client Socket Unbind 

#### <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind

**Icona** ![ Icona di annullamento dell'associazione del socket client C C](./media/user-guide/netx-events/image126.png)

**Descrizione**

Questo evento rappresenta l'annullamento dell'associazione della porta associata al socket tramite nx_tcp_client_socket_unbind.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="tcp-enable"></a>TCP Enable 

#### <a name="nx_tcp_enable"></a>nx_tcp_enable

**Icona** ![ Icona di abilitazione di T C P](./media/user-guide/netx-events/image127.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di TCP nx_tcp_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

###  <a name="tcp-free-port-find-tcp-free-port-find"></a>TCP Free Port Find TCP Free Port Find 

#### <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find

**Icona** ![ T CP free port find icon](./media/user-guide/netx-events/image128.png)

**Descrizione**

Questo evento rappresenta la ricerca di una porta TCP libera tramite nx_tcp_free_port_find.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Numero di porta di ricerca iniziale
- Campo informazioni 3: Numero di porta gratuito
- Campo informazioni 4: Non usato

###  <a name="tcp-infomation-get"></a>TCP Infomation Get 

#### <a name="nx_tcp_info_get"></a>nx_tcp_info_get

**Icona** ![ Icona per il get delle informazioni di T C P](./media/user-guide/netx-events/image129.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni TCP per l'istanza IP specificata tramite nx_tcp_info_get.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: numero di byte inviati
- Campo informazioni 3: Numero di byte ricevuti
- Campo informazioni 4: Numero di pacchetti non validi

###  <a name="tcp-server-socket-accept"></a>Accettazione socket server TCP 

#### <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept

**Icona** ![ Icona di accettazione del socket del server T C P](./media/user-guide/netx-events/image130.png)

**Descrizione**

Questo evento rappresenta la configurazione del socket del server dopo la ricezione di una richiesta di connessione attiva tramite nx_tcp_server_socket_accept.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Opzione di attesa
- Campo informazioni 4: Stato del socket

###  <a name="tcp-server-socket-listen"></a>Attesa socket server TCP 

#### <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen

**Icona** ![ Icona di lsten del socket del server T C P](./media/user-guide/netx-events/image131.png)

**Descrizione**

Questo evento rappresenta la registrazione di una richiesta di ascolto e di un socket del server per la porta TCP specificata tramite nx_tcp_server_socket_listen.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Numero di porta TCP
- Campo informazioni 3: Puntatore al socket
- Campo informazioni 4: numero massimo di connessioni che possono essere accodati

###  <a name="tcp-server-socket-relisten"></a>TCP Server Socket Relisten 

#### <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten

**Icona** ![ Icona di relisten del socket del server T C P](./media/user-guide/netx-events/image132.png)

**Descrizione**

Questo evento rappresenta la registrazione di un altro socket del server per una richiesta di ascolto esistente sulla porta TCP specificata tramite nx_tcp_server_socket_relisten.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Numero di porta TCP
- Campo informazioni 3: Puntatore al socket
- Campo informazioni 4: Stato del socket

###  <a name="tcp-server-socket-unaccept"></a>TCP Server Socket Unaccept 

#### <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept

**Icona** ![ Icona di annullamento dell'accezione del socket del server T C P](./media/user-guide/netx-events/image133.png)

**Descrizione**

Questo evento rappresenta la rimozione del socket del server dall'associazione con la porta che riceve una connessione passiva precedente tramite nx_tcp_server_socket_unaccept.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Stato del socket
- Campo informazioni 4: Non usato

###  <a name="tcp-server-socket-unlisten-tcp-server-socket-unlisten"></a>TCP Server Socket Unlisten TCP Server Socket Unlisten 

#### <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten

**Icona** ![ Icona di annullamento dell'elenco del socket del server C P](./media/user-guide/netx-events/image134.png)

**Descrizione**

Questo evento rappresenta la rimozione di una richiesta di ascolto precedente per la porta TCP specificata tramite nx_tcp_server_socket_unlisten.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Numero di porta TCP
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="tcp-socket-bytes-available"></a>Byte socket TCP disponibili 

#### <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available

**Icona** ![ Icona byte socket T C P disponibili](./media/user-guide/netx-events/image135.png)

**Descrizione**

Questo evento rappresenta il numero di byte attualmente disponibili nel socket di ricezione TCP specificato tramite nx_tcp_socket_bytes_available.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket TCP
- Campo informazioni 3: Byte ricevuti sul socket
- Campo informazioni 4: Non usato

### <a name="tcp-socket-create"></a>Creazione di socket TCP 

#### <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create

**Icona** ![ Icona di creazione del socket T C P](./media/user-guide/netx-events/image136.png)

**Descrizione**

Questo evento rappresenta la creazione di un socket TCP tramite nx_tcp_socket_create.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Tipo di servizio
- Campo informazioni 4: Dimensioni finestra di ricezione

### <a name="tcp-socket-delete"></a>Eliminazione socket TCP 

#### <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete

**Icona** ![ Icona T C P socket delete](./media/user-guide/netx-events/image137.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un socket tramite nx_tcp_socket_delete.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Stato del socket
- Campo informazioni 4: Non usato

### <a name="tcp-socket-disconnect"></a>Disconnessione socket TCP 

#### <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect

**Icona** ![ Icona di disconnessione del socket T C P](./media/user-guide/netx-events/image138.png)

**Descrizione**

Questo evento rappresenta la disconnessione di un socket tramite nx_tcp_socket_disconnect.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Opzione di attesa
- Campo informazioni 4: Stato del socket

### <a name="tcp-socket-information-get"></a>Ottenere informazioni sul socket TCP 

#### <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get

**Icona** ![ Icona get delle informazioni sul socket T C P](./media/user-guide/netx-events/image139.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un socket tramite nx_tcp_socket_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Byte inviati tramite questo socket
- Campo informazioni 4: Byte ricevuti tramite questo socket

### <a name="tcp-socket-mss-get"></a>TCP Socket MSS Get 

#### <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get

**Icona** ![ T C P socket M S S get icon](./media/user-guide/netx-events/image140.png)

**Descrizione**

Questo evento rappresenta il recupero di MSS del socket tramite nx_tcp_socket_mss_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Dimensioni massime segmento (MSS)
- Campo informazioni 4: Stato del socket

### <a name="tcp-socket-mss-peer-get"></a>TCP Socket MSS Peer Get 

#### <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get

**Icona** ![ T C P socket M S peer get icon](./media/user-guide/netx-events/image141.png)

**Descrizione**

Questo evento rappresenta il recupero del valore MSS del peer del socket tramite nx_tcp_socket_mss_peer_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: MSS del peer
- Campo informazioni 4: Stato del socket

### <a name="tcp-socket-mss-set"></a>TCP Socket MSS Set 

#### <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set

**Icona** ![ T C P socket M S set icon](./media/user-guide/netx-events/image142.png)

**Descrizione**

Questo evento rappresenta l'impostazione di MSS di un socket tramite nx_tcp_socket_mss_set.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: MSS
- Campo informazioni 4: Stato del socket

### <a name="tcp-socket-peer-info-get"></a>TCP Socket Peer Info Get 

#### <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get

**Icona** ![ T C P socket peer info get icon](./media/user-guide/netx-events/image143.png)

**Descrizione**

Questo evento rappresenta le informazioni recuperate dal socket TCP relative all'indirizzo IP e alla porta del peer (ad esempio, >host di connessione) tramite nx_tcp_socket_peer_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al socket TCP
- Campo informazioni 2: Indirizzo IP peer
- Campo informazioni 3: Numero di porta peer
- Campo informazioni 4: Non usato

### <a name="tcp-socket-receive"></a>Ricezione socket TCP 

#### <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive

**Icona** ![ Icona di ricezione del socket T C P](./media/user-guide/netx-events/image144.png)

**Descrizione**

Questo evento rappresenta la ricezione di dati da un socket tramite nx_tcp_socket_receive.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al socket
- Campo informazioni 2: puntatore al pacchetto ricevuto
- Campo informazioni 3: Lunghezza pacchetto ricevuta
- Campo informazioni 4: Numero di sequenza di ricezione

### <a name="tcp-socket-receive-notify"></a>Notifica ricezione socket TCP 

#### <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify

**Icona** ![ Icona di notifica ricezione socket T C](./media/user-guide/netx-events/image145.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback di notifica di ricezione per un socket tramite nx_tcp_socket_receive_notify.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Info Field 3: Pointer to receive notify callback Info Field 4: Not used (Campo informazioni callback notifica 4: Non usato)

### <a name="tcp-socket-send"></a>TCP Socket Send 

#### <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send

**Icona** ![ Icona di invio del socket T C P](./media/user-guide/netx-events/image146.png)

**Descrizione**

Questo evento rappresenta l'invio di dati su un socket tramite nx_tcp_socket_send.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al socket
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Lunghezza del pacchetto
- Campo informazioni 4: Trasmettere il numero di sequenza

### <a name="tcp-socket-state-wait"></a>Attesa stato socket TCP 

#### <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait

**Icona** ![ Icona di attesa dello stato del socket T C](./media/user-guide/netx-events/image147.png)

**Descrizione**

Questo evento rappresenta l'attesa che un socket entri in uno stato specifico tramite nx_tcp_socket_state_wait.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Stato del socket desiderato
- Campo informazioni 4: Stato precedente del socket

### <a name="tcp-socket-transmit-configure"></a>TCP Socket Transmit Configure 

#### <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure

**Icona** ![ Icona di configurazione T C P socket transmit configure](./media/user-guide/netx-events/image148.png)

**Descrizione**

Questo evento rappresenta la configurazione delle opzioni di trasmissione per un socket tramite nx_tcp_socket_transmit_configure.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Trasmettere la profondità della coda
- Campo informazioni 4: valore di timeout

### <a name="tcp-socket-window-update-notify-set"></a>TCP Socket Window Update Notify Set 

#### <a name="nx_tcp_window_update_notify_set"></a>nx_tcp_window_update_notify_set

**Icona** ![ Icona T C P socket window update notify set](./media/user-guide/netx-events/image149.png)

**Descrizione**

Questo evento rappresenta un socket TCP che riceve la notifica di un aumento nella finestra di ricezione dell'host remoto tramite nx_tcp_window_update_notify_set.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore al socket TCP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="udp-enable"></a>Abilitazione UDP 

#### <a name="nx_udp_enable"></a>nx_udp_enable

**Icona** ![ Icona di abilitazione U D P](./media/user-guide/netx-events/image150.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di UDP tramite nx_udp_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="udp-free-port-find"></a>Ricerca di porte gratuite UDP 

#### <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find

**Icona** ![ Icona U D P free port find](./media/user-guide/netx-events/image151.png)

**Descrizione**

Questo evento rappresenta la ricerca di una porta UDP gratuita tramite nx_udp_free_port_find.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Avvio della porta da cui eseguire la ricerca
- Campo informazioni 3: Porta gratuita
- Campo informazioni 4: Non usato

### <a name="udp-information-get"></a>Ottenere informazioni UDP 

#### <a name="nx_udp_info_get"></a>nx_udp_info_get

**Icona** ![ Icona U D P information get](./media/user-guide/netx-events/image152.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_udp_info_get.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: byte UDP inviati
- Campo informazioni 3: byte UDP ricevuti
- Campo informazioni 4: Pacchetti non validi

### <a name="udp-socket-bind"></a>Binding socket UDP 

#### <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind

**Icona** ![ Icona di associazione del socket U D P](./media/user-guide/netx-events/image153.png)

**Descrizione**

Questo evento rappresenta l'associazione di un socket UDP a una porta tramite nx_udp_socket_bind.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Numero di porta
- Campo informazioni 4: opzione di attesa

### <a name="udp-socket-bytes-available"></a>Byte socket UDP disponibili 

#### <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available

**Icona** ![ Icona byte socket U D P disponibili](./media/user-guide/netx-events/image154.png)

**Descrizione**

Questo evento rappresenta il numero corrente di byte ricevuti sul socket UDP tramite nx_udp_socket_bytes_available.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Byte ricevuti sul socket
- Campo informazioni 4: Non usato

### <a name="udp-socket-checksum-disable"></a>Disabilitazione checksum socket UDP 

#### <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable

**Icona** ![ Icona di disabilitazione del checksum del socket U D P](./media/user-guide/netx-events/image155.png)

**Descrizione**

Questo evento rappresenta la disabilitazione del checksum per i dati in un socket UDP tramite nx_udp_socket_checksum_disable.

**Campi di informazioni** 

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="udp-socket-checksum-enable"></a>Abilitare il checksum del socket UDP 

#### <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable

**Icona** ![ Icona di abilitazione del checksum del socket U D P](./media/user-guide/netx-events/image156.png)

**Descrizione**

Questo evento rappresenta l'abilitazione dell'elaborazione del checksum in un socket tramite nx_udp_socket_checksum_enable.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="udp-socket-create"></a>Creazione di socket UDP 

#### <a name="nx_udp_socket_create"></a>nx_udp_socket_create

**Icona** ![ Icona di creazione del socket U D P](./media/user-guide/netx-events/image157.png)

**Descrizione**

Questo evento rappresenta la creazione di un socket UDP tramite nx_udp_socket_create.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Tipo di servizio
- Campo informazioni 4: Coda di ricezione massima

### <a name="udp-socket-delete-event"></a>Evento di eliminazione socket UDP 

#### <a name="nx_udp_socket_delete-event"></a>nx_udp_socket_delete evento

**Icona** ![ Icona dell'evento U D P socket delete](./media/user-guide/netx-events/image158.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un socket UDP tramite nx_udp_socket_delete.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="udp-socket-information-get-event"></a>Evento Get delle informazioni sul socket UDP 

#### <a name="nx_udp_socket_info_get-event"></a>nx_udp_socket_info_get evento

**Icona** ![ Icona dell'evento UD P socket information get](./media/user-guide/netx-events/image159.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un socket UDP tramite nx_udp_socket_info_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Byte inviati tramite socket
- Campo informazioni 4: Byte ricevuti tramite socket

### <a name="udp-socket-interface-set"></a>Set di interfacce socket UDP 

#### <a name="nx_udp_socket_interface_set-event"></a>nx_udp_socket_interface_set evento

**Icona** ![ Icona del set di interfacce del socket U D P](./media/user-guide/netx-events/image160.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'interfaccia in uscita del socket UDP specificato con l'interfaccia specificata tramite nx_udp_socket_interface_set.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al socket UDP
- Campo informazioni 2: indice corrispondente all'interfaccia per il socket
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="udp-socket-port-get"></a>UDP Socket Port Get 

#### <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get

**Icona** ![ Icona get della porta del socket UD P](./media/user-guide/netx-events/image161.png)

**Descrizione**

Questo evento rappresenta il recupero della porta UDP a cui è associato il socket UDP specificato tramite nx_udp_socket_port_get.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket UDP
- Campo informazioni 3: Numero di porta
- Campo informazioni 4: Non usato

### <a name="udp-socket-receive"></a>Ricezione socket UDP 

#### <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive

**Icona** ![ Icona di ricezione del socket UD P](./media/user-guide/netx-events/image162.png)

**Descrizione**

Questo evento rappresenta la ricezione di dati sul socket UDP specificato tramite nx_udp_socket_receive.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket UDP
- Campo informazioni 3: Puntatore al pacchetto ricevuto
- Info Field 4: Received packet size (Campo informazioni 4: Dimensioni pacchetti ricevute)

### <a name="udp-socket-receive-notify"></a>Notifica ricezione socket UDP 

#### <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify

**Icona** ![ U D P socket receive notify icon s Description (Descrizione dell'icona di notifica del socket UD ](./media/user-guide/netx-events/image163.png) **P)**

Questo evento rappresenta la registrazione di un callback di notifica di ricezione tramite nx_udp_socket_receive_notify.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Puntatore a ricevere notifica funzione Info Campo 4: Non usato

### <a name="udp-socket-send"></a>Invio socket UDP 

#### <a name="nx_udp_socket_send"></a>nx_udp_socket_send

**Icona** ![ Icona di invio del socket U D P](./media/user-guide/netx-events/image164.png)

**Descrizione**

Questo evento rappresenta l'invio di dati tramite un socket UDP tramite nx_udp_socket_send.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al socket
- Campo informazioni 2: Puntatore al pacchetto
- Campo informazioni 3: Lunghezza pacchetto
- Campo Info 4: Indirizzo IP di destinazione

### <a name="udp-socket-unbind"></a>Annullamento dell'associazione del socket UDP 

#### <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind

**Icona** ![ Icona di annullamento dell'associazione del socket U D P](./media/user-guide/netx-events/image165.png)

**Descrizione**

Questo evento rappresenta l'annullamento del binding di una porta UDP a un socket tramite nx_udp_socket_unbind.

**Campi di informazioni**

- Campo informazioni 1: Puntatore all'istanza IP
- Campo informazioni 2: Puntatore al socket
- Campo informazioni 3: Numero di porta
- Campo informazioni 4: Non usato

### <a name="udp-source-extract"></a>Estrazione origine UDP 

#### <a name="nx_udp_socket_create"></a>nx_udp_socket_create

**Icona** ![ Icona di estrazione dell'origine UD P](./media/user-guide/netx-events/image166.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP e del numero di porta di un pacchetto UDP ricevuto tramite nx_udp_source_extract.

**Campi di informazioni**

- Campo informazioni 1: Puntatore al pacchetto
- Campo informazioni 2: indirizzo IP del mittente
- Campo informazioni 3: numero di porta del mittente
- Campo informazioni 4: Non usato