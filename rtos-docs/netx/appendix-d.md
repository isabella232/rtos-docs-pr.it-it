---
title: Appendice D - AZURE RTOS API Socket BSD-Compatible NetX
description: Informazioni sull'API BSD-Compatible Socket per IPv4.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bd4a35c19cd794a5135f01abe5595456d39b5306ba25ce2966c3bb1aea14ea17
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790089"
---
# <a name="appendix-d---azure-rtos-netx-bsd-compatible-socket-api"></a>Appendice D - AZURE RTOS API Socket BSD-Compatible NetX

## <a name="bsd-compatible-socket-api"></a>API BSD-Compatible Socket

LBSD-Compatible API Socket supporta un subset delle chiamate API BSD Sockets (con alcune limitazioni) usando Azure RTOS primitive NetX sottostanti. Sono supportati i protocolli IPv4 e l'indirizzamento di rete. Questo BSD-Compatible api Sockets deve essere veloce o leggermente più veloce delle implementazioni BSD tipiche perché questa API usa primitive NetX interne e ignora il controllo degli errori NetX non necessari.

Le opzioni configurabili consentono all'applicazione host di definire il numero massimo di socket, le dimensioni massime della finestra TCP e la profondità della coda di attesa.

A causa dei vincoli di prestazioni e architettura, questa API BSD-Compatible Sockets non supporta tutte le chiamate BSD Sockets. Inoltre, non tutte le opzioni BSD sono disponibili per i servizi BSD, in particolare:

- La funzione ***select** _ funziona solo con _fd_set readfds*, gli altri argomenti in questa chiamata, ad esempio \* *writefds*, *exceptfds* non sono supportati.
- *L'argomento int flags* non è supportato per le funzioni ***send** _, _*_recv_*_, _*_sendto_*_ e _ *_recvfrom_**. LBSD-Compatible API Socket supporta solo un set limitato di chiamate socket BSD.

Il codice sorgente è progettato per semplicità ed è costituito solo da due **file,* nx_bsd.c** _ _*_e nx_bsd.h_*_. L'installazione richiede l'aggiunta di questi due file al progetto di compilazione (non la libreria NetX) e la creazione dell'applicazione host che userà le chiamate al servizio Socket BSD. Il file _ *_nx_bsd.h_** deve essere incluso anche nell'origine dell'applicazione. I file demo di esempio sono inclusi nella distribuzione disponibile gratuitamente con NetX. Altri dettagli sono disponibili nella Guida per l BSD-Compatible'API Socket **417** e i file Leggimi in bundle con il pacchetto dell'API socket BSD-Compatible Socket.

L'API BSD-Compatible Sockets supporta le chiamate API BSD Sockets seguenti:

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
