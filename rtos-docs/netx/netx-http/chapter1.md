---
title: Capitolo 1-Introduzione a NetX HTTP
description: In questo documento viene illustrato come il protocollo HTTP è un protocollo progettato per il trasferimento di contenuto sul Web.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6137cc0d8deb753d784be844d5abc7778dd62295
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822622"
---
# <a name="chapter-1---introduction-to-netx-http"></a><span data-ttu-id="818e7-103">Capitolo 1-Introduzione a NetX HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-103">Chapter 1 - Introduction to NetX HTTP</span></span>

<span data-ttu-id="818e7-104">Il Hypertext Transfer Protocol (HTTP) è un protocollo progettato per il trasferimento del contenuto sul Web.</span><span class="sxs-lookup"><span data-stu-id="818e7-104">The Hypertext Transfer Protocol (HTTP) is a protocol designed for transferring content on the Web.</span></span> <span data-ttu-id="818e7-105">HTTP è un protocollo semplice che utilizza i servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento del contenuto.</span><span class="sxs-lookup"><span data-stu-id="818e7-105">HTTP is a simple protocol that utilizes reliable Transmission Control Protocol (TCP) services to perform its content transfer function.</span></span> <span data-ttu-id="818e7-106">Per questo motivo, HTTP è un protocollo di trasferimento del contenuto altamente affidabile.</span><span class="sxs-lookup"><span data-stu-id="818e7-106">Because of this, HTTP is a highly reliable content transfer protocol.</span></span> <span data-ttu-id="818e7-107">HTTP è uno dei protocolli applicativi più usati.</span><span class="sxs-lookup"><span data-stu-id="818e7-107">HTTP is one of the most used application protocols.</span></span> <span data-ttu-id="818e7-108">Tutte le operazioni sul Web utilizzano il protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="818e7-108">All operations on the Web utilize the HTTP protocol.</span></span>

## <a name="http-requirements"></a><span data-ttu-id="818e7-109">Requisiti HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-109">HTTP Requirements</span></span>

<span data-ttu-id="818e7-110">Per funzionare correttamente, il pacchetto HTTP NetX richiede l'installazione di un NetX (versione 5,2 o successiva).</span><span class="sxs-lookup"><span data-stu-id="818e7-110">In order to function properly, the NetX HTTP package requires that a NetX (version 5.2 or later) is installed.</span></span> <span data-ttu-id="818e7-111">Inoltre, è necessario che sia già stata creata un'istanza IP e che sia stato abilitato il protocollo TCP nella stessa istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="818e7-111">In addition, an IP instance must already be created and TCP must be enabled on that same IP instance.</span></span> <span data-ttu-id="818e7-112">Il file demo nella sezione "Small example System" del **capitolo 2** illustra come questa operazione viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="818e7-112">The demo file in section “Small Example System” in **Chapter 2** will demonstrate how this is done.</span></span>

<span data-ttu-id="818e7-113">La parte client HTTP del pacchetto HTTP NetX non ha altri requisiti.</span><span class="sxs-lookup"><span data-stu-id="818e7-113">The HTTP Client portion of the NetX HTTP package has no further requirements.</span></span>

<span data-ttu-id="818e7-114">La parte relativa al server HTTP del pacchetto HTTP NetX presenta diversi requisiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="818e7-114">The HTTP Server portion of the NetX HTTP package has several additional requirements.</span></span> <span data-ttu-id="818e7-115">Per prima cosa, è necessario l'accesso completo alla *porta TCP 80 nota* per la gestione di tutte le richieste HTTP del client.</span><span class="sxs-lookup"><span data-stu-id="818e7-115">First, it requires complete access to TCP *well-known port 80* for handling all Client HTTP requests.</span></span> <span data-ttu-id="818e7-116">Il server HTTP è anche progettato per l'uso con FileX Embedded file system.</span><span class="sxs-lookup"><span data-stu-id="818e7-116">The HTTP Server is also designed for use with the FileX embedded file system.</span></span> <span data-ttu-id="818e7-117">Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="818e7-117">If FileX is not available, the user may port the portions of FileX used to their own environment.</span></span> <span data-ttu-id="818e7-118">Questo argomento viene descritto nelle sezioni successive di questa guida.</span><span class="sxs-lookup"><span data-stu-id="818e7-118">This is discussed in later sections of this guide.</span></span>

## <a name="http-constraints"></a><span data-ttu-id="818e7-119">Vincoli HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-119">HTTP Constraints</span></span> 

<span data-ttu-id="818e7-120">Il protocollo HTTP NetX implementa lo standard HTTP 1,0.</span><span class="sxs-lookup"><span data-stu-id="818e7-120">The NetX HTTP protocol implements the HTTP 1.0 standard.</span></span> <span data-ttu-id="818e7-121">Tuttavia, sono presenti i vincoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="818e7-121">However, there are following constraints:</span></span>

1.  <span data-ttu-id="818e7-122">Le connessioni permanenti non sono supportate</span><span class="sxs-lookup"><span data-stu-id="818e7-122">Persistent connections are not supported</span></span>

