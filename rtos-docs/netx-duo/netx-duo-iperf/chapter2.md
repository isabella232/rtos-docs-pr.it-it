---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo Iperf
description: Questo capitolo fornisce istruzioni per l'installazione e l'uso dell'esempio Iperf.
author: v-condav
ms.author: v-condav
ms.date: 08/16/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7e80d89a334ceec3467b23574ab5c231a15f68a1
ms.sourcegitcommit: 4842f4cfe9e31b3ac59059f43e598eb70faebc8f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2021
ms.locfileid: "122609958"
---
# <a name="chapter-2-installation-and-use"></a>Capitolo 2 Installazione e uso

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso della dimostrazione Di NetX Duo Iperf.

## <a name="installing-the-demonstration"></a>Installazione della dimostrazione

Seguire le istruzioni di installazione specifiche della piattaforma fornite nella distribuzione.

## <a name="installing-iperf"></a>Installazione di Iperf

È possibile usare un'ampia gamma di programmi Iperf. Tuttavia, gli esempi in questo documento si basano sul ***Jperf 2.0.2*** basato su Java, disponibile da più origini su Internet.

> [Nota] *Jperf richiede che Java sia installato nel computer host.*

## <a name="setting-the-ip-address"></a>Impostazione dell'indirizzo IP

Per impostazione predefinita, l'indirizzo IP della dimostrazione iperf di NetX Duo è impostato su **192.2.2.149.** Questa impostazione viene impostata nel file **_demo_netx_duo_iperf.c_*_*** come parametro per la chiamata a _ nx_ip_create .

## <a name="network-assumptions"></a>Presupposti di rete

Questa dimostrazione presuppone che il computer host Iperf e la scheda di destinazione che esegue la dimostrazione di Iperf di NetX Duo siano connessi a un commutatore Ethernet full duplex a 100 Mbps. Per ottenere prestazioni ottimali, non deve essere presente altro traffico nella rete di test.

È anche possibile connettere l'host Iperf e la scheda di destinazione NetX Duo back-to-back con un cavo Ethernet cross-over.

## <a name="running-the-demonstration"></a>Esecuzione della dimostrazione

L'esecuzione della dimostrazione è semplice. È sufficiente caricare, compilare ed eseguire il progetto NetX Duo Iperf Demonstration, in genere ***denominato demo_netx_duo_iperf***.

## <a name="browse-to-the-demonstration"></a>Passare alla dimostrazione

Passare alla scheda di destinazione tramite un browser nella piattaforma host Iperf. Supponendo che l'indirizzo IP della scheda di destinazione **sia 192.2.2.149,** di seguito è riportato un esempio della pagina Web iniziale netx duo iperf demonstration.

![Esempio della pagina Web iniziale iperf](media/Picture1.jpg)

## <a name="running-jperf"></a>Esecuzione di Jperf

L'esecuzione di Jperf è semplice. È sufficiente fare doppio clic sul file batch Windows ***jperf.bat** _. Verrà avviato l'IDE Jperf, come illustrato di seguito. Dopo aver visualizzato l'IDE Jperf, il campo _ *Server Address** (Indirizzo server * ) deve essere impostato sull'indirizzo IP della scheda di destinazione NetX Duo Iperf Demonstration. In questo esempio l'indirizzo IP della scheda di destinazione NetX Duo è **192.2.2.149.** Vale anche la pena notare i **campi Larghezza di banda UDP** e Dimensioni pacchetto **UDP.** È necessario configurare queste opzioni per ottenere prestazioni ottimali di ricezione UDP, come illustrato di seguito.

![Ottimizzazione delle prestazioni UDP.](media/Picture2.jpg)
