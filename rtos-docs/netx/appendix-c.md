---
title: Appendice C-tipi di dati NetX di Azure RTO
description: Informazioni sui tipi di dati di Azure RTO NetX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d3b4a383270db7cfa85359e15c32adde7d45565f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821554"
---
# <a name="appendix-c---azure-rtos-netx-data-types"></a>Appendice C-tipi di dati NetX di Azure RTO

## <a name="nx_arp"></a>NX_ARP

```C
typedef struct NX_ARP_STRUCT
{
    UINT nx_arp_route_static;
    UINT nx_arp_entry_next_update;
    UINT nx_arp_retries;
    struct NX_ARP_STRUCT *nx_arp_pool_next,
    *nx_arp_pool_previous;
    struct NX_ARP_STRUCT *nx_arp_active_next,
    *nx_arp_active_previous,
    **nx_arp_active_list_head;
    ULONG nx_arp_ip_address;
    ULONG nx_arp_physical_address_msw;
    ULONG nx_arp_physical_address_lsw;
    struct NX_INTERFACE_STRUCT *nx_arp_ip_interface;
    struct NX_PACKET_STRUCT *nx_arp_packets_waiting;
}
```

## <a name="nx_interface"></a>NX_INTERFACE

```C
typedef struct NX_INTERFACE_STRUCT
{
    CHAR *nx_interface_name;
    UCHAR nx_interface_valid;
    UCHAR nx_interface_address_mapping_needed;
    UCHAR nx_interface_link_up;
    UCHAR nx_interface_link_status_change;
    struct NX_IP_STRUCT *nx_interface_ip_instance;
    ULONG nx_interface_physical_address_msw;
    ULONG nx_interface_physical_address_lsw;
    ULONG nx_interface_ip_address;
    ULONG nx_interface_ip_network_mask;
    ULONG nx_interface_ip_network;
    ULONG nx_interface_ip_mtu_size;
    VOID *nx_interface_additional_link_info;
    VOID (*nx_interface_link_driver_entry)
        (struct NX_IP_DRIVER_STRUCT *);
    ULONG nx_interface_arp_defend_timeout;
}
```

##  <a name="nx_ip"></a>NX_IP