2.  <span data-ttu-id="818e7-123">Il pipelining della richiesta non è supportato</span><span class="sxs-lookup"><span data-stu-id="818e7-123">Request pipelining is not supported</span></span>

3.  <span data-ttu-id="818e7-124">Il server HTTP supporta l'autenticazione di base e del digest MD5, ma non MD5-sess.</span><span class="sxs-lookup"><span data-stu-id="818e7-124">The HTTP Server supports both basic and MD5 digest authentication, but not MD5-sess.</span></span> <span data-ttu-id="818e7-125">Attualmente, il client HTTP supporta solo l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="818e7-125">At present, the HTTP Client supports only basic authentication.</span></span>

4.  <span data-ttu-id="818e7-126">Non è supportata alcuna compressione del contenuto.</span><span class="sxs-lookup"><span data-stu-id="818e7-126">No content compression is supported.</span></span>

5.  <span data-ttu-id="818e7-127">Le richieste di traccia, opzioni e connessione non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="818e7-127">TRACE, OPTIONS, and CONNECT requests are not supported.</span></span>

6.  <span data-ttu-id="818e7-128">Il pool di pacchetti associato al server o al client HTTP deve essere sufficientemente grande da contenere l'intestazione HTTP completa.</span><span class="sxs-lookup"><span data-stu-id="818e7-128">The packet pool associated with the HTTP Server or Client must be large enough to hold the complete HTTP header.</span></span>

7.  <span data-ttu-id="818e7-129">I servizi client HTTP sono destinati solo al trasferimento del contenuto. in questo pacchetto non sono disponibili utilità di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="818e7-129">HTTP Client services are for content transfer only—there are no display utilities provided in this package.</span></span>

## <a name="http-url-resource-names"></a><span data-ttu-id="818e7-130">URL HTTP (nomi di risorse)</span><span class="sxs-lookup"><span data-stu-id="818e7-130">HTTP URL (Resource Names)</span></span>

<span data-ttu-id="818e7-131">Il protocollo HTTP è progettato per trasferire il contenuto sul Web.</span><span class="sxs-lookup"><span data-stu-id="818e7-131">The HTTP protocol is designed to transfer content on Web.</span></span> <span data-ttu-id="818e7-132">Il contenuto richiesto viene specificato dall'URL (Universal Resource Locator).</span><span class="sxs-lookup"><span data-stu-id="818e7-132">The requested content is specified by the Universal Resource Locator (URL).</span></span> <span data-ttu-id="818e7-133">Questo è il componente principale di ogni richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="818e7-133">This is the primary component of every HTTP request.</span></span> <span data-ttu-id="818e7-134">Gli URL iniziano sempre con il carattere "/" e in genere corrispondono ai file nel server HTTP.</span><span class="sxs-lookup"><span data-stu-id="818e7-134">URLs always start with a “/” character and typically correspond to files on the HTTP Server.</span></span> <span data-ttu-id="818e7-135">Di seguito sono elencate le estensioni di file HTTP comuni:</span><span class="sxs-lookup"><span data-stu-id="818e7-135">Common HTTP file extensions are shown below:</span></span>

- <span data-ttu-id="818e7-136">**. htm (o. html)** Hypertext Markup Language (HTML)</span><span class="sxs-lookup"><span data-stu-id="818e7-136">**.htm (or .html)** Hypertext Markup Language (HTML)</span></span>
- <span data-ttu-id="818e7-137">**txt** Testo ASCII normale</span><span class="sxs-lookup"><span data-stu-id="818e7-137">**.txt** Plain ASCII text</span></span>
- <span data-ttu-id="818e7-138">**. gif** Immagine GIF binaria</span><span class="sxs-lookup"><span data-stu-id="818e7-138">**.gif** Binary GIF image</span></span>
- <span data-ttu-id="818e7-139">**. xbm** Immagine xbitmap binaria</span><span class="sxs-lookup"><span data-stu-id="818e7-139">**.xbm** Binary Xbitmap image</span></span>

## <a name="http-client-requests"></a><span data-ttu-id="818e7-140">Richieste client HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-140">HTTP Client Requests</span></span>

<span data-ttu-id="818e7-141">Il protocollo HTTP ha un meccanismo semplice per la richiesta di contenuto Web.</span><span class="sxs-lookup"><span data-stu-id="818e7-141">The HTTP has a simple mechanism for requesting Web content.</span></span> <span data-ttu-id="818e7-142">È fondamentalmente disponibile un set di comandi HTTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla *porta TCP 80*.</span><span class="sxs-lookup"><span data-stu-id="818e7-142">There is basically a set of standard HTTP commands that are issued by the Client after a connection has been successfully established on the TCP *well-known port 80*.</span></span> <span data-ttu-id="818e7-143">Di seguito sono riportati alcuni dei comandi HTTP di base:</span><span class="sxs-lookup"><span data-stu-id="818e7-143">The following shows some of the basic HTTP commands:</span></span>

