---
title: Capitolo 2-installazione e uso di Azure RTO ThreadX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del kernel ThreadX di Azure RTO ad alte prestazioni.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e1bf85d363b07c81f226d494107eae9ba18114a7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821359"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-threadx"></a>Capitolo 2-installazione e uso di Azure RTO ThreadX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del kernel ThreadX di Azure RTO ad alte prestazioni.

## <a name="host-considerations"></a>Considerazioni sull'host

Il software incorporato viene in genere sviluppato in computer host Windows o Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo. Al termine del download, il debugger è responsabile per fornire il controllo dell'esecuzione di destinazione (go, Halt, breakpoint e così via), nonché per accedere ai registri della memoria e del processore.

La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE). Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.

Per quanto riguarda le risorse usate nell'host, il codice sorgente per ThreadX viene fornito in formato ASCII e richiede circa 1 MB di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

ThreadX richiede tra 2 kbyte e 20 KByte di memoria di sola lettura (ROM) nella destinazione. Richiede anche un altro da 1 a 2 KB della memoria ad accesso casuale (RAM) della destinazione per lo stack di sistema ThreadX e altre strutture di dati globali.

Per le funzioni correlate al timer, ad esempio i timeout delle chiamate al servizio, il sezionamento di tempo e i timer dell'applicazione per funzionare, l'hardware di destinazione sottostante deve fornire un'origine di interrupt periodica. Se il processore dispone di questa funzionalità, viene utilizzato da ThreadX. In caso contrario, se il processore di destinazione non è in grado di generare un interrupt periodico, l'hardware dell'utente deve fornirlo. Il programma di installazione e configurazione dell'interrupt del timer si trova in genere nel file di assembly ***tx_initialize_low_level*** nella distribuzione di threadX.

> [!NOTE]
> *ThreadX è ancora funzionante anche se non è disponibile un'origine interrupt del timer periodica. Tuttavia, nessuno dei servizi correlati al timer è funzionante.*

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO ThreadX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/threadx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository.

| Nome file | Descrizione |
|------------------- | ----------- |
| **tx_api. h**                      | File di intestazione C contenente tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.                                                             |
| **tx_port. h**                     | File di intestazione C contenente tutte le strutture e le definizioni dei dati dello strumento di sviluppo e del targetspecific.                                                 |
| **demo_threadx. c**                | File C contenente una piccola applicazione demo.                                                                                                       |
| **TX. a (o TX. lib)**              | Versione binaria della libreria ThreadX C distribuita con il pacchetto *standard* .                                                          |
|                                   |                                                                                                                                                   |

>[!NOTE]
>*Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Linux (Unix).*

## <a name="threadx-installation"></a>Installazione di ThreadX

ThreadX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository ThreadX nel PC.

