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
# <a name="chapter-8---azure-rtos-netx-trace-events"></a>Capitolo 8-eventi di traccia di Azure RTO NetX

Questo capitolo contiene una descrizione degli eventi NetX di Azure RTO. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

Di seguito è riportato un elenco di eventi NetX visualizzati da TraceX.

| Icona                                           | Significato                 |
| -------------------------------- | ------------------------------------- |
| ![Icona di ricezione di una richiesta R P interna](./media/user-guide/netx-events/image1.png)    | Ricezione richiesta ARP interna |
| ![Icona di invio di una richiesta R P interna](./media/user-guide/netx-events/image2.png)    | Invio richiesta ARP interno |
| ![Icona di ricezione di risposta R P interna](./media/user-guide/netx-events/image3.png)    | Ricezione risposta ARP interna |
| ![Icona di invio risposta R P interna](./media/user-guide/netx-events/image4.png)    | Invio risposta ARP interna |
| ![Icona di ricezione interno I C M P](./media/user-guide/netx-events/image5.png)    | Ricezione ICMP interna |
| ![Icona di invio C M P interna](./media/user-guide/netx-events/image6.png)    | Invio ICMP interno |
| ![Icona di ricezione NetX I G M interna](./media/user-guide/netx-events/image7.png)    | Ricezione IGMP NetX interna |
| ![Icona di ricezione I P interni](./media/user-guide/netx-events/image8.png)    | Ricezione IP interna |
| ![Icona di invio di I P interni](./media/user-guide/netx-events/image9.png)    | Invio IP interno |
| ![Icona di ricezione dati T C P interna](./media/user-guide/netx-events/image10.png)    | Ricezione di dati TCP interni |
| ![Icona di invio dati T C P interna](./media/user-guide/netx-events/image11.png)    | Trasmissione dati TCP interni |
| ![Icona di ricezione T C P interna](./media/user-guide/netx-events/image12.png)    | Ricezione dell'aletta TCP interna |
| ![Icona di invio T C P F I N](./media/user-guide/netx-events/image13.png)    | Trasmissione aletta TCP interna |
| ![Icona di ricezione T C P R S interna](./media/user-guide/netx-events/image14.png)    | Ricezione RST TCP interna |
| ![Icona di invio T C P R S interna](./media/user-guide/netx-events/image15.png)    | Trasmissione RST TCP interna |
| ![Icona di ricezione T C P S interna](./media/user-guide/netx-events/image16.png)    | Ricezione SYN TCP interna |
| ![Icona di invio T C P S interna](./media/user-guide/netx-events/image17.png)    | Trasmissione SYN TCP interna |
| ![Icona di ricezione U D P interna](./media/user-guide/netx-events/image18.png)    | Ricezione UDP interna |
| ![Icona di invio di U D P interna](./media/user-guide/netx-events/image19.png)    | Invio UDP interno |
| ![Icona di ricezione r P interna](./media/user-guide/netx-events/image20.png)    | Ricezione RARP interna |
| ![Icona interna R A R P Send](./media/user-guide/netx-events/image21.png)    | Invio RARP interno |
| ![Icona di ripetizione dei tentativi interna di T C](./media/user-guide/netx-events/image22.png)    | Tentativo TCP interno |
| ![Icona di modifica dello stato T C P interno](./media/user-guide/netx-events/image23.png)    | Modifica dello stato TCP interna |
| ![Icona di invio pacchetti driver I/O interno](./media/user-guide/netx-events/image24.png)    | Invio di pacchetti di driver I/O interni |
| ![icon](./media/user-guide/netx-events/image25.png)    | Inizializzazione driver I/O interno |
| ![Icona di inizializzazione del driver I/O interno](./media/user-guide/netx-events/image26.png)    | Abilitazione collegamento driver I/O interno |
| ![Icona di disabilitazione collegamento driver I/O interno](./media/user-guide/netx-events/image27.png)    | Disabilitazione collegamento driver I/O interno |
| ![Icona trasmissione pacchetti I/O interno](./media/user-guide/netx-events/image28.png)    | Trasmissione di pacchetti di driver I/O interni |
| ![Icona di trasmissione ARP driver I/O interno](./media/user-guide/netx-events/image29.png)    | Invio ARP driver I/O interno |
| ![Icona di invio risposta ARP driver I/O interno](./media/user-guide/netx-events/image30.png)    | Invio risposta ARP driver I/O interno |
| ![Icona di invio RARP driver I/O interno](./media/user-guide/netx-events/image31.png)    | Invio di un driver di I/O interno RARP |
| ![Icona di join multicast driver I/O interno](./media/user-guide/netx-events/image32.png)    | Join multicast driver I/O interno |
| ![Icona di uscita multicast driver I/O interno](./media/user-guide/netx-events/image33.png)    | Uscita multicast driver I/O interno |
| ![Icona di Ottieni stato driver I/O interno](./media/user-guide/netx-events/image34.png)    | Stato Get driver I/O interno |
| ![Icona di Ottieni velocità driver I/O interno](./media/user-guide/netx-events/image35.png)    | Velocità di ottenimento del driver I/O interno |
| ![Icona del tipo di driver di I/O interno Get duplex](./media/user-guide/netx-events/image36.png)    | Tipo duplex Get driver I/O interno |
| ![Icona per il conteggio degli errori di Get di driver I/O interno](./media/user-guide/netx-events/image37.png)    | Conteggio errori di Get driver I/O interno |
| ![Icona del conteggio RX del driver I/O interno](./media/user-guide/netx-events/image38.png)    | Conteggio RX del driver I/O interno |
| ![Icona per il conteggio di un driver di I/O interno Get TX](./media/user-guide/netx-events/image39.png)    | Conteggio TX del driver I/O interno |
| ![Icona per ottenere gli errori di allocazione del driver I/O interno](./media/user-guide/netx-events/image40.png)    | Errore di allocazione del driver I/O interno |
| ![Icona di annullamento inizializzazione del driver I/O interno](./media/user-guide/netx-events/image41.png)    | Annulla inizializzazione del driver di I/O interno |
| ![Icona di elaborazione posticipata del driver I/O interno](./media/user-guide/netx-events/image42.png)    | Elaborazione posticipata del driver di I/O interno |
| ![Icona delle voci dinamiche di R P Invalidate](./media/user-guide/netx-events/image43.png)    | **Voci dinamiche ARP Invalidate** (*nx_arp_dynamic_entries_invalidate*) |
| ![Icona del set di voci dinamiche di R P](./media/user-guide/netx-events/image44.png)    | **Set di voci dinamiche ARP** (*nx_arp_dynamic_entry_set*) |
| ![Icona di abilitazione di R P](./media/user-guide/netx-events/image45.png)    | **Abilitazione ARP** (*nx_arp_enable*) |
| ![Icona di invio gratuito A R P](./media/user-guide/netx-events/image46.png)    | **Trasmissione gratuita ARP** (*nx_arp_gratuitous_send*) |
| ![Icona di ricerca indirizzo hardware R P](./media/user-guide/netx-events/image47.png)    | **Ricerca indirizzi hardware ARP** (*nx_arp_hardware_address_find*) |
| ![Icona di Get di informazioni R P](./media/user-guide/netx-events/image48.png)    | **Informazioni sul protocollo ARP Get** (*nx_arp_info_get*) |
| ![Icona di ricerca di indirizzi IP R P](./media/user-guide/netx-events/image49.png)    | **Ricerca indirizzi IP ARP** (*nx_arp_ip_address_find*) |
| ![Icona di creazione di una voce statica R P](./media/user-guide/netx-events/image50.png)    | **Creazione voce statica ARP** (*nx_arp_static_entry_create*) |
| ![Icona Elimina voci statiche R P](./media/user-guide/netx-events/image51.png)    | **Elimina voci statiche ARP** (*nx_arp_static_entries_delete*) |
| ![Icona di eliminazione della voce statica di R P](./media/user-guide/netx-events/image52.png)    | **Eliminazione voce statica ARP** (*nx_arp_static_entry_delete*) |
| ![Icona di eliminazione voce della cache Duo](./media/user-guide/netx-events/image53.png)    | **Eliminazione voce della cache Duo** (*nxd_nd_cache_entry_delete*) |
| ![Icona del set di voci della cache Duo](./media/user-guide/netx-events/image54.png)    | **Set di voci della cache Duo** (*nxd_nd_cache_entry_set*) |
| ![Icona di invalidamento della cache Duo](./media/user-guide/netx-events/image55.png)    | **Invalidamento della cache Duo** (*nxd_nd_cache_invalidate*) |
| ![Icona di ricerca dell'indirizzo del duo cache I P](./media/user-guide/netx-events/image56.png)    | **Ricerca indirizzo IP cache Duo** (*nxd_nd_cache_ip_address_find*) |
| ![Icona di abilitazione Duo I C M P](./media/user-guide/netx-events/image57.png)    | **Abilitazione ICMP Duo** (*nxd_icmp_enable*) |
| ![Icona di ping di duo I C M P I P v 6](./media/user-guide/netx-events/image58.png)    | **Ping IPv6 ICMP Duo** (*nxd_icmp_ping*) |
| ![Icona trova dimensioni del payload massimo Duo I P](./media/user-guide/netx-events/image59.png)    | **Ricerca dimensioni massime payload IP Duo** (*nx_max_payload_size_find*) |
| ![Icona di invio di pacchetti non elaborati Duo I P](./media/user-guide/netx-events/image60.png)    | **Trasmissione pacchetti non elaborati IP Duo** (*nxd_ip_raw_packet_send*) |
| ![Icona di aggiunta del router predefinito Duo I P v 6](./media/user-guide/netx-events/image61.png)    | **Aggiunta del router predefinito IPv6 Duo** (*nxd_ipv6_default_router_add*) |
| ![Icona di eliminazione del router predefinito Duo I P v 6](./media/user-guide/netx-events/image62.png)    | **Eliminazione router default IPv6 Duo** (*nxd_ipv6_default_router_delete)* |
| ![Icona abilitazione Duo I P v 6](./media/user-guide/netx-events/image63.png)    | **Abilitazione IPv6 Duo** (*nxd_ipv6_enable)* |
| ![Icona Get indirizzo globale Duo I P v 6](./media/user-guide/netx-events/image64.png)    | **Indirizzo globale IPv6 Duo Get** (*nxd_ipv6_global_address_get*) |
| ![Icona del set di indirizzi globale Duo I P v 6](./media/user-guide/netx-events/image65.png)    | **Set di indirizzi globali IPv6 Duo** (*nxd_ipv6_global_address_set*) |
| ![Icona del processo padre di avvio Duo I P v 6](./media/user-guide/netx-events/image66.png)    | **Processo padre di avvio IPv6 Duo** (*nxd_ipv6_initiate_dad_process*) |
| ![Icona di Get dell'indirizzo dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image67.png)    | **Indirizzo di interfaccia IPv6 del duo Get** (*nxd_ipv6_interface_address_get*) |
| ![Icona set di indirizzi dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image68.png)    | **Set di indirizzi di interfaccia IPv6 Duo** (*nxd_ipv6_interface_address_set*) |
| ![Icona di Get dell'indirizzo locale del collegamento Duo I P v 6](./media/user-guide/netx-events/image69.png)    | **Indirizzo locale del collegamento IPv6 Duo Get** (*nxd_ipv6_linklocal_address_get*) |
| ![Icona del set di indirizzi locali di collegamento I P v 6](./media/user-guide/netx-events/image70.png)    | **Set di indirizzi locali del collegamento IPv6 Duo** (*nxd_ipv6_linklocal_address_set*) |
| ![Icona di invio di pacchetti non elaborati Duo I P v 6](./media/user-guide/netx-events/image71.png)    | **Trasmissione pacchetti non elaborati IPv6 Duo** (*nxd_ipv6_raw_packet_send)* |
| ![Icona Get per le informazioni su peer di Duo T C P](./media/user-guide/netx-events/image72.png)    | **Informazioni su peer socket TCP Duo Get** (*nxd_tcp_socket_peer_info_get*) |
| ![Icona dell'interfaccia del set di socket T C P Duo](./media/user-guide/netx-events/image73.png)    | **Interfaccia del set di socket TCP Duo** (*nxd_tcp_socket_set_interface*) |
| ![Icona di invio del socket Duo U D P](./media/user-guide/netx-events/image74.png)    | **Invio socket UDP Duo** (*nxd_udp_socket_send*) |
| ![Icona dell'interfaccia del set di socket U D P Duo](./media/user-guide/netx-events/image75.png)    | **Interfaccia del set di socket UDP Duo** (*nxd_udp_socket_set_interface*) |
| ![Icona estrazione origine Duo U D P](./media/user-guide/netx-events/image76.png)    | **Estrai origine UDP Duo** (*nxd_udp_source_extract*) |
| ![Icona di abilitazione I C M P](./media/user-guide/netx-events/image77.png)    | **Abilita ICMP** (*nx_icmp_enable*) |
| ![Icona di Get di informazioni C M P](./media/user-guide/netx-events/image78.png)    | **Informazioni sul protocollo ICMP Get** (*nx_icmp_info_get*) |
| ![Icona ping I C M P](./media/user-guide/netx-events/image79.png)    | **Ping ICMP** (*nx_icmp_ping*) |
| ![Icona di abilitazione I G M P](./media/user-guide/netx-events/image80.png)    | **Abilitazione IGMP** (*nx_igmp_enable*) |
| ![Icona di informazioni Get di I G M P](./media/user-guide/netx-events/image81.png)    | **Informazioni IGMP Get** (*nx_igmp_info_get*) |
| ![Icona di disabilitazione loopback di I G M P](./media/user-guide/netx-events/image82.png)    | **Disabilita loopback loopback** (*nx_igmp_loopback_disable*) |
| ![Icona Abilita loopback I G M P](./media/user-guide/netx-events/image83.png)    | **Abilita loopback loopback** (*nx_igmp_loopback_enable*) |
| ![Icona di join multicast I G M P](./media/user-guide/netx-events/image84.png)    | **Join multicast IGMP** (*nx_igmp_multicast_join*) |
| ![Icona di uscita multicast I G M P](./media/user-guide/netx-events/image85.png)    | **Uscita multicast IGMP** (*nx_igmp_multicast_leave*) |
| ![Icona di notifica della modifica dell'indirizzo I P](./media/user-guide/netx-events/image86.png)    | **Notifica di modifica dell'indirizzo IP** (*nx_ip_address_change_notify*) |
| ![Icona Ottieni indirizzo I P](./media/user-guide/netx-events/image87.png)    | **Indirizzo IP Get** (*nx_ip_address_get*) |
| ![Icona del set di indirizzi I P](./media/user-guide/netx-events/image88.png)    | **Set di indirizzi IP** (*nx_ip_address_set*) |
| ![Icona di creazione P](./media/user-guide/netx-events/image89.png)    | **Creazione IP** (*nx_ip_create*) |
| ![Icona di eliminazione I P](./media/user-guide/netx-events/image90.png)    | **Eliminazione IP** (*nx_ip_delete*) |
| ![Icona comando diretto driver I P](./media/user-guide/netx-events/image91.png)    | **Comando Direct driver IP** (*nx_ip_driver_direct_command*) |
| ![Icona di disabilitazione dell'invio P](./media/user-guide/netx-events/image92.png)    | **Disabilitazione dell'invio IP** (*nx_ip_forwarding_disable*) |
| ![Icona Abilita l'invio P](./media/user-guide/netx-events/image93.png)    | **Abilitazione dell'invio IP** (*nx_ip_forwarding_enable*) |
| ![Icona di disabilitazione del frammento I P](./media/user-guide/netx-events/image94.png)    | **Disabilitazione frammenti IP** (*nx_ip_fragment_disable*) |
| ![Icona Abilita frammento I P](./media/user-guide/netx-events/image95.png)    | **Abilitazione frammenti IP** (*nx_ip_fragment_enable*)  |
| ![Icona del set di indirizzi del gateway I P](./media/user-guide/netx-events/image96.png)    | **Set di indirizzi IP gateway** (*nx_ip_gateway_address_set*) |
| ![Icona di Get delle informazioni P](./media/user-guide/netx-events/image97.png)    | **Informazioni IP Get** (*nx_ip_info_get*) |
| ![Icona di connessione interfaccia I P](./media/user-guide/netx-events/image98.png)    | **Connessione interfaccia IP** (*nx_ip_interface_attach*) |
| ![Icona di informazioni di interfaccia I P Get](./media/user-guide/netx-events/image99.png)    | **Informazioni sull'interfaccia IP Get** (*nx_ip_interface_info_get*) |
| ![Icona di disabilitazione pacchetti non elaborati](./media/user-guide/netx-events/image100.png)    | **Disabilitazione pacchetto non elaborato IP** (*nx_ip_raw_packet_disable*) |
| ![Icona di abilitazione di pacchetti non elaborati](./media/user-guide/netx-events/image101.png)    | **Abilitazione pacchetti non elaborati IP** (*nx_ip_raw_packet_enable*) |
| ![Icona di ricezione di pacchetti non elaborati](./media/user-guide/netx-events/image102.png)    | **Ricezione pacchetti non elaborati IP** (*nx_ip_raw_packet_receive*) |
| ![Icona di invio di pacchetti non elaborati](./media/user-guide/netx-events/image103.png)    | **Invio pacchetti non elaborati IP** (*nx_ip_raw_packet_send*) |
| ![Icona di aggiunta statica route I P](./media/user-guide/netx-events/image104.png)    | **Aggiunta route statica IP** (*nx_ip_static_route_add*) |
| ![Icona di eliminazione route statica I P](./media/user-guide/netx-events/image105.png)    | **Eliminazione route statica IP** (*nx_ip_static_route_delete)* |
| ![Icona di controllo stato I P](./media/user-guide/netx-events/image106.png)    | **Controllo stato IP** (*nx_ip_status_check*)|
| ![Icona Enable i P S E C](./media/user-guide/netx-events/image107.png)    | **Abilita IPSec** (*nx_ipsec_enable)* |
| ![Icona di allocazione pacchetti](./media/user-guide/netx-events/image108.png)    | **Allocazione pacchetti** (*nx_packet_allocate*) |
| ![Icona copia pacchetti](./media/user-guide/netx-events/image109.png)    | **Copia di pacchetti** (*nx_packet_copy*) |
| ![Icona Accodamento dati pacchetto](./media/user-guide/netx-events/image110.png)    | **Accodamento dati pacchetto** (*nx_packet_data_append*) |
| ![Icona di offset estrazione dati pacchetto](./media/user-guide/netx-events/image111.png)    | **Offset estrazione dati pacchetto** (*nx_packet_data_extract_offset*) |
| ![Icona recupero dati pacchetto](./media/user-guide/netx-events/image112.png)    | **Recupero dati pacchetto** (*nx_packet_data_retrieve*) |
| ![Icona Ottieni lunghezza pacchetto](./media/user-guide/netx-events/image113.png)    | **Lunghezza pacchetto Get** (*nx_packet_length_get*) |
| ![Icona di creazione pool di pacchetti](./media/user-guide/netx-events/image114.png)    | **Creazione pool di pacchetti** (*nx_packet_pool_create*) |
| ![Icona di eliminazione del pool di pacchetti](./media/user-guide/netx-events/image115.png)    | **Eliminazione pool di pacchetti** (*nx_packet_pool_delete*) |
| ![Icona Ottieni informazioni sul pool di pacchetti](./media/user-guide/netx-events/image116.png)    | **Informazioni sul pool di pacchetti Get** (*nx_packet_pool_info_get*) |
| ![Icona versione pacchetto](./media/user-guide/netx-events/image117.png)    | **Versione pacchetto** (*nx_packet_release*) |
| ![Icona della versione di trasmissione pacchetti](./media/user-guide/netx-events/image118.png)    | **Versione trasmissione pacchetti** (*nx_packet_transmit_release*) |
| ![Icona di disabilitazione r P](./media/user-guide/netx-events/image119.png)    | **Disabilitazione RARP** (*nx_rarp_disable*) |
| ![Icona di abilitazione r A r P](./media/user-guide/netx-events/image120.png)    | **Abilitazione di RARP** (*nx_rarp_enable*) |
| ![Icona di r A r P Information Get](./media/user-guide/netx-events/image121.png)    | **Informazioni su RARP Get** (*nx_rarp_info_get*) |
| ![Icona Inizializzazione sistema](./media/user-guide/netx-events/image122.png)    | **Inizializzazione sistema** (*nx_system_initialize*) |
| ![Icona di Binding socket client T C P](./media/user-guide/netx-events/image123.png)    | **Binding socket client TCP** (*nx_tcp_client_socket_bind*) |
| ![Icona di connessione socket client T C P](./media/user-guide/netx-events/image124.png)    | **Connessione socket client TCP** (*nx_tcp_client_socket_connect*) |
| ![Icona di Get della porta del socket client T C P](./media/user-guide/netx-events/image125.png)    | **Porta socket client TCP** (*nx_tcp_client_socket_port_get*) |
| ![Icona di disassociazione socket client T C P](./media/user-guide/netx-events/image126.png)    | **Disassociazione socket client TCP** (*nx_tcp_client_socket_unbind*) |
| ![Icona di abilitazione di T C P](./media/user-guide/netx-events/image127.png)    | **Abilitazione TCP** (*nx_tcp_enable*) |
| ![Icona trova porta disponibile T C P](./media/user-guide/netx-events/image128.png)    | **Ricerca porta TCP gratuita** (*nx_tcp_free_port_find*) |
| ![Icona di Get delle informazioni di T C P](./media/user-guide/netx-events/image129.png)    | **Informazioni sul protocollo TCP Get** (*nx_tcp_info_get*) |
| ![Icona di accettazione socket server T C P](./media/user-guide/netx-events/image130.png)    | **Accettazione socket server TCP** (*nx_tcp_server_socket_accept*) |
| ![Icona ascolto Socket Server T C P](./media/user-guide/netx-events/image131.png)    | **Ascolto socket server TCP** (*nx_tcp_server_socket_listen*) |
| ![Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image132.png)    | **Socket server TCP relisten** (*nx_tcp_server_socket_relisten*) |
| ![Icona di unaccept socket server T C P](./media/user-guide/netx-events/image133.png)    | **Unaccept socket server TCP** (*nx_tcp_server_socket_unaccept*) |
| ![Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image134.png)    | **Server socket TCP** non in elenco (*nx_tcp_server_socket_unlisten*) |
| ![Icona di byte socket a T C P disponibile](./media/user-guide/netx-events/image135.png)    | **Byte socket TCP disponibili** (*nx_tcp_socket_bytes_available*) |
| ![Icona di creazione socket T C P](./media/user-guide/netx-events/image136.png)    | **Creazione socket TCP** (*nx_tcp_socket_create*) |
| ![Icona di eliminazione Socket T C P](./media/user-guide/netx-events/image137.png)    | **Elimina socket TCP** (*nx_tcp_socket_delete*) |
| ![Icona di disconnessione Socket T C P](./media/user-guide/netx-events/image138.png)    | **Disconnessione socket TCP** (*nx_tcp_socket_disconnect*) |
| ![Icona di Get delle informazioni sul socket T C P](./media/user-guide/netx-events/image139.png)    | **Informazioni sul socket TCP Get** (*nx_tcp_socket_info_get*) |
| ![Icona di Get MSS Socket T C P](./media/user-guide/netx-events/image140.png)    | **TCP socket MSS Get** (*nx_tcp_socket_mss_get*) |
| ![Icona di Get del peer MSS di T C P](./media/user-guide/netx-events/image141.png)    | **Peer Get MSS socket TCP** (*nx_tcp_socket_mss_peer_get*) |
| ![Icona set MSS Socket T C P](./media/user-guide/netx-events/image142.png)    | **Set MSS socket TCP** (*nx_tcp_socket_mss_set*) |
| ![Icona di Get delle informazioni peer del socket T C P](./media/user-guide/netx-events/image143.png)    | **Get informazioni peer del socket TCP** (*nx_tcp_socket_peer_info_get*) |
| ![Icona di ricezione Socket T C P](./media/user-guide/netx-events/image144.png)    | **Ricezione socket TCP** (*nx_tcp_socket_receive*) |
| ![Icona di ricezione della notifica socket T C P](./media/user-guide/netx-events/image145.png)    | **Notifica ricezione socket TCP** (*nx_tcp_socket_receive_notify*) |
| ![Icona di invio socket T C P](./media/user-guide/netx-events/image146.png)    | **Invio socket TCP** (*nx_tcp_socket_send*) |
| ![Icona di attesa stato Socket T C P](./media/user-guide/netx-events/image147.png)    | **Attesa stato socket TCP** (*nx_tcp_socket_state_wait*) |
| ![Icona di configurazione di trasmissione Socket T C P](./media/user-guide/netx-events/image148.png)    | **Configurazione di trasmissione socket TCP** (*nx_tcp_socket_transmit_configure*) |
| ![Icona del set di notifiche di aggiornamento della finestra socket di T C P](./media/user-guide/netx-events/image149.png)    | **Set Notify di aggiornamento finestra socket TCP** (*nx_tcp_socket_window_update_notify_set*)  |
| ![Icona di abilitazione di U D P](./media/user-guide/netx-events/image150.png)    | **Abilita UDP** (*nx_udp_enable*) |
| ![Icona trova porta gratuita U D P](./media/user-guide/netx-events/image151.png)    | **Ricerca porta gratuita UDP** (*nx_udp_free_port_find*) |
| ![Icona di Get delle informazioni di U D P](./media/user-guide/netx-events/image152.png)    | **Informazioni UDP Get** (*nx_udp_info_get*) |
| ![Icona di Binding socket U D P](./media/user-guide/netx-events/image153.png)    | **Binding socket UDP** (*nx_udp_socket_bind*) |
| ![Icona di byte socket U D P disponibile](./media/user-guide/netx-events/image154.png)    | **Byte socket UDP disponibili** (*nx_udp_socket_bytes_available*) |
| ![Icona di disabilitazione checksum socket U D P](./media/user-guide/netx-events/image155.png)    | **Disabilita checksum socket UDP** (*nx_udp_socket_checksum_disable*) |
| ![Icona Abilita checksum socket U D P](./media/user-guide/netx-events/image156.png)    | **Enable UDP Socket checksum** *(nx_udp_socket_checksum_enable)* |
| ![Icona di creazione socket U D P](./media/user-guide/netx-events/image157.png)    | **Creazione socket UDP** (*nx_udp_socket_create*) |
| ![Icona di eliminazione socket U D P](./media/user-guide/netx-events/image158.png)    | **Elimina socket UDP** (*nx_udp_socket_delete*) |
| ![Icona di Get delle informazioni sul socket U D](./media/user-guide/netx-events/image159.png)    | **Informazioni sul socket UDP Get** (*nx_udp_socket_info_get*) |
| ![Icona del set di interfacce socket U D P](./media/user-guide/netx-events/image160.png)    | **Set di interfacce socket UDP** (*nx_udp_socket_interface_set*) |
| ![Icona di Get della porta socket U D P](./media/user-guide/netx-events/image161.png)    | **Porta del socket UDP Get** (*nx_udp_socket_port_get*) |
| ![Icona di ricezione socket U D P](./media/user-guide/netx-events/image162.png)    | **Ricezione socket UDP** (*nx_udp_socket_receive*) |
| ![Icona di ricezione della notifica socket U D P](./media/user-guide/netx-events/image163.png)    | **Notifica ricezione socket UDP** (*nx_udp_socket_receive_notify*) |
| ![Icona di invio socket U D P](./media/user-guide/netx-events/image164.png)    | **Invio socket UDP** (*nx_udp_socket_send*) |
| ![Icona di disassociazione socket U D P](./media/user-guide/netx-events/image165.png)    | **Disassociazione socket UDP** (*nx_udp_socket_unbind*) |
| ![Icona estrazione origine U D P](./media/user-guide/netx-events/image166.png)    | **Estrazione origine UDP** (*nx_udp_source_extract*) |

## <a name="event-descriptions"></a>Descrizioni di eventi

Nelle pagine seguenti vengono descritti gli eventi di traccia NetX.

### <a name="internal-arp-request-receive"></a>Ricezione richiesta ARP interna 

#### <a name="internal-arp-request-receive"></a>Ricezione richiesta ARP interna

**Icona** ![ di Icona di ricezione richiesta ARP interna](./media/user-guide/netx-events/image1.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione della richiesta ARP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di origine
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: non usato

### <a name="internal-arp-request-send"></a>Invio richiesta ARP interno 

#### <a name="internal-arp-request-send"></a>Invio richiesta ARP interno

**Icona** ![ di Icona di invio richiesta ARP interna](./media/user-guide/netx-events/image2.png)

**Descrizione**

Questo evento rappresenta un evento di invio della richiesta ARP NetX interna.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di destinazione
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: non usato

### <a name="internal-arp-response-receive"></a>Ricezione risposta ARP interna 

#### <a name="internal-arp-request-receive"></a>Ricezione richiesta ARP interna

**Icona** ![ di Icona di ricezione della richiesta ARP interna](./media/user-guide/netx-events/image3.png)

**Descrizione**

Questo evento rappresenta un evento interno di ricezione della risposta ARP NetX.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di origine
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: non usato

### <a name="internal-arp-response-send"></a>Invio risposta ARP interna 

#### <a name="internal-arp-request-send"></a>Invio richiesta ARP interno

**Icona** ![ di Icona di invio della richiesta ARP interna](./media/user-guide/netx-events/image4.png)

**Descrizione**

Questo evento rappresenta un evento di invio risposta NetX interna.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di destinazione
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: non usato

### <a name="internal-icmp-receive"></a>Ricezione ICMP interna 

#### <a name="internal-icmp-receive"></a>Ricezione ICMP interna

**Icona** ![ di Icona di ricezione interno I C M P](./media/user-guide/netx-events/image5.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione ICMP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di origine
- Informazioni sul campo 3: puntatore al pacchetto
- Informazioni sul campo 4: Word 0 dell'intestazione ICMP

### <a name="internal-icmp-send"></a>Invio ICMP interno 

#### <a name="internal-icmp-send"></a>Invio ICMP interno

**Icona** ![ di Icona di invio C M P interna](./media/user-guide/netx-events/image6.png)

**Descrizione**

Questo evento rappresenta un evento di invio ICMP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di destinazione
- Informazioni sul campo 3: puntatore al pacchetto
- Informazioni sul campo 4: Word 0 dell'intestazione ICMP

### <a name="internal-igmp-receive"></a>Ricezione IGMP interna 

#### <a name="internal-igmp-receive"></a>Ricezione IGMP interna

**Icona** ![ di Icona di ricezione I G M interna](./media/user-guide/netx-events/image7.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione IGMP NetX interno.

**Campi informazioni**

- Campo informazioni 1: puntatore IP
- Informazioni sul campo 2: indirizzo IP di origine
- Informazioni sul campo 3: puntatore al pacchetto
- Informazioni sul campo 4: parola 0 dell'intestazione IGMP

### <a name="internal-ip-receive"></a>Ricezione IP interna 

#### <a name="internal-ip-receive"></a>Ricezione IP interna

**Icona** ![ di Icona di ricezione I P interni](./media/user-guide/netx-events/image8.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione IP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di origine
- Informazioni sul campo 3: puntatore al pacchetto
- Campo dati 4: lunghezza pacchetto

### <a name="internal-ip-send"></a>Invio IP interno

#### <a name="internal-ip-send"></a>Invio IP interno

**Icona** ![ di Icona di invio di I P interni](./media/user-guide/netx-events/image9.png)

**Descrizione**

Questo evento rappresenta un evento di invio IP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di destinazione
- Informazioni sul campo 3: puntatore al pacchetto
- Campo dati 4: lunghezza pacchetto

### <a name="internal-tcp-data-receive"></a>Ricezione di dati TCP interni 

#### <a name="internal-tcp-data-receive"></a>Ricezione di dati TCP interni

**Icona** ![ di Icona di ricezione dati T C P interna](./media/user-guide/netx-events/image10.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione dati TCP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di origine
- Informazioni sul campo 3: puntatore al pacchetto
- Campo dati 4: numero di sequenza di ricezione

### <a name="internal-tcp-data-send"></a>Trasmissione dati TCP interni 

#### <a name="internal-tcp-data-send"></a>Trasmissione dati TCP interni

**Icona** ![ di Icona di invio dati T C P interna](./media/user-guide/netx-events/image11.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione dati TCP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: numero di sequenza di trasmissione

### <a name="internal-tcp-fin-receive"></a>Ricezione dell'aletta TCP interna 

#### <a name="internal-tcp-fin-receive"></a>Ricezione dell'aletta TCP interna

**Icona** ![ di Icona di ricezione T C P interna](./media/user-guide/netx-events/image12.png)

**Descrizione**

Questo evento rappresenta un evento interno di ricezione di NetX TCP.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Campo dati 4: numero di sequenza di ricezione

### <a name="internal-tcp-fin-send"></a>Trasmissione aletta TCP interna 

#### <a name="internal-tcp-fin-send"></a>Trasmissione aletta TCP interna

**Icona** ![ di Icona di invio T C P F I N](./media/user-guide/netx-events/image13.png)

**Descrizione**

Questo evento rappresenta un evento NetX TCP aletta di invio interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: numero di sequenza di trasmissione

### <a name="internal-tcp-rst-receive"></a>Ricezione RST TCP interna 

#### <a name="internal-tcp-rst-receive"></a>Ricezione RST TCP interna

**Icona** ![ di Icona di ricezione T C P R S interna](./media/user-guide/netx-events/image14.png)

**Descrizione**

Questo evento rappresenta un evento interno di ricezione della reimpostazione di NetX TCP.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Informazioni sul campo 2: puntatore al socket.
- Informazioni sul campo 3: puntatore al pacchetto.
- Informazioni sul campo 4: numero di sequenza di ricezione.

### <a name="internal-tcp-rst-send"></a>Trasmissione RST TCP interna 

#### <a name="internal-tcp-rst-send"></a>Trasmissione RST TCP interna

**Icona** ![ di Icona di invio T C P R S interna](./media/user-guide/netx-events/image15.png)

**Descrizione**

Questo evento rappresenta un evento di invio di reimpostazione TCP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: numero di sequenza di trasmissione

### <a name="internal-tcp-syn-receive"></a>Ricezione SYN TCP interna 

#### <a name="internal-tcp-syn-receive"></a>Ricezione SYN TCP interna

**Icona** ![ di Icona di ricezione T C P S interna](./media/user-guide/netx-events/image16.png)

**Descrizione**

Questo evento rappresenta un evento NetX TCP SYN Receive interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Campo dati 4: numero di sequenza di ricezione

### <a name="internal-tcp-syn-send"></a>Trasmissione SYN TCP interna 

#### <a name="internal-tcp-syn-send"></a>Trasmissione SYN TCP interna

**Icona** ![ di Icona di invio T C P S interna](./media/user-guide/netx-events/image17.png)

**Descrizione**

Questo evento rappresenta un evento interno NetX TCP SYN Send.

Campi informazioni 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Info Field 3: puntatore a Packet-Info Field 4: trasmissione numero di sequenza

### <a name="internal-udp-receive"></a>Ricezione UDP interna 

#### <a name="internal-udp-receive"></a>Ricezione UDP interna

**Icona** ![ di Icona di ricezione U D P interna](./media/user-guide/netx-events/image18.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione UDP NetX interno.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Informazioni sul campo 4: Word 0 dell'intestazione UDP

### <a name="internal-udp-send"></a>Invio UDP interno 

#### <a name="internal-udp-send"></a>Invio UDP interno

**Icona** ![ di Icona di invio di U D P interna](./media/user-guide/netx-events/image19.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione UDP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Informazioni sul campo 4: Word 0 dell'intestazione UDP

### <a name="internal-rarp-receive"></a>Ricezione RARP interna 

#### <a name="internal-rarp-receive"></a>Ricezione RARP interna 

**Icona** ![ di Icona di ricezione r P interna](./media/user-guide/netx-events/image20.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione RARP NetX interno.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di destinazione
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: parola 1 dell'intestazione RARP

### <a name="internal-rarp-send"></a>Invio RARP interno 

#### <a name="internal-rarp-send"></a>Invio RARP interno 

**Icona** ![ di Icona interna R A R P Send](./media/user-guide/netx-events/image21.png)

**Descrizione**

Questo evento rappresenta un evento di invio NetX RARP interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP di destinazione
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: parola 1 dell'intestazione RARP

### <a name="internal-tcp-retry"></a>Tentativo TCP interno 

#### <a name="internal-tcp-retry"></a>Tentativo TCP interno 

**Icona** ![ di Icona di ripetizione dei tentativi interna di T C](./media/user-guide/netx-events/image22.png)

**Descrizione**

Questo evento rappresenta un evento di ripetizione NetX TCP interno.

**Campi informazioni**
- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore al pacchetto
- Campo informazioni 4: numero di tentativi

### <a name="internal-tcp-state-change"></a>Modifica dello stato TCP interna 

#### <a name="internal-tcp-state-change"></a>Modifica dello stato TCP interna 

**Icona** ![ di Icona di modifica dello stato T C P interno](./media/user-guide/netx-events/image23.png)

**Descrizione**

Questo evento rappresenta un evento di modifica dello stato del socket TCP NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: stato precedente
- Campo informazioni 4: nuovo stato

### <a name="internal-io-driver-packet-send"></a>Invio di pacchetti di driver I/O interni 

#### <a name="internal-io-driver-packet-send"></a>Invio di pacchetti di driver I/O interni

**Icona** ![ di Icona di invio pacchetti driver I/O interno](./media/user-guide/netx-events/image24.png)

**Descrizione**

Questo evento rappresenta un evento di invio di pacchetti di driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: dimensioni del pacchetto
- Campo informazioni 4: non usato

### <a name="internal-io-driver-initialize"></a>Inizializzazione driver I/O interno 

#### <a name="internal-io-driver-initialize"></a>Inizializzazione driver I/O interno

**Icona** ![ di Icona di inizializzazione del driver I/O interno](./media/user-guide/netx-events/image25.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione del driver I/O interno di NetX.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-link-enable"></a>Abilitazione collegamento driver I/O interno 

#### <a name="internal-io-driver-link-enable"></a>Abilitazione collegamento driver I/O interno

**Icona** ![ di Icona Abilita collegamento driver I/O interno](./media/user-guide/netx-events/image26.png)

**Descrizione**

Questo evento rappresenta un evento di abilitazione del collegamento del driver I/O interno di NetX.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-link-disable"></a>Disabilitazione collegamento driver I/O interno 

#### <a name="internal-io-driver-link-disable"></a>Disabilitazione collegamento driver I/O interno

**Icona** ![ di Icona di disabilitazione collegamento driver I/O interno](./media/user-guide/netx-events/image27.png)

**Descrizione**

Questo evento rappresenta un evento di disabilitazione del collegamento del driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-packet-broadcast"></a>Trasmissione di pacchetti di driver I/O interni 

#### <a name="internal-io-driver-packet-broadcast"></a>Trasmissione di pacchetti di driver I/O interni

**Icona** ![ di Icona trasmissione pacchetti I/O interno](./media/user-guide/netx-events/image28.png)

**Descrizione**

Questo evento rappresenta un evento interno di trasmissione pacchetti di driver I/O di NetX.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: dimensioni del pacchetto
- Campo informazioni 4: non usato

### <a name="internal-io-driver-arp-send"></a>Invio ARP driver I/O interno 

#### <a name="internal-io-driver-arp-send"></a>Invio ARP driver I/O interno

**Icona** ![ di Icona di trasmissione ARP driver I/O interno](./media/user-guide/netx-events/image29.png)

**Descrizione**

Questo evento rappresenta un evento di invio ARP di un driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: dimensioni del pacchetto
- Campo informazioni 4: non usato

### <a name="internal-io-driver-arp-response-send"></a>Invio risposta ARP driver I/O interno 

#### <a name="internal-io-driver-arp-response-send"></a>Invio risposta ARP driver I/O interno

**Icona** ![ di Icona di invio risposta ARP driver I/O interno](./media/user-guide/netx-events/image30.png)

**Descrizione**

Questo evento rappresenta un evento di invio risposta ARP di un driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: dimensioni del pacchetto
- Campo informazioni 4: non usato

### <a name="internal-io-driver-rarp-send"></a>Invio di un driver di I/O interno RARP 

#### <a name="internal-io-driver-rarp-send"></a>Invio di un driver di I/O interno RARP

**Icona** ![ di Icona di invio RARP driver I/O interno](./media/user-guide/netx-events/image31.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione RARP NetX I/O driver interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: dimensioni del pacchetto
- Campo informazioni 4: non usato

### <a name="internal-io-driver-multicast-join"></a>Join multicast driver I/O interno 

#### <a name="internal-io-driver-multicast-join"></a>Join multicast driver I/O interno

**Icona** ![ di Icona di join multicast driver I/O interno](./media/user-guide/netx-events/image32.png)

**Descrizione**

Questo evento rappresenta un evento interno di join multicast driver I/O di NetX.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-multicast-leave"></a>Uscita multicast driver I/O interno 

#### <a name="internal-io-driver-multicast-leave"></a>Uscita multicast driver I/O interno

**Icona** ![ di Icona di uscita multicast driver I/O interno](./media/user-guide/netx-events/image33.png)

**Descrizione**

Questo evento rappresenta un evento di uscita multicast del driver I/O interno di NetX.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-status"></a>Stato Get driver I/O interno 

#### <a name="internal-io-driver-get-status"></a>Stato Get driver I/O interno

**Icona** ![ di Icona di Ottieni stato driver I/O interno](./media/user-guide/netx-events/image34.png)

**Descrizione**

Questo evento rappresenta un evento di stato Get driver I/O interno NetX.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-speed"></a>Velocità di ottenimento del driver I/O interno 

#### <a name="internal-io-driver-get-speed"></a>Velocità di ottenimento del driver I/O interno

**Icona** ![ di Icona di Ottieni velocità driver I/O interno](./media/user-guide/netx-events/image35.png)

**Descrizione**

Questo evento rappresenta un evento di velocità di ottenimento di un driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-duplex-type"></a>Tipo duplex Get driver I/O interno 

#### <a name="internal-io-driver-get-duplex-type"></a>Tipo duplex Get driver I/O interno

**Icona** ![ di Icona del tipo di driver di I/O interno Get duplex](./media/user-guide/netx-events/image36.png)

**Descrizione**

Questo evento rappresenta un evento Internal NetX I/O driver Get duplex.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-error-count"></a>Conteggio errori di Get driver I/O interno

#### <a name="internal-io-driver-get-error-count"></a>Conteggio errori di Get driver I/O interno

**Icona** ![ di Icona per il conteggio degli errori di Get di driver I/O interno](./media/user-guide/netx-events/image37.png)

**Descrizione**

Questo evento rappresenta un evento di conteggio degli errori di un driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-rx-count"></a>Conteggio RX del driver I/O interno 

#### <a name="internal-io-driver-get-rx-count"></a>Conteggio RX del driver I/O interno

**Icona** ![ di Icona del conteggio RX del driver I/O interno](./media/user-guide/netx-events/image38.png)

**Descrizione**

Questo evento rappresenta un evento di conteggio di un driver di I/O NetX interno Get RX.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-tx-count"></a>Conteggio TX del driver I/O interno 

#### <a name="internal-io-driver-get-tx-count"></a>Conteggio TX del driver I/O interno

**Icona** ![ di Icona di conteggio del driver I/O interno get T X](./media/user-guide/netx-events/image39.png)

**Descrizione**

Questo evento rappresenta un evento di conteggio di un driver di I/O NetX interno Get TX.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-get-allocation-errors"></a>Errore di allocazione del driver I/O interno 

#### <a name="internal-io-driver-get-allocation-errors"></a>Errore di allocazione del driver I/O interno

**Icona** ![ di Icona per ottenere gli errori di allocazione del driver I/O interno](./media/user-guide/netx-events/image40.png)

**Descrizione**

Questo evento rappresenta un evento di errore di allocazione di un driver di I/O NetX interno.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-un-initialize"></a>Annulla inizializzazione del driver di I/O interno 

#### <a name="internal-io-driver-un-initialize"></a>Annulla inizializzazione del driver di I/O interno 

**Icona** ![ di Icona di annullamento inizializzazione del driver I/O interno](./media/user-guide/netx-events/image41.png)

**Descrizione**

Questo evento rappresenta un evento di annullamento inizializzazione del driver di I/O NetX interno.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="internal-io-driver-deferred-processing"></a>Elaborazione posticipata del driver di I/O interno 

#### <a name="internal-io-driver-deferred-processing"></a>Elaborazione posticipata del driver di I/O interno 

**Icona** ![ di Icona di elaborazione posticipata del driver I/O interno](./media/user-guide/netx-events/image42.png)

**Descrizione**

Questo evento rappresenta un evento di elaborazione posticipato del driver di I/O NetX interno.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: lunghezza del pacchetto
- Campo informazioni 4: non usato

### <a name="arp-dynamic-entries-invalidate"></a>Voci dinamiche ARP invalide 

#### <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate

**Icona** ![ di Icona delle voci dinamiche di R P Invalidate](./media/user-guide/netx-events/image43.png)

**Descrizione**

Questo evento rappresenta l'invalidamento di tutte le intere ARP dinamiche tramite nx_arp_dynamic_entries_invalidate.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: voci Invalidate
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="arp-dynamic-entry-set"></a>Set di voci dinamiche ARP 

#### <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set

**Icona** ![ di Icona del set di voci dinamiche di R P](./media/user-guide/netx-events/image44.png)

**Descrizione**

Questo evento rappresenta l'impostazione di una voce ARP dinamica tramite nx_arp_dynamic_entry_set.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: indirizzo fisico (RSU)
- Campo dati 4: indirizzo fisico (LSW)

### <a name="arp-enable"></a>Abilitazione ARP 

#### <a name="nx_arp_enable"></a>nx_arp_enable

**Icona** ![ di Icona di abilitazione di R P](./media/user-guide/netx-events/image45.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di ARP tramite nx_arp_enable.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore di memoria della cache ARP
- Informazioni sul campo 3: dimensioni della memoria della cache ARP
- Campo informazioni 4: non usato

### <a name="arp-gratuitous-send"></a>Invio gratuito ARP 

#### <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send

**Icona** ![ di Icona di invio gratuito A R P](./media/user-guide/netx-events/image46.png)

**Descrizione**

Questo evento rappresenta una trasmissione ARP gratuita tramite nx_arp_gratuitous_send.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="arp-hardware-address-find"></a>Ricerca indirizzo hardware ARP 

#### <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find

**Icona** ![ di Icona di ricerca indirizzo hardware R P](./media/user-guide/netx-events/image47.png)

**Descrizione**

Questo evento rappresenta la ricerca di un indirizzo fisico tramite nx_arp_hardware_address_find.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: indirizzo fisico (RSU)
- Campo dati 4: indirizzo fisico (LSW)

### <a name="arp-information-get"></a>Informazioni sul protocollo ARP Get 

#### <a name="nx_arp_info_get"></a>nx_arp_info_get

**Icona** ![ di Icona di R P informition Get](./media/user-guide/netx-events/image48.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_arp_info_get.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: ARPs inviato
- Informazioni sul campo 3: risposte ARP
- Campo dati 4: ARPs ricevuto

### <a name="arp-ip-address-find"></a>Ricerca di indirizzi IP ARP 

#### <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find

**Icona** ![ di Icona trova Indirizzo R P I P](./media/user-guide/netx-events/image49.png)

**Descrizione**

Questo evento rappresenta la ricerca di un indirizzo IP associato all'indirizzo fisico fornito tramite nx_arp_ip_address_find.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: indirizzo fisico (RSU)
- Campo dati 4: indirizzo fisico (LSW)

### <a name="arp-static-entry-create"></a>Creazione voce statica ARP 

#### <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create

**Icona** ![ di Icona di creazione di una voce statica R P](./media/user-guide/netx-events/image50.png)

**Descrizione**

Questo evento rappresenta la creazione di una voce ARP statica tramite nx_arp_static_entry_create.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: indirizzo fisico (RSU)
- Campo dati 4: indirizzo fisico (LSW)

### <a name="arp-static-entries-delete"></a>Elimina voci statiche ARP 

#### <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

**Icona** ![ di Icona Elimina voci statiche R P](./media/user-guide/netx-events/image51.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di tutte le voci statiche ARP tramite nx_arp_static_entries_delete.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: voci eliminate
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="arp-static-entry-delete"></a>Eliminazione voce statica ARP 

### <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete

**Icona** ![ di Icona di eliminazione della voce statica di R P](./media/user-guide/netx-events/image52.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di una voce ARP statica tramite nx_arp_static_entry_delete.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Campo informazioni 3: indirizzo fisico (RSU)
- Campo dati 4: indirizzo fisico (LSW)

### <a name="duo-cache-entry-delete"></a>Eliminazione voce della cache Duo 

#### <a name="nxd_und_cache_entry_delete"></a>nxd_und_cache_entry_delete

**Icona** ![ di Icona di eliminazione voce della cache Duo](./media/user-guide/netx-events/image53.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di una voce nella tabella della cache vicina tramite nx_udp_socket_create.

**Campi informazioni** 

- Campo informazioni 1: quarto (meno significativo) parola dell'indirizzo locale del collegamento IPv6 da eliminare
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-cache-entry-set"></a>Set di voci della cache Duo 

#### <a name="nxd_nd_cache_entry_set"></a>nxd_nd_cache_entry_set

**Icona** ![ di Icona del set di voci della cache Duo](./media/user-guide/netx-events/image54.png)

**Descrizione**

Questo evento rappresenta la creazione di una voce della cache e l'aggiunta alla tabella della cache vicina tramite nxd_nd_cache_entry_set.

**Campi informazioni** 

- Campo informazioni 1: quarto (meno significativo) parola dell'indirizzo IPv6 da aggiungere
- Informazioni sul campo 2: indirizzo fisico MSB
- Informazioni sul campo 3: indirizzo fisico lsb
- Campo informazioni 4: non usato

### <a name="duo-cache-invalidate"></a>Invalidamento della cache Duo 

#### <a name="nxd_nd_cache_invalidate"></a>nxd_nd_cache_invalidate

**Icona** ![ di Icona di invalidamento della cache Duo](./media/user-guide/netx-events/image55.png)

**Descrizione**

Questo evento rappresenta l'invalidamento dell'intera tabella della cache vicina tramite nxd_nd_cache_invalidate.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-cache-ip-address-find"></a>Ricerca indirizzo IP cache Duo 

#### <a name="nxd_nd_cache_ip_address_find"></a>nxd_nd_cache_ip_address_find

**Icona** ![ di Icona di ricerca dell'indirizzo del duo cache I P](./media/user-guide/netx-events/image56.png)

**Descrizione**

Questo evento rappresenta il recupero di un indirizzo IP corrispondente all'indirizzo fisico fornito dalla tabella della cache tramite nxd_nd_cache_ip_address_find.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo Info 2: quarto (meno significativo) parola dell'indirizzo IPv6
- Informazioni sul campo 3: indirizzo fisico MSB
- Informazioni sul campo 4: indirizzo fisico lsb

### <a name="duo-icmp-enable"></a>Abilitazione ICMP Duo 

#### <a name="nxd_icmp_enable"></a>nxd_icmp_enable

**Icona** ![ di Icona di abilitazione Duo I C M P](./media/user-guide/netx-events/image57.png)

**Descrizione**

Questo evento rappresenta i servizi ICMPv4 e ICMPv6 abilitati nell'istanza IP specificata tramite nxd_icmp_enable.

**Campi informazioni**
- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-icmp-ping"></a>Ping ICMP Duo 

#### <a name="nxd_icmp_ping"></a>nxd_icmp_ping

**Icona** ![ di Icona di ping di duo I C M P](./media/user-guide/netx-events/image58.png)

**Descrizione**

Questo evento rappresenta l'invio di un ping (richiesta echo) a un host IPv6 tramite nxd_icmp_ping.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IPv6
- Informazioni sul campo 3: puntatore ai dati echo
- Informazioni sul campo 4: dimensioni dei dati echo

### <a name="duo-ip-max-payload-size-find"></a>Ricerca dimensioni massime payload IP Duo 

#### <a name="nxd_ip_max_payload_size"></a>nxd_ip_max_payload_size

**Icona** ![ di Icona trova dimensioni del payload massimo Duo I P](./media/user-guide/netx-events/image59.png)

**Descrizione**

Questo evento Calcola il payload massimo che il pacchetto specificato può eseguire senza richiedere la frammentazione.

**Campi informazioni**

- Campo informazioni 1: puntatore socket
- Informazioni sul campo 2: indirizzo IP peer
- Informazioni sul campo 3: campo informazioni porta peer 4: non utilizzato

### <a name="duo-ip-raw-packet-send"></a>Invio pacchetti non elaborati IP Duo 

#### <a name="nxd_ip_max_packet_send"></a>nxd_ip_max_packet_send

**Icona** ![ di Icona di invio di pacchetti non elaborati Duo I P](./media/user-guide/netx-events/image60.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto IP non elaborato dall'interfaccia di rete specificata alla destinazione IP addressvia nxd_ip_raw_packet_send.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto da inviare
- Informazioni sul campo 3: puntatore all'indirizzo di destinazione
- Informazioni sul campo 4: protocollo Packet

### <a name="duo-ipv6-default-router-add"></a>Aggiunta router IPv6 predefinito Duo 

#### <a name="nxd_ipv6_default_router_add"></a>nxd_ipv6_default_router_add

**Icona** ![ di Icona di aggiunta del router predefinito Duo I P v 6](./media/user-guide/netx-events/image61.png)

**Descrizione**

Questo evento rappresenta l'aggiunta di un router predefinito alla tabella di routing IPv6 dell'istanza IP tramite nxd_ipv6_default_router_add.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Informazioni sul campo 2: indirizzo di rete di destinazione.
- Informazioni sul campo 3: informazioni sulla durata.
- Campo informazioni 4: non utilizzato.

### <a name="duo-ipv6-default-router-delete"></a>Eliminazione router default IPv6 Duo 

#### <a name="nxd_ipv6_default_router_delete"></a>nxd_ipv6_default_router_delete

**Icona** ![ di Icona di eliminazione del router predefinito Duo I P v 6](./media/user-guide/netx-events/image62.png)

**Descrizione**

Questo evento rappresenta la rimozione di un router predefinito dalla tabella di routing IPv6 dell'istanza IP tramite nxd_ipv6_default_router_delete.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo IPv6 del router predefinito.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="duo-ipv6-enable"></a>Abilitazione IPv6 Duo 

#### <a name="nxd_ipv6_enable"></a>nxd_ipv6_enable

**Icona** ![ di Icona abilitazione Duo I P v 6](./media/user-guide/netx-events/image63.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di servizi IPv6 sull'istanza IP fornita tramite nxd_ipv6_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-ipv6-global-address-get"></a>Indirizzo globale IPv6 Duo Get 

#### <a name="nxd_ipv6_global_address_get"></a>nxd_ipv6_global_address_get

**Icona** ![ di Icona Get indirizzo globale Duo I P v 6](./media/user-guide/netx-events/image64.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP globale (primario) nell'istanza IP situata in corrispondenza dell'indice 1 nella tabella dell'interfaccia dell'istanza IP tramite nxd_ipv6_global_address_get.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo globale
- Informazioni sul campo 3: lunghezza del prefisso dell'indirizzo IPv6.
- Campo informazioni 4: indice nella tabella dell'interfaccia IP (1).

### <a name="duo-ipv6-global-address-set"></a>Set di indirizzi globali IPv6 Duo 

#### <a name="nxd_ipv6_global_address_set"></a>nxd_ipv6_global_address_set

**Icona** ![ di Icona del set di indirizzi globale Duo I P v 6](./media/user-guide/netx-events/image65.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP globale (primario) nell'istanza IP presente in corrispondenza dell'indice 1 nella tabella dell'interfaccia dell'istanza IP tramite nxd_ipv6_global_address_set.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: quarta parola (meno significativa) dell'indirizzo globale
- Informazioni campo 3: lunghezza prefisso indirizzo IPv6
- Campo informazioni 4: indice nella tabella dell'interfaccia IP (1)

### <a name="duo-ipv6-initiate-dad-process"></a>Processo padre di avvio IPv6 Duo 

#### <a name="nxd_ipv6_initiate_dad_process"></a>nxd_ipv6_initiate_dad_process

**Icona** ![ di Icona del processo padre di avvio Duo I P v 6](./media/user-guide/netx-events/image66.png)

**Descrizione**

Questo evento rappresenta l'inizio del processo di rilevamento degli indirizzi duplicati (DAD) quando all'istanza IP viene assegnato un indirizzo di collegamento locale o di interfaccia IP tramite nxd_ipv6_initiate_dad_process.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-ipv6-interface-address-get"></a>Indirizzo dell'interfaccia IPv6 Duo Get 

#### <a name="nxd_ipv6_interface_address_get"></a>nxd_ipv6_interface_address_get

**Icona** ![ di Icona di Get dell'indirizzo dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image67.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP e del prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'interfaccia dell'istanza IP tramite nxd_ipv6_interface_address_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo IPv6 da restituire
- Informazioni sul campo 4: Indice dell'interfaccia nella tabella dell'interfaccia dell'istanza IP

### <a name="duo-ipv6-interface-address-set"></a>Set di indirizzi dell'interfaccia IPv6 Duo 

### <a name="nxd_ipv6_interface_address_set"></a>nxd_ipv6_interface_address_set

**Icona** ![ di Icona degli indirizzi dell'interfaccia Duo I P v 6](./media/user-guide/netx-events/image68.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP e del prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'interfaccia dell'istanza IP. Non consentito in corrispondenza dell'indice zero (indirizzo locale collegamento) tramite nxd_ipv6_interface_address_set.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo IPv6 da restituire
- Informazioni sul campo 3: lunghezza del prefisso
- Informazioni sul campo 4: Indice dell'interfaccia nella tabella dell'interfaccia dell'istanza IP

### <a name="duo-ipv6-link-local-address-get"></a>Indirizzo locale del collegamento IPv6 Duo Get 

#### <a name="nxd_ipv6_linklocal_address_get"></a>nxd_ipv6_linklocal_address_get

**Icona** ![ di Icona di Get dell'indirizzo locale del collegamento Duo I P v 6](./media/user-guide/netx-events/image69.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo locale del collegamento dell'istanza IP specificata tramite nxd_ipv6_linklocal_address_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: quarta parola (meno significativa) dell'indirizzo locale del collegamento IP V6
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-ipv6-link-local-address-set"></a>Set di indirizzi locali collegamento IPv6 Duo 

#### <a name="nxd_ipv6_linklocal_address_set"></a>nxd_ipv6_linklocal_address_set

**Icona** ![ di Icona del set di indirizzi locali di collegamento I P v 6](./media/user-guide/netx-events/image70.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo locale del collegamento dell'istanza IP tramite nxd_ipv6_linklocal_address_set.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: quarta (meno significativa) parola dell'indirizzo locale del collegamento IPv6
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-ipv6-raw-packet-send"></a>Invio pacchetti non elaborati IPv6 Duo 

#### <a name="nxd_ipv6_raw_packet_send"></a>nxd_ipv6_raw_packet_send

**Icona** ![ di Icona di invio di pacchetti non elaborati Duo I P v 6](./media/user-guide/netx-events/image71.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto IP non elaborato tramite l'interfaccia IP primaria alla destinazione specificare tramite nxd_ip_raw_packet_send.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto da inviare
- Informazioni sul campo 3: indirizzo IP di destinazione
- Campo informazioni 4: non usato

### <a name="duo-tcp-socket-peer-info-get"></a>Informazioni Get peer socket TCP Duo 

#### <a name="nxd_tcp_socket_peer_info_get"></a>nxd_tcp_socket_peer_info_get

**Icona** ![ di Icona Get per le informazioni su peer di Duo T C P](./media/user-guide/netx-events/image72.png)

**Descrizione**

Questo evento estrae i dati del mittente da un pacchetto TCP ricevuto sul socket specificato. Restituisce l'indirizzo IP e la porta del mittente.

**Campi informazioni**

- Campo informazioni 1: puntatore socket
- Informazioni sul campo 2: indirizzo IP peer
- Informazioni sul campo 3: porta peer
- Info Field 4: il lease significativo 32 bit dell'indirizzo IP

### <a name="duo-tcp-socket-set-interface"></a>Interfaccia del set di socket TCP Duo 

#### <a name="nxd_tcp_socket_set_interface"></a>nxd_tcp_socket_set_interface

**Icona** ![ di Icona dell'interfaccia del set di socket T C P Duo](./media/user-guide/netx-events/image73.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'interfaccia socket in uscita dopo che un client si connette con un server TCP nell'indirizzo IP del server specificato tramite nxd_tcp_client_socket_connect.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al socket TCP
- Informazioni sul campo 2: ID interfaccia
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-udp-socket-send"></a>Invio socket UDP Duo 

#### <a name="nxd_udp_socket_send"></a>nxd_udp_socket_send

**Icona** ![ di Icona di invio del socket Duo U D P](./media/user-guide/netx-events/image74.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto UDP tramite il socket specificato con l'indirizzo IP e la porta di input tramite nxd_udp_socket_send.

**Campi informazioni** 

- Informazioni sul campo 1: socket UDP puntatore
- Informazioni sul campo 2: puntatore al pacchetto UDP
- Informazioni sul campo 3: lunghezza del pacchetto
- Campo informazioni 4: non usato


### <a name="duo-udp-socket-set-interface"></a>Interfaccia del set di socket UDP Duo 

#### <a name="nxd_udp_socket_set_interface"></a>nxd_udp_socket_set_interface

**Icona** ![ di Icona dell'interfaccia del set di socket U D P Duo](./media/user-guide/netx-events/image75.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'interfaccia in uscita del socket UDP specificato sull'interfaccia corrispondente all'ID dell'interfaccia di input tramite nxd_udp_socket_set_interface.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al socket UDP
- Informazioni sul campo 2: ID interfaccia
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="duo-udp-source-extract"></a>Estrazione origine UDP Duo 

#### <a name="nxd_udp_socket_extract"></a>nxd_udp_socket_extract

**Icona** ![ di Icona estrazione origine Duo U D P](./media/user-guide/netx-events/image76.png)

**Descrizione**

Questo evento rappresenta l'estrazione dell'indirizzo IP e della porta di origine di un pacchetto ricevuto (IPv4 o IPv6). Se IPv6, la quarta parola (meno significativa) dell'indirizzo IP viene restituita tramite nxd_udp_source_extract.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: versione IP
- Informazioni sul campo 3: indirizzo IP di origine (IPv4 o IPv6)
- Campo dati 4: porta di origine

### <a name="icmp-enable"></a>Abilita ICMP 

#### <a name="nx_icmp_enable"></a>nx_icmp_enable

**Icona** ![ di Icona di abilitazione I C M P](./media/user-guide/netx-events/image77.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di ICMP tramite nx_icmp_enable.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP l;
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="icmp-information-get"></a>Informazioni sul protocollo ICMP Get 

#### <a name="nx_icmp_info_get"></a>nx_icmp_info_get

**Icona** ![ di Icona di Get di informazioni C M P](./media/user-guide/netx-events/image78.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_icmp_info_get.

**Campi informazioni**
- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: ping inviati
- Informazioni sul campo 3: ping risposte
- Campo dati 4: ping ricevuti

### <a name="icmp-ping"></a>Ping ICMP 

#### <a name="nx_icmp_ping"></a>nx_icmp_ping

**Icona** ![ di Icona ping I C M P](./media/user-guide/netx-events/image79.png)

**Descrizione**

Questo evento rappresenta il ping di un indirizzo IP di destinazione tramite nx_icmp_ping.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Informazioni sul campo 3: puntatore ai dati
- Informazioni sul campo 4: dimensioni dei dati

### <a name="igmp-enable"></a>Abilitazione IGMP 

#### <a name="nx_icmp_enable"></a>nx_icmp_enable

**Icona** ![ di Icona di abilitazione I G M P](./media/user-guide/netx-events/image80.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di IGMP tramite nx_igmp_enable.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="igmp-information-get"></a>Get informazioni IGMP 

#### <a name="nx_icmp_info_get"></a>nx_icmp_info_get

**Icona** ![ di Icona di informazioni Get di I G M P](./media/user-guide/netx-events/image81.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_igmp_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: report inviati
- Campo informazioni 3: query ricevute
- Campo informazioni 4: gruppi aggiunti

### <a name="igmp-loopback-disable"></a>Disabilita loopback loopback 

#### <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable

**Icona** ![ di Icona di disabilitazione loopback di I G M P](./media/user-guide/netx-events/image82.png)

**Descrizione**

Questo evento rappresenta la disabilitazione del loopback IGMP tramite nx_igmp_loopback_disable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="igmp-loopback-enable"></a>Abilita loopback loopback 

#### <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable

**Icona** ![ di Icona Abilita loopback I G M P](./media/user-guide/netx-events/image83.png)

**Descrizione**

Questo evento rappresenta l'abilitazione del loopback IGMP tramite nx_igmp_loopback_enable.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="igmp-multicast-join"></a>Join multicast IGMP 

#### <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join

**Icona** ![ di Icona di join multicast I G M P](./media/user-guide/netx-events/image84.png)

**Descrizione**

Questo evento rappresenta l'Unione di un gruppo multicast tramite nx_igmp_multicast_join.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP del gruppo
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="igmp-multicast-leave"></a>Uscita multicast IGMP 

#### <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave

**Icona** ![ di Icona di uscita multicast I G M P](./media/user-guide/netx-events/image85.png)

**Descrizione**

Questo evento rappresenta l'uscita da un gruppo multicast tramite nx_igmp_multicast_leave.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP del gruppo
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-address-change-notify"></a>Notifica di modifica degli indirizzi IP 

#### <a name="nx_ip_address_change_notify"></a>nx_ip_address_change_notify

**Icona** ![ di Icona di notifica della modifica dell'indirizzo I P](./media/user-guide/netx-events/image86.png)

**Descrizione**

Questo evento rappresenta la registrazione per la notifica di modifica IP tramite nx_ip_address_change_notify.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore alla funzione di callback
- Campo informazioni 3: puntatore a informazioni aggiuntive
- Campo informazioni 4: non usato

### <a name="ip-address-get"></a>Indirizzo IP Get 

#### <a name="nx_ip_address_get"></a>nx_ip_address_get

**Icona** ![ di Icona Ottieni indirizzo I P](./media/user-guide/netx-events/image87.png)

**Descrizione**

Questo evento rappresenta l'ottenimento dell'indirizzo IP tramite nx_ip_address_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Informazioni sul campo 3: Network mask
- Campo informazioni 4: non usato

### <a name="ip-address-set"></a>Set di indirizzi IP 

#### <a name="nx_ip_address_set"></a>nx_ip_address_set

**Icona** ![ di Icona del set di indirizzi I P](./media/user-guide/netx-events/image88.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP tramite nx_ip_address_set.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Informazioni sul campo 3: Network mask
- Campo informazioni 4: non usato

### <a name="ip-create"></a>Creazione IP 

#### <a name="nx_ip_create"></a>nx_ip_create

**Icona** ![ di Icona di creazione P](./media/user-guide/netx-events/image89.png)

**Descrizione**

Questo evento rappresenta la creazione di un'istanza IP tramite nx_ip_create.

**Campi informazioni** 
- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: indirizzo IP
- Informazioni sul campo 3: Network mask
- Informazioni sul campo 4: puntatore al pool di pacchetti predefinito

### <a name="ip-delete"></a>Eliminazione IP 

#### <a name="nx_ip_delete"></a>nx_ip_delete

**Icona** ![ di Icona di eliminazione I P](./media/user-guide/netx-events/image90.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un'istanza IP tramite nx_ip_delete.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-driver-direct-command"></a>Comando Direct driver IP 

#### <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command

**Icona** ![ di Icona comando diretto driver I P](./media/user-guide/netx-events/image91.png)

**Descrizione**

Questo evento rappresenta un comando di driver I/O diretto tramite nx_ip_driver_direct_command.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: comando driver
- Informazioni campo 3: valore restituito
- Campo informazioni 4: non usato

### <a name="ip-forwarding-disable"></a>Disabilitazione dell'invio IP 

#### <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable

**Icona** ![ di Icona di disabilitazione dell'invio P](./media/user-guide/netx-events/image92.png)

**Descrizione**

Questo evento rappresenta la disabilitazione dell'invio IP tramite nx_ip_forwarding_disable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-forwarding-enable"></a>Abilitazione dell'invio IP 

#### <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable

**Icona** ![ di Icona Abilita l'invio P](./media/user-guide/netx-events/image93.png)

**Descrizione**

Questo evento rappresenta l'abilitazione dell'invio IP tramite nx_ip_forwarding_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-fragment-disable"></a>Disabilitazione frammenti IP 

#### <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable

**Icona** ![ di Icona di disabilitazione del frammento I P](./media/user-guide/netx-events/image94.png)

**Descrizione**

Questo evento rappresenta la disabilitazione della frammentazione IP tramite nx_ip_fragment_disable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-fragment-enable"></a>Abilitazione frammenti IP 

#### <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable

**Icona** ![ di Icona Abilita frammento I P](./media/user-guide/netx-events/image95.png)

**Descrizione**

Questo evento rappresenta l'abilitazione della frammentazione IP tramite nx_ip_fragment_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-gateway-address-set"></a>Set di indirizzi IP gateway 

#### <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set

**Icona** ![ di Icona del set di indirizzi del gateway I P](./media/user-guide/netx-events/image96.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'indirizzo IP del gateway tramite nx_ip_gateway_address_set.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP del gateway
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-information-get"></a>Informazioni IP Get 

#### <a name="nx_ip_info_get"></a>nx_ip_info_get

**Icona** ![ di Icona di Get delle informazioni P](./media/user-guide/netx-events/image97.png)

**Descrizione** di Questo evento rappresenta l'acquisizione di informazioni IP tramite nx_ip_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: byte IP inviati
- Campo informazioni 3: byte IP ricevuti
- Campo dati 4: pacchetti IP eliminati

### <a name="ip-interface-attach"></a>Connessione interfaccia IP 

#### <a name="nx_interface_attach"></a>nx_interface_attach

**Icona** ![ di Icona di connessione Iterface P](./media/user-guide/netx-events/image98.png)

**Descrizione**

Questo evento rappresenta un'interfaccia di rete secondaria da collegare all'istanza IP tramite nx_ip_interface_attach.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP dell'interfaccia
- Campo informazioni 3: indice nella tabella dell'interfaccia IP
- Campo informazioni 4: non usato

### <a name="ip-interface-info-get"></a>Informazioni sull'interfaccia IP Get 

#### <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get

**Icona** ![ di Icona di informazioni sull'interfaccia IP Get](./media/user-guide/netx-events/image99.png)

**Descrizione**

Questo evento rappresenta le informazioni recuperate dall'interfaccia di rete specificata tramite nx_ip_interface_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo IP dell'interfaccia
- Informazioni sul campo 3: indirizzo MAC dell'interfaccia MSB
- Informazioni campo 4: indirizzo MAC interfaccia lsb

### <a name="ip-raw-packet-disable"></a>Disabilitazione pacchetto non elaborato IP 

#### <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable

**Icona** ![ di Icona di disabilitazione pacchetti non elaborati](./media/user-guide/netx-events/image100.png)

**Descrizione**

Questo evento rappresenta la disabilitazione della comunicazione di pacchetti IP non elaborati tramite nx_ip_raw_packet_disable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-raw-packet-enable"></a>Abilitazione pacchetti non elaborati IP 

#### <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable

**Icona** ![ di Icona di abilitazione di pacchetti non elaborati](./media/user-guide/netx-events/image101.png)

**Descrizione**

Questo evento rappresenta l'abilitazione della comunicazione di pacchetti IP non elaborati tramite nx_ip_raw_packet_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="ip-raw-packet-receive"></a>Ricezione pacchetti non elaborati IP 

#### <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive

**Icona** ![ di Icona di ricezione di pacchetti non elaborati](./media/user-guide/netx-events/image102.png)

**Descrizione**

Questo evento rappresenta la ricezione di un pacchetto IP non elaborato tramite nx_ip_raw_packet_receive.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: wait-opzione
- Campo informazioni 4: non usato

### <a name="ip-raw-packet-send"></a>Invio pacchetti non elaborati IP 

#### <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send

**Icona** ![ di Icona di invio di pacchetti non elaborati](./media/user-guide/netx-events/image103.png)

**Descrizione**

Questo evento rappresenta l'invio di un pacchetto IP non elaborato tramite nx_ip_raw_packet_send.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: indirizzo IP di destinazione
- Informazioni sul campo 4: tipo di servizio

### <a name="ip-static-route-add"></a>Aggiunta route statica IP 

#### <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add

**Icona** ![ di Icona di aggiunta statica route I P](./media/user-guide/netx-events/image104.png)

**Descrizione**

Questo evento rappresenta una route statica da aggiungere alla tabella di routing dell'istanza IP tramite nx_ip_static_route_add.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo di rete
- Informazioni sul campo 3: Network mask
- Campo informazioni 4: hop successivo

### <a name="ip-static-route-delete"></a>Eliminazione route statica IP 

#### <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete

**Icona** ![ di Icona di eliminazione statica di I P](./media/user-guide/netx-events/image105.png)

**Descrizione**

Questo evento rappresenta una route statica che viene rimossa dalla tabella di routing dell'istanza IP tramite nx_ip_static_route_delete.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: indirizzo di rete
- Informazioni sul campo 3: Network mask
- Campo informazioni 4: non usato

### <a name="ip-status-check"></a>Verifica stato IP 

#### <a name="nx_ip_status_check"></a>nx_ip_status_check

**Icona** ![ di Icona di controllo stato I P](./media/user-guide/netx-events/image106.png)

**Descrizione**

Questo evento rappresenta il controllo dello stato IP tramite nx_ip_status_check.

Campi informazioni 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: stato richiesto
- Campo informazioni 3: stato effettivo
- Informazioni sul campo 4: Wait (opzione)

### <a name="ipsec-enable"></a>Abilita IPSEC 

#### <a name="nx_ipsec_enable"></a>nx_ipsec_enable

**Icona** ![ di Icona Enable i P S E C](./media/user-guide/netx-events/image107.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di servizi IPSec nell'istanza IP fornita tramite nx_ipsec_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="packet-allocate"></a>Allocazione pacchetti 

#### <a name="nx_packet_allocate"></a>nx_packet_allocate

**Icona** ![ di Icona di allocazione pacchetti](./media/user-guide/netx-events/image108.png)

**Descrizione**

Questo evento rappresenta l'allocazione di un pacchetto tramite nx_packet_allocate.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pool di pacchetti
- Informazioni sul campo 2: puntatore al pacchetto allocato
- Campo informazioni 3: tipo di pacchetto
- Campo dati 4: pacchetti disponibili

### <a name="packet-copy"></a>Copia pacchetti 

#### <a name="nx_packet_copy"></a>nx_packet_copy

**Icona** ![ di Icona di CPY del pacchetto](./media/user-guide/netx-events/image109.png)

**Descrizione**

Questo evento rappresenta la copia di un pacchetto tramite nx_packet_copy.

**Campi informazioni**

- Campo informazioni 2: nuovo puntatore al pacchetto
- Informazioni sul campo 3: puntatore al pool di pacchetti
- Informazioni sul campo 4: Wait (opzione)

### <a name="packet-data-append"></a>Accodamento dati pacchetto 

#### <a name="nx_packet_data_append"></a>nx_packet_data_append

**Icona** ![ di Icona Accodamento dati pacchetto](./media/user-guide/netx-events/image110.png)

**Descrizione**

Questo evento rappresenta l'accodamento dei dati a un pacchetto tramite nx_packet_data_append.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: puntatore ai dati
- Informazioni sul campo 3: dimensioni dei dati
- Informazioni sul campo 4: puntatore al pool di pacchetti

### <a name="packet-data-extract-offset"></a>Offset estrazione dati pacchetto 

#### <a name="nx_udp_source_extract_offset"></a>nx_udp_source_extract_offset

**Icona** ![ di Icona di offset estrazione dati pacchetto](./media/user-guide/netx-events/image111.png)

**Descrizione**

Questo evento rappresenta i dati dei pacchetti estratti in un buffer fornito da un pacchetto tramite nx_udp_source_extract_offset.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: dimensioni del buffer specificato
- Campo informazioni 3: numero di byte copiati
- Campo informazioni 4: non usato

### <a name="packet-data-retrieve"></a>Recupero dati pacchetto 

#### <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve

**Icona** ![ di Icona recupero dati pacchetto](./media/user-guide/netx-events/image112.png)

**Descrizione**

Questo evento rappresenta il recupero di dati da un pacchetto tramite nx_packet_data_retrieve.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: puntatore all'inizio del buffer
- Campo info 3: byte copiati
- Campo informazioni 4: non usato

### <a name="packet-length-get"></a>Lunghezza pacchetto Get 

#### <a name="nx_packet_length_get"></a>nx_packet_length_get

**Icona** ![ di Icona Ottieni lunghezza pacchetto](./media/user-guide/netx-events/image113.png)

**Descrizione**

Questo evento rappresenta il recupero della lunghezza di un pacchetto tramite nx_packet_length_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: lunghezza del pacchetto
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="packet-pool-create"></a>Creazione pool di pacchetti 

#### <a name="nx_packet_pool_create"></a>nx_packet_pool_create

**Icona** ![ di Icona di creazione pool di pacchetti](./media/user-guide/netx-events/image114.png)

**Descrizione**

Questo evento rappresenta la creazione di un pool di pacchetti tramite nx_packet_pool_create.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al pool di pacchetti
- Informazioni sul campo 2: dimensioni del payload del pacchetto
- Informazioni sul campo 3: puntatore all'area di memoria del pool
- Informazioni campo 4: dimensioni dell'area di memoria del pool

### <a name="packet-pool-delete"></a>Eliminazione pool di pacchetti 

#### <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete

**Icona** ![ di Icona di eliminazione del pool di pacchetti](./media/user-guide/netx-events/image115.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un pool di pacchetti tramite nx_packet_pool_delete.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al pool di pacchetti
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

#### <a name="packet-pool-information-get"></a>Ottenere informazioni sul pool di pacchetti 

#### <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get

**Icona** ![ di Icona Ottieni informazioni sul pool di pacchetti](./media/user-guide/netx-events/image116.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sul pool di pacchetti tramite nx_packet_pool_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pool di pacchetti
- Campo informazioni 2: totale pacchetti
- Informazioni sul campo 3: pacchetti disponibili
- Campo informazioni 4: richieste vuote

### <a name="packet-release"></a>Versione pacchetto 

#### <a name="nx_packet_data_release"></a>nx_packet_data_release

**Icona** ![ di Icona versione pacchetto](./media/user-guide/netx-events/image117.png)

**Descrizione**

Questo evento rappresenta il rilascio di un pacchetto tramite nx_packet_release.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: stato del pacchetto
- Informazioni sul campo 3: pacchetti disponibili
- Campo informazioni 4: non usato

### <a name="packet-transmit-release"></a>Versione di trasmissione pacchetti 

#### <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release

**Icona** ![ di Icona della versione di trasmissione pacchetti](./media/user-guide/netx-events/image118.png)

**Descrizione**

Questo evento rappresenta il rilascio di un pacchetto di trasmissione tramite nx_packet_transmit_release.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Informazioni sul campo 2: stato del pacchetto
- Informazioni sul campo 3: pacchetti disponibili
- Campo informazioni 4: non usato

### <a name="rarp-disable"></a>Disabilitazione RARP 

#### <a name="nx_rarp_disable"></a>nx_rarp_disable

**Icona** ![ di Icona di disabilitazione r P](./media/user-guide/netx-events/image119.png)

**Descrizione**

Questo evento rappresenta la disabilitazione di RARP tramite nx_rarp_disable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="rarp-enable"></a>Abilitazione di RARP 

#### <a name="nx_rarp_enable"></a>nx_rarp_enable

**Icona** ![ di Icona di abilitazione r A r P](./media/user-guide/netx-events/image120.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di RARP tramite nx_rarp_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="rarp-information-get"></a>Informazioni su RARP Get 

#### <a name="nx_rarp_info_get"></a>nx_rarp_info_get

**Icona** ![ di Icona di r A r P Information Get](./media/user-guide/netx-events/image121.png)

**Descrizione**

Questo evento rappresenta l'acquisizione di informazioni RARP tramite nx_rarp_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: richieste inviate
- Informazioni sul campo 3: risposte ricevute
- Campo informazioni 4: risposte non valide

### <a name="system-initialize"></a>Inizializzazione sistema 

#### <a name="nx_system_initialize"></a>nx_system_initialize

**Icona** ![ di Icona Inizializzazione sistema](./media/user-guide/netx-events/image122.png)

**Descrizione**

Questo evento rappresenta l'inizializzazione di NetX tramite nx_system_initialize.

**Campi informazioni**

- Campo informazioni 1: non usato
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="tcp-client-socket-bind"></a>Binding socket client TCP 

#### <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind

**Icona** ![ di Icona di Binding socket client T P](./media/user-guide/netx-events/image123.png)

**Descrizione**

Questo evento rappresenta l'associazione di un socket client a una porta tramite nx_tcp_client_socket_bind.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: porta richiesta
- Informazioni sul campo 4: Wait (opzione)

### <a name="tcp-client-socket-connect"></a>Connessione socket client TCP 

#### <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect

**Icona** ![ di Icona di connessione socket client T C P](./media/user-guide/netx-events/image124.png)

**Descrizione**

Questo evento rappresenta la creazione di una connessione socket client tramite nx_tcp_client_socket_connect.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: indirizzo IP del server
- Campo informazioni 4: porta server richiesta

### <a name="tcp-client-socket-port-get"></a>Porta socket client TCP Get 

#### <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get

**Icona** ![ di Icona di Get della porta del socket client T C P](./media/user-guide/netx-events/image125.png)

**Descrizione**

Questo evento rappresenta il recupero del numero di porta del socket client tramite nx_tcp_client_socket_port_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: numero di porta
- Campo informazioni 4: non usato

### <a name="tcp-client-socket-unbind"></a>Disassociazione socket client TCP 

#### <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind

**Icona** ![ di Icona di disassociazione socket client T C P](./media/user-guide/netx-events/image126.png)

**Descrizione**

Questo evento rappresenta l'annullamento dell'associazione della porta associata al socket tramite nx_tcp_client_socket_unbind.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="tcp-enable"></a>Abilitazione TCP 

#### <a name="nx_tcp_enable"></a>nx_tcp_enable

**Icona** ![ di Icona di abilitazione di T C P](./media/user-guide/netx-events/image127.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di TCP tramite nx_tcp_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

###  <a name="tcp-free-port-find-tcp-free-port-find"></a>Porta TCP gratuita-trova porta TCP gratuita 

#### <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find

**Icona** ![ di Icona trova porta libera di T CP](./media/user-guide/netx-events/image128.png)

**Descrizione**

Questo evento rappresenta la ricerca di una porta TCP gratuita tramite nx_tcp_free_port_find.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni campo 2: avvio del numero di porta di ricerca
- Campo informazioni 3: numero di porta disponibile
- Campo informazioni 4: non usato

###  <a name="tcp-infomation-get"></a>TCP opuscolo Get 

#### <a name="nx_tcp_info_get"></a>nx_tcp_info_get

**Icona** ![ di Icona di Get delle informazioni di T C P](./media/user-guide/netx-events/image129.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni TCP per l'istanza IP specificata tramite nx_tcp_info_get.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: numero di byte inviati
- Campo informazioni 3: numero di byte ricevuti
- Campo informazioni 4: numero di pacchetti non validi

###  <a name="tcp-server-socket-accept"></a>Accettazione socket server TCP 

#### <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept

**Icona** ![ di Icona di accettazione socket server T C P](./media/user-guide/netx-events/image130.png)

**Descrizione**

Questo evento rappresenta la configurazione del socket del server dopo la ricezione di una richiesta di connessione attiva tramite nx_tcp_server_socket_accept.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: wait-opzione
- Informazioni sul campo 4: stato socket

###  <a name="tcp-server-socket-listen"></a>Ascolto socket server TCP 

#### <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen

**Icona** ![ di Icona lsten socket server T C P](./media/user-guide/netx-events/image131.png)

**Descrizione**

Questo evento rappresenta la registrazione di una richiesta di ascolto e un socket server per la porta TCP specificata tramite nx_tcp_server_socket_listen.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: numero di porta TCP
- Informazioni sul campo 3: puntatore al socket
- Campo dati 4: numero massimo di connessioni che possono essere accodate

###  <a name="tcp-server-socket-relisten"></a>Socket server TCP rielenco 

#### <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten

**Icona** ![ di Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image132.png)

**Descrizione**

Questo evento rappresenta la registrazione di un altro socket server per una richiesta di ascolto esistente sulla porta TCP specificata tramite nx_tcp_server_socket_relisten.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: numero di porta TCP
- Informazioni sul campo 3: puntatore al socket
- Informazioni sul campo 4: stato socket

###  <a name="tcp-server-socket-unaccept"></a>Socket server TCP non accettato 

#### <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept

**Icona** ![ di Icona di unaccept socket server T C P](./media/user-guide/netx-events/image133.png)

**Descrizione**

Questo evento rappresenta la rimozione del socket del server dall'associazione alla porta che riceve una connessione passiva precedente tramite nx_tcp_server_socket_unaccept.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: stato socket
- Campo informazioni 4: non usato

###  <a name="tcp-server-socket-unlisten-tcp-server-socket-unlisten"></a>Il socket del server TCP non è in elenco 

#### <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten

**Icona** ![ di Icona dell'elenco dei socket del server T C P](./media/user-guide/netx-events/image134.png)

**Descrizione**

Questo evento rappresenta la rimozione di una richiesta di ascolto precedente per la porta TCP specificata tramite nx_tcp_server_socket_unlisten.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: numero di porta TCP
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="tcp-socket-bytes-available"></a>Byte socket TCP disponibili 

#### <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available

**Icona** ![ di Icona di byte socket a T C P disponibile](./media/user-guide/netx-events/image135.png)

**Descrizione**

Questo evento rappresenta il numero di byte attualmente disponibili nel socket di ricezione TCP specificato tramite nx_tcp_socket_bytes_available.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket TCP
- Campo info 3: byte ricevuti sul socket
- Campo informazioni 4: non usato

### <a name="tcp-socket-create"></a>Creazione socket TCP 

#### <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create

**Icona** ![ di Icona di creazione socket T C P](./media/user-guide/netx-events/image136.png)

**Descrizione**

Questo evento rappresenta la creazione di un socket TCP tramite nx_tcp_socket_create.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: tipo di servizio
- Informazioni sul campo 4: dimensioni della finestra di ricezione

### <a name="tcp-socket-delete"></a>Eliminazione socket TCP 

#### <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete

**Icona** ![ di Icona di eliminazione Socket T C P](./media/user-guide/netx-events/image137.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un socket tramite nx_tcp_socket_delete.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: stato socket
- Campo informazioni 4: non usato

### <a name="tcp-socket-disconnect"></a>Connessione socket TCP 

#### <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect

**Icona** ![ di Icona di disconnessione Socket T C P](./media/user-guide/netx-events/image138.png)

**Descrizione**

Questo evento rappresenta la disconnessione di un socket tramite nx_tcp_socket_disconnect.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: wait-opzione
- Informazioni sul campo 4: stato socket

### <a name="tcp-socket-information-get"></a>Informazioni sul socket TCP Get 

#### <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get

**Icona** ![ di Icona di Get delle informazioni sul socket T C P](./media/user-guide/netx-events/image139.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un socket tramite nx_tcp_socket_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: byte inviati tramite questo socket
- Campo dati 4: byte ricevuti tramite questo socket

### <a name="tcp-socket-mss-get"></a>Socket TCP MSS Get 

#### <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get

**Icona** ![ di Icona di Get del socket T C P s](./media/user-guide/netx-events/image140.png)

**Descrizione**

Questo evento rappresenta il recupero della MSS del socket tramite nx_tcp_socket_mss_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni campo 3: dimensioni massime segmento (MSS)
- Informazioni sul campo 4: stato socket

### <a name="tcp-socket-mss-peer-get"></a>Peer Get MSS socket TCP 

#### <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get

**Icona** ![ di Icona di peer Get di T C P Socket M S](./media/user-guide/netx-events/image141.png)

**Descrizione**

Questo evento rappresenta il recupero del valore MSS del peer del socket tramite nx_tcp_socket_mss_peer_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: MSS del peer
- Informazioni sul campo 4: stato socket

### <a name="tcp-socket-mss-set"></a>Set MSS socket TCP 

#### <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set

**Icona** ![ di Icona set di socket M S T s](./media/user-guide/netx-events/image142.png)

**Descrizione**

Questo evento rappresenta l'impostazione di un MSS del socket tramite nx_tcp_socket_mss_set.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo informazioni 3: MSS
- Informazioni sul campo 4: stato socket

### <a name="tcp-socket-peer-info-get"></a>Get informazioni peer socket TCP 

#### <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get

**Icona** ![ di Icona di Get delle informazioni peer del socket T C P](./media/user-guide/netx-events/image143.png)

**Descrizione**

Questo evento rappresenta le informazioni recuperate dal socket TCP per quanto concerne il peer, ad esempio >connessione host, l'indirizzo IP e la porta tramite nx_tcp_socket_peer_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al socket TCP
- Informazioni sul campo 2: indirizzo IP peer
- Informazioni sul campo 3: numero di porta peer
- Campo informazioni 4: non usato

### <a name="tcp-socket-receive"></a>Ricezione socket TCP 

#### <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive

**Icona** ![ di Icona di ricezione Socket T C P](./media/user-guide/netx-events/image144.png)

**Descrizione**

Questo evento rappresenta la ricezione di dati da un socket tramite nx_tcp_socket_receive.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al socket
- Informazioni sul campo 2: puntatore al pacchetto ricevuto
- Informazioni campo 3: lunghezza pacchetto ricevuta
- Campo dati 4: numero di sequenza di ricezione

### <a name="tcp-socket-receive-notify"></a>Ricezione notifica socket TCP 

#### <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify

**Icona** ![ di Icona di ricezione della notifica socket T C P](./media/user-guide/netx-events/image145.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback di notifica di ricezione per un socket tramite nx_tcp_socket_receive_notify.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore a Receive Notify info callback campo 4: non utilizzato

### <a name="tcp-socket-send"></a>Invio socket TCP 

#### <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send

**Icona** ![ di Icona di invio socket T C P](./media/user-guide/netx-events/image146.png)

**Descrizione**

Questo evento rappresenta l'invio di dati in un socket tramite nx_tcp_socket_send.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al socket
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: lunghezza del pacchetto
- Campo informazioni 4: numero di sequenza di trasmissione

### <a name="tcp-socket-state-wait"></a>Attesa stato socket TCP 

#### <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait

**Icona** ![ di Icona di attesa stato Socket T C P](./media/user-guide/netx-events/image147.png)

**Descrizione**

Questo evento rappresenta l'attesa di un socket per l'immissione di un determinato stato tramite nx_tcp_socket_state_wait.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: stato socket desiderato
- Informazioni sul campo 4: stato del socket precedente

### <a name="tcp-socket-transmit-configure"></a>Configurazione trasmissione socket TCP 

#### <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure

**Icona** ![ di Icona di configurazione di trasmissione Socket T C P](./media/user-guide/netx-events/image148.png)

**Descrizione**

Questo evento rappresenta la configurazione delle opzioni di trasmissione per un socket tramite nx_tcp_socket_transmit_configure.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: profondità della coda di trasmissione
- Informazioni campo 4: valore di timeout

### <a name="tcp-socket-window-update-notify-set"></a>Set di notifiche aggiornamento finestra socket TCP 

#### <a name="nx_tcp_window_update_notify_set"></a>nx_tcp_window_update_notify_set

**Icona** ![ di Icona del set di notifiche di aggiornamento della finestra socket di T C P](./media/user-guide/netx-events/image149.png)

**Descrizione**

Questo evento rappresenta un socket TCP che riceve la notifica di un aumento nella finestra di ricezione dell'host remoto tramite nx_tcp_window_update_notify_set.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al socket TCP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="udp-enable"></a>Abilita UDP 

#### <a name="nx_udp_enable"></a>nx_udp_enable

**Icona** ![ di Icona di abilitazione di U D P](./media/user-guide/netx-events/image150.png)

**Descrizione**

Questo evento rappresenta l'abilitazione di UDP tramite nx_udp_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="udp-free-port-find"></a>Ricerca porta gratuita UDP 

#### <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find

**Icona** ![ di Icona trova porta gratuita U D P](./media/user-guide/netx-events/image151.png)

**Descrizione**

Questo evento rappresenta la ricerca di una porta UDP gratuita tramite nx_udp_free_port_find.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: avvio della porta da cui eseguire la ricerca
- Informazioni sul campo 3: porta gratuita
- Campo informazioni 4: non usato

### <a name="udp-information-get"></a>Get informazioni UDP 

#### <a name="nx_udp_info_get"></a>nx_udp_info_get

**Icona** ![ di Icona di Get delle informazioni di U D P](./media/user-guide/netx-events/image152.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni tramite nx_udp_info_get.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Campo informazioni 2: byte UDP inviati
- Campo informazioni 3: byte UDP ricevuti
- Campo dati 4: pacchetti non validi

### <a name="udp-socket-bind"></a>Binding socket UDP 

#### <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind

**Icona** ![ di Icona di Binding socket U D P](./media/user-guide/netx-events/image153.png)

**Descrizione**

Questo evento rappresenta l'associazione di un socket UDP a una porta tramite nx_udp_socket_bind.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: numero di porta
- Informazioni sul campo 4: Wait (opzione)

### <a name="udp-socket-bytes-available"></a>Byte socket UDP disponibili 

#### <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available

**Icona** ![ di Icona di byte socket U D P disponibile](./media/user-guide/netx-events/image154.png)

**Descrizione**

Questo evento rappresenta il numero corrente di byte ricevuti sul socket UDP tramite nx_udp_socket_bytes_available.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: byte ricevuti sul socket
- Campo informazioni 4: non usato

### <a name="udp-socket-checksum-disable"></a>Disabilita checksum socket UDP 

#### <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable

**Icona** ![ di Icona di disabilitazione checksum socket U D P](./media/user-guide/netx-events/image155.png)

**Descrizione**

Questo evento rappresenta la disabilitazione del checksum per i dati in un socket UDP tramite nx_udp_socket_checksum_disable.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="udp-socket-checksum-enable"></a>Abilita checksum socket UDP 

#### <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable

**Icona** ![ di Icona Abilita checksum socket U D P](./media/user-guide/netx-events/image156.png)

**Descrizione**

Questo evento rappresenta l'abilitazione dell'elaborazione di checksum su un socket tramite nx_udp_socket_checksum_enable.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="udp-socket-create"></a>Creazione socket UDP 

#### <a name="nx_udp_socket_create"></a>nx_udp_socket_create

**Icona** ![ di Icona di creazione socket U D P](./media/user-guide/netx-events/image157.png)

**Descrizione**

Questo evento rappresenta la creazione di un socket UDP tramite nx_udp_socket_create.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: tipo di servizio
- Campo informazioni 4: coda di ricezione massima

### <a name="udp-socket-delete-event"></a>Evento di eliminazione socket UDP 

#### <a name="nx_udp_socket_delete-event"></a>evento nx_udp_socket_delete

**Icona** ![ di Icona dell'evento di eliminazione socket U D P](./media/user-guide/netx-events/image158.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un socket UDP tramite nx_udp_socket_delete.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="udp-socket-information-get-event"></a>Evento di Get delle informazioni sul socket UDP 

#### <a name="nx_udp_socket_info_get-event"></a>evento nx_udp_socket_info_get

**Icona** ![ di Icona dell'evento Get delle informazioni sul socket U D P](./media/user-guide/netx-events/image159.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un socket UDP tramite nx_udp_socket_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Campo info 3: byte inviati tramite socket
- Campo dati 4: byte ricevuti tramite socket

### <a name="udp-socket-interface-set"></a>Set di interfacce socket UDP 

#### <a name="nx_udp_socket_interface_set-event"></a>evento nx_udp_socket_interface_set

**Icona** ![ di Icona del set di interfacce socket U D P](./media/user-guide/netx-events/image160.png)

**Descrizione**

Questo evento rappresenta l'impostazione dell'interfaccia in uscita del socket UDP specificato con l'interfaccia specificata tramite nx_udp_socket_interface_set.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al socket UDP
- Campo informazioni 2: indice corrispondente all'interfaccia per il socket
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="udp-socket-port-get"></a>Porta socket UDP Get 

#### <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get

**Icona** ![ di Icona di Get della porta socket U D P](./media/user-guide/netx-events/image161.png)

**Descrizione**

Questo evento rappresenta il recupero della porta UDP a cui è associato il socket UDP specificato tramite nx_udp_socket_port_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket UDP
- Informazioni sul campo 3: numero di porta
- Campo informazioni 4: non usato

### <a name="udp-socket-receive"></a>Ricezione socket UDP 

#### <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive

**Icona** ![ di Icona di ricezione socket U D P](./media/user-guide/netx-events/image162.png)

**Descrizione**

Questo evento rappresenta la ricezione di dati sul socket UDP specificato tramite nx_udp_socket_receive.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket UDP
- Informazioni sul campo 3: puntatore al pacchetto ricevuto
- Informazioni sul campo 4: dimensioni del pacchetto ricevute

### <a name="udp-socket-receive-notify"></a>Ricezione notifica socket UDP 

#### <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify

**Icona** ![ di Descrizione icona di ricezione di un socket U D P ](./media/user-guide/netx-events/image163.png) 

Questo evento rappresenta la registrazione di un callback di notifica di ricezione tramite nx_udp_socket_receive_notify.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: puntatore a Receive Notify Function info Field 4: not used

### <a name="udp-socket-send"></a>Invio socket UDP 

#### <a name="nx_udp_socket_send"></a>nx_udp_socket_send

**Icona** ![ di Icona di invio socket U D P](./media/user-guide/netx-events/image164.png)

**Descrizione**

Questo evento rappresenta l'invio di dati tramite un socket UDP tramite nx_udp_socket_send.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al socket
- Informazioni sul campo 2: puntatore al pacchetto
- Informazioni sul campo 3: lunghezza del pacchetto
- Campo dati 4: indirizzo IP di destinazione

### <a name="udp-socket-unbind"></a>Disassociazione socket UDP 

#### <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind

**Icona** ![ di Icona di disassociazione socket U D P](./media/user-guide/netx-events/image165.png)

**Descrizione**

Questo evento rappresenta l'annullamento dell'associazione di una porta UDP con un socket tramite nx_udp_socket_unbind.

**Campi informazioni**

- Informazioni sul campo 1: puntatore all'istanza IP
- Informazioni sul campo 2: puntatore al socket
- Informazioni sul campo 3: numero di porta
- Campo informazioni 4: non usato

### <a name="udp-source-extract"></a>Estrazione origine UDP 

#### <a name="nx_udp_socket_create"></a>nx_udp_socket_create

**Icona** ![ di Icona estrazione origine U D P](./media/user-guide/netx-events/image166.png)

**Descrizione**

Questo evento rappresenta il recupero dell'indirizzo IP e del numero di porta di un pacchetto UDP ricevuto tramite nx_udp_source_extract.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al pacchetto
- Campo informazioni 2: indirizzo IP del mittente
- Informazioni campo 3: numero di porta del mittente
- Campo informazioni 4: non usato