- <span data-ttu-id="818e7-144">OTTENERE la risorsa HTTP/1.0 *ottenere la risorsa specificata*</span><span class="sxs-lookup"><span data-stu-id="818e7-144">GET resource HTTP/1.0 *Get the specified resource*</span></span>
- <span data-ttu-id="818e7-145">POST Resource HTTP/1.0 *ottenere la risorsa specificata e passare l'input collegato al server http*</span><span class="sxs-lookup"><span data-stu-id="818e7-145">POST resource HTTP/1.0 *Get the specified resource and pass attached input to the HTTP Server*</span></span>
- <span data-ttu-id="818e7-146">Risorsa HEAD HTTP/1.0 *trattata come Get ma non il contenuto viene restituito dal server http*</span><span class="sxs-lookup"><span data-stu-id="818e7-146">HEAD resource HTTP/1.0 *Treated like a GET but not content is returned by the HTTP Server*</span></span>
- <span data-ttu-id="818e7-147">Inserisci risorsa HTTP/1.0 *posizione sul server http*</span><span class="sxs-lookup"><span data-stu-id="818e7-147">PUT resource HTTP/1.0 *Place resource on HTTP Server*</span></span>
- <span data-ttu-id="818e7-148">Elimina risorsa HTTP/1.0 *Delete risorsa nel server*</span><span class="sxs-lookup"><span data-stu-id="818e7-148">DELETE resource HTTP/1.0 *Delete resource on the Server*</span></span>

<span data-ttu-id="818e7-149">Questi comandi ASCII vengono generati internamente dai Web browser e dai servizi client HTTP NetX per eseguire operazioni HTTP con un server HTTP.</span><span class="sxs-lookup"><span data-stu-id="818e7-149">These ASCII commands are generated internally by Web browsers and the NetX HTTP Client services to perform HTTP operations with an HTTP Server.</span></span>

>[!NOTE] 
> <span data-ttu-id="818e7-150">Per impostazione predefinita, l'applicazione client HTTP viene impostata sulla porta di connessione 80.</span><span class="sxs-lookup"><span data-stu-id="818e7-150">The HTTP Client application default to the connect port of 80.</span></span> <span data-ttu-id="818e7-151">Tuttavia, può modificare la porta di connessione al server HTTP in fase di esecuzione usando il servizio *nx_http_client_set_connect_port* .</span><span class="sxs-lookup"><span data-stu-id="818e7-151">However, it can change the connect port to the HTTP Server at runtime using the *nx_http_client_set_connect_port* service.</span></span> <span data-ttu-id="818e7-152">Per ulteriori informazioni su questo servizio, vedere il capitolo 4.</span><span class="sxs-lookup"><span data-stu-id="818e7-152">See Chapter 4 for more details of this service.</span></span> <span data-ttu-id="818e7-153">In questo modo è possibile gestire i server Web che occasionalmente utilizzano porte alternative per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="818e7-153">This is to accommodate web servers that occasionally use alternate ports for Client connections.</span></span>

## <a name="http-server-responses"></a><span data-ttu-id="818e7-154">Risposte al server HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-154">HTTP Server Responses</span></span>

<span data-ttu-id="818e7-155">Il server HTTP utilizza la stessa *porta TCP 80 nota* per inviare le risposte del comando client.</span><span class="sxs-lookup"><span data-stu-id="818e7-155">The HTTP Server utilizes the same *well-known TCP port 80* to send Client command responses.</span></span> <span data-ttu-id="818e7-156">Una volta che il server HTTP elabora il comando client, restituisce una stringa di risposta ASCII che include un codice di stato numerico a 3 cifre.</span><span class="sxs-lookup"><span data-stu-id="818e7-156">Once the HTTP Server processes the Client command, it returns an ASCII response string that includes a 3-digit numeric status code.</span></span> <span data-ttu-id="818e7-157">La risposta numerica viene utilizzata dal software client HTTP per determinare se l'operazione ha avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="818e7-157">The numeric response is used by the HTTP Client software to determine whether the operation succeeded or failed.</span></span> <span data-ttu-id="818e7-158">Di seguito è riportato un elenco di varie risposte del server HTTP ai comandi client:</span><span class="sxs-lookup"><span data-stu-id="818e7-158">Following is a list of various HTTP Server responses to Client commands:</span></span>

- <span data-ttu-id="818e7-159">la *richiesta 200 è stata completata*</span><span class="sxs-lookup"><span data-stu-id="818e7-159">200 *Request was successful*</span></span>
- <span data-ttu-id="818e7-160">la *richiesta 400 non è stata creata correttamente*</span><span class="sxs-lookup"><span data-stu-id="818e7-160">400 *Request was not formed properly*</span></span>
- <span data-ttu-id="818e7-161">401 *richiesta non autorizzata, il client deve inviare l'autenticazione*</span><span class="sxs-lookup"><span data-stu-id="818e7-161">401 *Unauthorized request, client needs to send authentication*</span></span>
- <span data-ttu-id="818e7-162">404 la *risorsa specificata nella richiesta non è stata trovata*</span><span class="sxs-lookup"><span data-stu-id="818e7-162">404 *Specified resource in request was not found*</span></span>
- <span data-ttu-id="818e7-163">500 *errore interno del server http*</span><span class="sxs-lookup"><span data-stu-id="818e7-163">500 *Internal HTTP Server error*</span></span>
- <span data-ttu-id="818e7-164">*richiesta 501 non implementata dal server http*</span><span class="sxs-lookup"><span data-stu-id="818e7-164">501 *Request not implemented by HTTP Server*</span></span>
- <span data-ttu-id="818e7-165">502 il *servizio non è disponibile*</span><span class="sxs-lookup"><span data-stu-id="818e7-165">502 *Service is not available*</span></span>

