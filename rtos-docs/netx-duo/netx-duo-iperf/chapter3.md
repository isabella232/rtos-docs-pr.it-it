---
title: Capitolo 3 - Esecuzione del test di trasmissione UDP
description: Questo capitolo fornisce istruzioni per l'esecuzione dell'esempio Iperf.
author: v-condav
ms.author: v-condav
ms.date: 08/16/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2a68ba3ddb71adc424002c815fd023f50b552997
ms.sourcegitcommit: 4842f4cfe9e31b3ac59059f43e598eb70faebc8f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2021
ms.locfileid: "122609959"
---
# <a name="chapter-3-running-the-demonstration"></a>Capitolo 3 Esecuzione della dimostrazione

Supponendo che nel browser host sia visualizzata la pagina Web NetX Duo Iperf Demonstration come illustrato in precedenza e Jperf sia in esecuzione nell'host, questo capitolo descrive come eseguire ogni test iperf.

## <a name="running-the-udp-transmit-test"></a>Esecuzione del test di trasmissione UDP

Il test di trasmissione UDP determina le prestazioni della trasmissione UDP NetX Duo all'host. In questo test, la destinazione NetX Duo è il client e l'host Jperf è il server. Per prima cosa, **selezionare Server** **e UDP** nell'IDE Jperf. Selezionare quindi **Esegui IPerf!** per avviare il server Iperf, come illustrato di seguito.

![Esecuzione del test di trasmissione UDP.](media/picture3.jpg)

A questo punto, nella pagina Web NetX Duo Iperf Demonstration (Dimostrazione di NetX Duo Iperf) selezionare il pulsante Start UDP Transmit Test (Avvia test trasmissione **UDP)** per avviare il test. È ora necessario osservare le statistiche sulle prestazioni nell'IDE Jperf e nella pagina Web NetX Duo aggiornata, come illustrato di seguito.

![Statistiche dei test di trasmissione UDP.](media/picture4.jpg)

Per completare il test, selezionare **qui** il collegamento nella pagina Web NetX Duo Iperf Demonstration (Dimostrazione di NetX Duo Iperf). È ora necessario osservare i risultati delle prestazioni del test. In questo esempio le prestazioni di trasmissione UDP nella destinazione NetX Duo all'host Iperf erano di 94 Mbps nella destinazione NetX Duo, come illustrato di seguito.

![Risultati del test di trasmissione UDP.](media/picture5.jpg)

## <a name="running-the-udp-receive-test"></a>Esecuzione del test di ricezione UDP

Il test di ricezione UDP determina le prestazioni della ricezione UDP di NetX Duo nella destinazione NetX Duo. In questo test, la destinazione NetX Duo è il server e l'host Jperf è il client. Selezionare innanzitutto **Client** e **UDP nell'IDE** Jperf. Selezionare quindi **Avvia test ricezione UDP** nella pagina Web NetX Duo Iperf Demonstration, come illustrato nella figura seguente.

![Esecuzione del test di ricezione UDP.](media/picture6.jpg)

Selezionare Run **IPerf! (Esegui IPerf!** dall'IDE Jperf e osservare le statistiche nell'IDE Jperf, come illustrato di seguito.

![UDP riceve le statistiche di test.](media/picture7.jpg)

Per completare il test, selezionare **il collegamento qui** nella pagina Web NetX Duo Iperf Demonstration (Dimostrazione di NetX Duo Iperf). È ora necessario osservare i risultati delle prestazioni del test. In questo esempio le prestazioni di ricezione UDP nella destinazione NetX Duo sono 95 Mbps, come illustrato di seguito.

![UDP riceve i risultati dei test](media/picture8.jpg)

## <a name="running-the-tcp-transmit-test"></a>Esecuzione del test di trasmissione TCP

Il test di trasmissione TCP determina le prestazioni della trasmissione TCP NetX Duo all'host. In questo test, la destinazione NetX Duo è il client e l'host Jperf è il server. Per prima cosa, **selezionare Server** **e TCP** nell'IDE Jperf. Selezionare quindi **Esegui IPerf!** per avviare il server Iperf, come illustrato di seguito.

![Esecuzione del test di trasmissione TCP.](media/picture9.jpg)

A questo punto, nella pagina Web NetX Duo Iperf Demonstration (Dimostrazione di NetX Duo Iperf) selezionare il pulsante Start TCP Transmit Test (Avvia test trasmissione **TCP)** per avviare il test. È ora necessario osservare le statistiche sulle prestazioni nell'IDE Jperf e nella pagina Web NetX Duo Iperf Demonstration aggiornata, come illustrato di seguito.

![Statistiche di test di trasmissione TCP.](media/picture10.jpg)

Per completare il test, selezionare ***il collegamento qui*** nella pagina Web NetX Duo Iperf Demonstration (Dimostrazione di NetX Duo Iperf). È ora necessario osservare i risultati delle prestazioni del test. In questo esempio le prestazioni di trasmissione TCP nella destinazione NetX Duo erano di 91 Mbps, come illustrato di seguito.

![TCP trasmette i risultati dei test.](media/picture11.jpg)

## <a name="running-the-tcp-receive-test"></a>Esecuzione del test di ricezione TCP

Il test di ricezione TCP determina le prestazioni della ricezione TCP di NetX Duo nella destinazione NetX Duo. In questo test, la destinazione NetX Duo è il server e l'host Jperf è il client. Selezionare innanzitutto **Client** e **TCP nell'IDE** Jperf. Selezionare quindi **Avvia test ricezione TCP** nella pagina Web NetX Duo, come illustrato.

![Esecuzione del test di ricezione TCP](media/picture12.jpg)

Selezionare Run **IPerf! (Esegui IPerf!** dall'IDE Jperf e osservare le statistiche nell'IDE Jperf, come illustrato di seguito.

![TCP riceve statistiche di test.](media/picture13.jpg)

Per completare il test, selezionare ***il collegamento qui*** nella pagina Web NetX Duo Iperf Demonstration (Dimostrazione di NetX Duo Iperf). È ora necessario osservare i risultati delle prestazioni del test. In questo esempio le prestazioni di ricezione TCP nella destinazione NetX Duo erano di 71 Mbps, come illustrato di seguito.

![TCP riceve i risultati dei test.](media/picture14.jpg)
