---
title: Appendice D - Azure RTOS NetX Duo BSD-Compatible Socket API
description: Informazioni sull'API BSD-Compatible Socket per IPv4 e IPv6.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cd43c3efa18dd76f6eb996c84091024f48ad65aa5839958066161080dc02127e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789749"
---
# <a name="appendix-d---azure-rtos-netx-duo-bsd-compatible-socket-api"></a>Appendice D - Azure RTOS NetX Duo BSD-Compatible Socket API

## <a name="bsd-compatible-socket-api"></a>API socket BSD-Compatible 
LBSD-Compatible API Socket supporta un subset delle chiamate API socket BSD (con alcune limitazioni) usando le primitive di NetX Duo &reg; sottostanti. Sono supportati sia i protocolli IPv6 che IPv4 e gli indirizzi di rete. Questo livello BSD-Compatible'API Sockets deve essere veloce o leggermente più veloce rispetto alle implementazioni BSD tipiche perché questa API usa primitive di NetX Duo interne e ignora il controllo degli errori NetX non necessario.  

Le opzioni configurabili consentono all'applicazione host di definire il numero massimo di socket, le dimensioni massime della finestra TCP e la profondità della coda di ascolto.

A causa dei vincoli di prestazioni e architettura, BSD-Compatible aPI Sockets non supporta tutte le chiamate BSD Sockets. Inoltre, non tutte le opzioni BSD sono disponibili per i servizi BSD, in particolare le seguenti:

  - ***select** _ call funziona solo con fd_set readfds, altri argomenti in questa chiamata, ad esempio \_ writefds, exceptfds non sono supportati.
  - L'argomento "int flags" non è supportato per le chiamate ***send** _, _*_recv_*_ _*_, sendto_*_ e _ *_recvfrom_**. 
  - LBSD-Compatible API Socket supporta solo un set limitato di chiamate socket BSD.

Il codice sorgente è progettato per semplicità ed è costituito solo da due file, ***nxd_bsd.c** _ _*_e nxd_bsd.h_*_. L'installazione richiede l'aggiunta di questi due file al progetto di compilazione (non alla libreria NetX) e la creazione dell'applicazione host che userà le chiamate al servizio socket BSD. Il file _ *_nxd_bsd.h_** deve essere incluso anche nell'origine dell'applicazione. I file demo di esempio per le applicazioni basate su IPv4 e IPv6 sono inclusi nella distribuzione disponibile gratuitamente con NetX Duo. Altri dettagli sono disponibili nella Guida e nei file Leggimi in bundle con il pacchetto API socket BSDCompatible.

LBSD-Compatible API Sockets supporta le chiamate API BSD Sockets seguenti:

```c
INT     bsd_initialize (NX_IP *default_ip, NX_PACKET_POOL *default_pool, CHAR
        *bsd_memory_not_used);
```
```c
INT     getpeername( INT sockID, struct sockaddr *remoteAddress, INT
        *addressLength);
```
```c
INT     getsockname( INT sockID, struct sockaddr *localAddress, INT *addressLength);
```
```c
INT     recvfrom(INT sockID, CHAR *buffer, INT buffersize, INT flags,struct sockaddr
        *fromAddr, INT *fromAddrLen);
```
```c        
INT     recv(INT sockID, VOID *rcvBuffer, INT bufferLength, INT flags);
```
```c
INT     sendto(INT sockID, CHAR *msg, INT msgLength, INT flags, struct sockaddr
        *destAddr, INT destAddrLen);
```
```c        
INT     send(INT sockID, const CHAR *msg, INT msgLength, INT flags);
```
```c
INT     accept(INT sockID, struct sockaddr *ClientAddress, INT *addressLength);
```
```c
INT     listen(INT sockID, INT backlog);
```
```c
INT     bind (INT sockID, struct sockaddr *localAddress, INT addressLength);
```
```c
INT     connect(INT sockID, struct sockaddr *remoteAddress, INT addressLength);
```
```c
INT     socket( INT protocolFamily, INT type, INT protocol);
```
```c
INT     soc_close ( INT sockID);
```
```c
INT     select(INT nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct
        timeval *timeout);
```
```c
VOID    FD_SET(INT fd, fd_set *fdset);
```
```c
VOID    FD_CLR(INT fd, fd_set *fdset);
```
```c
INT     FD_ISSET(INT fd, fd_set *fdset);
```
```c
VOID    FD_ZERO(fd_set *fdset);
```