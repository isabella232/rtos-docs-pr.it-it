---
title: Appendice D - Dump e buffer di traccia
description: Il dump del buffer di traccia creato da Azure RTOS ThreadX in un file nel computer host viene eseguito tramite comandi e/o utilità forniti dallo strumento di sviluppo specifico in uso.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: afbbabbd04ac4c33a747bb0cce4a9f36ca2d197a819cb48d834429e29fe5572c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802396"
---
# <a name="appendix-d---dumping-and-trace-buffer"></a>Appendice D - Dump e buffer di traccia

Il dump del buffer di traccia creato da Azure RTOS ThreadX in un file nel computer host viene eseguito tramite comandi e/o utilità forniti dallo strumento di sviluppo specifico in uso. Questa appendice contiene esempi di dump di un buffer di traccia in un file host in alcuni degli strumenti di sviluppo più diffusi usati con ThreadX. 

## <a name="benchx-tools"></a>BenchX Tools

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti BenchX selezionando il pulsante * Store Memory To File _ (Archivia memoria su **file)** nella visualizzazione memoria __*_**, come illustrato di seguito:

![Screenshot della visualizzazione memoria negli strumenti BenchX.](./media/user-guide/image642.jpg)

A questo punto, specificare l'indirizzo del buffer di traccia, le dimensioni, il nome del file di destinazione (incluso il percorso) e selezionare il ***pulsante Salva*** come illustrato di seguito. Verrà creato il file di traccia binario per la visualizzazione all'interno di TraceX.

![Screenshot della finestra di dialogo di salvataggio degli strumenti BenchX.](./media/user-guide/image643.jpg)

## <a name="realview-tools"></a>Strumenti RealView

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti Arm RealView immettendo il comando seguente al prompt della riga di comando in RealView:

```c 
> WRITEFILE,raw trace_file.trx=0x6860..0xE560
```

Al termine, il file ***trace_file.trx*** conterrà il buffer di traccia che si trova a partire dall'indirizzo 0x6860 e passa fino all'indirizzo 0xE560. Questo file è pronto per la visualizzazione da parte di TraceX.

## <a name="iar-tools"></a>Strumenti IAR

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti IAR facendo semplicemente clic con il pulsante destro del mouse nella visualizzazione della memoria e scegliendo ***Il salvataggio della memoria...*** , come illustrato di seguito.

