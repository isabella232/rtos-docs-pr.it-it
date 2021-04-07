---
title: Capitolo 2-installazione & uso di Azure RTO ThreadX SMP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del kernel SMP di HighPerformance Azure RTO ThreadX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cc352ebd7965c84c341d25dfa7bff2671dfb5e66
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550253"
---
# <a name="chapter-2---installation--use-of-azure-rtos-threadx-smp"></a>Capitolo 2-installazione & uso di Azure RTO ThreadX SMP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del kernel SMP di HighPerformance Azure RTO ThreadX.

## <a name="host-considerations"></a>Considerazioni sull'host

Il software incorporato viene in genere sviluppato in computer host Windows o Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo di esecuzione di destinazione (go, Halt, breakpoint e così via), nonché di accedere ai registri della memoria e del processore.

La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE). Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.

Per quanto riguarda le risorse usate nell'host, il codice sorgente per ThreadX SMP viene distribuito in formato ASCII e richiede circa 1 MB di spazio sul disco rigido del computer host.

> [!IMPORTANT]
> Per ulteriori considerazioni e opzioni relative al sistema host, consultare il file di **readme_threadx.txt** fornito.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

ThreadX SMP richiede tra 2 kbyte e 20 KByte di memoria di sola lettura (ROM) nella destinazione. Per lo stack di sistema ThreadX SMP e altre strutture di dati globali sono necessari un altro da 1 a 2 KB della memoria ad accesso casuale (RAM) della destinazione.

Per le funzioni correlate al timer, ad esempio i timeout delle chiamate al servizio, il sezionamento di tempo e i timer dell'applicazione per funzionare, l'hardware di destinazione sottostante deve fornire un'origine di interrupt periodica. Se il processore dispone di questa funzionalità, viene utilizzato da ThreadX SMP. In caso contrario, se il processore di destinazione non è in grado di generare un interrupt periodico, l'hardware dell'utente deve fornirlo. Il programma di installazione e configurazione dell'interrupt del timer si trova in genere nel file di assembly ***tx_initialize_low_level*** nella distribuzione SMP di threadX.

> [!IMPORTANT]
> ThreadX SMP è ancora funzionante anche se non è disponibile un'origine interrupt del timer periodica. Tuttavia, nessuno dei servizi correlati al timer è funzionante. Verificare il file di **readme_threadx.txt** fornito per eventuali considerazioni e/o opzioni aggiuntive relative al sistema host.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il contenuto esatto del disco di distribuzione dipende dal processore di destinazione, dagli strumenti di sviluppo e dal pacchetto SMP ThreadX acquistato. Tuttavia, di seguito è riportato un elenco di diversi file importanti comuni alla maggior parte delle distribuzioni di prodotti:

### <a name="threadx_express_startuppdf"></a>ThreadX_Express_Startup.pdf

Questo PDF fornisce una semplice procedura in quattro passaggi per l'esecuzione di ThreadX SMP in uno specifico processore/lavagna di destinazione e strumenti di sviluppo specifici.

### <a name="readme_threadxtxt"></a>readme_threadx.txt

File di testo contenente informazioni specifiche sulla porta SMP di ThreadX, incluse le informazioni sul processore di destinazione e gli strumenti di sviluppo.

| Strumento | Descrizione |
| -------------- | ------------------------------------------------------------------------------------------------- |
| **tx_api. h**  | File di intestazione C contenente tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.             |
| **tx_port. h** | File di intestazione C contenente tutte le strutture e le definizioni dei dati dello strumento di sviluppo e del targetspecific. |
|**demo_threadx. c**| File C contenente una piccola applicazione demo.|
|**TX. a (o TX. lib)**| Versione binaria della libreria ThreadX SMP C distribuita con il pacchetto *standard* .|

> [!IMPORTANT]
> Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Linux (Unix).

## <a name="threadx-smp-installation"></a>Installazione SMP di ThreadX

L'installazione di ThreadX SMP è semplice. Per informazioni specifiche sull'installazione di ThreadX SMP per un ambiente specifico, vedere il file ***ThreadX_Express_Startup.pdf** _ e il file _ *_readme_threadx.txt_**.

> [!IMPORTANT]
> Assicurarsi di eseguire il backup del disco di distribuzione SMP di ThreadX e archiviarlo in un luogo sicuro.

> [!IMPORTANT]
> Il software applicativo deve accedere al file della libreria SMP di ThreadX (in genere **TX. a** o **TX. lib**) e i file di inclusione C **tx_api. h** e **tx_port. h**. Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.

## <a name="using-threadx-smp"></a>Uso di ThreadX SMP

L'uso di ThreadX SMP è facile. In pratica, il codice dell'applicazione deve includere ***tx_api. h** _ durante la compilazione e il collegamento con la libreria di runtime threadX SMP _*_TX. a_*_ (o _ *_TX. lib)_* *.