<span data-ttu-id="818e7-166">Ad esempio, una richiesta client corretta per inserire il file "test.htm" viene risposto con il messaggio "HTTP/1.0 200 OK".</span><span class="sxs-lookup"><span data-stu-id="818e7-166">For example, a successful Client request to PUT the file “test.htm” is responded with the message “HTTP/1.0 200 OK.”</span></span>

## <a name="http-communication"></a><span data-ttu-id="818e7-167">Comunicazione HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-167">HTTP Communication</span></span>

<span data-ttu-id="818e7-168">Come indicato in precedenza, il server HTTP utilizza la *porta TCP nota 80* per il campo richieste client.</span><span class="sxs-lookup"><span data-stu-id="818e7-168">As mentioned previously, the HTTP Server utilizes the *well-known TCP port 80* to field Client requests.</span></span> <span data-ttu-id="818e7-169">I client HTTP possono usare qualsiasi porta TCP disponibile.</span><span class="sxs-lookup"><span data-stu-id="818e7-169">HTTP Clients may use any available TCP port.</span></span> <span data-ttu-id="818e7-170">La sequenza generale degli eventi HTTP è la seguente:</span><span class="sxs-lookup"><span data-stu-id="818e7-170">The general sequence of HTTP events is as follows:</span></span>

<span data-ttu-id="818e7-171">**Richiesta HTTP Get**:</span><span class="sxs-lookup"><span data-stu-id="818e7-171">**HTTP GET Request**:</span></span>

1.  <span data-ttu-id="818e7-172">Il client invia la connessione TCP alla porta del server 80.</span><span class="sxs-lookup"><span data-stu-id="818e7-172">Client issues TCP connect to Server port 80.</span></span>

2.  <span data-ttu-id="818e7-173">Il client invia la richiesta "**Get Resource http/1.0**" (insieme ad altre informazioni di intestazione).</span><span class="sxs-lookup"><span data-stu-id="818e7-173">Client sends “**GET resource HTTP/1.0**” request (along with other header information).</span></span>

3.  <span data-ttu-id="818e7-174">Il server compila un messaggio "**http/1.0 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa (se presente).</span><span class="sxs-lookup"><span data-stu-id="818e7-174">Server builds an “**HTTP/1.0 200 OK**” message with additional information followed immediately by the resource content (if any).</span></span>

4.  <span data-ttu-id="818e7-175">Il server esegue una disconnessione.</span><span class="sxs-lookup"><span data-stu-id="818e7-175">Server performs a disconnection.</span></span>

5.  <span data-ttu-id="818e7-176">Il client esegue una disconnessione.</span><span class="sxs-lookup"><span data-stu-id="818e7-176">Client performs a disconnection.</span></span>

<span data-ttu-id="818e7-177">**Richiesta HTTP PUT**:</span><span class="sxs-lookup"><span data-stu-id="818e7-177">**HTTP PUT Request**:</span></span>

1. <span data-ttu-id="818e7-178">Il client invia la connessione TCP alla porta del server 80.</span><span class="sxs-lookup"><span data-stu-id="818e7-178">Client issues TCP connect to Server port 80.</span></span>

2. <span data-ttu-id="818e7-179">Il client invia la richiesta "**put Resource http/1.0**", insieme ad altre informazioni di intestazione e seguita dal contenuto della risorsa.</span><span class="sxs-lookup"><span data-stu-id="818e7-179">Client sends “**PUT resource HTTP/1.0**” request, along with other header information, and followed by the resource content.</span></span>

3. <span data-ttu-id="818e7-180">Il server compila un messaggio "**http/1.0 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa.</span><span class="sxs-lookup"><span data-stu-id="818e7-180">Server builds an “**HTTP/1.0 200 OK**” message with additional information followed immediately by the resource content.</span></span>

4. <span data-ttu-id="818e7-181">Il server esegue una disconnessione.</span><span class="sxs-lookup"><span data-stu-id="818e7-181">Server performs a disconnection.</span></span>

5. <span data-ttu-id="818e7-182">Il client esegue una disconnessione.</span><span class="sxs-lookup"><span data-stu-id="818e7-182">Client performs a disconnection.</span></span>

>[!NOTE] 
> <span data-ttu-id="818e7-183">Come indicato in precedenza, il client HTTP può modificare la porta di connessione predefinita da 80 a un'altra porta usando il *nx_http_client_set_connect_port* per i server Web che usano porte alternative per connettersi ai client.</span><span class="sxs-lookup"><span data-stu-id="818e7-183">As mentioned previously, the HTTP Client can change the default connect port from 80 to another port using the *nx_http_client_set_connect_port* for web servers that use alternate ports to connect to clients.</span></span>

