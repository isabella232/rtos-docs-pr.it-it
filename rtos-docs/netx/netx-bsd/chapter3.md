---
title: Capitolo 3-servizi BSD NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi di base di Azure RTO NetX BSD elencati di seguito in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9fe96f9896b76294a32543e9a4e0ae11da601ca6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821503"
---
# <a name="chapter-3---azure-rtos-netx-bsd-services"></a>Capitolo 3-servizi BSD NetX di Azure RTO

Questo capitolo contiene una descrizione di tutti i servizi di base di Azure RTO NetX BSD elencati di seguito in ordine alfabetico.

```c
INT accept(INT sockID, struct sockaddr *ClientAddress, INT *addressLength);

INT bind (INT sockID, struct sockaddr *localAddress, INT addressLength);

INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool, CHAR
                    *bsd_thread_stack_area, ULONG bsd_thread_stack_size,
                    *UINT bsd_thread_priority);

INT connect(INT sockID, struct sockaddr *remoteAddress, INT addressLength);

INT getpeername( INT sockID, struct sockaddr *remoteAddress, INT *addressLength);

INT getsockname( INT sockID, struct sockaddr *localAddress, INT *addressLength);

INT ioctl(INT sockID, INT command, INT *result);

in_addr_t inet_addr(const_CHAR *buffer);

INT inet_aton(const CHAR *cp_arg, struct in_addr *addr);

CHAR inet_ntoa(struct in_addr address_to_convert);

const CHAR *inet_ntop(INT af, const VOID *src, CHAR *dst, socklen_t size);

INT inet_pton(INT af, const CHAR *src, VOID *dst);

INT listen(INT sockID, INT backlog);

INT recvfrom(INT sockID, CHAR *buffer, INT buffersize, INT flags,
            struct sockaddr *fromAddr, INT *fromAddrLen);

INT recv(INT sockID, VOID *rcvBuffer, INT bufferLength, INT flags);
INT sendto(INT sockID, CHAR *msg, INT msgLength, INT flags,
            struct sockaddr *destAddr, INT destAddrLen);

INT send(INT sockID, const CHAR *msg, INT msgLength, INT flags);

INT select(INT nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds,
            struct timeval *timeout);

INT soc_close ( INT sockID);

INT socket( INT protocolFamily, INT type, INT protocol);

INT fcntl(INT sock_ID, UINT flag_type, UINT f_options);

INT getsockopt(INT sockID, INT option_level, INT option_name, VOID *option_value,
                INT *option_length);

INT setsockopt(INT sockID, INT option_level, INT option_name,
                const VOID *option_value, INT option_length);

INT getaddrinfo(const CHAR *node, const CHAR *service, const struct addrinfo *hints,
                struct addrinfo **res);

VOID freeaddrinfo(struct addrinfo *res);

INT getnameinfo(const struct sockaddr *sa, socklen_t salen, char *host,
                size_t hostlen, char *serv, size_t servlen, int flags);

VOID nx_bsd_set_service_list(struct NX_BSD_SERVICE_LIST *serv_list_ptr,
                            ULONG serv_list_len);

VOID FD_SET(INT fd, fd_set *fdset);

VOID FD_CLR(INT fd, fd_set *fdset);

INT FD_ISSET(INT fd, fd_set *fdset);

VOID FD_ZERO (fd_set *fdset);
```