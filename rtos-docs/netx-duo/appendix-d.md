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
# <a name="appendix-d---azure-rtos-netx-duo-bsd-compatible-socket-api"></a><span data-ttu-id="64d82-103">Appendice D-Azure RTO NetX Duo BSD-Compatible socket API</span><span class="sxs-lookup"><span data-stu-id="64d82-103">Appendix D - Azure RTOS NetX Duo BSD-Compatible Socket API</span></span>

## <a name="bsd-compatible-socket-api"></a><span data-ttu-id="64d82-104">API socket BSD-Compatible</span><span class="sxs-lookup"><span data-stu-id="64d82-104">BSD-Compatible Socket API</span></span> 
<span data-ttu-id="64d82-105">L'API socket BSD-Compatible supporta un subset delle chiamate all'API per i socket BSD (con alcune limitazioni) usando le &reg; primitive NETX duo sotto.</span><span class="sxs-lookup"><span data-stu-id="64d82-105">The BSD-Compatible Socket API supports a subset of the BSD Sockets API calls (with some limitations) by utilizing NetX Duo&reg; primitives underneath.</span></span> <span data-ttu-id="64d82-106">Sono supportati sia i protocolli IPv6 che IPv4 e l'indirizzamento di rete.</span><span class="sxs-lookup"><span data-stu-id="64d82-106">Both IPv6 and IPv4 protocols and network addressing are supported.</span></span> <span data-ttu-id="64d82-107">Questo livello API di BSD-Compatible Sockets deve essere eseguito come veloce o leggermente più veloce delle implementazioni BSD tipiche perché questa API USA primitive NetX Duo interne e ignora il controllo degli errori NetX non necessari.</span><span class="sxs-lookup"><span data-stu-id="64d82-107">This BSD-Compatible Sockets API layer should perform as fast or slightly faster than typical BSD implementations because this API utilizes internal NetX Duo primitives and bypasses unnecessary NetX error checking.</span></span>  

<span data-ttu-id="64d82-108">Le opzioni configurabili consentono all'applicazione host di definire il numero massimo di socket, le dimensioni massime della finestra TCP e la profondità della coda di ascolto.</span><span class="sxs-lookup"><span data-stu-id="64d82-108">Configurable options allow the host application to define the maximum number of sockets, TCP maximum window size, and depth of listen queue.</span></span>

<span data-ttu-id="64d82-109">A causa di vincoli di prestazioni e di architettura, questa API di BSD-Compatible Sockets non supporta tutte le chiamate a socket BSD.</span><span class="sxs-lookup"><span data-stu-id="64d82-109">Due to performance and architecture constraints, this BSD-Compatible Sockets API does not support all BSD Sockets calls.</span></span> <span data-ttu-id="64d82-110">Inoltre, non tutte le opzioni BSD sono disponibili per i servizi BSD, in particolare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="64d82-110">In addition, not all BSD options are available for the BSD services, specifically the following:</span></span>

  - <span data-ttu-id="64d82-111">\***Select** _ Call funziona solo con fd_set \_ readfds, altri argomenti in questa chiamata, ad esempio writefds, exceptfds non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="64d82-111">\***select** _ call works with only fd_set \_readfds, other arguments in this call e.g., writefds, exceptfds are not supported.</span></span>
  - <span data-ttu-id="64d82-112">L'argomento "flag int" non è supportato per le chiamate ***Send** _, _*_ricezione_*_, _*_SendTo_\*_ e _ \*_recvfrom_\*\*.</span><span class="sxs-lookup"><span data-stu-id="64d82-112">The "int flags" argument is not supported for ***send** _, _*_recv_*_, _*_sendto,_*_ and _ *_recvfrom_** calls.</span></span> 
  - <span data-ttu-id="64d82-113">L'API socket BSD-Compatible supporta solo un set limitato di chiamate a socket BSD.</span><span class="sxs-lookup"><span data-stu-id="64d82-113">The BSD-Compatible Socket API supports only limited set of BSD Sockets calls.</span></span>

<span data-ttu-id="64d82-114">Il codice sorgente è progettato per semplicità ed è costituito solo da due file, ***nxd_bsd. c** _ e _*_nxd_bsd. h_\*_.</span><span class="sxs-lookup"><span data-stu-id="64d82-114">The source code is designed for simplicity and is comprised of only two files, ***nxd_bsd.c** _ and _*_nxd_bsd.h_\*_.</span></span> <span data-ttu-id="64d82-115">L'installazione richiede l'aggiunta di questi due file al progetto di compilazione (non la libreria NetX) e la creazione dell'applicazione host che utilizzerà le chiamate al servizio socket BSD.</span><span class="sxs-lookup"><span data-stu-id="64d82-115">Installation requires adding these two files to the build project (not the NetX library) and creating the host application which will use BSD Socket service calls.</span></span> <span data-ttu-id="64d82-116">Il file _ *_nxd_bsd. h_*\* deve anche essere incluso nell'origine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="64d82-116">The _ *_nxd_bsd.h_*\* file must also be included in your application source.</span></span> <span data-ttu-id="64d82-117">I file demo di esempio per le applicazioni basate su IPv4 e IPv6 sono inclusi nella distribuzione, disponibile gratuitamente con NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="64d82-117">Sample demo files for both IPv4 and IPv6  based applications are included with the distribution which is freely available with NetX Duo.</span></span> <span data-ttu-id="64d82-118">Ulteriori informazioni sono disponibili nella guida e nei file Leggimi inclusi nel pacchetto API socket BSDCompatible.</span><span class="sxs-lookup"><span data-stu-id="64d82-118">Further details are available in the help and Readme files bundled with the BSDCompatible Socket API package.</span></span>

<span data-ttu-id="64d82-119">L'API di BSD-Compatible Sockets supporta le chiamate all'API di socket BSD seguenti:</span><span class="sxs-lookup"><span data-stu-id="64d82-119">The BSD-Compatible Sockets API supports the following BSD Sockets API calls:</span></span>

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