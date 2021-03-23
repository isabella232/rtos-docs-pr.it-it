---
title: Capitolo 2-installazione e utilizzo del client RTO NetX Duo LWM2M
description: Questo capitolo illustra come installare e usare il client RTO NetX Duo LWM2M.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 536225de30f54356157c222917fc904c6aa039fe
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821854"
---
# <a name="chapter-2--installation-and-use-of-lwm2m-client"></a>Capitolo 2 installazione e utilizzo del client LWM2M

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client di LWM2M.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il client LWM2M di Azure RTO può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netxduo/tree/master/addons/lwm2m](https://github.com/azure-rtos/netxduo/tree/master/addons/lwm2m/) . Il pacchetto include tre file di origine, uno di inclusione, come indicato di seguito.

* file di intestazione **\_ \_ client. h NX Lwm2m** per il client lwm2m

* file di origine di **NX \_ lwm2m \_ client. c** c per il client lwm2m

* **Demo \_ NETX \_ lwm2m \_ client. c** file di origine per lwm2m client demo

## <a name="lwm2m-client-installation"></a>Installazione client di LWM2M

Il client LWM2M fa parte di NetX Duo. Quindi, dopo la clonazione di NetX Duo dal repository GitHub, l'origine client LWM2M è reperibile in ***netxduo/addons/LWM2M***.

## <a name="using-lwm2m_client"></a>Uso del \_ client LWM2M

L'uso di LWM2M client è semplice. In pratica, il codice dell'applicazione deve includere ***NX \_ lwm2m \_ client. h **_ dopo aver incluso _*_TX \_ API. h_*_ e _*_NX \_ API. h_*_, per usare threadX e NETX. Una volta che è incluso _*_NX \_ lwm2m \_ client. h_*_, il codice dell'applicazione è quindi in grado di effettuare le chiamate di funzione client lwm2m specificate più avanti in questa guida. L'applicazione deve inoltre importare la _* _nx \_ lwm2m \_ client \_ . \**** files nella libreria NETX.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione quando si compila la libreria client di LWM2M e l'applicazione usando il client LWM2M. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando, se non diversamente specificato.

| Opzione di configurazione &nbsp; | Descrizione |
| --- | --- |
| **\_ \_ MTU client NX \_ LWM2M** | Specifica la dimensione massima di un messaggio CoAP, incluse le intestazioni IP e UDP. Il valore predefinito è 1280. |
| **\_ \_ \_ TOS socket client LWM2M \_ NX** | Tipo di servizio richiesto per UDP LwM2M. Per impostazione predefinita, questo valore è definito come \_ IP NX \_ normale per indicare il normale servizio pacchetti IP. |
| **\_ \_ \_ TTL socket client NX \_ LWM2M** | Specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80. |
| **\_ \_ \_ \_ Massimo coda socket client NX LWM2M \_** | Specifica il numero massimo di profondità della coda di ricezione. Il valore predefinito è impostato su 4. |
| **\_ \_ \_ \_ \_ Percorso URI CoAP \_ client NX LWM2M max** | Specifica il numero massimo di lunghezze per l'opzione di Uri-Path CoAP. Il valore predefinito è impostato su 32. |
| **\_ \_ \_ \_ Errori dispositivo max del client NX LWM2M \_** | Specifica il numero massimo di codici di errore archiviati dall'oggetto dispositivo. Il valore predefinito è 8. |
| **\_Istanze di \_ \_ sicurezza Max \_ del client NX LWM2M \_** | Specifica il numero massimo di istanze di oggetti di sicurezza. Il valore predefinito è 2 per supportare un server bootstrap e un server standard. |
| **\_Istanze del \_ \_ server max \_ del client NX LWM2M \_** | Specifica il numero massimo di istanze di oggetti server. Il valore predefinito è 1 per il supporto di un singolo server standard. |
| **\_ \_ \_ Numero massimo di \_ istanze del \_ controllo di accesso \_ del client NX LWM2M** | Specifica il numero massimo di istanze del controllo di accesso. Il valore predefinito è 0, che disabilita il controllo di accesso. Se l'applicazione supporta più di un server LWM2M, il numero massimo di istanze del controllo di accesso deve essere impostato sul numero massimo di istanze di oggetti che il client LWM2M supporterà, perché è necessario creare un'istanza del controllo di accesso per ogni istanza dell'oggetto, ad eccezione delle istanze degli oggetti di sicurezza. |
| **\_Elenchi di \_ \_ controllo di \_ accesso massimo del \_ client \_ NX LWM2M** | Specifica il numero massimo di risorse ACL per ogni istanza del controllo di accesso. Il valore predefinito è 4. |
| **\_ \_ \_ Notifiche massime del client NX LWM2M \_** | Specifica il numero massimo di notifiche che il client LWM2M supporterà. Un server LWM2M può impostare notifiche su oggetti, istanze di oggetti e risorse. Il valore predefinito è 8. |
| **\_ \_ \_ Risorse massime del client NX LWM2M \_** | Specifica il numero massimo di risorse per oggetto. Il valore predefinito è (32). |
| **\_ \_ \_ Numero massimo di \_ \_ risorse per il client NX LWM2M** | Specifica il numero massimo di istanze di risorse per più risorse. Il valore predefinito è 8. |
| **\_Timer di \_ \_ \_ inattività bootstrap client NX \_ LWM2M** | Specifica il tempo massimo di attesa per le richieste del server di bootstrap quando viene avviata la sessione bootstrap prima di interrompere la sessione. Il valore predefinito è 60 secondi. |
| **\_Timeout di \_ \_ avvio DTLS \_ del client NX LWM2M \_** | Specifica il tempo massimo di attesa per il completamento dell'handshake DTLS. Il valore predefinito è 30 secondi. |
| **\_ \_ \_ \_ Timeout finale DTLS del client NX LWM2M \_** | Specifica il tempo massimo di attesa per il completamento dell'arresto del DTLS. Il valore predefinito è 5 secondi. |
| **\_ \_ \_ \_ \_ URI server di sicurezza client NX LWM2M Max \_** | Specifica la lunghezza massima di un URI del server, incluso il carattere di terminazione null. Il valore predefinito è 128. |
| **\_ \_ \_ \_ \_ \_ Chiave pubblica \_ o \_ identità max di sicurezza del client NX LWM2M** | Specifica la lunghezza massima della chiave pubblica o dell'identità per DTLS. Il valore predefinito è 128. |
| **\_Chiave pubblica per la sicurezza del \_ \_ \_ \_ server max \_ \_ del client NX LWM2M** | Specifica la lunghezza massima della chiave pubblica del server per DTLS. Il valore predefinito è 128. |
| **\_ \_ \_ \_ \_ Chiave privata massima sicurezza client \_ NX LWM2M** | Specifica la lunghezza massima della chiave privata per DTLS. Il valore predefinito è 128. |
| **\_LWM2M \_ client NX \_ \_** | Specifica il numero di secondi di attesa prima di avviare il bootstrap. Il valore predefinito è 1 secondo. |
| **\_Durata del \_ client \_ LWM2M \_ NX** | Specifica il numero di secondi per la durata della registrazione. Il valore predefinito è 600 secondi. |
