---
title: Capitolo 2 - Installazione &'uso di Azure RTOS ThreadX SMP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del kernel SMP Azure RTOS ThreadX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d0a63f3798adbc634a43cdda7e9d44941de655d9333f9ae0fb4181f1a6c0566e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801904"
---
# <a name="chapter-2---installation--use-of-azure-rtos-threadx-smp"></a>Capitolo 2 - Installazione &'uso di Azure RTOS ThreadX SMP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del kernel SMP Azure RTOS ThreadX.

## <a name="host-considerations"></a>Considerazioni sull'host

Il software incorporato viene in genere sviluppato Windows computer host Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

In genere il download di destinazione viene eseguito dall'interno del debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile del controllo dell'esecuzione di destinazione (go, halt, breakpoint e così via), nonché dell'accesso ai registri di memoria e del processore.

La maggior parte dei debugger degli strumenti di sviluppo comunica con l'hardware di destinazione tramite connessioni OCD (On-Chip Debug), ad esempio JTAG (IEEE 1149.1) e modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite In-Circuit di emulazione (ICE). Entrambe le connessioni OCD e ICE offrono soluzioni affidabili con intrusioni minime sul software residente di destinazione.

Come per le risorse usate nell'host, il codice sorgente per ThreadX SMP viene fornito in formato ASCII e richiede circa 1 MByte di spazio sul disco rigido del computer host.

> [!IMPORTANT]
> Per altre considerazioni e opzioni **sul sistema host, vedere** il filereadme_threadx.txtfornito.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

ThreadX SMP richiede da 2 KByte a 20 KByte di memoria di sola lettura (ROM) nella destinazione. Altri 1-2 KByte della memoria ad accesso casuale (RAM) della destinazione sono necessari per lo stack di sistema SMP ThreadX e altre strutture di dati globali.

Per il funzionamento di funzioni correlate al timer come timeout delle chiamate al servizio, sezione temporale e timer dell'applicazione, l'hardware di destinazione sottostante deve fornire un'origine di interrupt periodica. Se il processore ha questa funzionalità, viene utilizzato da ThreadX SMP. In caso contrario, se il processore di destinazione non è in grado di generare un interrupt periodico, l'hardware dell'utente deve fornirlo. L'installazione e la configurazione dell'interrupt timer si trovano in genere nel file ***tx_initialize_low_level*** assembly nella distribuzione SMP ThreadX.

> [!IMPORTANT]
> ThreadX SMP è ancora funzionante anche se non è disponibile alcuna origine di interrupt timer periodico. Tuttavia, nessuno dei servizi correlati al timer funziona. Esaminare il file di **readme_threadx.txt** per eventuali considerazioni aggiuntive sul sistema host e/o opzioni.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il contenuto esatto del disco di distribuzione dipende dal processore di destinazione, dagli strumenti di sviluppo e dal pacchetto ThreadX SMP acquistato. Tuttavia, di seguito è riportato un elenco di diversi file importanti comuni alla maggior parte delle distribuzioni di prodotti:

### <a name="threadx_express_startuppdf"></a>ThreadX_Express_Startup.pdf

Questo FILE PDF offre una procedura semplice in quattro passaggi per l'esecuzione di ThreadX SMP in uno specifico processore/scheda di destinazione e in strumenti di sviluppo specifici.

### <a name="readme_threadxtxt"></a>readme_threadx.txt

File di testo contenente informazioni specifiche sulla porta SMP ThreadX, incluse le informazioni sul processore di destinazione e sugli strumenti di sviluppo.

| Strumento | Descrizione |
| -------------- | ------------------------------------------------------------------------------------------------- |
| **tx_api.h**  | File di intestazione C contenente tutti gli elementi di sistema, le strutture dei dati e i prototipi di servizio.             |
| **tx_port.h** | File di intestazione C contenente tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo e della destinazione. |
|**demo_threadx.c**| File C contenente una piccola applicazione demo.|
|**tx.a (o tx.lib)**| Versione binaria della libreria ThreadX SMP C distribuita con il *pacchetto standard.*|