## <a name="http-authentication"></a><span data-ttu-id="818e7-184">Autenticazione HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-184">HTTP Authentication</span></span>

<span data-ttu-id="818e7-185">L'autenticazione HTTP è facoltativa e non è obbligatoria per tutte le richieste Web.</span><span class="sxs-lookup"><span data-stu-id="818e7-185">HTTP authentication is optional and isn’t required for all Web requests.</span></span> <span data-ttu-id="818e7-186">Esistono due tipi di autenticazione, ovvero *Basic* e *digest*.</span><span class="sxs-lookup"><span data-stu-id="818e7-186">There are two flavors of authentication, namely *basic* and *digest*.</span></span> <span data-ttu-id="818e7-187">L'autenticazione di base equivale all'autenticazione del *nome* e della *password* presente in molti protocolli.</span><span class="sxs-lookup"><span data-stu-id="818e7-187">Basic authentication is equivalent to the *name* and *password* authentication found in many protocols.</span></span> <span data-ttu-id="818e7-188">Nell'autenticazione di base HTTP, il nome e le password vengono concatenati e codificati nel formato Base64.</span><span class="sxs-lookup"><span data-stu-id="818e7-188">In HTTP basic authentication, the name and passwords are concatenated and encoded in the base64 format.</span></span> <span data-ttu-id="818e7-189">Lo svantaggio principale dell'autenticazione di base è il nome e la password vengono trasmessi apertamente nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="818e7-189">The main disadvantage of basic authentication is the name and password are transmitted openly in the request.</span></span> <span data-ttu-id="818e7-190">In questo modo è piuttosto semplice che il nome e la password vengano rubati.</span><span class="sxs-lookup"><span data-stu-id="818e7-190">This makes it somewhat easy for the name and password to be stolen.</span></span> <span data-ttu-id="818e7-191">L'autenticazione del digest risolve questo problema senza trasmettere mai il nome e la password nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="818e7-191">Digest authentication addresses this problem by never transmitting the name and password in the request.</span></span> <span data-ttu-id="818e7-192">Viene invece utilizzato un algoritmo per derivare una chiave o un digest a 128 bit dal nome, dalla password e da altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="818e7-192">Instead, an algorithm is used to derive a 128-bit key or digest from the name, password, and other information.</span></span> <span data-ttu-id="818e7-193">Il server HTTP NetX supporta l'algoritmo digest MD5 standard.</span><span class="sxs-lookup"><span data-stu-id="818e7-193">The NetX HTTP Server supports the standard MD5 digest algorithm.</span></span>

<span data-ttu-id="818e7-194">Quando è richiesta l'autenticazione?</span><span class="sxs-lookup"><span data-stu-id="818e7-194">When is authentication required?</span></span> <span data-ttu-id="818e7-195">In sostanza, il server HTTP decide se una risorsa richiesta richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="818e7-195">Basically, the HTTP Server decides if a requested resource requires authentication.</span></span> <span data-ttu-id="818e7-196">Se è richiesta l'autenticazione e la richiesta del client non include l'autenticazione corretta, al client viene inviata una risposta "HTTP/1.0 401 non autorizzato" con il tipo di autenticazione richiesto.</span><span class="sxs-lookup"><span data-stu-id="818e7-196">If authentication is required and the Client request did not include the proper authentication, a “HTTP/1.0 401 Unauthorized” response with the type of authentication required is sent to the Client.</span></span> <span data-ttu-id="818e7-197">Il client deve quindi creare una nuova richiesta con l'autenticazione corretta.</span><span class="sxs-lookup"><span data-stu-id="818e7-197">The Client is then expected to form a new request with the proper authentication.</span></span>

## <a name="http-authentication-callback"></a><span data-ttu-id="818e7-198">Callback di autenticazione HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-198">HTTP Authentication Callback</span></span>

<span data-ttu-id="818e7-199">Come indicato in precedenza, l'autenticazione HTTP è facoltativa e non è necessaria per tutti i trasferimenti Web.</span><span class="sxs-lookup"><span data-stu-id="818e7-199">As mentioned before, HTTP authentication is optional and isn’t required on all Web transfers.</span></span> <span data-ttu-id="818e7-200">Inoltre, l'autenticazione è in genere dipendente dalle risorse.</span><span class="sxs-lookup"><span data-stu-id="818e7-200">In addition, authentication is typically resource dependent.</span></span> <span data-ttu-id="818e7-201">L'accesso ad alcune risorse sul server richiede l'autenticazione, mentre altri no.</span><span class="sxs-lookup"><span data-stu-id="818e7-201">Access of some resources on the Server require authentication, while others do not.</span></span> <span data-ttu-id="818e7-202">Il pacchetto del server HTTP NetX consente all'applicazione di specificare (tramite la chiamata ***nx_http_server_create*** ) una routine di callback di autenticazione che viene chiamata all'inizio della gestione di ogni richiesta del client http.</span><span class="sxs-lookup"><span data-stu-id="818e7-202">The NetX HTTP Server package allows the application to specify (via the ***nx_http_server_create*** call) an authentication callback routine that is called at the beginning of handling each HTTP Client request.</span></span>

