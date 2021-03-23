---
title: Appendice D-dump e buffer di traccia
description: Il dump del buffer di traccia creato da Azure RTO ThreadX in un file nel computer host viene eseguito tramite i comandi e/o le utilità forniti dallo strumento di sviluppo specifico usato.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 30f6b5e329feeb2dca37dda391fd738aba587c9a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823627"
---
# <a name="appendix-d---dumping-and-trace-buffer"></a>Appendice D-dump e buffer di traccia

Il dump del buffer di traccia creato da Azure RTO ThreadX in un file nel computer host viene eseguito tramite i comandi e/o le utilità forniti dallo strumento di sviluppo specifico usato. Questa appendice contiene esempi di dump di un buffer di traccia in un file host in alcuni degli strumenti di sviluppo più diffusi usati con ThreadX. 

## <a name="benchx-tools"></a>Strumenti BenchX

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti BenchX selezionando il pulsante ***Archivia memoria nel file** _ nella _visualizzazione di memoria_* *, come illustrato di seguito:

![Screenshot della visualizzazione della memoria negli strumenti BenchX.](./media/user-guide/image642.jpg)

A questo punto, specificare l'indirizzo del buffer di traccia, le dimensioni, il nome del file di destinazione (incluso il percorso), quindi selezionare il pulsante ***Salva*** come illustrato di seguito. Verrà creato il file di traccia binario per la visualizzazione in TraceX.

![Screenshot della finestra di dialogo Salva strumenti BenchX.](./media/user-guide/image643.jpg)

## <a name="realview-tools"></a>Strumenti RealView

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti ARM RealView immettendo il comando seguente al prompt della riga di comando in RealView:

```c 
> WRITEFILE,raw trace_file.trx=0x6860..0xE560
```

Al termine, il file ***trace_file. TRX*** conterrà il buffer di traccia che si trova a partire dall'indirizzo 0x6860 e passa all'indirizzo 0xE560. Questo file è pronto per la visualizzazione da TraceX.

## <a name="iar-tools"></a>Strumenti IAR

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti IAR semplicemente facendo clic con il pulsante destro del mouse nella visualizzazione memoria e selezionando la ***memoria Salva...*** come illustrato di seguito.

![Screenshot dell'opzione di salvataggio della memoria negli strumenti IAR.](./media/user-guide/image0_311.jpg)

Questa operazione comporta la visualizzazione della finestra di dialogo ***Save Memory** _. Immettere l'indirizzo iniziale e finale e il nome del file di traccia, quindi selezionare il pulsante _*_Salva_*_ . Nell'esempio riportato di seguito, gli strumenti IAR salvano il buffer di traccia specificato in record ESADECIMALi Intel nel file _ *_trace_file. Hex_* *.

![Screenshot della finestra di dialogo di salvataggio della memoria per gli strumenti IAR.](./media/user-guide/image648.jpg)

A questo punto, il buffer di traccia è stato salvato nel file ***trace_file. Hex*** nell'host ed è pronto per la visualizzazione con TraceX.

## <a name="codewarrior-tools"></a>Strumenti di CodeWarrior

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti di CodeWarrior immettendo il comando ***Save** _ nella finestra di comando. Il comando di esempio _ *_Save_** seguente presuppone che il buffer di traccia inizi in corrispondenza di 0x102200 e termina in corrispondenza di 0x109F00:

```c
> save –b p:0x102200..0x109F00 trace_file.trx -a 32bit
```

Ciò comporta il salvataggio del buffer di traccia nel file ***trace_file. TRX*** nell'host.

## <a name="mplab-tools"></a>Strumenti MPLAB

MPLAB è in grado di creare un file di traccia compatibile con TraceX tramite l'utilità di esportazione tabella, che consente l'esportazione di qualsiasi intervallo di memoria in un file host. Per utilizzare questa utilità per creare un file di traccia per TraceX, procedere come segue:

**Passaggio 1** Aprire una finestra memoria selezionando Visualizza-> memoria.

![Screenshot della memoria selezionata dal menu Visualizza.](./media/user-guide/image0_316.jpg)

**Passaggio 2** Fare clic con il pulsante destro del mouse nella **visualizzazione memoria** per visualizzare un elenco di opzioni. Specificare il **formato di visualizzazione-1 byte** per selezionare la visualizzazione di byte.

![Screenshot della visualizzazione memoria con l'opzione formato di visualizzazione selezionata.](./media/user-guide/image650.png)

![Screenshot della finestra di dialogo Vai a.](./media/user-guide/image651.jpg)

**Passaggio 3** Fare di nuovo clic con il pulsante destro del mouse nella finestra **visualizzazione memoria** e scegliere **Vai a**. verrà visualizzata una finestra di dialogo in cui è possibile specificare l'indirizzo del buffer dell'evento. Questo esempio Mostra **_event_buffer_** visualizzato.

![Screenshot della visualizzazione memoria con l'opzione Vai a selezionata.](./media/user-guide/image0_312.jpg)

![Screenshot di un esempio che mostra il event_buffer visualizzato.](./media/user-guide/image653.png)

**Passaggio 4** In questo modo viene evidenziato il contenuto della prima posizione del buffer di traccia, che è sempre la stringa BTXT....

![Screenshot della prima posizione del buffer di traccia.](./media/user-guide/image0_313.jpg)

**Passaggio 5** A questo punto, fare di nuovo clic con il pulsante destro del mouse per visualizzare il menu opzioni e selezionare **Esporta tabella**.

![Screenshot della visualizzazione memoria con l'opzione Esporta tabella selezionata.](./media/user-guide/image0_314.jpg)

**Passaggio 6** Verrà visualizzata la finestra di dialogo **Esporta tabella** , come illustrato. Consente di specificare l'intervallo di indirizzi da esportare. Per un buffer di traccia da 8 KB, come nel caso di questo esempio, specificare l'intervallo da 0xA00006AC a 0xA00026AC e immettere un nome per il file host da creare (demo_threadx. TRX in questo esempio).

! [[Screenshot della finestra di dialogo Esporta come.](./media/user-guide/image656.jpg)

**Passaggio 7** Viene creato un file denominato **demo_threadx. TRX** nell'host e questo file può essere aperto da TraceX.

## <a name="ghs-tools"></a>Strumenti GHS

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti GHS immettendo il comando seguente al prompt della riga di comando nella finestra di comando debug:

```c
memdump raw c:releasethreadxdemo_threadx.trx event_buffer 32768
```

Al termine, il file **demo_threadx. TRX** conterrà il buffer di traccia che si trova nel event_buffer con una dimensione di 32.768 byte ed è pronto per la visualizzazione da parte di TraceX.

## <a name="renesas-hew"></a>Renesas

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti di reimpostazione della NASA, seguendo i tre passaggi seguenti:

**Passaggio 1** Aprire la finestra memoria.

! [[Screenshot della finestra memoria.](./media/user-guide/image657.jpg)

**Passaggio 2** Posizionare il cursore nella finestra memoria e fare clic con il pulsante destro del mouse.

![Screenshot della finestra memoria con l'opzione Salva selezionata.](./media/user-guide/image0_315.jpg)

**Passaggio 3** Selezionare Salva, quindi nella finestra Salva memoria come eseguire le operazioni seguenti:

- Selezionare formato file: Binary.
- Specificare filename: come desiderato
- Specificare l'indirizzo iniziale: trace_buffer
- Specifica indirizzo finale: (trace_buffer + dimensioni)
- Specificare le dimensioni di accesso: 1
- Fare clic su Salva.

![Screenshot della finestra di dialogo Salva memoria con nome.](./media/user-guide/image659.jpg)