```C
typedef struct NX_IP_STRUCT
{
    ULONG nx_ip_id;
    CHAR *nx_ip_name;
    #define nx_ip_address nx_ip_interface[0].nx_interface_ip_address
    #define nx_ip_driver_mtu nx_ip_interface[0].nx_interface_ip_mtu_size
    #define nx_ip_driver_mapping_needed nx_ip_interface[0].nx_interface_address_mapping_needed
    #define nx_ip_network_mask nx_ip_interface[0].nx_interface_ip_network_mask
    #define nx_ip_network nx_ip_interface[0].nx_interface_ip_network
    #define nx_ip_arp_physical_address_msw nx_ip_interface[0].nx_interface_physical_address_msw
    #define nx_ip_arp_physical_address_lsw nx_ip_interface[0].nx_interface_physical_address_lsw
    #define nx_ip_driver_link_up nx_ip_interface[0].nx_interface_link_up
    #define nx_ip_link_driver_entry nx_ip_interface[0].nx_interface_link_driver_entry
    #define nx_ip_additional_link_info nx_ip_interface[0].nx_interface_additional_link_info

    ULONG nx_ip_gateway_address;
    struct NX_INTERFACE_STRUCT *nx_ip_gateway_interface;
    ULONG nx_ip_total_packet_send_requests;
    ULONG nx_ip_total_packets_sent;
    ULONG nx_ip_total_bytes_sent;
    ULONG nx_ip_total_packets_received;
    ULONG nx_ip_total_packets_delivered;
    ULONG nx_ip_total_bytes_received;
    ULONG nx_ip_packets_forwarded;
    ULONG nx_ip_packets_reassembled;
    ULONG nx_ip_reassembly_failures;
    ULONG nx_ip_invalid_packets;
    ULONG nx_ip_invalid_transmit_packets;
    ULONG nx_ip_invalid_receive_address;
    ULONG nx_ip_unknown_protocols_received;
    ULONG nx_ip_transmit_resource_errors;
    ULONG nx_ip_transmit_no_route_errors;
    ULONG nx_ip_receive_packets_dropped;
    ULONG nx_ip_receive_checksum_errors;
    ULONG nx_ip_send_packets_dropped;
    ULONG nx_ip_total_fragment_requests;
    ULONG nx_ip_successful_fragment_requests;
    ULONG nx_ip_fragment_failures;
    ULONG nx_ip_total_fragments_sent;
    ULONG nx_ip_total_fragments_received;
    ULONG nx_ip_arp_requests_sent;
    ULONG nx_ip_arp_requests_received;
    ULONG nx_ip_arp_responses_sent;
    ULONG nx_ip_arp_responses_received;
    ULONG nx_ip_arp_aged_entries;
    ULONG nx_ip_arp_invalid_messages;
    ULONG nx_ip_arp_static_entries;
    ULONG nx_ip_udp_packets_sent;
    ULONG nx_ip_udp_bytes_sent;
    ULONG nx_ip_udp_packets_received;
    ULONG nx_ip_udp_bytes_received;
    ULONG nx_ip_udp_invalid_packets;
    ULONG nx_ip_udp_no_port_for_delivery;
    ULONG nx_ip_udp_receive_packets_dropped;
    ULONG nx_ip_udp_checksum_errors;
    ULONG nx_ip_tcp_packets_sent;
    ULONG nx_ip_tcp_bytes_sent;
    ULONG nx_ip_tcp_packets_received;
    ULONG nx_ip_tcp_bytes_received;
    ULONG nx_ip_tcp_invalid_packets;
    ULONG nx_ip_tcp_receive_packets_dropped;
    ULONG nx_ip_tcp_checksum_errors;
    ULONG nx_ip_tcp_connections;
    ULONG nx_ip_tcp_passive_connections;
    ULONG nx_ip_tcp_active_connections;
    ULONG nx_ip_tcp_disconnections;
    ULONG nx_ip_tcp_connections_dropped;
    ULONG nx_ip_tcp_retransmit_packets;
    ULONG nx_ip_tcp_resets_received;
    ULONG nx_ip_tcp_resets_sent;
    ULONG nx_ip_icmp_total_messages_received;
    ULONG nx_ip_icmp_checksum_errors;
    ULONG nx_ip_icmp_invalid_packets;
    ULONG nx_ip_icmp_unhandled_messages;
    ULONG nx_ip_pings_sent;
    ULONG nx_ip_ping_timeouts;
    ULONG nx_ip_ping_threads_suspended;
    ULONG nx_ip_ping_responses_received;
    ULONG nx_ip_pings_received;
    ULONG nx_ip_pings_responded_to;
    ULONG nx_ip_igmp_invalid_packets;
    ULONG nx_ip_igmp_reports_sent;
    ULONG nx_ip_igmp_queries_received;
    ULONG nx_ip_igmp_checksum_errors;
    ULONG nx_ip_igmp_groups_joined;

    #ifndef NX_DISABLE_IGMPV2
        ULONG nx_ip_igmp_router_version;
    #endif

    ULONG nx_ip_rarp_requests_sent;
    ULONG nx_ip_rarp_responses_received;
    ULONG nx_ip_rarp_invalid_messages;
    VOID (*nx_ip_forward_packet_process) (struct NX_IP_STRUCT *, NX_PACKET *);
    ULONG nx_ip_packet_id;
    struct NX_PACKET_POOL_STRUCT *nx_ip_default_packet_pool;
    TX_MUTEX nx_ip_protection;
    UINT nx_ip_initialize_done;
    NX_PACKET *nx_ip_driver_deferred_packet_head, *nx_ip_driver_deferred_packet_tail;
    VOID (*nx_ip_driver_deferred_packet_handler)(struct NX_IP_STRUCT *, NX_PACKET *);
    NX_PACKET *nx_ip_deferred_received_packet_head, *nx_ip_deferred_received_packet_tail;
    UINT (*nx_ip_raw_ip_processing)(struct NX_IP_STRUCT *, ULONG, NX_PACKET *);

    #ifdef NX_ENABLE_IP_RAW_PACKET_FILTER
    UINT (*nx_ip_raw_packet_filter)(struct NX_IP_STRUCT *, ULONG, NX_PACKET *);
    #endif /* NX_ENABLE_IP_RAW_PACKET_FILTER */

    NX_PACKET *nx_ip_raw_received_packet_head, *nx_ip_raw_received_packet_tail;
    ULONG nx_ip_raw_received_packet_count;
    ULONG nx_ip_raw_received_packet_max;
    TX_THREAD *nx_ip_raw_packet_suspension_list;
    ULONG nx_ip_raw_packet_suspended_count;
    TX_THREAD nx_ip_thread;
    TX_EVENT_FLAGS_GROUP nx_ip_events;
    TX_TIMER nx_ip_periodic_timer;
    VOID (*nx_ip_fragment_processing)(struct NX_IP_DRIVER_STRUCT *);
    VOID (*nx_ip_fragment_assembly)(struct NX_IP_STRUCT *);
    VOID (*nx_ip_fragment_timeout_check) (struct NX_IP_STRUCT *);
    NX_PACKET *nx_ip_timeout_fragment;
    NX_PACKET *nx_ip_received_fragment_head, *nx_ip_received_fragment_tail;
    NX_PACKET *nx_ip_fragment_assembly_head, *nx_ip_fragment_assembly_tail;
    VOID (*nx_ip_address_change_notify)(struct NX_IP_STRUCT *, VOID *);
    VOID *nx_ip_address_change_notify_additional_info;
    ULONG nx_ip_igmp_join_list[NX_MAX_MULTICAST_GROUPS];
    NX_INTERFACE *nx_ip_igmp_interfacejoin_list[NX_MAX_MULTICAST_GROUPS];
    ULONG nx_ip_igmp_join_count[NX_MAX_MULTICAST_GROUPS];
    ULONG nx_ip_igmp_update_time[NX_MAX_MULTICAST_GROUPS];
    UINT nx_ip_igmp_global_loopback_enable;
    ULONG nx_ip_igmp_group_loopback_enable[NX_MAX_MULTICAST_GROUPS]
        void (*nx_ip_igmp_packet_receive)(struct NX_IP_STRUCT *,
        struct NX_PACKET_STRUCT *);
    void (*nx_ip_igmp_periodic_processing) (struct NX_IP_STRUCT *);
    void (*nx_ip_igmp_queue_process)(struct NX_IP_STRUCT *);
    NX_PACKET *nx_ip_igmp_queue_head;
    ULONG nx_ip_icmp_sequence;
    void (*nx_ip_icmp_packet_receive)(struct NX_IP_STRUCT *,
        struct NX_PACKET_STRUCT *);
    void (*nx_ip_icmp_queue_process)(struct NX_IP_STRUCT *);
    NX_PACKET *nx_ip_icmp_queue_head;
    TX_THREAD *nx_ip_icmp_ping_suspension_list;
    ULONG nx_ip_icmp_ping_suspended_count;
    struct NX_UDP_SOCKET_STRUCT *nx_ip_udp_port_table[NX_UDP_PORT_TABLE_SIZE];
    struct NX_UDP_SOCKET_STRUCT *nx_ip_udp_created_sockets_ptr;
    ULONG nx_ip_udp_created_sockets_count;
    void (*nx_ip_udp_packet_receive)(struct NX_IP_STRUCT *,
        struct NX_PACKET_STRUCT *);
    UINT nx_ip_udp_port_search_start;
    struct NX_TCP_SOCKET_STRUCT *nx_ip_tcp_port_table[NX_TCP_PORT_TABLE_SIZE];
    struct NX_TCP_SOCKET_STRUCT *nx_ip_tcp_created_sockets_ptr;
    ULONG nx_ip_tcp_created_sockets_count;
    void (*nx_ip_tcp_packet_receive)(struct NX_IP_STRUCT *,
        struct NX_PACKET_STRUCT *);
    void (*nx_ip_tcp_periodic_processing)
        (struct NX_IP_STRUCT *);
    void (*nx_ip_tcp_fast_periodic_processing)(struct NX_IP_STRUCT *);
    void (*nx_ip_tcp_queue_process)(struct NX_IP_STRUCT *);
    NX_PACKET *nx_ip_tcp_queue_head, *nx_ip_tcp_queue_tail;
    ULONG nx_ip_tcp_received_packet_count;
    struct NX_TCP_LISTEN_STRUCT nx_ip_tcp_server_listen_reqs[NX_MAX_LISTEN_REQUESTS];
    struct NX_TCP_LISTEN_STRUCT *nx_ip_tcp_available_listen_requests;
    struct NX_TCP_LISTEN_STRUCT *nx_ip_tcp_active_listen_requests;
    UINT nx_ip_tcp_port_search_start;
    UINT nx_ip_fast_periodic_timer_created;
    TX_TIMER nx_ip_fast_periodic_timer;
    struct NX_ARP_STRUCT *nx_ip_arp_table[NX_ARP_TABLE_SIZE];
    struct NX_ARP_STRUCT *nx_ip_arp_static_list;
    struct NX_ARP_STRUCT *nx_ip_arp_dynamic_list;
    ULONG nx_ip_arp_dynamic_active_count;
    NX_PACKET *nx_ip_arp_deferred_received_packet_head,
        *nx_ip_arp_deferred_received_packet_tail;
    UINT (*nx_ip_arp_allocate)(struct NX_IP_STRUCT *, struct NX_ARP_STRUCT **, UINT);
    void (*nx_ip_arp_periodic_update)(struct NX_IP_STRUCT *);
    void (*nx_ip_arp_queue_process)(struct NX_IP_STRUCT *);
    void (*nx_ip_arp_packet_send)(struct NX_IP_STRUCT *, ULONG destination_ip,
        NX_INTERFACE     *nx_interface);
    void (*nx_ip_arp_gratuitous_response_handler)(struct NX_IP_STRUCT *, NX_PACKET *);
    void (*nx_ip_arp_collision_notify_response_handler) (void *);
    void *nx_ip_arp_collision_notify_parameter;
    ULONG nx_ip_arp_collision_notify_ip_address;
    struct NX_ARP_STRUCT *nx_ip_arp_cache_memory;
    ULONG nx_ip_arp_total_entries;
    void (*nx_ip_rarp_periodic_update)(struct NX_IP_STRUCT *);
    void (*nx_ip_rarp_queue_process)(struct NX_IP_STRUCT *);
    NX_PACKET *nx_ip_rarp_deferred_received_packet_head,
        *nx_ip_rarp_deferred_received_packet_tail;
    struct NX_IP_STRUCT *nx_ip_created_next, *nx_ip_created_previous;
    void *nx_ip_reserved_ptr;
    void (*nx_tcp_deferred_cleanup_check) (struct NX_IP_STRUCT *);
    NX_INTERFACE nx_ip_interface[NX_MAX_IP_INTERFACES];

    #ifdef NX_ENABLE_IP_STATIC_ROUTING
        NX_IP_ROUTING_ENTRY nx_ip_routing_table[NX_IP_ROUTING_TABLE_SIZE];
        ULONG nx_ip_routing_table_entry_count;
    #endif /* NX_ENABLE_IP_STATIC_ROUTING */

    VOID (*nx_ip_link_status_change_callback)(struct NX_IP_STRUCT *, UINT, UINT);

    #ifdef NX_ENABLE_IP_PACKET_FILTER
        UINT (*nx_ip_packet_filter)(VOID *, UINT);
    #endif /* NX_ENABLE_IP_PACKET_FILTER */
}
```