Per compilare un'applicazione SMP di ThreadX, è necessario eseguire quattro passaggi:

Includere il file ***tx_api. h*** in tutti i file dell'applicazione che utilizzano i servizi o le strutture di dati threadX SMP.

Creare la funzione C ***Main** _ standard. Questa funzione deve chiamare _ *_tx_kernel_enter_** per avviare threadX SMP. Prima di immettere il kernel, è possibile aggiungere un'inizializzazione specifica dell'applicazione che non implica ThreadX SMP.

> [!IMPORTANT]
> La funzione entry SMP di ThreadX **tx_kernel_enter** non restituisce alcun risultato. Assicurarsi pertanto di non inserire alcuna chiamata di elaborazione o di funzione dopo di esso.

Creare la funzione ***tx_application_define*** . Questo è il punto in cui vengono create le risorse di sistema iniziali. Esempi di risorse di sistema includono thread, code, pool di memoria, gruppi di flag di evento, mutex e semafori.

Compilare l'origine e il collegamento dell'applicazione con la libreria di runtime SMP di ThreadX, ***TX. lib***. L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Il piccolo sistema di esempio nella figura 1 nella pagina 28 Mostra la creazione di un singolo thread con la priorità 3. Il thread viene eseguito, incrementa un contatore, quindi dorme per un tick del clock. Questo processo continua per sempre.

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

Sebbene questo sia un semplice esempio, fornisce un modello efficace per lo sviluppo di applicazioni reali. Per ulteriori informazioni, vedere il file di ***readme_threadx.txt*** .

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta SMP ThreadX viene fornita con un'applicazione dimostrativa. È sempre consigliabile ottenere prima di tutto il sistema dimostrativo in esecuzione, nell'hardware di destinazione effettivo o nell'ambiente simulato.

> [!IMPORTANT]
> Per informazioni più specifiche sul sistema dimostrativo, vedere il file di **readme_threadx.txt** fornito con la distribuzione.

Se il sistema dimostrativo non viene eseguito correttamente, di seguito sono riportati alcuni suggerimenti per la risoluzione dei problemi:

  - Determinare la quantità della dimostrazione eseguita.

  - Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice dell'applicazione effettivo rispetto a quello per la dimostrazione).

  - Ricompilare la libreria SMP di ThreadX con TX_ENABLE_STACK_CHECKING definito. In questo modo verrà abilitato il controllo dello stack SMP di ThreadX incorporato.

  - Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato. Tali informazioni dovrebbero risultare utili per supportare i tecnici.

Seguire le procedure descritte in "cosa è necessario per l'utente" nella pagina 12 per inviare le informazioni raccolte dalle procedure per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione quando si compila la libreria SMP di ThreadX e l'applicazione usando ThreadX SMP. Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***tx_user. h*** .

> [!IMPORTANT]
> Le opzioni definite in **tx_user. h** vengono applicate solo se l'applicazione e la libreria SMP threadX sono compilate con **TX_INCLUDE_USER_DEFINE_FILE** definito.

### <a name="smallest-configuration"></a>Configurazione minima
Per le dimensioni del codice più ridotte, è necessario considerare le seguenti opzioni di configurazione di ThreadX SMP (in assenza di tutte le altre opzioni):

- TX_DISABLE_ERROR_CHECKING
- TX_DISABLE_PREEMPTION_THRESHOLD
- TX_DISABLE_NOTIFY_CALLBACKS 
- TX_DISABLE_REDUNDANT_CLEARING 
- TX_DISABLE_STACK_FILLING 
- TX_NOT_INTERRUPTABLE 
- TX_TIMER_PROCESS_IN_ISR

### <a name="fastest-configuration"></a>Configurazione più veloce 
Per l'esecuzione più veloce, le stesse opzioni di configurazione usate per la configurazione più piccola in precedenza, ma con questa opzione anche:

- TX_REACTIVATE_INLINE

Esaminare il file di ***readme_threadx.txt*** per ottenere opzioni aggiuntive per la versione specifica di threadX SMP. Le opzioni di configurazione dettagliate sono descritte a partire dalla pagina 28.

### <a name="global-time-source"></a>Origine ora globale  
Per altri prodotti Azure RTO (FileX, NetX, GUIX, USBX e così via), ThreadX SMP definisce il numero di cicli del timer SMP ThreadX che rappresentano un secondo. Altre derivano i requisiti temporali in base a questa costante. Per impostazione predefinita, il valore è 100, supponendo un interrupt 10 ms periodico. È possibile che l'utente esegua l'override di questo valore definendo TX_TIMER_TICKS_PER_SECOND con il valore desiderato in ***tx_port. h*** o all'interno dell'IDE o della riga di comando.