> [!IMPORTANT]
> Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione semplifica la conversione dei comandi in piattaforme di sviluppo Linux (Unix).

## <a name="threadx-smp-installation"></a>Installazione di ThreadX SMP

L'installazione di ThreadX SMP è semplice. Fare riferimento al file ***ThreadX_Express_Startup.pdf** _ e al file _ *_readme_threadx.txt_** per informazioni specifiche sull'installazione di ThreadX SMP per l'ambiente specifico.

> [!IMPORTANT]
> Assicurarsi di eseguire il backup del disco di distribuzione SMP ThreadX e archiviarlo in una posizione sicura.

> [!IMPORTANT]
> Il software dell'applicazione deve accedere al file di libreria ThreadX SMP (in genere **tx.a** o **tx.lib)** e ai file di inclusione C **tx_api.h** **e tx_port.h**. Questa operazione viene eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.

## <a name="using-threadx-smp"></a>Uso di ThreadX SMP

L'uso di ThreadX SMP è semplice. Fondamentalmente, il codice dell'applicazione deve includere ***tx_api.h** _ durante la compilazione e il collegamento con la libreria di runtime ThreadX SMP _*_tx.a_*_ (o _*_tx.lib)_**.

Per compilare un'applicazione ThreadX SMP sono necessari quattro passaggi:

Includere il ***file tx_api.h*** in tutti i file dell'applicazione che usano i servizi ThreadX SMP o le strutture di dati.

Creare la funzione C ***main** _ standard. Questa funzione deve chiamare alla fine _ *_tx_kernel_enter_** per avviare ThreadX SMP. L'inizializzazione specifica dell'applicazione che non coinvolge ThreadX SMP può essere aggiunta prima di accedere al kernel.

> [!IMPORTANT]
> La funzione di ingresso ThreadX SMP **tx_kernel_enter** non restituisce . Assicurarsi quindi di non inserire alcuna elaborazione o chiamata di funzione dopo di essa.

Creare la ***tx_application_define*** funzione. Qui vengono create le risorse di sistema iniziali. Esempi di risorse di sistema includono thread, code, pool di memoria, gruppi di flag di eventi, mutex e semafori.

Compilare l'origine dell'applicazione e collegarsi alla libreria di runtime ThreadX SMP ***tx.lib***. L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Il piccolo sistema di esempio nella figura 1 a pagina 28 illustra la creazione di un singolo thread con priorità 3. Il thread viene eseguito, incrementa un contatore e quindi viene in sospensione per un clock tick. Questo processo continua per sempre.

```c
#include              "tx_api.h"

unsigned long         my_thread_counter = 0;
TX_THREAD             my_thread;

main( )
{
      /* Enter the ThreadX SMP kernel. */
      tx_kernel_enter( );
}

void tx_application_define(void *first_unused_memory)
{

      /* Create my_thread! */
      tx_thread_create(&my_thread, "My Thread",
          my_thread_entry, 0x1234, first_unused_memory, 1024,
             3, 3, TX_NO_TIME_SLICE, TX_AUTO_START);
}

void my_thread_entry(ULONG thread_input)
{
      /* Enter into a forever loop. */
      while(1)
      {

            /* Increment thread counter. */
            my_thread_counter++;

            /* Sleep for 1 tick. */
            tx_thread_sleep(1);
      }
}
```
**FIGURA 1. Modello per lo sviluppo di applicazioni**

Anche se si tratta di un esempio semplice, fornisce un buon modello per lo sviluppo di applicazioni reali. Ancora una volta, vedere il file ***readme_threadx.txt*** per altri dettagli.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta SMP ThreadX viene recapitata con un'applicazione dimostrativa. È sempre una buona idea far eseguire prima il sistema dimostrativo, ovvero sull'hardware di destinazione effettivo o sull'ambiente simulato.

> [!IMPORTANT]
> Vedere **il** readme_threadx.txtfile fornito con la distribuzione per informazioni più specifiche sul sistema dimostrativo.