##  <a name="nx_ip_driver"></a>NX_IP_DRIVER

```C
typedef struct NX_IP_DRIVER_STRUCT
{
    UINT nx_ip_driver_command;
    UINT nx_ip_driver_status;
    ULONG nx_ip_driver_physical_address_msw;
    ULONG nx_ip_driver_physical_address_lsw;
    NX_PACKET *nx_ip_driver_packet;
    ULONG *nx_ip_driver_return_ptr;
    struct NX_IP_STRUCT *nx_ip_driver_ptr;
    NX_INTERFACE *nx_ip_driver_interface;
}
```

## <a name="nx_ip_routing_entry"></a>NX_IP_ROUTING_ENTRY


```C
typedef struct NX_IP_ROUTING_ENTRY_STRUCT
{
    ULONG nx_ip_routing_dest_ip;
    ULONG nx_ip_routing_net_mask;
    412 NetX User Guide
    User Guide
    ULONG nx_ip_routing_next_hop_address;
    NX_INTERFACE *nx_ip_routing_entry_ip_interface;
}
```

## <a name="nx_packet"></a>NX_PACKET

```C
typedef struct NX_PACKET_STRUCT
{
    struct NX_PACKET_POOL_STRUCT *nx_packet_pool_owner;
    struct NX_PACKET_STRUCT *nx_packet_queue_next;
    struct NX_PACKET_STRUCT *nx_packet_tcp_queue_next;
    struct NX_PACKET_STRUCT *nx_packet_next;
    struct NX_PACKET_STRUCT *nx_packet_last;
    struct NX_PACKET_STRUCT *nx_packet_fragment_next;
    ULONG nx_packet_length;
    struct NX_INTERFACE_STRUCT *nx_packet_ip_interface;
    ULONG nx_packet_next_hop_address;
    UCHAR *nx_packet_data_start;
    UCHAR *nx_packet_data_end;
    UCHAR *nx_packet_prepend_ptr;
    UCHAR *nx_packet_append_ptr;

    #ifdef NX_PACKET_HEADER_PAD
        ULONG nx_packet_pad[NX_PACKET_HEADER_PAD_SIZE];
    #endif
}
```

