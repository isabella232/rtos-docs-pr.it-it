---
title: Appendice D-Azure RTO NetX BSD-Compatible socket API
description: Informazioni sull'API socket BSD-Compatible per IPv4.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9062e27d8f447ac8d36e7a09afee5ac14f86f8c3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822802"
---
# <a name="appendix-d---azure-rtos-netx-bsd-compatible-socket-api"></a>Appendice D-Azure RTO NetX BSD-Compatible socket API

## <a name="bsd-compatible-socket-api"></a>API socket BSD-Compatible

L'API socket BSD-Compatible supporta un subset delle chiamate all'API di socket BSD (con alcune limitazioni) usando le primitive NetX di Azure RTO sotto. Sono supportati i protocolli IPv4 e l'indirizzamento di rete. Questo livello API di BSD-Compatible Sockets deve essere eseguito come veloce o leggermente più veloce delle implementazioni BSD tipiche perché questa API usa le primitive NetX interne e ignora il controllo degli errori NetX non necessari.

Le opzioni configurabili consentono all'applicazione host di definire il numero massimo di socket, le dimensioni massime della finestra TCP e la profondità della coda di ascolto.

A causa di vincoli di prestazioni e di architettura, questa API di BSD-Compatible Sockets non supporta tutte le chiamate a socket BSD. Inoltre, non tutte le opzioni BSD sono disponibili per i servizi BSD, in particolare quanto segue:

- La funzione ***Select** _ funziona solo con _fd_set \* readfds *, altri argomenti in questa chiamata, ad esempio *writefds* e *exceptfds* , non sono supportati.
- L'argomento dei *flag int* non è supportato per le funzioni ***Send** _, _*_ricezione_*_, _*_SendTo_*_ e _ *_recvfrom_**. L'API socket BSD-Compatible supporta solo un set limitato di chiamate a socket BSD.

Il codice sorgente è progettato per semplicità ed è costituito solo da due file, ***nx_bsd. c** _ e _*_nx_bsd. h_*_. L'installazione richiede l'aggiunta di questi due file al progetto di compilazione (non la libreria NetX) e la creazione dell'applicazione host che utilizzerà le chiamate al servizio socket BSD. Il file _ *_nx_bsd. h_** deve anche essere incluso nell'origine dell'applicazione. I file demo di esempio sono inclusi nella distribuzione, disponibile gratuitamente con NetX. Ulteriori dettagli sono disponibili nella Guida BSD-Compatible API socket **417** e i file Leggimi inclusi nel pacchetto dell'api socket BSD-Compatible.

L'API di BSD-Compatible Sockets supporta le chiamate all'API di socket BSD seguenti:

```C
*INT bsd_initialize (NX_IP *default_ip, NX_PACKET_POOL *default_pool,
    CHAR *bsd_memory_not_used);*

*INT getpeername( INT sockID, struct sockaddr *remoteAddress, INT *addressLength);*

*INT getsockname( INT sockID, struct sockaddr *localAddress, INT *addressLength);*

*INT recvfrom(INT sockID, CHAR *buffer, INT buffersize,
    INT flags,struct sockaddr *fromAddr, INT *fromAddrLen);*

*INT recv(INT sockID, VOID *rcvBuffer, INT bufferLength, INT flags);*

*INT sendto(INT sockID, CHAR *msg, INT msgLength, INT flags,
    struct sockaddr *destAddr, INT destAddrLen);*

*INT send(INT sockID, const CHAR *msg, INT msgLength, INT flags);*

 *INT accept(INT sockID, struct sockaddr *ClientAddress, INT *addressLength);*

*INT listen(INT sockID, INT backlog);*

*INT bind (INT sockID, struct sockaddr *localAddress, INT addressLength);*

*INT connect(INT sockID, struct sockaddr *remoteAddress, INT addressLength);*

*INT socket( INT protocolFamily, INT type, INT protocol);*

*INT soc_close ( INT sockID);*

*INT select(INT nfds, fd_set *readfds, fd_set *writefds,
    fd_set *exceptfds, struct timeval *timeout);*

*VOID FD_SET(INT fd, fd_set *fdset);*

*VOID FD_CLR(INT fd, fd_set *fdset);*

*INT FD_ISSET(INT fd, fd_set *fdset);*

*VOID FD_ZERO(fd_set *fdset);*

```
