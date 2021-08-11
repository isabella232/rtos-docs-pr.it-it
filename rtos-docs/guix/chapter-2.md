---
title: Capitolo 2 - Installazione e uso di GUIX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dell'interfaccia utente GUIX dell'interfaccia utente ad alte prestazioni.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a4572dbf4691869d9a1c32d68fbf9cc1c7dbfbee7e58ad69dd944e668e382b76
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784113"
---
# <a name="chapter-2---installation-and-use-of-guix"></a>Capitolo 2 - Installazione e uso di GUIX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dell'interfaccia utente GUIX dell'interfaccia utente ad alte prestazioni.  

## <a name="host-considerations"></a>Considerazioni sull'host

Lo sviluppo incorporato viene in genere eseguito in Windows o nei computer host Linux (Unix). Dopo la compilazione, il collegamento e la generazione dell'eseguibile nell'host, l'applicazione viene scaricata nell'hardware di destinazione per l'esecuzione.

In genere il download di destinazione viene eseguito dall'interno del debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo dell'esecuzione di destinazione (go, halt, breakpoint e così via), nonché l'accesso ai registri della memoria e del processore.

La maggior parte dei debugger degli strumenti di sviluppo comunica con l'hardware di destinazione tramite connessioni OCD (On-Chip Debug), ad esempio JTAG (IEEE 1149.1) e BDM (Background Debug Mode). I debugger comunicano anche con l'hardware di destinazione In-Circuit connessioni ICE (In-Circuit Emulation). Entrambe le connessioni OCD e ICE offrono soluzioni affidabili con intrusioni minime nel software residente di destinazione.

Come per le risorse usate nell'host, il codice sorgente per GUXI viene fornito in formato ASCII e richiede circa 30 Mbyte di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

GUIX richiede da 5 kByte a 80 Kbyte di memoria Read-Only memoria (ROM) nella destinazione. Altri 5-10 KB di memoria ad accesso casuale (RAM) della destinazione sono necessari per lo stack di thread GUIX e altre strutture di dati globali.

GuiX richiede anche l'uso di un timer ThreadX e di un oggetto mutex ThreadX. Queste funzionalità vengono usate per esigenze di elaborazione periodiche e per la protezione dei thread all'interno di GUIX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS GUIX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/guix/> .

Di seguito è riportato un elenco dei file importanti comuni alla maggior parte delle distribuzioni di prodotti:

| Filename&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Descrizione   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| gx_api.h        | Questo file di intestazione C contiene tutti gli equilibrazioni di sistema, le strutture di dati e i prototipi di servizio. |
| gx_port.h       | Questo file di intestazione C contiene tutte le definizioni e le strutture di dati specifiche dello strumento di sviluppo e della destinazione.                                                                                                                                         |
| gx.a (o gx.lib) | Questa è la versione binaria della libreria GUIX C. Questa operazione viene in genere creata compilando e archiviando i file di origine della libreria GUIX forniti, tuttavia questa libreria può essere fornita in formato precompilato a seconda della destinazione hardware e del tipo di licenza. |
|

> [!IMPORTANT]
> *Tutti i file sono in lettere minuscole, semplificando la conversione dei comandi in piattaforme di sviluppo Linux (Unix).*

## <a name="guix-installation"></a>Installazione GUIX

GUIX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository GUIX nel PC:

```c
    git clone https://github.com/azure-rtos/guix
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante di download nella GitHub pagina principale.

Le istruzioni per la creazione della libreria GUIX sono disponibili anche nella prima pagina del repository online.

>[!NOTE]  
> *Il software applicativo deve accedere al file della libreria GUIX, in genere denominato **gx.a** (o **gx.lib)** e ai file di inclusione C **gx_api.h** **e gx_port.h**. Questa operazione viene eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.*

## <a name="using-guix"></a>Uso di GUIX

L'uso di GUIX è semplice. Fondamentalmente, il codice dell'applicazione deve includere ***gx_api.h** _ durante la compilazione e il collegamento alla libreria GUIX _*_gx.a_*_ (o _ *_gx.lib_*)*.

Per compilare un'applicazione GUIX sono necessari quattro semplici passaggi:

| Passaggi   | Descrizione    |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Passaggio &nbsp; 1: | Includere il file ***gx_api.h*** in tutti i file dell'applicazione che usano servizi GUIX o strutture di dati.                                                               |
| Passaggio &nbsp; 2: | Inizializzare il sistema GUIX chiamando ***gx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.                       |
| Passaggio &nbsp; 3: | Creare un'istanza di visualizzazione, creare un'area di disegno per la visualizzazione e creare la finestra radice e qualsiasi altra finestra o widget necessario.                                 |
| Passaggio &nbsp; 4: | Compilare l'origine dell'applicazione e collegarsi alla libreria di runtime GUIX ***gx.a** _ (o _*_gx.lib_**). L'immagine risultante può essere scaricata nella destinazione ed eseguita. |

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta GUIX viene recapitata con un'applicazione dimostrativa che viene eseguita su hardware di visualizzazione specifico. La stessa dimostrazione di base viene recapitata con tutte le versioni di GUIX. È sempre una buona idea fare in modo che il sistema dimostrativo sia in esecuzione per primo.

Se il sistema dimostrativo non viene eseguito correttamente, eseguire le operazioni seguenti per limitare il problema:

1. Determinare la parte della dimostrazione in esecuzione.

2. Aumentare le dimensioni dello stack del thread GUIX modificando la costante in fase di **GX_THREAD_STACK_SIZE** e ricompilando la libreria GUIX

3. Ricompilare la libreria GUIX con le opzioni di debug appropriate elencate nella sezione delle opzioni di configurazione.

4. Esaminare lo stato restituito da tutte le chiamate API.

5. Determinare se è presente un errore di sistema interno impostando un punto di interruzione in corrispondenza della ***funzione _gx_system_error_process***. Il codice di errore e il chiamante devono fornire indicazioni su ciò che potrebbe andare storto.

6. Ignorare temporaneamente eventuali modifiche recenti per verificare se il problema scompare o cambia. Tali informazioni dovrebbero risultare utili ai tecnici del supporto tecnico Microsoft.

Seguire le procedure descritte nella sezione intitolata "What We Need From You" per inviare le informazioni raccolte dai passaggi per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria GUIX e l'applicazione tramite GUIX, sono disponibili diverse opzioni di configurazione. Queste opzioni vengono usate per ottimizzare le dimensioni della libreria e il set di funzionalità in base ai requisiti dell'applicazione. Ad esempio, se l'applicazione avrà un solo thread che usa i servizi API GUIX, è necessario definire il flag di configurazione **GX_DISABLE_MULTITHREAD_SUPPORT** per eliminare il sovraccarico associato alla protezione delle sezioni di codice critiche dalla pre-svuotamento da parte di più thread. I vari flag di configurazione possono essere definiti nell'origine dell'applicazione, nella riga di comando o nel file **_di inclusione gx_user.h._**

Ogni volta che i flag di configurazione della libreria GUIX vengono modificati, è necessario ricompilare sia la libreria GUIX che i moduli dell'applicazione per l'applicazione delle modifiche di configurazione.

L'elenco completo dei flag di configurazione è documentato nell'Appendice H: GUIX Build-Time di configurazione.

## <a name="guix-version-id"></a>ID versione GUIX

La versione corrente di GUIX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione GUIX dall'esame del file *** gx_port.h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software dell'applicazione può ottenere la versione GUIX esaminando la stringa globale *_ __ gx_version_id_* _ in _*_gx_port.h_**.

Il software applicativo può anche ottenere informazioni sulla versione dalle costanti indicate di seguito definite in ***gx_api.h .*** Queste costanti identificano la versione corrente del prodotto in base al nome e alla versione principale e secondaria del prodotto.

```C
#define __PRODUCT_GUIX__

#define __GUIX_MAJOR_VERSION__

#define __GUIX_MINOR_VERSION__
```