## <a name="nx_packet_pool"></a>NX_PACKET_POOL

```C
typedef struct NX_PACKET_POOL_STRUCT
{
    ULONG nx_packet_pool_id;
    CHAR *nx_packet_pool_name;
    ULONG nx_packet_pool_available;
    ULONG nx_packet_pool_total;
    ULONG nx_packet_pool_empty_requests;
    ULONG nx_packet_pool_empty_suspensions;
    ULONG nx_packet_pool_invalid_releases;
    struct NX_PACKET_STRUCT *nx_packet_pool_available_list;
    CHAR *nx_packet_pool_start;
    ULONG nx_packet_pool_size;
    ULONG nx_packet_pool_payload_size;
    TX_THREAD *nx_packet_pool_suspension_list;
    ULONG nx_packet_pool_suspended_count;
    struct NX_PACKET_POOL_STRUCT *nx_packet_pool_created_next,
    *nx_packet_pool_created_previous;
}
```

## <a name="nx_tcp_listen"></a>NX_TCP_LISTEN

```C
typedef struct NX_TCP_LISTEN_STRUCT
{
    UINT nx_tcp_listen_port;
    VOID (*nx_tcp_listen_callback)(NX_TCP_SOCKET *socket_ptr,
    UINT port);
    NX_TCP_SOCKET *nx_tcp_listen_socket_ptr;
    ULONG nx_tcp_listen_queue_maximum;
    ULONG nx_tcp_listen_queue_current;
    NX_PACKET *nx_tcp_listen_queue_head, *nx_tcp_listen_queue_tail;
    struct NX_TCP_LISTEN_STRUCT *nx_tcp_listen_next, *nx_tcp_listen_previous;
}
```