![Screenshot dell'opzione Memory Save (Salvataggio memoria) negli strumenti IAR.](./media/user-guide/image0_311.jpg)

Verrà visualizzata la finestra di dialogo ***Memory Save** _. Immettere l'indirizzo iniziale e finale e il nome del file di traccia, quindi selezionare il _*_pulsante_*_ Salva. Nell'esempio illustrato di seguito, gli strumenti IAR salvano il buffer di traccia specificato nei record Intel HEX nel file _*_trace_file.hex_**.

![Screenshot della finestra di dialogo Memory Save (Salva memoria) degli strumenti IAR.](./media/user-guide/image648.jpg)

A questo punto, il buffer di traccia viene salvato nel file ***trace_file.hex*** nell'host ed è pronto per la visualizzazione con TraceX.

## <a name="codewarrior-tools"></a>Strumenti CodeWarrior

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti CodeWarrior immettendo il comando ***save** _ nella finestra di comando. Nell'esempio seguente il comando _ *_save_** presuppone che il buffer di traccia inizi 0x102200 e termini in corrispondenza 0x109F00:

```c
> save –b p:0x102200..0x109F00 trace_file.trx -a 32bit
```

In questo modo il buffer di traccia viene salvato nel file ***trace_file.trx*** nell'host.

## <a name="mplab-tools"></a>Strumenti MPLAB

MPLAB può creare un file di traccia compatibile con TraceX tramite l'utilità Esporta tabella, che consente l'esportazione di qualsiasi intervallo di memoria in un file host. Per utilizzare questa utilità per creare un file di traccia per TraceX, procedere come segue:

**Passaggio 1** Aprire una finestra di memoria selezionando Visualizza -> memoria.

![Screenshot della memoria selezionata nel menu Visualizza.](./media/user-guide/image0_316.jpg)

**Passaggio 2** Fare clic con il pulsante destro **del mouse nella visualizzazione Memoria** per visualizzare un elenco di opzioni. Specificare **il formato di visualizzazione -1 byte** per selezionare la visualizzazione dei byte.

![Screenshot della visualizzazione memoria con l'opzione Formato di visualizzazione selezionata.](./media/user-guide/image650.png)

![Screenshot della finestra di dialogo Vai a.](./media/user-guide/image651.jpg)

**Passaggio 3** Fare di nuovo clic con il pulsante **destro** del mouse all'interno della finestra di visualizzazione della memoria e scegliere **Vai** a per aprire una finestra di dialogo che consente di specificare l'indirizzo del buffer eventi. Questo esempio mostra **_event_buffer_** visualizzato.

![Screenshot della visualizzazione memoria con l'opzione Vai a selezionata.](./media/user-guide/image0_312.jpg)

![Screenshot di un esempio che mostra la event_buffer visualizzata.](./media/user-guide/image653.png)

**Passaggio 4** In questo modo viene evidenziato il contenuto della prima posizione del buffer di traccia, che è sempre la stringa BTXT.

![Screenshot della prima posizione del buffer di traccia.](./media/user-guide/image0_313.jpg)

**Passaggio 5** A questo punto, fare di nuovo clic con il pulsante destro del mouse per visualizzare il menu delle opzioni e **selezionare Esporta tabella.**

![Screenshot della visualizzazione Memoria con l'opzione Esporta tabella selezionata.](./media/user-guide/image0_314.jpg)

**Passaggio 6** Verrà visualizzata la finestra **di dialogo Esporta** tabella, come illustrato. Specificare l'intervallo di indirizzi da esportare. Per un buffer di traccia 8K, come nel caso di questo esempio, specificare l'intervallo da 0xA00006AC a 0xA00026AC e immettere un nome per il file host da creare (demo_threadx.trx in questo esempio).

! [[Screenshot della finestra di dialogo Esporta con nome.](./media/user-guide/image656.jpg)

**Passaggio 7** Nell'host verrà creato un file denominato **demo_threadx.trx** che può essere aperto da TraceX.

## <a name="ghs-tools"></a>Strumenti GHS

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti GHS immettendo il comando seguente al prompt della riga di comando nella finestra di comando di debug:

```c
memdump raw c:releasethreadxdemo_threadx.trx event_buffer 32768
```

Al termine, il file **demo_threadx.trx** conterrà il buffer di traccia che si trova nel event_buffer con una dimensione di 32.768 byte ed è pronto per la visualizzazione da parte di TraceX.

## <a name="renesas-hew"></a>Renesas HEW

È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti HEW renasas seguendo i tre passaggi (e i passaggi secondari) seguenti:

**Passaggio 1** Aprire la finestra Memoria.

! [[Screenshot della finestra Memoria.](./media/user-guide/image657.jpg)

**Passaggio 2** Posizionare il cursore all'interno della finestra della memoria e fare clic con il pulsante destro del mouse.

![Screenshot della finestra Memoria con l'opzione Salva selezionata.](./media/user-guide/image0_315.jpg)

**Passaggio 3** Selezionare Salva e quindi nella finestra Salva memoria con nome eseguire le operazioni seguenti:

- Selezionare Formato file: Binario.
- Specificare il nome file: in base alle esigenze
- Specificare l'indirizzo iniziale: trace_buffer
- Specificare l'indirizzo finale: (trace_buffer+dimensioni)
- Specificare le dimensioni di accesso: 1
- Fare clic su Salva.

![Screenshot della finestra di dialogo Salva memoria con nome.](./media/user-guide/image659.jpg)