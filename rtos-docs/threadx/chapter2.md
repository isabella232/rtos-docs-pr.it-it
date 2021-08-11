---
title: Capitolo 2 - Installazione e uso di Azure RTOS ThreadX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del kernel ThreadX Azure RTOS prestazioni elevate.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a88dc75c3b01e8054f72b3e1475791f064eac0ded02b22ccd18dd46da8c7200a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785040"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-threadx"></a>Capitolo 2 - Installazione e uso di Azure RTOS ThreadX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del kernel ThreadX Azure RTOS prestazioni elevate.

## <a name="host-considerations"></a>Considerazioni sull'host

Il software incorporato viene in genere sviluppato in Windows o su computer host Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

In genere il download di destinazione viene eseguito dall'interno del debugger dello strumento di sviluppo. Al termine del download, il debugger è responsabile di fornire il controllo dell'esecuzione di destinazione (go, halt, breakpoint e così via), nonché l'accesso ai registri della memoria e del processore.

La maggior parte dei debugger degli strumenti di sviluppo comunica con l'hardware di destinazione tramite connessioni OCD (On-Chip Debug), ad esempio JTAG (IEEE 1149.1) e BDM (Background Debug Mode). I debugger comunicano anche con l'hardware di destinazione In-Circuit connessioni ICE (In-Circuit Emulation). Entrambe le connessioni OCD e ICE offrono soluzioni affidabili con intrusioni minime nel software residente di destinazione.

Come per le risorse usate nell'host, il codice sorgente per ThreadX viene fornito in formato ASCII e richiede circa 1 MByte di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

ThreadX richiede da 2 KByte a 20 KByte di memoria di sola lettura (ROM) nella destinazione. Richiede anche altri 1-2 KByte di memoria ad accesso casuale (RAM) della destinazione per lo stack di sistema ThreadX e altre strutture di dati globali.

Per il funzionamento di funzioni correlate al timer, ad esempio timeout delle chiamate al servizio, time-slicing e timer dell'applicazione, l'hardware di destinazione sottostante deve fornire un'origine di interrupt periodica. Se il processore ha questa funzionalità, viene utilizzato da ThreadX. In caso contrario, se il processore di destinazione non è in grado di generare un interrupt periodico, l'hardware dell'utente deve fornirlo. L'installazione e la configurazione dell'interrupt timer si trovano in genere nel file ***tx_initialize_low_level*** assembly nella distribuzione ThreadX.

> [!NOTE]
> *ThreadX è ancora funzionante anche se non è disponibile alcuna origine di interrupt timer periodico. Tuttavia, nessuno dei servizi correlati al timer è funzionale.*

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS ThreadX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/threadx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository.

| Nome file | Descrizione |
|------------------- | ----------- |
| **tx_api.h**                      | File di intestazione C contenente tutti gli elementi di sistema, le strutture di dati e i prototipi di servizio.                                                             |
| **tx_port.h**                     | File di intestazione C contenente tutte le strutture e le definizioni di dati specifiche dello strumento di sviluppo e della destinazione.                                                 |
| **demo_threadx.c**                | File C contenente una piccola applicazione demo.                                                                                                       |
| **tx.a (o tx.lib)**              | Versione binaria della libreria ThreadX C distribuita con il *pacchetto standard.*                                                          |
|                                   |                                                                                                                                                   |

>[!NOTE]
>*Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione semplifica la conversione dei comandi in piattaforme di sviluppo Linux (Unix).*

## <a name="threadx-installation"></a>Installazione di ThreadX

ThreadX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository ThreadX nel PC.

