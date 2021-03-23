---
title: Capitolo 2-installazione e uso di GUIX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dell'interfaccia utente di HighPerformance GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6527227062fc667b3f527a798d6621914c374c5c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822295"
---
# <a name="chapter-2---installation-and-use-of-guix"></a>Capitolo 2-installazione e uso di GUIX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dell'interfaccia utente di HighPerformance GUIX.  

## <a name="host-considerations"></a>Considerazioni sull'host

Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e il file eseguibile viene generato nell'host, viene scaricato nell'hardware di destinazione per l'esecuzione.

Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo di esecuzione di destinazione (go, Halt, breakpoint e così via), nonché di accedere ai registri della memoria e del processore.

La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE). Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.

Per quanto riguarda le risorse usate nell'host, il codice sorgente per GUXI viene fornito in formato ASCII e richiede circa 30 Mbyte di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

GUIX richiede tra 5 Kbyte e 80 KByte di memoria Read-Only (ROM) nella destinazione. Per lo stack di thread GUIX e altre strutture di dati globali sono necessarie altre 5 10KBytes della memoria ad accesso casuale (RAM) della destinazione.

Inoltre, GUIX richiede l'uso di un timer ThreadX e di un oggetto mutex ThreadX. Queste strutture vengono usate per le esigenze di elaborazione periodica e la protezione dei thread all'interno di GUIX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO GUIX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/guix/> .

Di seguito è riportato un elenco dei file importanti comuni alla maggior parte delle distribuzioni di prodotti:

| Filename&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Descrizione   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| gx_api. h        | Questo file di intestazione C contiene tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio. |
| gx_port. h       | Questo file di intestazione C contiene tutte le definizioni e le strutture dei dati specifiche della destinazione e dello strumento di sviluppo.                                                                                                                                         |
| GX. a (o GX. lib) | Si tratta della versione binaria della libreria C GUIX. Questa operazione viene in genere compilata mediante la compilazione e l'archiviazione dei file di origine della libreria GUIX specificati, tuttavia questa libreria può essere fornita in un modulo predefinito a seconda della destinazione hardware e del tipo di licenza. |
|

> [!IMPORTANT]
> *Tutti i file sono in minuscolo, semplificando la conversione dei comandi in piattaforme di sviluppo Linux (Unix).*

## <a name="guix-installation"></a>Installazione di GUIX

GUIX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository GUIX nel PC:

```c
    git clone https://github.com/azure-rtos/guix
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria GUIX nella pagina iniziale del repository online.

>[!NOTE]  
> *Il software applicativo deve accedere al file della libreria GUIX, in genere denominato **GX. a** (o **GX. lib**), e i file di inclusione C **gx_api. h** e **gx_port. h**. Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.*

## <a name="using-guix"></a>Uso di GUIX

L'uso di GUIX è facile. In pratica, il codice dell'applicazione deve includere ***gx_api. h** _ durante la compilazione e il collegamento con la libreria GUIX _*_GX. a_*_ (o _ *_GX. lib_*) *.

Per creare un'applicazione GUIX, è necessario eseguire quattro semplici passaggi:

| Passaggi   | Descrizione    |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Passaggio &nbsp; 1: | Includere il file ***gx_api. h*** in tutti i file dell'applicazione che utilizzano i servizi o le strutture di dati GUIX.                                                               |
| Passaggio &nbsp; 2: | Inizializzare il sistema GUIX chiamando ***gx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.                       |
| Passaggio &nbsp; 3: | Creare un'istanza di visualizzazione, creare un'area di disegno per la visualizzazione e creare la finestra radice e tutte le altre finestre o widget necessari.                                 |
| Passaggio &nbsp; 4: | Compilare l'origine dell'applicazione e il collegamento con la libreria di runtime GUIX ***GX. a** _ (o _ *_GX. lib_* *). L'immagine risultante può essere scaricata nella destinazione ed eseguita. |

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta GUIX viene fornita con un'applicazione dimostrativa eseguita su hardware di visualizzazione specifico. La stessa dimostrazione di base viene fornita con tutte le versioni di GUIX. È sempre consigliabile che il sistema dimostrativo venga eseguito per primo.

Se il sistema dimostrativo non viene eseguito correttamente, eseguire le operazioni seguenti per restringere il problema:

1. Determinare la quantità della dimostrazione in esecuzione.

2. Aumentare le dimensioni dello stack del thread GUIX modificando la costante in fase di compilazione **GX_THREAD_STACK_SIZE** e ricompilando la libreria GUIX

3. Ricompilare la libreria GUIX con le opzioni di debug appropriate elencate nella sezione opzione di configurazione.

4. Esaminare lo stato di restituzione di tutte le chiamate API.

5. Determinare se si è verificato un errore interno del sistema impostando un punto di interruzione in corrispondenza della funzione ***_gx_system_error_process***. Il codice di errore e il chiamante dovrebbero fornire indizi relativi a ciò che potrebbe essere errato.

6. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato. Tali informazioni dovrebbero risultare utili per i tecnici del supporto tecnico Microsoft.

Seguire le procedure descritte nella sezione intitolata "cosa è necessario per l'utente" per inviare le informazioni raccolte dalla procedura di risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compilano la libreria GUIX e l'applicazione tramite GUIX, sono disponibili diverse opzioni di configurazione. Queste opzioni vengono usate per ottimizzare le dimensioni della libreria e il set di funzionalità in base ai requisiti dell'applicazione. Se, ad esempio, l'applicazione avrà un solo thread che usa i servizi API GUIX, è necessario definire il flag di configurazione **GX_DISABLE_MULTITHREAD_SUPPORT** per eliminare l'overhead associato alla protezione delle sezioni di codice critiche dalla prelazione di più thread. I diversi flag di configurazione possono essere definiti nell'origine dell'applicazione, nella riga di comando o nel file di inclusione **_gx_user. h_** .

Ogni volta che vengono modificati i flag di configurazione della libreria GUIX, è necessario ricompilare sia la libreria GUIX che i moduli dell'applicazione per rendere effettive le modifiche alla configurazione.

L'elenco completo dei flag di configurazione è documentato in Appendice H: GUIX Build-Time flag di configurazione.

## <a name="guix-version-id"></a>ID versione GUIX

La versione corrente di GUIX è disponibile sia per l'utente sia per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione di GUIX dall'esame del file ***gx_port. h** _. Inoltre, questo file contiene anche una cronologia delle versioni del software delle applicazioni porta corrispondente che può ottenere la versione di GUIX esaminando la stringa globale _ *_ _gx_version_id_* _ in _ *_gx_port. h_* *.

Il software applicativo può inoltre ottenere informazioni sulla versione dalle costanti indicate di seguito definite in ***gx_api. h**. * queste costanti identificano la versione corrente del prodotto in base al nome e alla versione principale e secondaria del prodotto.

```C
#define __PRODUCT_GUIX__

#define __GUIX_MAJOR_VERSION__

#define __GUIX_MINOR_VERSION__
```
