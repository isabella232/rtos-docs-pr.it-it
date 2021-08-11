---
title: Appendice A - Azure RTOS Servizi NetX
description: Esplorare i Azure RTOS NetX Services.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e2ec90a63fba9a3464a5984a005ce83abe410af387787c792b19314bcb6d27c5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784139"
---
# <a name="appendix-a---azure-rtos-netx-services"></a>Appendice A - Azure RTOS Servizi NetX

## <a name="address-resolution-protocol-arp"></a>ARP (Address Resolution Protocol)  

```c
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr, 
    ULONG ip_address, 
    ULONG physical_msw, 
    ULONG physical_lsw);
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory,
    ULONG arp_cache_size);
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler)(NX_IP *ip_ptr,NX_PACKET *packet_ptr));
UINT nx_arp_hardware_address_find(
    NX_IP *ip_ptr,
    ULONG ip_address, ULONG*physical_msw,
    ULONG *physical_lsw);
UINT nx_arp_info_get(
    NX_IP *ip_ptr, 
    ULONG *arp_requests_sent, 
    ULONG*arp_requests_received,
    ULONG *arp_responses_sent,
    ULONG*arp_responses_received,
    ULONG *arp_dynamic_entries,
    ULONG *arp_static_entries,
    ULONG *arp_aged_entries,
    ULONG *arp_invalid_messages);
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr,
    ULONG *ip_address, 
    ULONG physical_msw,
    ULONG physical_lsw);
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address, 
    ULONG physical_msw,
    ULONG physical_lsw);
```

## <a name="internet-control-message-protocol-icmp"></a>Internet Control Message Protocol (ICMP)  

```c
UINT nx_icmp_enable(NX_IP *ip_ptr);
UINT nx_icmp_info_get(
    NX_IP *ip_ptr, 
    ULONG *pings_sent,
    ULONG *ping_timeouts, 
    ULONG *ping_threads_suspended,
    ULONG *ping_responses_received,
    ULONG *icmp_checksum_errors,
     ULONG *icmp_unhandled_messages);
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data,
    ULONG data_size, 
    NX_PACKET **response_ptr, ULONG wait_option);
```

## <a name="internet-group-management-protocol-igmp"></a>IGMP (Internet Group Management Protocol)  

```c
UINT nx_igmp_enable(NX_IP *ip_ptr);
UINT nx_igmp_info_get(
    NX_IP *ip_ptr, 
    ULONG *igmp_reports_sent, 
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
UINT nx_igmp_loopback_disable(NX_IP *ip_ptr);
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address, 
    UINT interface_index);
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr,
    ULONG group_address);
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr,
    ULONG group_address);
```

## <a name="internet-protocol-ip"></a>Ip (Internet Protocol)  

```c
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID (*change_notify)(NX_IP *, VOID *),
    VOID *additional_info);
UINT nx_ip_address_get(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG *network_mask);
UINT nx_ip_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address,
    ULONG network_mask);
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name,
    ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr,
    ULONG memory_size, 
    UINT priority);
UINT nx_ip_delete(NX_IP *ip_ptr);
UINT nx_ip_driver_direct_command(
    NX_IP *ip_ptr,
    UINT command, 
    ULONG *return_value_ptr);
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG
    *return_value_ptr);
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
UINT nx_ip_gateway_address_set(NX_IP *ip_ptr,
    ULONG ip_address);
UINT nx_ip_info_get(NX_IP *ip_ptr,
    ULONG *ip_total_packets_sent,
    ULONG *ip_total_bytes_sent,
    ULONG *ip_total_packets_received,
    ULONG *ip_total_bytes_received,
    ULONG *ip_invalid_packets,
    ULONG *ip_receive_packets_dropped,
    ULONG *ip_receive_checksum_errors,
    ULONG *ip_send_packets_dropped,
    ULONG *ip_total_fragments_sent,
    ULONG *ip_total_fragments_received);
UINT nx_ip_interface_address_get(
    NX_IP *ip_ptr,
    ULONG interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    ULONG interface_index,
    ULONG ip_address, ULONG
    network_mask);
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr,
    CHAR* interface_name, 
    ULONG ip_address,
    ULONG network_mask,
    VOID (*ip_link_driver)(struct NX_IP_DRIVER_STRUCT *));
UINT nx_ip_interface_info_get(
    NX_IP *ip_ptr,
    UINT interface_index, 
    CHAR **interface_name,
    ULONG *ip_address,
    ULONG *network_mask, 
    ULONG *mtu_size,
    ULONG *physical_address_msw, 
    ULONG *physical_address_lsw);
UINT nx_ip_interface_status_check(
    NX_IP *ip_ptr,
    UINT interface_index, 
    ULONG needed_status,
    ULONG *actual_status, 
    ULONG wait_option);
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID (*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
UINT nx_ip_raw_packet_disable(NX_IP *ip_ptr);
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
UINT nx_ip_raw_packet_interface_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr, 
    ULONG destination_ip,
    UINT interface_index, 
    ULONG type_of_service);
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip, 
    ULONG type_of_service);
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask,
    ULONG next_hop);
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask);
UINT nx_ip_status_check(
    NX_IP *ip_ptr, 
    ULONG needed_status,
    ULONG *actual_status, 
    ULONG wait_option);
```