### <a name="detailed-configuration-options"></a>Opzioni di configurazione dettagliate

- **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni nei pool di blocchi. Per impostazione predefinita, questa opzione non è definita.
- **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni nei pool di byte. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_ERROR_CHECKING**: ignora il controllo degli errori di chiamata al servizio di base. Quando viene definito nell'origine dell'applicazione, tutto il controllo degli errori dei parametri di base è disabilitato. Questo può migliorare le prestazioni fino al 30% e può anche ridurre le dimensioni dell'immagine.

> [!NOTE]
> *È possibile disabilitare il controllo degli errori solo se l'applicazione è in grado di garantire che tutti i parametri di input siano sempre validi in tutte le circostanze, inclusi i parametri di input derivati dall'input esterno. Se all'API viene fornito un input non valido con il controllo degli errori disabilitato, il comportamento risultante non è definito e potrebbe causare un danneggiamento della memoria o un arresto anomalo del sistema.*

> [!NOTE]
> *I valori restituiti dell'API SMP di ThreadX non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella sezione "valori restituiti" della descrizione di ogni API del capitolo 4. I valori restituiti non in grassetto sono void se il controllo degli errori viene disabilitato usando l'opzione TX_DISABLE_ERROR_CHECKING.*
- **TX_DISABLE_NOTIFY_CALLBACKS** : se definito, Disabilita i callback di notifica per diversi oggetti SMP di threadX. L'utilizzo di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_PREEMPTION_THRESHOLD** : se definito, Disabilita la funzionalità di soglia di precedenza e riduce leggermente le dimensioni del codice e migliora le prestazioni. Naturalmente, le funzionalità di preemptionthreshold non sono più disponibili. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_REDUNDANT_CLEARING** : se definito, rimuove la logica per l'inizializzazione di strutture di dati C globali threadX SMP su zero. Questa operazione deve essere usata solo se il codice di inizializzazione del compilatore imposta tutti i dati globali non inizializzati su zero. L'utilizzo di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni durante l'inizializzazione. Per impostazione predefinita, questa opzione non è definita.
- **TX_DISABLE_STACK_FILLING** : se definito, Disabilita l'inserimento del valore 0xEF in ogni byte dello stack di ogni thread al momento della creazione. Per impostazione predefinita, questa opzione non è definita.
- **TX_ENABLE_EVENT_TRACE** : quando viene definito, threadX SMP Abilita il codice di raccolta eventi per la creazione di un buffer di traccia TraceX. Per ulteriori informazioni, vedere la guida dell'utente di TraceX.
- **TX_ENABLE_STACK_CHECKING** : quando viene definito, Abilita il controllo dello stack di runtime SMP di threadX, che include l'analisi dello stack usato e l'esame del modello di dati "barriere" prima e dopo l'area dello stack. Se viene rilevato un errore dello stack, viene chiamato il gestore degli errori dello stack dell'applicazione registrato. Questa opzione comporta un sovraccarico leggermente maggiore e una dimensione del codice. Per ulteriori informazioni, vedere l'API **_tx_-thread_stack_error_notify_** . Per impostazione predefinita, questa opzione non è definita.
- **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni nei gruppi di flag di evento. Per impostazione predefinita, questa opzione non è definita.
- **TX_INLINE_THREAD_RESUME_SUSPEND** : quando viene definito, threadX SMP migliora le chiamate API **_tx_thread_resume_*_ e _*_tx_thread_suspend_** tramite codice inline. Questo aumenta le dimensioni del codice, ma migliora le prestazioni di queste due chiamate API.
- **TX_MAX_PRIORITIES** : definisce i livelli di priorità per threadX SMP. I valori validi sono compresi tra 32 e 1024 (inclusi) e devono essere divisibile in modo uniforme per 32. L'aumento del numero di livelli di priorità supportati aumenta l'utilizzo della RAM di 128 byte per ogni gruppo di 32 priorità. Tuttavia, esiste solo un effetto trascurabile sulle prestazioni. Per impostazione predefinita, questo valore è impostato su 32 livelli di priorità.
- **TX_MINIMUM_STACK** : definisce la dimensione minima dello stack (in byte). Viene usato per il controllo degli errori quando vengono creati i thread. Il valore predefinito è specifico della porta ed è disponibile in **_tx_port. h._**
- **TX_MISRA_ENABLE** : quando viene definito, threadX SMP usa le convenzioni conformi a MISRA C. Per informazioni dettagliate, fare riferimento al **_ThreadX_MISRA_Compliance.pdf_** .
- **TX_MUTEX_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni nei mutex. Per impostazione predefinita, questa opzione non è definita.
- **TX_NO_TIMER** : quando è definito, la logica del timer SMP di threadX è completamente disabilitata. Questa operazione è utile nei casi in cui le funzionalità del timer SMP di ThreadX (sospensione thread, timeout API, sezionamento del tempo e timer applicazione) non vengono utilizzate.
- **TX_NOT_INTERRUPTABLE** : quando viene definito, threadX SMP non tenta di ridurre al minimo il tempo di blocco dell'interrupt. Questo comporta un'esecuzione più rapida, ma aumenta leggermente il tempo di blocco dell'interrupt.
- **TX_QUEUE_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni sulle code. Per impostazione predefinita, questa opzione non è definita.
- **TX_REACTIVATE_INLINE** : se definito, esegue la riattivazione dei timer SMP di threadX inline anziché usare una chiamata di funzione. Ciò migliora le prestazioni, ma aumenta leggermente le dimensioni del codice. Per impostazione predefinita, questa opzione non è definita.
- **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni sui semafori. Per impostazione predefinita, questa opzione non è definita.
- **TX_THREAD_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni nei thread. Per impostazione predefinita, questa opzione non è definita.
- **TX_THREAD_SMP_CORE_MASK** : definisce la maschera della mappa di bit per l'esclusione di base. Ad esempio, un ambiente con 4 core ha un valore 0xF per questa definizione.
- **TX_THREAD_SMP_DEBUG_ENABLE** : se definito, le informazioni di debug SMP di threadX vengono salvate in un buffer circolare.
- **TX_THREAD_SMP_DYNAMIC_CORE_MAX** : se definito, Abilita il numero massimo dinamico di core che possono essere modificati in fase di esecuzione.
- **TX_THREAD_SMP_EQUAL_PRIORITY** : quando viene definito, threadX SMP Pianifica solo i thread con priorità uguale in parallelo. Questa operazione deve essere definita prima di compilare la libreria SMP di ThreadX.
- **TX_THREAD_SMP_INTER_CORE_INTERRUPT** : quando viene definito, threadX SMP genera interrupt tra core.
- **TX_THREAD_SMP_MAX_CORES** : definisce il numero massimo di core.
- **TX_THREAD_SMP_ONLY_CORE_0_DEFAULT** : quando viene definito, threadX SMP imposta come predefinite tutti i thread e i timer per l'esecuzione solo su Core 0 per impostazione predefinita. È possibile che l'applicazione esegua l'override di questa operazione chiamando le API principali di esclusione. Questa operazione deve essere definita prima di compilare la libreria SMP di ThreadX.
- **TX_THREAD_SMP_WAKEUP_LOGIC** : se definito, viene richiamata la macro dell'applicazione per riattivare "i" core. Questo deve essere definito prima dell'inclusione di **_tx_port. h._**
- **TX_THREAD_SMP_WAKEUP (i)** : definisce una macro dell'applicazione per riattivare i core "i". Questo deve essere definito prima dell'inclusione di **_tx_port. h._**
- **TX_TIMER_ENABLE_PERFORMANCE_INFO** : se definito, Abilita la raccolta di informazioni sulle prestazioni sui timer. Per impostazione predefinita, questa opzione non è definita.
- **TX_TIMER_PROCESS_IN_ISR** : se definito, Elimina il thread del timer di sistema interno per threadX SMP. Ciò comporta un miglioramento delle prestazioni sugli eventi del timer e requisiti di RAM più piccoli, perché lo stack del timer e il blocco di controllo non sono più necessari. Tuttavia, se si usa questa opzione, l'elaborazione della scadenza del timer viene spostata al livello ISR del timer. Per impostazione predefinita, questa opzione non è definita.

    > [!NOTE]
    > I servizi consentiti dai timer potrebbero non essere consentiti da ISRs, pertanto potrebbe non essere consentito quando si utilizza questa opzione.

- **TX_TIMER_THREAD_PRIORITY** : definisce la priorità del thread timer di sistema threadX SMP interno. Il valore predefinito è priority 0, ovvero la priorità più alta in ThreadX SMP. Il valore predefinito è definito in **_tx_port. h._**
- **TX_TIMER_THREAD_STACK_SIZE** : definisce la dimensione dello stack (in byte) del thread del timer di sistema threadX SMP interno. Questo thread elabora tutte le richieste di sospensione del thread, nonché tutti i timeout delle chiamate al servizio. Inoltre, tutte le routine di callback del timer applicazione vengono richiamate da questo contesto. Il valore predefinito è specifico della porta ed è disponibile in **_tx_port. h._**

## <a name="threadx-smp-version-id"></a>ID versione SMP di ThreadX

L'ID della versione SMP di ThreadX è disponibile nel file ***readme_threadx.txt** _. Questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di ThreadX SMP esaminando la stringa globale _ *_ _tx_version_id._**