<span data-ttu-id="818e7-203">La routine di callback fornisce il server HTTP NetX con le stringhe di nome utente, password e area di autenticazione associate alla risorsa e restituisce il tipo di autenticazione necessario.</span><span class="sxs-lookup"><span data-stu-id="818e7-203">The callback routine provides the NetX HTTP Server with the username, password, and realm strings associated with the resource and return the type of authentication necessary.</span></span> <span data-ttu-id="818e7-204">Se non è necessaria alcuna autenticazione per la risorsa, il callback di autenticazione deve restituire il valore di **NX_HTTP_DONT_AUTHENTICATE**.</span><span class="sxs-lookup"><span data-stu-id="818e7-204">If no authentication is necessary for the resource, the authentication callback should return the value of **NX_HTTP_DONT_AUTHENTICATE**.</span></span> <span data-ttu-id="818e7-205">In caso contrario, se è richiesta l'autenticazione di base per la risorsa specificata, la routine deve restituire **NX_HTTP_BASIC_AUTHENTICATE**.</span><span class="sxs-lookup"><span data-stu-id="818e7-205">Otherwise, if basic authentication is required for the specified resource, the routine should return **NX_HTTP_BASIC_AUTHENTICATE**.</span></span> <span data-ttu-id="818e7-206">Infine, se è richiesta l'autenticazione digest MD5, la routine di callback deve restituire **NX_HTTP_DIGEST_AUTHENTICATE**.</span><span class="sxs-lookup"><span data-stu-id="818e7-206">And finally, if MD5 digest authentication is required, the callback routine should return **NX_HTTP_DIGEST_AUTHENTICATE**.</span></span> <span data-ttu-id="818e7-207">Se non è necessaria alcuna autenticazione per le risorse fornite dal server HTTP, il callback non è necessario e può essere fornito un puntatore NULL alla chiamata di creazione del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="818e7-207">If no authentication is required for any resource provided by the HTTP Server, the callback is not needed and a NULL pointer can be provided to the HTTP Server create call.</span></span>

<span data-ttu-id="818e7-208">Il formato della routine di callback dell'applicazione di autenticazione è molto semplice e viene definito di seguito:</span><span class="sxs-lookup"><span data-stu-id="818e7-208">The format of the application authenticate callback routine is very simple and is defined below:</span></span>

```c
UINT nx_http_server_authentication_check (NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, CHAR **password,
                                         CHAR **realm);
```

<span data-ttu-id="818e7-209">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="818e7-209">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="818e7-210">*request_type* Specifica la richiesta client HTTP, le richieste valide sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="818e7-210">*request_type* Specifies the HTTP Client request, valid requests are defined as:</span></span>
  - <span data-ttu-id="818e7-211">**NX_HTTP_SERVER_GET_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-211">**NX_HTTP_SERVER_GET_REQUEST**</span></span>
  - <span data-ttu-id="818e7-212">**NX_HTTP_SERVER_POST_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-212">**NX_HTTP_SERVER_POST_REQUEST**</span></span>
  - <span data-ttu-id="818e7-213">**NX_HTTP_SERVER_HEAD_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-213">**NX_HTTP_SERVER_HEAD_REQUEST**</span></span>
  - <span data-ttu-id="818e7-214">**NX_HTTP_SERVER_PUT_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-214">**NX_HTTP_SERVER_PUT_REQUEST**</span></span>
  - <span data-ttu-id="818e7-215">**NX_HTTP_SERVER_DELETE_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-215">**NX_HTTP_SERVER_DELETE_REQUEST**</span></span>
- <span data-ttu-id="818e7-216">*risorsa* di Risorsa specifica richiesta.</span><span class="sxs-lookup"><span data-stu-id="818e7-216">*resource* Specific resource requested.</span></span>
- <span data-ttu-id="818e7-217">*nome* Destinazione per il puntatore al nome utente obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="818e7-217">*name* Destination for the pointer to the required username.</span></span>
- <span data-ttu-id="818e7-218">*password* di Destinazione per il puntatore alla password richiesta.</span><span class="sxs-lookup"><span data-stu-id="818e7-218">*password* Destination for the pointer to the required password.</span></span>
- <span data-ttu-id="818e7-219">*area di autenticazione* Destinazione per il puntatore all'area di autenticazione per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="818e7-219">*realm* Destination for the pointer to the realm for this authentication.</span></span>

<span data-ttu-id="818e7-220">Il valore restituito della routine di autenticazione specifica se è richiesta l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="818e7-220">The return value of the authentication routine specifies if authentication is required.</span></span> <span data-ttu-id="818e7-221">il nome, la password e i puntatori dell'area di autenticazione non vengono utilizzati se **NX_HTTP_DONT_AUTHENTICATE** viene restituito dalla routine di callback di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="818e7-221">name, password, and realm pointers are not used if **NX_HTTP_DONT_AUTHENTICATE** is returned by the authentication callback routine.</span></span> <span data-ttu-id="818e7-222">In caso contrario, lo sviluppatore del server HTTP deve garantire che **NX_HTTP_MAX_USERNAME** e **NX_HTTP_MAX_PASSWORD** definiti in *nx_http_server. h* siano sufficientemente grandi per il nome utente e la password specificati nel callback di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="818e7-222">Otherwise the HTTP server developer must ensure that **NX_HTTP_MAX_USERNAME** and **NX_HTTP_MAX_PASSWORD** defined in *nx_http_server.h* are large enough for the username and password specified in the authentication callback.</span></span> <span data-ttu-id="818e7-223">Per impostazione predefinita, le dimensioni sono pari a 20 caratteri.</span><span class="sxs-lookup"><span data-stu-id="818e7-223">These are both defaulted to size 20 chars.</span></span>