## <a name="packet-management"></a>Gestione pacchetti  

```c
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr, 
    ULONG packet_type,
    ULONG wait_option);
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr, 
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, 
    ULONG data_size,
    NX_PACKET_POOL *pool_ptr, 
    ULONG wait_option);
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset, 
    VOID *buffer_start,
    ULONG buffer_length, 
    ULONG *bytes_copied);
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start, 
    ULONG *bytes_copied);
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
UINT nx_packet_pool_create(
    NX_PACKET_POOL *pool_ptr,
    CHAR *name,
    ULONG block_size,
    VOID *memory_ptr,
    ULONG memory_size);
UINT nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
UINT nx_packet_pool_info_get(
    NX_PACKET_POOL *pool_ptr,
    ULONG *total_packets, 
    ULONG *free_packets,
    ULONG *empty_pool_requests,
    ULONG *empty_pool_suspensions,
    ULONG *invalid_packet_releases);
UINT nx_packet_release(NX_PACKET *packet_ptr);
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```

## <a name="reverse-address-resolution-protocol-rarp"></a>RaRP (Reverse Address Resolution Protocol)  

```c
UINT nx_rarp_disable(NX_IP *ip_ptr);
UINT nx_rarp_enable(NX_IP *ip_ptr);
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```

## <a name="system-management"></a>Gestione dei sistemi  

```c
VOID nx_system_initialize(VOID);
```

## <a name="transmission-control-protocol-tcp"></a>TCP (Transmission Control Protocol)  

```c
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port, ULONG wait_option);
UINT nx_tcp_client_socket_connect(NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip, UINT server_port,
    ULONG wait_option);
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
UINT nx_tcp_enable(NX_IP *ip_ptr);
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
UINT nx_tcp_info_get(
    NX_IP *ip_ptr, 
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent, 
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received, 
    ULONG *tcp_invalid_packets,
    ULONG *tcp_receive_packets_dropped,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_connections,
    ULONG *tcp_disconnections,
    ULONG *tcp_connections_dropped,
    ULONG*tcp_retransmit_packets);
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr,
    UINT port, NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*tcp_listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr,
    UINT port, 
    NX_TCP_SOCKET *socket_ptr);
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
UINT nx_tcp_server_socket_unlisten(NX_IP *ip_ptr, UINT port);
UINT nx_tcp_socket_bytes_available(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *bytes_available);
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr,
    NX_TCP_SOCKET *socket_ptr, 
    CHAR *name,
    ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*tcp_urgent_data_callback)(NX_TCP_SOCKET*socket_ptr),
    VOID (*tcp_disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID *tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)(NX_TCP_SOCKET *socket_ptr));
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback)(NX_TCP_SOCKET *socket_ptr));
UINT nx_tcp_socket_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *tcp_packets_sent, 
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received, 
    ULONG *tcp_bytes_received,
    ULONG *tcp_retransmit_packets, 
    ULONG *tcp_packets_queued,
    ULONG *tcp_checksum_errors, 
    ULONG *tcp_socket_state,
    ULONG *tcp_transmit_queue_depth, 
    ULONG *tcp_transmit_window,
    ULONG *tcp_receive_window);
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *peer_mss);
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address, 
    ULONG *peer_port);
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
N    X_PACKET **packet_ptr, 
    ULONG wait_option);
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_receive_notify)(NX_TCP_SOCKET *socket_ptr));
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG wait_option);
UINT nx_tcp_socket_state_wait(
    NX_TCP_SOCKET *socket_ptr,
    UINT desired_state, 
    ULONG wait_option);
UINT nx_tcp_socket_transmit_configure(
    NX_TCP_SOCKET *socket_ptr,
    ULONG max_queue_depth, 
    ULONG timeout,
    ULONG max_retries, 
    ULONG timeout_shift);
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_window_update_notify) (NX_TCP_SOCKET *socket_ptr));
```

## <a name="user-datagram-protocol-udp"></a>Udp (User Datagram Protocol)  

```c
UINT nx_udp_enable(NX_IP *ip_ptr);
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, UINT port,
    UINT *free_port_ptr);
UINT nx_udp_info_get(
    NX_IP *ip_ptr, 
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent, 
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_invalid_packets,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, 
    UINT *protocol, UINT *port,
    UINT *interface_index);
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr,
UINT port, ULONG wait_option);
UINT nx_udp_socket_bytes_available(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *bytes_available);
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
UINT nx_udp_socket_create(
    NX_IP *ip_ptr, 
    NX_UDP_SOCKET *socket_ptr,
    CHAR *name, 
    ULONG type_of_service,
    ULONG fragment,
    UINT time_to_live, 
    ULONG queue_maximum);
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
UINT nx_udp_socket_info_get(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *udp_packets_sent, 
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received, 
    ULONG *udp_bytes_received,
    ULONG *udp_packets_queued,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
UINT nx_udp_socket_interface_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG ip_address,
    UINT port, 
    UINT address_index);
UINT nx_udp_socket_port_get(
    NX_UDP_SOCKET *socket_ptr,
    UINT *port_ptr);
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)(NX_UDP_SOCKET *socket_ptr));
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG ip_address, 
    UINT port);
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, 
    UINT *port);
```
