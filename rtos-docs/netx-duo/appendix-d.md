---
title: Appendice D-Azure RTO NetX Duo BSD-Compatible socket API
description: Informazioni sull'API socket BSD-Compatible per IPv4 e IPv6.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 82439184d9facb6ddcc08ce81bc51182d7f34429
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822136"
---
# <a name="appendix-d---azure-rtos-netx-duo-bsd-compatible-socket-api"></a>Appendice D-Azure RTO NetX Duo BSD-Compatible socket API

## <a name="bsd-compatible-socket-api"></a>API socket BSD-Compatible 
L'API socket BSD-Compatible supporta un subset delle chiamate all'API per i socket BSD (con alcune limitazioni) usando le &reg; primitive NETX duo sotto. Sono supportati sia i protocolli IPv6 che IPv4 e l'indirizzamento di rete. Questo livello API di BSD-Compatible Sockets deve essere eseguito come veloce o leggermente più veloce delle implementazioni BSD tipiche perché questa API USA primitive NetX Duo interne e ignora il controllo degli errori NetX non necessari.  

Le opzioni configurabili consentono all'applicazione host di definire il numero massimo di socket, le dimensioni massime della finestra TCP e la profondità della coda di ascolto.

A causa di vincoli di prestazioni e di architettura, questa API di BSD-Compatible Sockets non supporta tutte le chiamate a socket BSD. Inoltre, non tutte le opzioni BSD sono disponibili per i servizi BSD, in particolare quanto segue:

  - ***Select** _ Call funziona solo con fd_set \_ readfds, altri argomenti in questa chiamata, ad esempio writefds, exceptfds non sono supportati.
  - L'argomento "flag int" non è supportato per le chiamate ***Send** _, _*_ricezione_*_, _*_SendTo_*_ e _ *_recvfrom_**. 
  - L'API socket BSD-Compatible supporta solo un set limitato di chiamate a socket BSD.

Il codice sorgente è progettato per semplicità ed è costituito solo da due file, ***nxd_bsd. c** _ e _*_nxd_bsd. h_*_. L'installazione richiede l'aggiunta di questi due file al progetto di compilazione (non la libreria NetX) e la creazione dell'applicazione host che utilizzerà le chiamate al servizio socket BSD. Il file _ *_nxd_bsd. h_** deve anche essere incluso nell'origine dell'applicazione. I file demo di esempio per le applicazioni basate su IPv4 e IPv6 sono inclusi nella distribuzione, disponibile gratuitamente con NetX Duo. Ulteriori informazioni sono disponibili nella guida e nei file Leggimi inclusi nel pacchetto API socket BSDCompatible.

L'API di BSD-Compatible Sockets supporta le chiamate all'API di socket BSD seguenti:

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