## <a name="http-invalid-usernamepassword-callback"></a><span data-ttu-id="818e7-224">Callback di nome utente/password non valido HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-224">HTTP Invalid Username/Password Callback</span></span>

<span data-ttu-id="818e7-225">Il callback facoltativo di nome utente/password non valido nel server HTTP NetX viene richiamato se il server HTTP riceve una combinazione di nome utente e password non valida in una richiesta client.</span><span class="sxs-lookup"><span data-stu-id="818e7-225">The optional invalid username/password callback in NetX HTTP Server is invoked if HTTP server receives an invalid username and password combination in a Client request.</span></span> <span data-ttu-id="818e7-226">Se l'applicazione server HTTP registra un callback con il server HTTP, verrà richiamato se l'autenticazione di base o Digest ha esito negativo *in nx_http_server_get_process*, in *nx_http_server_put_process* o *in nx_http_server_delete_process.*</span><span class="sxs-lookup"><span data-stu-id="818e7-226">If the HTTP server application registers a callback with HTTP server it will be invoked if either basic or digest authentication fails *in nx_http_server_get_process*, in *nx_http_server_put_process,* or *in nx_http_server_delete_process.*</span></span>

<span data-ttu-id="818e7-227">Per registrare un callback con il server HTTP, il servizio seguente viene definito nel server HTTP NetX.</span><span class="sxs-lookup"><span data-stu-id="818e7-227">To register a callback with the HTTP server, the following service is defined in NetX HTTP Server.</span></span>

```c
UINT nx_http_server_invalid_userpassword_notify_set (NX_HTTP_SERVER *http_server_ptr,
                                                    UINT *invalid_username_password_callback)
                                                    (CHAR *resource,
                                                    ULONG *client_nx_address,
                                                    UINT request_type));
```
<span data-ttu-id="818e7-228">I tipi di richiesta sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="818e7-228">The request types are defined as follows:</span></span>

- <span data-ttu-id="818e7-229">**NX_HTTP_SERVER_GET_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-229">**NX_HTTP_SERVER_GET_REQUEST**</span></span>
- <span data-ttu-id="818e7-230">**NX_HTTP_SERVER_POST_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-230">**NX_HTTP_SERVER_POST_REQUEST**</span></span>
- <span data-ttu-id="818e7-231">**NX_HTTP_SERVER_HEAD_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-231">**NX_HTTP_SERVER_HEAD_REQUEST**</span></span>
- <span data-ttu-id="818e7-232">**NX_HTTP_SERVER_PUT_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-232">**NX_HTTP_SERVER_PUT_REQUEST**</span></span>
- <span data-ttu-id="818e7-233">**NX_HTTP_SERVER_DELETE_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="818e7-233">**NX_HTTP_SERVER_DELETE_REQUEST**</span></span>

## <a name="http-insert-gmt-date-header-callback"></a><span data-ttu-id="818e7-234">Callback intestazione Data GMT inserimento HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-234">HTTP Insert GMT Date Header Callback</span></span>

<span data-ttu-id="818e7-235">È disponibile un callback facoltativo nel server HTTP NetX per inserire un'intestazione di data nei messaggi di risposta.</span><span class="sxs-lookup"><span data-stu-id="818e7-235">There is an optional callback in NetX HTTP Server to insert a date header in its response messages.</span></span> <span data-ttu-id="818e7-236">Questo callback viene richiamato quando il server HTTP sta rispondendo a una richiesta PUT o Get</span><span class="sxs-lookup"><span data-stu-id="818e7-236">This callback is invoked when the HTTP Server is responding to a put or get request</span></span>

<span data-ttu-id="818e7-237">Per registrare un callback della data GMT con il server HTTP, il servizio seguente viene definito nel server HTTP NetX.</span><span class="sxs-lookup"><span data-stu-id="818e7-237">To register a GMT date callback with the HTTP server, the following service is defined in the NetX HTTP Server.</span></span>

```c
UINT _nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

<span data-ttu-id="818e7-238">Il tipo di dati NX_HTTP_SERVER_DATE viene definito nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="818e7-238">The NX_HTTP_SERVER_DATE data type is defined as follows:</span></span>

```c
typedef struct NX_HTTP_SERVER_DATE_STRUCT
{
    USHORT     nx_http_server_year;         /* Year        */
    UCHAR      nx_http_server_month;        /* Month       */
    UCHAR      nx_http_server_day;          /* Day         */
    UCHAR      nx_http_server_hour;         /* Hour        */
    UCHAR      nx_http_server_minute;       /* Minute      */
    UCHAR      nx_http_server_second;       /* Second      */
    UCHAR      nx_http_server_weekday;      /* Weekday     */
} NX_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a><span data-ttu-id="818e7-239">Callback informazioni cache HTTP Get</span><span class="sxs-lookup"><span data-stu-id="818e7-239">HTTP Cache Info Get Callback</span></span>