Se il sistema dimostrativo non viene eseguito correttamente, di seguito sono riportati alcuni suggerimenti per la risoluzione dei problemi:

  - Determinare la quantità di esecuzione della dimostrazione.

  - Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice dell'applicazione effettivo rispetto alla dimostrazione).

  - Ricompilare la libreria ThreadX SMP con TX_ENABLE_STACK_CHECKING definito. In questo modo verrà abilitato il controllo dello stack SMP ThreadX incorporato.

  - Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o cambia. Tali informazioni dovrebbero risultare utili per supportare i tecnici.

Seguire le procedure descritte in "What We Need From You" a pagina 12 per inviare le informazioni raccolte dai passaggi per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria ThreadX SMP e l'applicazione usando ThreadX SMP, sono disponibili diverse opzioni di configurazione. Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file ***di inclusione tx_user.h.***

> [!IMPORTANT]
> Le opzioni definite in **tx_user.h** vengono applicate solo se l'applicazione  e la libreria ThreadX SMP vengono compilate con TX_INCLUDE_USER_DEFINE_FILE definite.

### <a name="smallest-configuration"></a>Configurazione più piccola
Per le dimensioni del codice più piccole, devono essere considerate le opzioni di configurazione SMP ThreadX seguenti (in assenza di tutte le altre opzioni):

- TX_DISABLE_ERROR_CHECKING
- TX_DISABLE_PREEMPTION_THRESHOLD
- TX_DISABLE_NOTIFY_CALLBACKS 
- TX_DISABLE_REDUNDANT_CLEARING 
- TX_DISABLE_STACK_FILLING 
- TX_NOT_INTERRUPTABLE 
- TX_TIMER_PROCESS_IN_ISR

### <a name="fastest-configuration"></a>Configurazione più veloce 
Per l'esecuzione più rapida, le stesse opzioni di configurazione usate in precedenza per la configurazione più piccola, ma con questa opzione vengono considerate anche:

- TX_REACTIVATE_INLINE

Esaminare il ***readme_threadx.txt*** file per altre opzioni per la versione specifica di ThreadX SMP. Le opzioni di configurazione dettagliate sono descritte a partire dalla pagina 28.

### <a name="global-time-source"></a>Origine ora globale  
Per altri prodotti Azure RTOS (FileX, NetX, GUIX, USBX e così via), ThreadX SMP definisce il numero di tick del timer SMP ThreadX che rappresenta un secondo. Altri derivano i requisiti di tempo in base a questa costante. Per impostazione predefinita, il valore è 100, presupponendo un interrupt periodico di 10 ms. L'utente può eseguire l'override di questo valore definendo TX_TIMER_TICKS_PER_SECOND con il valore desiderato in ***tx_port.h*** o all'interno dell'IDE o della riga di comando.

### <a name="detailed-configuration-options"></a>Opzioni di configurazione dettagliate

- **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni nei pool di blocchi. Per impostazione predefinita, questa opzione non è definita.
- **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni nei pool di byte. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_ERROR_CHECKING**: ignora il controllo degli errori di base delle chiamate al servizio. Se definito nell'origine dell'applicazione, il controllo degli errori dei parametri di base è disabilitato. Questo può migliorare le prestazioni fino al 30% e può anche ridurre le dimensioni dell'immagine.

> [!NOTE]
> *È possibile disabilitare il controllo degli errori solo se l'applicazione è assolutamente in grado di garantire che tutti i parametri di input siano sempre validi in tutte le circostanze, inclusi i parametri di input derivati dall'input esterno. Se all'API viene fornito un input non valido con il controllo degli errori disabilitato, il comportamento risultante non è definito e potrebbe causare il danneggiamento della memoria o l'arresto anomalo del sistema.*