```c
    git clone https://github.com/azure-rtos/threadx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante di download nella GitHub pagina principale.

Le istruzioni per la compilazione della libreria ThreadX sono disponibili anche nella prima pagina del repository online.

> [!NOTE]
> *Il software applicativo deve accedere al file di libreria ThreadX (in **genere tx.a** o **tx.lib)** e ai file di inclusione C **_tx_api.h_* _ e _*_tx_port.h_*_. Questa operazione viene eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nel percorso di sviluppo dell'area._

## <a name="using-threadx"></a>Uso di ThreadX

Per usare ThreadX, il codice dell'applicazione deve includere ***tx_api.h** _ durante la compilazione e collegarsi alla libreria di runtime ThreadX _*_tx.a_*_ (o _*_tx.lib_**).

Per compilare un'applicazione ThreadX sono necessari quattro passaggi.

1. Includere il file ***tx_api.h*** in tutti i file dell'applicazione che usano servizi ThreadX o strutture di dati.

1. Creare la funzione C ***main** _ standard. Questa funzione deve infine chiamare _ *_tx_kernel_enter_** per avviare ThreadX. L'inizializzazione specifica dell'applicazione che non coinvolge ThreadX può essere aggiunta prima di accedere al kernel.

      > [!IMPORTANT]
      > *La funzione di immissione ThreadX ***tx_kernel_enter** _ non restituisce un valore. Assicurarsi quindi di non effettuare chiamate di elaborazione o di funzione dopo it._

1. Creare la ***tx_application_define*** funzione. Qui vengono create le risorse di sistema iniziali. Esempi di risorse di sistema includono thread, code, pool di memoria, gruppi di flag di eventi, mutex e semafori.

1. Compilare l'origine dell'applicazione e collegarsi alla libreria di runtime ***ThreadX tx.lib.*** L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="small-example-system"></a>Small Example System

Il piccolo sistema di esempio nella figura 1 mostra la creazione di un singolo thread con priorità 3. Il thread viene eseguito, incrementa un contatore, quindi viene sostratta per un tick del clock.
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

Anche se si tratta di un esempio semplice, fornisce un buon modello per lo sviluppo di applicazioni reali.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta ThreadX viene recapitata con un'applicazione dimostrativa. È sempre una buona idea far eseguire prima il sistema dimostrativo, sia nell'hardware di destinazione effettivo che nell'ambiente simulato.

Se il sistema dimostrativo non viene eseguito correttamente, di seguito sono riportati alcuni suggerimenti per la risoluzione dei problemi.

1. Determinare la parte della dimostrazione in esecuzione.
1. Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice effettivo dell'applicazione rispetto alla dimostrazione).
1. Ricompilare la libreria ThreadX con TX_ENABLE_STACK_CHECKING definito. Ciò consente il controllo dello stack ThreadX incorporato.
1. Ignorare temporaneamente eventuali modifiche recenti per verificare se il problema scompare o cambia. Tali informazioni dovrebbero risultare utili per supportare i tecnici.

Seguire le procedure descritte in "[Customer Support Center](about-this-guide.md#customer-support-center)" per inviare le informazioni raccolte dai passaggi di risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria ThreadX e l'applicazione usando ThreadX, sono disponibili diverse opzioni di configurazione. Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file ***di inclusione tx_user.h.***

> [!IMPORTANT]
> *Le opzioni definite in ***tx_user.h** _ vengono applicate solo se l'applicazione e la libreria ThreadX vengono compilate con _ *TX_INCLUDE_USER_DEFINE_FILE** definito.*

### <a name="smallest-configuration"></a>Configurazione più piccola

Per le dimensioni minime del codice, è consigliabile prendere in considerazione le opzioni di configurazione ThreadX seguenti (in assenza di tutte le altre opzioni).

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

Per l'esecuzione più veloce, le stesse opzioni di configurazione usate in precedenza per la configurazione più piccola, ma con queste opzioni considerate.

```c
TX_REACTIVATE_INLINE
TX_INLINE_THREAD_RESUME_SUSPEND
```

[Vengono descritte le opzioni di](#detailed-configuration-options) configurazione dettagliate.

### <a name="global-time-source"></a>Origine ora globale

Per altri Microsoft Azure RTOS (FileX, NetX, GUIX, USBX e così via), ThreadX definisce il numero di tick del timer ThreadX che rappresenta un secondo. Altri derivano i requisiti di tempo in base a questa costante. Per impostazione predefinita, il valore è 100, presupponendo un interrupt periodico di 10 ms. L'utente può eseguire l'override di questo valore definendo TX_TIMER_TICKS_PER_SECOND con il valore desiderato in ***tx_port.h*** o all'interno dell'IDE o della riga di comando.

### <a name="detailed-configuration-options"></a>Opzioni di configurazione dettagliate

**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**

Se definita, questa opzione consente la raccolta di informazioni sulle prestazioni nei pool di byte. Per impostazione predefinita, questa opzione non è definita.

**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**

Se definita, questa opzione consente la raccolta di informazioni sulle prestazioni nei pool di byte. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_ERROR_CHECKING**

Ignora il controllo degli errori di base delle chiamate al servizio. Se definito nell'origine dell'applicazione, il controllo degli errori di tutti i parametri di base è disabilitato. Questo può migliorare le prestazioni fino al 30% e può anche ridurre le dimensioni dell'immagine.

> [!NOTE]
> *È possibile disabilitare il controllo degli errori solo se l'applicazione può garantire assolutamente che tutti i parametri di input siano sempre validi in tutte le circostanze, inclusi i parametri di input derivati dall'input esterno. Se all'API viene fornito un input non valido con il controllo degli errori disabilitato, il comportamento risultante non è definito e potrebbe causare il danneggiamento della memoria o l'arresto anomalo del sistema.*

> [!NOTE]
> *I valori restituiti dell'API ThreadX non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella sezione "Valori restituiti" di ogni descrizione dell'API nel capitolo 4. I valori restituiti nonbold sono void se il controllo degli errori è disabilitato usando l'TX_DISABLE_ERROR_CHECKING predefinita.*

**TX_DISABLE_NOTIFY_CALLBACKS**

Se definito, disabilita i callback di notifica per vari oggetti ThreadX. L'uso di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_PREEMPTION_THRESHOLD**

Quando è definito, disabilita la funzionalità preemption-threshold e riduce leggermente le dimensioni del codice e migliora le prestazioni. Naturalmente, le funzionalità di soglia di preemption non sono più disponibili. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_REDUNDANT_CLEARING**

Se definito, rimuove la logica per l'inizializzazione delle strutture di dati C globali ThreadX su zero. Deve essere usato solo se il codice di inizializzazione del compilatore imposta tutti i dati globali C non inizializzati su zero. L'uso di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni durante l'inizializzazione. Per impostazione predefinita, questa opzione non è definita.

**TX_DISABLE_STACK_FILLING**

Se definito, disabilita l'inserimento 0xEF valore in ogni byte dello stack di ogni thread al momento della creazione. Per impostazione predefinita, questa opzione non è definita.

**TX_ENABLE_EVENT_TRACE**

Se definito, ThreadX abilita il codice di raccolta degli eventi per la creazione di un buffer di traccia TraceX.

**TX_ENABLE_STACK_CHECKING**

Se definito, abilita il controllo dello stack di run-time ThreadX, che include l'analisi della quantità di stack usata e l'esame dei "recinti" del modello di dati prima e dopo l'area dello stack. Se viene rilevato un errore dello stack, viene chiamato il gestore degli errori dello stack dell'applicazione registrato. Questa opzione comporta un leggero aumento del sovraccarico e delle dimensioni del codice. Per altre ***informazioni, vedere tx_thread_stack_error_notify*** funzione API. Per impostazione predefinita, questa opzione non è definita.

**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**

Se definito, abilita la raccolta di informazioni sulle prestazioni nei gruppi di flag di evento. Per impostazione predefinita, questa opzione non è definita.

**TX_INLINE_THREAD_RESUME_SUSPEND**

Se definito, ThreadX migliora le chiamate API ***tx_thread_resume** _ e _ *_tx_thread_suspend_** tramite codice inline. Ciò aumenta le dimensioni del codice, ma migliora le prestazioni di queste due chiamate API.

**TX_MAX_PRIORITIES**

Definisce i livelli di priorità per ThreadX. I valori validi sono compresi tra 32 e 1024 (inclusi) e *devono* essere divisibile uniformemente per 32. L'aumento del numero di livelli di priorità supportati aumenta l'utilizzo della RAM di 128 byte per ogni gruppo di 32 priorità. Tuttavia, esiste solo un effetto trascurabile sulle prestazioni. Per impostazione predefinita, questo valore è impostato su 32 livelli di priorità.

**TX_MINIMUM_STACK**

Definisce le dimensioni minime dello stack (in byte). Viene usato per il controllo degli errori quando vengono creati i thread. Il valore predefinito è specifico della porta e si trova in ***tx_port.h.***

**TX_MISRA_ENABLE**

Se definito, ThreadX usa convenzioni conformi a MISRA C. Per informazioni  ***dettagliate,ThreadX_MISRA_Compliance.pdf*** riferimento a questa pagina.

**TX_MUTEX_ENABLE_PERFORMANCE_INFO**

Se definito, abilita la raccolta di informazioni sulle prestazioni sui mutex. Per impostazione predefinita, questa opzione non è definita.

**TX_NO_TIMER**

Se definita, la logica del timer ThreadX è completamente disabilitata. Ciò è utile nei casi in cui le funzionalità del timer ThreadX (sospensione thread, timeout API, sezione temporale e timer dell'applicazione) non vengono utilizzate. Se **TX_NO_TIMER** specificato, è necessario **definire TX_TIMER_PROCESS_IN_ISR'opzione.**

**TX_NOT_INTERRUPTABLE**

Se definito, ThreadX non tenta di ridurre al minimo il tempo di blocco dell'interrupt. Ciò comporta un'esecuzione più rapida, ma aumenta leggermente il tempo di blocco dell'interrupt.

**TX_QUEUE_ENABLE_PERFORMANCE_INFO**

Se definito, abilita la raccolta di informazioni sulle prestazioni nelle code. Per impostazione predefinita, questa opzione non è definita.

**TX_REACTIVATE_INLINE**

Se definito, esegue la riattivazione dei timer ThreadX inline invece di usare una chiamata di funzione. Ciò migliora le prestazioni, ma aumenta leggermente le dimensioni del codice. Per impostazione predefinita, questa opzione non è definita.

**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**

Se definito, abilita la raccolta di informazioni sulle prestazioni nei semafori. Per impostazione predefinita, questa opzione non è definita.

**TX_THREAD_ENABLE_PERFORMANCE_INFO**

Se definito, abilita la raccolta di informazioni sulle prestazioni nei thread. Per impostazione predefinita, questa opzione non è definita.

**TX_TIMER_ENABLE_PERFORMANCE_INFO**

Se definito, abilita la raccolta di informazioni sulle prestazioni sui timer. Per impostazione predefinita, questa opzione non è definita.

**TX_TIMER_PROCESS_IN_ISR**

Se definito, elimina il thread timer di sistema interno per ThreadX. Ciò comporta prestazioni migliorate per gli eventi timer e requisiti di RAM più piccoli perché lo stack timer e il blocco di controllo non sono più necessari. Tuttavia, l'uso di questa opzione sposta tutta l'elaborazione della scadenza del timer al livello ISR del timer. Per impostazione predefinita, questa opzione non è definita.

> [!NOTE]
> *I servizi consentiti dai timer potrebbero non essere consentiti dagli ISR e pertanto potrebbero non essere consentiti quando si usa questa opzione.*

**TX_TIMER_THREAD_PRIORITY**

Definisce la priorità del thread del timer di sistema ThreadX interno. Il valore predefinito è la priorità 0, ovvero la priorità più alta in ThreadX. Il valore predefinito è definito in ***tx_port.h.***

**TX_TIMER_THREAD_STACK_SIZE**

Definisce le dimensioni dello stack (in byte) del thread del timer di sistema ThreadX interno. Questo thread elabora tutte le richieste di sospensione dei thread, nonché tutti i timeout delle chiamate al servizio. Inoltre, tutte le routine di callback del timer dell'applicazione vengono richiamate da questo contesto. Il valore predefinito è specifico della porta e si trova in ***tx_port.h.***

## <a name="threadx-version-id"></a>ID versione ThreadX

Il programmatore può ottenere la versione ThreadX dall'esame del file *** tx_port.h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software dell'applicazione può ottenere la versione ThreadX esaminando la stringa globale _*_tx_version_id**.
