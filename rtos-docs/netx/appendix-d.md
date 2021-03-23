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
# <a name="appendix-d---azure-rtos-netx-bsd-compatible-socket-api"></a><span data-ttu-id="78732-103">Appendice D-Azure RTO NetX BSD-Compatible socket API</span><span class="sxs-lookup"><span data-stu-id="78732-103">Appendix D - Azure RTOS NetX BSD-Compatible Socket API</span></span>

## <a name="bsd-compatible-socket-api"></a><span data-ttu-id="78732-104">API socket BSD-Compatible</span><span class="sxs-lookup"><span data-stu-id="78732-104">BSD-Compatible Socket API</span></span>

<span data-ttu-id="78732-105">L'API socket BSD-Compatible supporta un subset delle chiamate all'API di socket BSD (con alcune limitazioni) usando le primitive NetX di Azure RTO sotto.</span><span class="sxs-lookup"><span data-stu-id="78732-105">The BSD-Compatible Socket API supports a subset of the BSD Sockets API calls (with some limitations) by utilizing Azure RTOS NetX primitives underneath.</span></span> <span data-ttu-id="78732-106">Sono supportati i protocolli IPv4 e l'indirizzamento di rete.</span><span class="sxs-lookup"><span data-stu-id="78732-106">IPv4 protocols and network addressing are supported.</span></span> <span data-ttu-id="78732-107">Questo livello API di BSD-Compatible Sockets deve essere eseguito come veloce o leggermente più veloce delle implementazioni BSD tipiche perché questa API usa le primitive NetX interne e ignora il controllo degli errori NetX non necessari.</span><span class="sxs-lookup"><span data-stu-id="78732-107">This BSD-Compatible Sockets API layer should perform as fast or slightly faster than typical BSD implementations because this API utilizes internal NetX primitives and bypasses unnecessary NetX error checking.</span></span>

<span data-ttu-id="78732-108">Le opzioni configurabili consentono all'applicazione host di definire il numero massimo di socket, le dimensioni massime della finestra TCP e la profondità della coda di ascolto.</span><span class="sxs-lookup"><span data-stu-id="78732-108">Configurable options allow the host application to define the maximum number of sockets, TCP maximum window size, and depth of listen queue.</span></span>

<span data-ttu-id="78732-109">A causa di vincoli di prestazioni e di architettura, questa API di BSD-Compatible Sockets non supporta tutte le chiamate a socket BSD.</span><span class="sxs-lookup"><span data-stu-id="78732-109">Due to performance and architecture constraints, this BSD-Compatible Sockets API does not support all BSD Sockets calls.</span></span> <span data-ttu-id="78732-110">Inoltre, non tutte le opzioni BSD sono disponibili per i servizi BSD, in particolare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="78732-110">In addition, not all BSD options are available for the BSD services, specifically the following:</span></span>

- <span data-ttu-id="78732-111">La funzione \***Select** _ funziona solo con _fd_set \* readfds \*, altri argomenti in questa chiamata, ad esempio *writefds* e *exceptfds* , non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="78732-111">The ***select** _ function works with only _fd_set \*readfds*, other arguments in this call e.g., *writefds*, *exceptfds* are not supported.</span></span>
- <span data-ttu-id="78732-112">L'argomento dei *flag int* non è supportato per le funzioni ***Send** _, _*_ricezione_*_, _*_SendTo_\*_ e _ \*_recvfrom_\*\*.</span><span class="sxs-lookup"><span data-stu-id="78732-112">The *int flags* argument is not supported for the ***send** _, _*_recv_*_, _*_sendto,_*_ and _ *_recvfrom_** functions.</span></span> <span data-ttu-id="78732-113">L'API socket BSD-Compatible supporta solo un set limitato di chiamate a socket BSD.</span><span class="sxs-lookup"><span data-stu-id="78732-113">The BSD-Compatible Socket API supports only limited set of BSD Sockets calls.</span></span>

<span data-ttu-id="78732-114">Il codice sorgente è progettato per semplicità ed è costituito solo da due file, ***nx_bsd. c** _ e _*_nx_bsd. h_\*_.</span><span class="sxs-lookup"><span data-stu-id="78732-114">The source code is designed for simplicity and is comprised of only two files,***nx_bsd.c** _ and _*_nx_bsd.h_\*_.</span></span> <span data-ttu-id="78732-115">L'installazione richiede l'aggiunta di questi due file al progetto di compilazione (non la libreria NetX) e la creazione dell'applicazione host che utilizzerà le chiamate al servizio socket BSD.</span><span class="sxs-lookup"><span data-stu-id="78732-115">Installation requires adding these two files to the build project (not the NetX library) and creating the host application which will use BSD Socket service calls.</span></span> <span data-ttu-id="78732-116">Il file _ *_nx_bsd. h_*\* deve anche essere incluso nell'origine dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78732-116">The _ *_nx_bsd.h_*\* file must also be included in your application source.</span></span> <span data-ttu-id="78732-117">I file demo di esempio sono inclusi nella distribuzione, disponibile gratuitamente con NetX.</span><span class="sxs-lookup"><span data-stu-id="78732-117">Sample demo files are included with the distribution which is freely available with NetX.</span></span> <span data-ttu-id="78732-118">Ulteriori dettagli sono disponibili nella Guida BSD-Compatible API socket **417** e i file Leggimi inclusi nel pacchetto dell'api socket BSD-Compatible.</span><span class="sxs-lookup"><span data-stu-id="78732-118">Further details are available in the help BSD-Compatible Socket API **417** and Readme files bundled with the BSD-Compatible Socket API package.</span></span>

<span data-ttu-id="78732-119">L'API di BSD-Compatible Sockets supporta le chiamate all'API di socket BSD seguenti:</span><span class="sxs-lookup"><span data-stu-id="78732-119">The BSD-Compatible Sockets API supports the following BSD Sockets API calls:</span></span>

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