> [!NOTE]
> *I valori restituiti dell'API SMP ThreadX non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella sezione "Valori restituiti" di ogni descrizione dell'API nel capitolo 4. I valori restituiti nonbold sono void se il controllo degli errori è disabilitato usando l'TX_DISABLE_ERROR_CHECKING predefinita.*
- **TX_DISABLE_NOTIFY_CALLBACKS:** se definito, disabilita i callback di notifica per vari oggetti SMP ThreadX. L'uso di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_PREEMPTION_THRESHOLD:** se definita, disabilita la funzionalità di soglia di precedenza e riduce leggermente le dimensioni del codice e migliora le prestazioni. Naturalmente, le funzionalità di preemptionthreshold non sono più disponibili. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_REDUNDANT_CLEARING:** se definito, rimuove la logica per l'inizializzazione delle strutture di dati C globali ThreadX SMP su zero. Deve essere usato solo se il codice di inizializzazione del compilatore imposta tutti i dati globali C non inizializzati su zero. L'uso di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni durante l'inizializzazione. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_STACK_FILLING:** se definito, disabilita l'inserimento del 0xEF in ogni byte dello stack di ogni thread al momento della creazione. Per impostazione predefinita, questa opzione non è definita.
- **TX_ENABLE_EVENT_TRACE:** se definito, ThreadX SMP abilita il codice di raccolta eventi per la creazione di un buffer di traccia TraceX. Per altri dettagli, vedere la Guida dell'utente di TraceX.
- **TX_ENABLE_STACK_CHECKING:** se definito, abilita il controllo dello stack di run-time SMP ThreadX, che include l'analisi della quantità di stack usata e l'esame dei "recinti" del modello di dati prima e dopo l'area dello stack. Se viene rilevato un errore dello stack, viene chiamato il gestore degli errori dello stack dell'applicazione registrato. Questa opzione comporta un leggero aumento del sovraccarico e delle dimensioni del codice. Per altre **_informazioni,_ vedere l'API tx - thread_stack_error_notify_.** Per impostazione predefinita, questa opzione non è definita.
- **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni sui gruppi di flag di evento. Per impostazione predefinita, questa opzione non è definita.
- **TX_INLINE_THREAD_RESUME_SUSPEND:** se definito, ThreadX SMP migliora le tx_thread_resume _ e ***_*_tx_thread_suspend_** api tramite codice inline. Ciò aumenta le dimensioni del codice, ma migliora le prestazioni di queste due chiamate API.
- **TX_MAX_PRIORITIES** : definisce i livelli di priorità per ThreadX SMP. I valori validi sono compresi tra 32 e 1024 (inclusi) e devono essere divisibile uniformemente per 32. L'aumento del numero di livelli di priorità supportati aumenta l'utilizzo della RAM di 128 byte per ogni gruppo di 32 priorità. Tuttavia, esiste solo un effetto trascurabile sulle prestazioni. Per impostazione predefinita, questo valore è impostato su 32 livelli di priorità.
- **TX_MINIMUM_STACK** : definisce le dimensioni minime dello stack (in byte). Viene usato per il controllo degli errori quando vengono creati i thread. Il valore predefinito è specifico della porta e si trova in **_tx_port.h._**
- **TX_MISRA_ENABLE:** se definito, ThreadX SMP usa convenzioni conformi a MISRA C. Per informazioni **_dettagliate, vedere_** ThreadX_MISRA_Compliance.pdf.
- **TX_MUTEX_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni sui mutex. Per impostazione predefinita, questa opzione non è definita.
- **TX_NO_TIMER:** se definita, la logica del timer SMP ThreadX è completamente disabilitata. Ciò è utile nei casi in cui le funzionalità del timer SMP ThreadX (sospensione thread, timeout API, sezione temporale e timer dell'applicazione) non vengono utilizzate.
- **TX_NOT_INTERRUPTABLE:** se definito, ThreadX SMP non tenta di ridurre al minimo il tempo di blocco dell'interrupt. Ciò comporta un'esecuzione più rapida, ma aumenta leggermente il tempo di blocco dell'interrupt.
- **TX_QUEUE_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni nelle code. Per impostazione predefinita, questa opzione non è definita.
- **TX_REACTIVATE_INLINE:** se definito, esegue la riattivazione dei timer SMP ThreadX in linea invece di usare una chiamata di funzione. Ciò migliora le prestazioni, ma aumenta leggermente le dimensioni del codice. Per impostazione predefinita, questa opzione non è definita.
- **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni sui semafori. Per impostazione predefinita, questa opzione non è definita.
- **TX_THREAD_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni nei thread. Per impostazione predefinita, questa opzione non è definita.
- **TX_THREAD_SMP_CORE_MASK** : definisce la maschera della mappa di bit per l'esclusione CORE. Ad esempio, un ambiente a 4 core ha un valore di 0xF per questa definizione.
- **TX_THREAD_SMP_DEBUG_ENABLE:** se definite, le informazioni di debug SMP Di ThreadX vengono salvate in un buffer circolare.
- **TX_THREAD_SMP_DYNAMIC_CORE_MAX:** se definito, abilita il numero massimo dinamico di core che possono essere modificati in fase di esecuzione.
- **TX_THREAD_SMP_EQUAL_PRIORITY:** se definito, ThreadX SMP pianifica solo thread con uguale priorità in parallelo. Questo valore deve essere definito prima di compilare la libreria ThreadX SMP.
- **TX_THREAD_SMP_INTER_CORE_INTERRUPT:** se definito, ThreadX SMP genera interrupt inter-core.
- **TX_THREAD_SMP_MAX_CORES** : definisce il numero massimo di core.
- **TX_THREAD_SMP_ONLY_CORE_0_DEFAULT:** se definito, ThreadX SMP consente l'esecuzione di tutti i thread e i timer solo nel core 0 per impostazione predefinita. L'applicazione può eseguire l'override chiamando le API di esclusione core. Questo valore deve essere definito prima di compilare la libreria ThreadX SMP.
- **TX_THREAD_SMP_WAKEUP_LOGIC:** quando è definito, viene richiamata la macro dell'applicazione per riattivare il core "i". Deve essere definito prima dell'inclusione di **_tx_port.h._**
- **TX_THREAD_SMP_WAKEUP(i)** : definisce una macro dell'applicazione per riattivare il core "i". Deve essere definito prima dell'inclusione di **_tx_port.h._**
- **TX_TIMER_ENABLE_PERFORMANCE_INFO:** se definito, consente la raccolta di informazioni sulle prestazioni sui timer. Per impostazione predefinita, questa opzione non è definita.
- **TX_TIMER_PROCESS_IN_ISR:** se definito, elimina il thread timer di sistema interno per ThreadX SMP. Ciò comporta prestazioni migliorate per gli eventi timer e requisiti di RAM più piccoli perché lo stack timer e il blocco di controllo non sono più necessari. Tuttavia, l'uso di questa opzione sposta tutta l'elaborazione della scadenza del timer al livello ISR del timer. Per impostazione predefinita, questa opzione non è definita.

    > [!NOTE]
    > I servizi consentiti dai timer potrebbero non essere consentiti dagli ISR e pertanto potrebbero non essere consentiti quando si usa questa opzione.

- **TX_TIMER_THREAD_PRIORITY** : definisce la priorità del thread del timer di sistema SMP ThreadX interno. Il valore predefinito è la priorità 0, ovvero la priorità più alta in ThreadX SMP. Il valore predefinito è definito in **_tx_port.h._**
- **TX_TIMER_THREAD_STACK_SIZE** : definisce le dimensioni dello stack (in byte) del thread del timer di sistema SMP ThreadX interno. Questo thread elabora tutte le richieste di sospensione dei thread, nonché tutti i timeout delle chiamate al servizio. Inoltre, tutte le routine di callback del timer dell'applicazione vengono richiamate da questo contesto. Il valore predefinito è specifico della porta e si trova in **_tx_port.h._**

## <a name="threadx-smp-version-id"></a>ID versione SMP ThreadX

L'ID versione di ThreadX SMP è disponibile nel file ***readme_threadx.txt** _. Questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software dell'applicazione può ottenere la versione di ThreadX SMP esaminando la stringa globale _ *_ _tx_version_id._**