## <a name="nx_tcp_socket"></a>NX_TCP_SOCKET;

```C
typedef struct NX_TCP_SOCKET_STRUCT
{
    ULONG nx_tcp_socket_id;
    CHAR *nx_tcp_socket_name;
    UINT nx_tcp_socket_client_type;
    UINT nx_tcp_socket_port;
    ULONG nx_tcp_socket_mss;
    ULONG nx_tcp_socket_connect_ip;
    UINT nx_tcp_socket_connect_port;
    ULONG nx_tcp_socket_connect_mss;
    NetX Data Types 413
    struct NX_INTERFACE_STRUCT *nx_tcp_socket_connect_interface;
    ULONG nx_tcp_socket_next_hop_address;
    ULONG nx_tcp_socket_connect_mss2;
    ULONG nx_tcp_socket_tx_slow_start_threshold;
    UINT nx_tcp_socket_state;
    ULONG nx_tcp_socket_tx_sequence;
    ULONG nx_tcp_socket_rx_sequence;
    ULONG nx_tcp_socket_rx_sequence_acked;
    ULONG nx_tcp_socket_delayed_ack_timeout;
    ULONG nx_tcp_socket_fin_sequence;
    USHORT nx_tcp_socket_fin_received;
    ULONG nx_tcp_socket_tx_window_advertised;
    ULONG nx_tcp_socket_tx_window_congestion;
    ULONG nx_tcp_socket_tx_outstanding_bytes;
    ULONG nx_tcp_socket_tx_sequence_recover;
    ULONG nx_tcp_socket_previous_highest_ack;
    UCHAR nx_tcp_socket_fast_recovery;
    UCHAR nx_tcp_socket_reserved[3];
    ULONG nx_tcp_socket_ack_n_packet_counter;
    UINT nx_tcp_socket_duplicated_ack_received;
    ULONG nx_tcp_socket_rx_window_default;
    ULONG nx_tcp_socket_rx_window_current;
    ULONG nx_tcp_socket_rx_window_last_sent;
    ULONG nx_tcp_socket_packets_sent;
    ULONG nx_tcp_socket_bytes_sent;
    ULONG nx_tcp_socket_packets_received;
    ULONG nx_tcp_socket_bytes_received;
    ULONG nx_tcp_socket_retransmit_packets;
    ULONG nx_tcp_socket_checksum_errors;
    struct NX_IP_STRUCT *nx_tcp_socket_ip_ptr;
    ULONG nx_tcp_socket_type_of_service;
    UINT nx_tcp_socket_time_to_live;
    ULONG nx_tcp_socket_fragment_enable;
    ULONG nx_tcp_socket_receive_queue_count;
    NX_PACKET *nx_tcp_socket_receive_queue_head,
        *nx_tcp_socket_receive_queue_tail;
    ULONG nx_tcp_socket_transmit_queue_maximum;
    ULONG nx_tcp_socket_transmit_sent_count;
    NX_PACKET *nx_tcp_socket_transmit_sent_head,
        nx_tcp_socket_transmit_sent_tail;
    ULONG nx_tcp_socket_timeout;
    ULONG nx_tcp_socket_timeout_rate;
    ULONG nx_tcp_socket_timeout_retries;
    ULONG nx_tcp_socket_timeout_max_retries;
    ULONG nx_tcp_socket_timeout_shift;

    #ifdef NX_ENABLE_TCP_WINDOW_SCALING
        ULONG nx_tcp_socket_rx_window_maximum;
        ULONG nx_tcp_rcv_win_scale_value;
        ULONG nx_tcp_snd_win_scale_value;
    #endif /* NX_ENABLE_TCP_WINDOW_SCALING */

    ULONG nx_tcp_socket_keepalive_timeout;
    ULONG nx_tcp_socket_keepalive_retries;
    struct NX_TCP_SOCKET_STRUCT *nx_tcp_socket_bound_next,
        *nx_tcp_socket_bound_previous;
    TX_THREAD *nx_tcp_socket_bind_in_progress;
    TX_THREAD *nx_tcp_socket_receive_suspension_list;
    ULONG nx_tcp_socket_receive_suspended_count;
    TX_THREAD *nx_tcp_socket_transmit_suspension_list;
    ULONG nx_tcp_socket_transmit_suspended_count;
    TX_THREAD *nx_tcp_socket_connect_suspended_thread;
    TX_THREAD *nx_tcp_socket_disconnect_suspended_thread;
    TX_THREAD *nx_tcp_socket_bind_suspension_list;
    ULONG nx_tcp_socket_bind_suspended_count;
    struct NX_TCP_SOCKET_STRUCT *nx_tcp_socket_created_next,
        *nx_tcp_socket_created_previous;
    VOID (*nx_tcp_urgent_data_callback)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);

    #ifndef NX_DISABLE_EXTENDED_NOTIFY_SUPPORT
        UINT (*nx_tcp_socket_syn_received_notify)(struct NX_TCP_SOCKET_STRUCT *socket_ptr,
            NX_PACKET *packet_ptr);
        VOID (*nx_tcp_establish_notify)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);
        VOID (*nx_tcp_disconnect_complete_notify)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);
        VOID (*nx_tcp_timed_wait_callback)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);
    #endif
    VOID (*nx_tcp_disconnect_callback)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);
    VOID (*nx_tcp_receive_callback)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);
    VOID (*nx_tcp_socket_window_update_notify)(struct NX_TCP_SOCKET_STRUCT *socket_ptr);
    void *nx_tcp_socket_reserved_ptr;
    ULONG nx_tcp_socket_transmit_queue_maximum_default;
    UINT nx_tcp_socket_keepalive_enabled;
}
```