```c
    git clone https://github.com/azure-rtos/threadx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria ThreadX nella pagina iniziale del repository online.

> [!NOTE]
> * Il software applicativo deve accedere al file di libreria ThreadX (in genere **TX. a** o **TX. lib**) e i file di inclusione C **_tx_api. h_* _ e _*_tx_port. h_*_. Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nello sviluppo di applicazioni area._

## <a name="using-threadx"></a>Uso di ThreadX

Per utilizzare ThreadX, è necessario che il codice dell'applicazione includa ***tx_api. h** _ durante la compilazione e il collegamento con la libreria di runtime threadX _*_TX. a_*_ (o _ *_TX. lib_* *).

Per compilare un'applicazione ThreadX, è necessario eseguire quattro passaggi.

1. Includere il file ***tx_api. h*** in tutti i file dell'applicazione che utilizzano i servizi o le strutture di dati threadX.

1. Creare la funzione C ***Main** _ standard. Questa funzione deve chiamare _ *_tx_kernel_enter_** per avviare threadX. Prima di immettere il kernel, è possibile aggiungere un'inizializzazione specifica dell'applicazione che non include ThreadX.

      > [!IMPORTANT]
      > * La funzione di immissione ThreadX ***tx_kernel_enter** _ non restituisce alcun risultato. Quindi, assicurarsi di non inserire alcuna chiamata di elaborazione o di funzione dopo it._

1. Creare la funzione ***tx_application_define*** . Questo è il punto in cui vengono create le risorse di sistema iniziali. Esempi di risorse di sistema includono thread, code, pool di memoria, gruppi di flag di evento, mutex e semafori.

1. Compilare l'origine e il collegamento dell'applicazione con la libreria di runtime ThreadX ***TX. lib***. L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Il piccolo sistema di esempio nella figura 1 illustra la creazione di un singolo thread con priorità 3. Il thread viene eseguito, incrementa un contatore, quindi dorme per un tick del clock.
Questo processo continua per sempre.

```c
#include "tx_api.h"
unsigned long my_thread_counter = 0;
TX_THREAD my_thread;
main( )
{
    /* Enter the ThreadX kernel. */
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

Sebbene questo sia un semplice esempio, fornisce un modello efficace per lo sviluppo di applicazioni reali.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta ThreadX viene fornita con un'applicazione dimostrativa. È sempre consigliabile ottenere prima di tutto il sistema dimostrativo in esecuzione, nell'hardware di destinazione effettivo o nell'ambiente simulato.

Se il sistema dimostrativo non viene eseguito correttamente, di seguito sono riportati alcuni suggerimenti per la risoluzione dei problemi.

1. Determinare la quantità della dimostrazione in esecuzione.
1. Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice dell'applicazione effettivo rispetto a quello per la dimostrazione).
1. Ricompilare la libreria ThreadX con TX_ENABLE_STACK_CHECKING definito. Questo consente il controllo dello stack ThreadX incorporato.
1. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato. Tali informazioni dovrebbero risultare utili per supportare i tecnici.

Seguire le procedure descritte in "[Customer Support Center](about-this-guide.md#customer-support-center)" per inviare le informazioni raccolte dalle procedure per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compilano la libreria ThreadX e l'applicazione tramite ThreadX, sono disponibili diverse opzioni di configurazione. Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***tx_user. h*** .

> [!IMPORTANT]
> * Le opzioni definite in ***tx_user. h** _ vengono applicate solo se l'applicazione e la libreria threadX sono compilate con _ *TX_INCLUDE_USER_DEFINE_FILE** definito.*

### <a name="smallest-configuration"></a>Configurazione minima

Per le dimensioni del codice più ridotte, è necessario considerare le seguenti opzioni di configurazione di ThreadX (in assenza di tutte le altre opzioni).

```c
TX_DISABLE_ERROR_CHECKING
TX_DISABLE_PREEMPTION_THRESHOLD
TX_DISABLE_NOTIFY_CALLBACKS
TX_DISABLE_REDUNDANT_CLEARING
TX_DISABLE_STACK_FILLING
TX_NOT_INTERRUPTABLE
TX_TIMER_PROCESS_IN_ISR
```

### <a name="fastest-configuration"></a>Configurazione più veloce

Per l'esecuzione più veloce, le stesse opzioni di configurazione usate per la configurazione più piccola in precedenza, ma con queste opzioni considerate anche.

```c
TX_REACTIVATE_INLINE
TX_INLINE_THREAD_RESUME_SUSPEND
```

Sono descritte le [Opzioni di configurazione dettagliate](#detailed-configuration-options) .

### <a name="global-time-source"></a>Origine ora globale

Per altri Microsoft Azure prodotti RTO (FileX, NetX, GUIX, USBX e così via), ThreadX definisce il numero di cicli del timer ThreadX che rappresentano un secondo. Altre derivano i requisiti temporali in base a questa costante. Per impostazione predefinita, il valore è 100, supponendo un interrupt 10 ms periodico. È possibile che l'utente esegua l'override di questo valore definendo TX_TIMER_TICKS_PER_SECOND con il valore desiderato in ***tx_port. h*** o all'interno dell'IDE o della riga di comando.

### <a name="detailed-configuration-options"></a>Opzioni di configurazione dettagliate

**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**

Quando viene definita, questa opzione consente di raccogliere informazioni sulle prestazioni nei pool di byte. Per impostazione predefinita, questa opzione non è definita.

**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**

Quando viene definita, questa opzione consente di raccogliere informazioni sulle prestazioni nei pool di byte. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_ERROR_CHECKING**

Ignora il controllo degli errori di chiamata al servizio di base. Quando viene definito nell'origine dell'applicazione, tutto il controllo degli errori dei parametri di base è disabilitato. Questo può migliorare le prestazioni fino al 30% e può anche ridurre le dimensioni dell'immagine.

> [!NOTE]
> *È possibile disabilitare il controllo degli errori solo se l'applicazione è in grado di garantire che tutti i parametri di input siano sempre validi in tutte le circostanze, inclusi i parametri di input derivati dall'input esterno. Se all'API viene fornito un input non valido con il controllo degli errori disabilitato, il comportamento risultante non è definito e potrebbe causare un danneggiamento della memoria o un arresto anomalo del sistema.*

> [!NOTE]
> *I valori restituiti dell'API ThreadX non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella sezione "valori restituiti" della descrizione di ogni API del capitolo 4. I valori restituiti non in grassetto sono void se il controllo degli errori viene disabilitato usando l'opzione TX_DISABLE_ERROR_CHECKING.*

**TX_DISABLE_NOTIFY_CALLBACKS**

Quando definito, Disabilita i callback di notifica per diversi oggetti ThreadX. L'utilizzo di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_PREEMPTION_THRESHOLD**

Una volta definito, Disabilita la funzionalità di soglia di precedenza e riduce leggermente le dimensioni del codice e migliora le prestazioni. Naturalmente, le funzionalità di soglia di precedenza non sono più disponibili. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_REDUNDANT_CLEARING**

Quando definito, rimuove la logica per l'inizializzazione di strutture di dati C globali ThreadX su zero. Questa operazione deve essere usata solo se il codice di inizializzazione del compilatore imposta tutti i dati globali non inizializzati su zero. L'utilizzo di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni durante l'inizializzazione. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_STACK_FILLING**

Quando viene definito, Disabilita l'inserimento del valore 0xEF in ogni byte dello stack di ogni thread al momento della creazione. Per impostazione predefinita, questa opzione non è definita.

**TX_ENABLE_EVENT_TRACE**

Quando viene definito, ThreadX Abilita il codice di raccolta eventi per la creazione di un buffer di traccia TraceX.

**TX_ENABLE_STACK_CHECKING**

Quando definito, Abilita il controllo dello stack in fase di esecuzione ThreadX, che include l'analisi dello stack usato e l'esame dei "limiti" del modello di dati prima e dopo l'area dello stack. Se viene rilevato un errore dello stack, viene chiamato il gestore degli errori dello stack dell'applicazione registrato. Questa opzione comporta un sovraccarico leggermente maggiore e una dimensione del codice. Per ulteriori informazioni, esaminare la funzione API ***tx_thread_stack_error_notify*** . Per impostazione predefinita, questa opzione non è definita.

**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**

Quando definito, Abilita la raccolta di informazioni sulle prestazioni nei gruppi di flag di evento. Per impostazione predefinita, questa opzione non è definita.

**TX_INLINE_THREAD_RESUME_SUSPEND**

Quando viene definito, ThreadX migliora le chiamate API ***tx_thread_resume** _ e _ *_tx_thread_suspend_** tramite il codice inline. Questo aumenta le dimensioni del codice, ma migliora le prestazioni di queste due chiamate API.

**TX_MAX_PRIORITIES**

Definisce i livelli di priorità per ThreadX. I valori validi sono compresi tra 32 e 1024 (inclusi) e *devono* essere divisibile in modo uniforme per 32. L'aumento del numero di livelli di priorità supportati aumenta l'utilizzo della RAM di 128 byte per ogni gruppo di 32 priorità. Tuttavia, esiste solo un effetto trascurabile sulle prestazioni. Per impostazione predefinita, questo valore è impostato su 32 livelli di priorità.

**TX_MINIMUM_STACK**

Definisce la dimensione minima dello stack (in byte). Viene usato per il controllo degli errori quando vengono creati i thread. Il valore predefinito è specifico della porta ed è disponibile in ***tx_port. h***.

**TX_MISRA_ENABLE**

Quando viene definito, ThreadX utilizza le convenzioni conformi a MISRA C. Per informazioni dettagliate, vedere  ***ThreadX_MISRA_Compliance.pdf*** .

**TX_MUTEX_ENABLE_PERFORMANCE_INFO**

Quando definito, Abilita la raccolta di informazioni sulle prestazioni nei mutex. Per impostazione predefinita, questa opzione non è definita.

**TX_NO_TIMER**

Quando è definito, la logica del timer ThreadX è completamente disabilitata. Questa operazione è utile nei casi in cui le funzionalità del timer ThreadX (sospensione thread, timeout API, sezionamento del tempo e timer applicazione) non vengono utilizzate. Se **TX_NO_TIMER** è specificato, è necessario definire anche l'opzione **TX_TIMER_PROCESS_IN_ISR** .

**TX_NOT_INTERRUPTABLE**

Quando viene definito, ThreadX non tenta di ridurre al minimo il tempo di blocco dell'interrupt. Questo comporta un'esecuzione più rapida, ma aumenta leggermente il tempo di blocco dell'interrupt.

**TX_QUEUE_ENABLE_PERFORMANCE_INFO**

Quando definito, consente la raccolta di informazioni sulle prestazioni sulle code. Per impostazione predefinita, questa opzione non è definita.

**TX_REACTIVATE_INLINE**

Quando definito, esegue la riattivazione dei timer ThreadX inline invece di usare una chiamata di funzione. Ciò migliora le prestazioni, ma aumenta leggermente le dimensioni del codice. Per impostazione predefinita, questa opzione non è definita.

**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**

Quando definito, Abilita la raccolta di informazioni sulle prestazioni sui semafori. Per impostazione predefinita, questa opzione non è definita.

**TX_THREAD_ENABLE_PERFORMANCE_INFO**

Quando definito, Abilita la raccolta di informazioni sulle prestazioni nei thread. Per impostazione predefinita, questa opzione non è definita.

**TX_TIMER_ENABLE_PERFORMANCE_INFO**

Quando definito, consente la raccolta di informazioni sulle prestazioni sui timer. Per impostazione predefinita, questa opzione non è definita.

**TX_TIMER_PROCESS_IN_ISR**

Una volta definito, Elimina il thread del timer interno di sistema per ThreadX. Ciò comporta un miglioramento delle prestazioni sugli eventi del timer e requisiti di RAM più piccoli, perché lo stack del timer e il blocco di controllo non sono più necessari. Tuttavia, se si usa questa opzione, l'elaborazione della scadenza del timer viene spostata al livello ISR del timer. Per impostazione predefinita, questa opzione non è definita.

> [!NOTE]
> *I servizi consentiti dai timer potrebbero non essere consentiti da ISRs e pertanto potrebbero non essere consentiti quando si usa questa opzione.*

**TX_TIMER_THREAD_PRIORITY**

Definisce la priorità del thread timer interno di sistema ThreadX. Il valore predefinito è priority 0, ovvero la priorità più alta in ThreadX. Il valore predefinito è definito in ***tx_port. h***.

**TX_TIMER_THREAD_STACK_SIZE**

Definisce la dimensione dello stack (in byte) del thread del timer di sistema ThreadX interno. Questo thread elabora tutte le richieste di sospensione del thread, nonché tutti i timeout delle chiamate al servizio. Inoltre, tutte le routine di callback del timer applicazione vengono richiamate da questo contesto. Il valore predefinito è specifico della porta ed è disponibile in ***tx_port. h***.

## <a name="threadx-version-id"></a>ID versione ThreadX

Il programmatore può ottenere la versione di ThreadX dall'esame del file ***tx_port. h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di ThreadX esaminando la stringa globale _ * _tx_version_id * *.
