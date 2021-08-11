---
title: Capitolo 2 - Installazione e uso del client RTOS NetX Duo LWM2M
description: Questo capitolo illustra come installare e usare il client RTOS NetX Duo LWM2M.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f804ae59dd639ca05d1b8f5251cf8b878e78bb9ad2575e08c21d43b14e727a19
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796515"
---
# <a name="chapter-2--installation-and-use-of-lwm2m-client"></a>Capitolo 2 Installazione e uso del client LWM2M

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client LWM2M.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS LWM2M Client può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netxduo/tree/master/addons/lwm2m](https://github.com/azure-rtos/netxduo/tree/master/addons/lwm2m/) . Il pacchetto include tre file di origine, uno di inclusione, come indicato di seguito.

* **nx \_ lwm2m \_ client.h** File di intestazione per il client LWM2M

* **nx \_ lwm2m \_ client.c** File di origine C per il client LWM2M

* **demo \_ netx \_ lwm2m \_ client.c** File di origine C per LWM2M Client Demo

## <a name="lwm2m-client-installation"></a>Installazione del client LWM2M

Il client LWM2M fa parte di NetX Duo. Pertanto, dopo la clonazione di NetX Duo dal repository GitHub, l'origine client LWM2M è disponibile in ***netxduo/addons/lwm2m.***

## <a name="using-lwm2m_client"></a>Uso del client LWM2M \_

L'uso del client LWM2M è semplice. Fondamentalmente, il codice dell'applicazione deve includere ***nx \_ lwm2m client.h* _ dopo aver incluso \_ *_*_tx \_ api.h_*_ e _*_nx \_ api.h_ _, per poter usare ThreadX e *NetX. Dopo aver* incluso _ _nx \_ lwm2m \_ client.h_ _, il codice dell'applicazione è in grado di effettuare le chiamate di funzione client LWM2M specificate più avanti *in questa guida. L'applicazione deve anche importare* i file con estensione _nx \_ lwm2m \_ client \_ nella \**** libreria NetX.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria client LWM2M e l'applicazione usando il client LWM2M, sono disponibili diverse opzioni di configurazione. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando, se non diversamente specificato.

| Opzione di &nbsp; configurazione | Descrizione |
| --- | --- |
| **NX \_ LWM2M \_ CLIENT \_ MTU** | Specifica la dimensione massima di un messaggio CoAP, incluse le intestazioni IP e UDP. Il valore predefinito è 1280. |
| **NX \_ LWM2M \_ CLIENT \_ SOCKET \_ TOS** | Tipo di servizio necessario per l'UDP LwM2M. Per impostazione predefinita, questo valore è definito come NX \_ IP NORMAL per indicare il normale servizio di pacchetti \_ IP. |
| **TTL DEL SOCKET CLIENT \_ NX LWM2M \_ \_ \_** | Specifica il numero di router che il pacchetto può superare prima di essere eliminato. Il valore predefinito è impostato su 0x80. |
| **NX \_ LWM2M \_ CLIENT \_ SOCKET \_ QUEUE \_ MAX** | Specifica il numero massimo di profondità della coda di ricezione. Il valore predefinito è impostato su 4. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ COAP \_ URI \_ PATH** | Specifica il numero di lunghezze massime dell'opzione coAP Uri-Path proprietà. Il valore predefinito è impostato su 32. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ DEVICE \_ ERRORS** | Specifica il numero massimo di codici di errore archiviati dall'oggetto dispositivo. Il valore predefinito è 8. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ SECURITY \_ INSTANCES** | Specifica il numero massimo di istanze dell'oggetto di sicurezza. Il valore predefinito è 2 per il supporto di un server Bootstrap e di un server standard. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ SERVER \_ INSTANCES** | Specifica il numero massimo di istanze dell'oggetto server. Il valore predefinito è 1 per il supporto di un singolo server standard. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ ACCESS \_ CONTROL \_ INSTANCES** | Specifica il numero massimo di istanze di controllo di accesso. Il valore predefinito è 0, che disabilita il controllo di accesso. Se l'applicazione supporta più di un server LWM2M, il numero massimo di istanze di controllo di accesso deve essere impostato sul numero massimo di istanze di oggetto che il client LWM2M supporterà, perché è necessario creare un'istanza di controllo di accesso per ogni istanza dell'oggetto (ad eccezione delle istanze degli oggetti di sicurezza). |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ ACCESS \_ CONTROL \_ ACLS** | Specifica il numero massimo di risorse ACL per ogni istanza di controllo di accesso. Il valore predefinito è 4. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ NOTIFICATIONS** | Specifica il numero massimo di notifiche che il client LWM2M supporterà. Un server LWM2M può impostare notifiche su oggetti, istanze di oggetti e risorse. Il valore predefinito è 8. |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ RESOURCES** | Specifica il numero massimo di risorse per oggetto. Il valore predefinito è (32). |
| **NX \_ LWM2M \_ CLIENT \_ MAX \_ MULTIPLE \_ RESOURCES** | Specifica il numero massimo di istanze di Risorse per più risorse. Il valore predefinito è 8. |
| **NX \_ LWM2M \_ CLIENT \_ BOOTSTRAP \_ IDLE \_ TIMER** | Specifica il tempo massimo di attesa per le richieste del server bootstrap quando viene avviata la sessione di bootstrap prima di interrompere la sessione. Il valore predefinito è 60 secondi. |
| **NX \_ LWM2M \_ CLIENT \_ DTLS \_ START \_ TIMEOUT** | Specifica il tempo massimo di attesa per il completamento dell'handshake DTLS. Il valore predefinito è 30 secondi. |
| **NX \_ LWM2M \_ CLIENT \_ DTLS \_ END \_ TIMEOUT** | Specifica il tempo massimo di attesa per il completamento dell'arresto DTLS. Il valore predefinito è 5 secondi. |
| **NX \_ LWM2M \_ CLIENT \_ SECURITY \_ MAX \_ SERVER \_ URI** | Specifica la lunghezza massima di un URI del server, incluso il carattere Null di terminazione. Il valore predefinito è 128. |
| **NX \_ LWM2M \_ CLIENT \_ SECURITY \_ MAX \_ PUBLIC \_ KEY \_ OR \_ IDENTITY** | Specifica la lunghezza massima della chiave pubblica o dell'identità per DTLS. Il valore predefinito è 128. |
| **NX \_ LWM2M \_ CLIENT \_ SECURITY \_ MAX \_ SERVER \_ PUBLIC \_ KEY** | Specifica la lunghezza massima della chiave pubblica del server per DTLS. Il valore predefinito è 128. |
| **NX \_ LWM2M \_ CLIENT \_ SECURITY \_ MAX \_ SECRET \_ KEY** | Specifica la lunghezza massima della chiave privata per DTLS. Il valore predefinito è 128. |
| **NX \_ LWM2M \_ CLIENT \_ HOLD \_ OFF** | Specifica il numero di secondi di attesa prima dell'avvio del bootstrap. Il valore predefinito è 1 secondo. |
| **DURATA \_ DEL CLIENT NX LWM2M \_ \_ \_** | Specifica il numero di secondi per la durata della registrazione. Il valore predefinito è 600 secondi. |