## <a name="nx_udp_socket"></a>NX_UDP_SOCKET

```C
typedef struct NX_UDP_SOCKET_STRUCT
{
    ULONG nx_udp_socket_id;
    CHAR *nx_udp_socket_name;
    UINT nx_udp_socket_port;
    struct NX_IP_STRUCT *nx_udp_socket_ip_ptr;
    ULONG nx_udp_socket_packets_sent;
    ULONG nx_udp_socket_bytes_sent;
    ULONG nx_udp_socket_packets_received;
    ULONG nx_udp_socket_bytes_received;
    ULONG nx_udp_socket_invalid_packets;
    ULONG nx_udp_socket_packets_dropped;
    ULONG nx_udp_socket_checksum_errors;
    ULONG nx_udp_socket_type_of_service;
    UINT nx_udp_socket_time_to_live;
    ULONG nx_udp_socket_fragment_enable;
    UINT nx_udp_socket_disable_checksum;
    ULONG nx_udp_socket_receive_count;
    ULONG nx_udp_socket_queue_maximum;
    NX_PACKET *nx_udp_socket_receive_head,
        *nx_udp_socket_receive_tail;
    struct NX_UDP_SOCKET_STRUCT *nx_udp_socket_bound_next,
        *nx_udp_socket_bound_previous;
    TX_THREAD *nx_udp_socket_bind_in_progress;
    TX_THREAD *nx_udp_socket_receive_suspension_list;
    ULONG nx_udp_socket_receive_suspended_count;
    TX_THREAD *nx_udp_socket_bind_suspension_list;
    ULONG nx_udp_socket_bind_suspended_count;
    struct NX_UDP_SOCKET_STRUCT *nx_udp_socket_created_next,
        *nx_udp_socket_created_previous;
    VOID (*nx_udp_receive_callback)(struct NX_UDP_SOCKET_STRUCT
    *socket_ptr);
    void *nx_udp_socket_reserved_ptr;
    struct NX_INTERFACE_STRUCT *nx_udp_socket_ip_interface;
}
```