<span data-ttu-id="818e7-240">Il server HTTP ha un callback per richiedere la validità massima e la data dall'applicazione HTTP per una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="818e7-240">The HTTP Server has a callback to request the max age and date from the HTTP application for a specific resource.</span></span> <span data-ttu-id="818e7-241">Queste informazioni vengono usate per determinare se il server HTTP invia l'intera pagina in risposta a una richiesta Get del client.</span><span class="sxs-lookup"><span data-stu-id="818e7-241">This information is used to determine if the HTTP server sends the entire page in response to a Client Get request.</span></span> <span data-ttu-id="818e7-242">Se il "se modificato da" nella richiesta del client non viene trovato o non corrisponde alla data dell'Ultima modifica restituita dal callback Get cache, viene inviata l'intera pagina.</span><span class="sxs-lookup"><span data-stu-id="818e7-242">If the “if modified since” in the Client request is not found or does not match the “last modified” date returned by the get cache callback, the entire page is sent.</span></span>

<span data-ttu-id="818e7-243">Per registrare il callback con il server HTTP, viene definito il seguente servizio:</span><span class="sxs-lookup"><span data-stu-id="818e7-243">To register the callback with the HTTP server the following service is defined:</span></span>

```c
UINT _nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                            UINT (*cache_info_get)
                                            (CHAR *, UINT *, NX_HTTP_SERVER_DATE *));
```

## <a name="http-multipart-support"></a><span data-ttu-id="818e7-244">Supporto multipart HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-244">HTTP Multipart Support</span></span>

<span data-ttu-id="818e7-245">Multipurpose Internet Mail Extensions (MIME) è stato originariamente progettato per il protocollo SMTP, ma il suo utilizzo è stato distribuito in HTTP.</span><span class="sxs-lookup"><span data-stu-id="818e7-245">Multipurpose Internet Mail Extensions (MIME) was originally intended for the SMTP protocol, but its use has spread to HTTP.</span></span> <span data-ttu-id="818e7-246">MIME consente ai messaggi di contenere tipi di messaggi misti, ad esempio image/jpg e text/plain, all'interno dello stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="818e7-246">MIME allows messages to contain mixed message types (e.g. image/jpg and text/plain) within the same message.</span></span> <span data-ttu-id="818e7-247">Il server HTTP NetX ha aggiunto servizi per determinare il tipo di contenuto nei messaggi HTTP che contengono MIME dal client.</span><span class="sxs-lookup"><span data-stu-id="818e7-247">NetX HTTP Server has added services to determine content type in HTTP messages containing MIME from the Client.</span></span> <span data-ttu-id="818e7-248">Per abilitare il supporto multipart HTTP e utilizzare questi servizi, è necessario definire l'opzione di configurazione **NX_HTTP_MULTIPART_ENABLE** .</span><span class="sxs-lookup"><span data-stu-id="818e7-248">To enable HTTP multipart support and use these services, the configuration option **NX_HTTP_MULTIPART_ENABLE** must be defined.</span></span>

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);

UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

<span data-ttu-id="818e7-249">Per altri dettagli sull'uso di questi servizi, vedere la descrizione nel capitolo 3 "Descrizione dei servizi HTTP".</span><span class="sxs-lookup"><span data-stu-id="818e7-249">For more details on the use of these services, see their description in Chapter 3 “Description of HTTP Services”.</span></span>

## <a name="http-multi-thread-support"></a><span data-ttu-id="818e7-250">Supporto multithreading HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-250">HTTP Multi-Thread Support</span></span>

<span data-ttu-id="818e7-251">I servizi client HTTP NetX possono essere chiamati da più thread contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="818e7-251">The NetX HTTP Client services can be called from multiple threads simultaneously.</span></span> <span data-ttu-id="818e7-252">Tuttavia, le richieste di lettura o scrittura per un'istanza specifica del client HTTP devono essere eseguite in sequenza dallo stesso thread.</span><span class="sxs-lookup"><span data-stu-id="818e7-252">However, read or write requests for a particular HTTP Client instance should be done in sequence from the same thread.</span></span>

## <a name="http-rfcs"></a><span data-ttu-id="818e7-253">RFC HTTP</span><span class="sxs-lookup"><span data-stu-id="818e7-253">HTTP RFCs</span></span>

<span data-ttu-id="818e7-254">Il protocollo HTTP di NetX è conforme a RFC1945 "Hypertext Transfer Protocol/1.0", RFC 2581 "TCP congestione del controllo", RFC 1122 "requisiti per gli host Internet" e RFC correlate.</span><span class="sxs-lookup"><span data-stu-id="818e7-254">NetX HTTP is compliant with RFC1945 “Hypertext Transfer Protocol/1.0”, RFC 2581 “TCP Congestion Control”, RFC 1122 “Requirements for Internet Hosts”, and related RFCs.</span></span>