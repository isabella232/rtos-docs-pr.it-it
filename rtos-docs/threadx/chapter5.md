---
title: Capitolo 5-driver di dispositivo per Azure RTO ThreadX
description: Questo capitolo contiene una descrizione dei driver di dispositivo per Azure RTO ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2432b291f2b3fa7d6d798b8b4c187dd20b97db6b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823261"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx"></a>Capitolo 5-driver di dispositivo per Azure RTO ThreadX

Questo capitolo contiene una descrizione dei driver di dispositivo per Azure RTO ThreadX. Le informazioni presentate in questo capitolo sono progettate per aiutare gli sviluppatori a scrivere driver specifici dell'applicazione.

## <a name="device-driver-introduction"></a>Introduzione al driver di dispositivo

La comunicazione con l'ambiente esterno è un componente importante della maggior parte delle applicazioni incorporate. Questa comunicazione viene eseguita tramite dispositivi hardware accessibili al software dell'applicazione incorporato. I componenti software responsabili della gestione di tali dispositivi sono comunemente denominati *driver di dispositivo*.

I driver di dispositivo in sistemi incorporati e in tempo reale sono intrinsecamente dipendenti dall'applicazione. Questo vale per due motivi principali: la vasta gamma di hardware di destinazione e i requisiti di prestazioni ugualmente vasti imposti sulle applicazioni in tempo reale. Per questo motivo, è praticamente impossibile fornire un set comune di driver che soddisfino i requisiti di ogni applicazione. Per questi motivi, le informazioni contenute in questo capitolo sono progettate per aiutare gli utenti a personalizzare i driver di dispositivo threadX *fuori piano* e scrivere i propri driver specifici.

## <a name="driver-functions"></a>Funzioni driver

I driver di dispositivo ThreadX sono costituiti da otto aree funzionali di base, come indicato di seguito.

- **Inizializzazione driver**
- **Controllo driver**
- **Accesso driver**
- **Input driver**
- **Output driver**
- **Interrupt driver**
- **Stato driver**
- **Terminazione driver**

Ad eccezione dell'inizializzazione, ogni area funzionale del driver è facoltativa. L'elaborazione esatta in ogni area è inoltre specifica del driver di dispositivo.

### <a name="driver-initialization"></a>Inizializzazione driver
Questa area funzionale è responsabile dell'inizializzazione del dispositivo hardware effettivo e delle strutture di dati interne del driver. La chiamata di altri servizi driver non è consentita fino al completamento dell'inizializzazione.

> [!NOTE]
> * Il componente della funzione di inizializzazione del driver viene in genere chiamato dalla funzione ***tx_application_define** _ o da un'inizializzazione thread._

### <a name="driver-control"></a>Controllo driver

Una volta che il driver è stato inizializzato e pronto per l'operazione, l'area funzionale è responsabile del controllo di Runtime. In genere, il controllo in fase di esecuzione è costituito da modifiche al dispositivo hardware sottostante. Gli esempi includono la modifica della velocità in baud di un dispositivo seriale o la ricerca di un nuovo settore su un disco.

### <a name="driver-access"></a>Accesso driver

Alcuni driver di dispositivo vengono chiamati solo da un singolo thread dell'applicazione. In questi casi, questa area funzionale non è necessaria. Tuttavia, nelle applicazioni in cui più thread necessitano dell'accesso simultaneo ai driver, l'interazione deve essere controllata aggiungendo le funzionalità di assegnazione/rilascio nel driver di dispositivo. In alternativa, l'applicazione può utilizzare un semaforo per controllare l'accesso dei driver ed evitare overhead e complicazioni aggiuntive all'interno del driver.

### <a name="driver-input"></a>Input driver

Questa area funzionale è responsabile di tutti gli input del dispositivo. I problemi principali associati all'input del driver coinvolgono in genere il modo in cui l'input viene memorizzato nel buffer e il modo in cui i thread attendono tale input.

### <a name="driver-output"></a>Output driver

Questa area funzionale è responsabile di tutti gli output del dispositivo. I problemi principali associati all'output del driver comportano in genere il modo in cui l'output viene memorizzato nel buffer e i thread in attesa di eseguire l'output.

### <a name="driver-interrupts"></a>Interrupt driver

La maggior parte dei sistemi in tempo reale si basa su interrupt hardware per notificare al driver l'input, l'output, il controllo e gli eventi di errore del dispositivo. Gli interrupt forniscono tempi di risposta garantiti a tali eventi esterni. Anziché gli interrupt, il software del driver potrebbe controllare periodicamente l'hardware esterno per tali eventi. Questa tecnica è denominata *polling*. È meno tempo reale degli interrupt, ma il polling può essere utile per alcune applicazioni meno in tempo reale.

### <a name="driver-status"></a>Stato driver

Questa area di funzione è responsabile della fornitura di statistiche e stato di run-time associate all'operazione del driver. Le informazioni gestite da questa area di funzione includono in genere quanto segue.

- Stato corrente del dispositivo
- Byte di input
- Byte di output
- Conteggi errori del dispositivo

### <a name="driver-termination"></a>Terminazione driver

Questa area funzionale è facoltativa. È necessario solo se il driver e/o il dispositivo hardware fisico devono essere arrestati. Dopo la terminazione, il driver non deve essere chiamato di nuovo fino a quando non viene reinizializzato.

## <a name="simple-driver-example"></a>Esempio di driver semplice

Un esempio è il modo migliore per descrivere un driver di dispositivo. In questo esempio, il driver presuppone un semplice dispositivo hardware seriale con un registro di configurazione, un registro di input e un registro di output. Questo semplice esempio di driver illustra le aree funzionali di inizializzazione, input, output e interrupt.

### <a name="simple-driver-initialization"></a>Inizializzazione driver semplice

La funzione ***tx_sdriver_initialize*** del driver semplice crea due semafori di conteggio usati per gestire l'operazione di input e output del driver. Il semaforo di input viene impostato dall'ISR di input quando un carattere viene ricevuto dal dispositivo hardware seriale. Per questo motivo, il semaforo di input viene creato con un conteggio iniziale pari a zero.

Viceversa, il semaforo di output indica la disponibilità del registro di trasmissione hardware seriale. Viene creato con un valore di uno per indicare che il registro di trasmissione è inizialmente disponibile.

La funzione di inizializzazione è anche responsabile dell'installazione dei gestori di interrupt vettori di basso livello per le notifiche di input e output. Analogamente ad altre routine del servizio di interrupt ThreadX, il gestore di basso livello deve chiamare ***_tx_thread_context_save** _ prima di chiamare il semplice PVR del driver. Una volta che il driver ISR restituisce, il gestore di basso livello deve chiamare _ * _ _tx_thread_context_restore_* *.

> [!IMPORTANT]
> * È importante che l'inizializzazione venga chiamata prima di qualsiasi altra funzione del driver. L'inizializzazione del driver viene in genere chiamata da ***tx_application_define***.

```c
VOID tx_sdriver_initialize(VOID)
{
    /* Initialize the two counting semaphores used to control
    the simple driver I/O. */
    tx_semaphore_create(&tx_sdriver_input_semaphore,
                        "simple driver input semaphore", 0);
    tx_semaphore_create(&tx_sdriver_output_semaphore,
                        "simple driver output semaphore", 1);

    /* Setup interrupt vectors for input and output ISRs.
    The initial vector handling should call the ISRs
    defined in this file. */

    /* Configure serial device hardware for RX/TX interrupt
    generation, baud rate, stop bits, etc. */
}
```
**FIGURA 9. Inizializzazione driver semplice**

### <a name="simple-driver-input"></a>Input di driver semplice

Input per il driver semplice Centra intorno al semaforo di input. Quando viene ricevuto un interrupt di input seriale del dispositivo, viene impostato il semaforo di input. Se uno o più thread sono in attesa di un carattere dal driver, il thread in attesa del più lungo viene ripreso. Se nessun thread è in attesa, il semaforo rimane semplicemente impostato fino a quando un thread non chiama la funzione di input dell'unità.

Esistono diverse limitazioni alla gestione semplice dell'input dei driver. Il più significativo è il potenziale per eliminare i caratteri di input. Questa operazione è possibile perché non esiste la possibilità di memorizzare nel buffer i caratteri di input che arrivano prima che il carattere precedente venga elaborato. Questa operazione viene gestita facilmente mediante l'aggiunta di un buffer di caratteri di input.

> [!NOTE]
> *Solo i thread sono autorizzati a chiamare il*  * **tx_sdriver_input** _ _function. *

Nella figura 10 è illustrato il codice sorgente associato all'input di un driver semplice.

```c
UCHAR tx_sdriver_input(VOID)
{
  /* Determine if there is a character waiting. If not,
  suspend. */
  tx_semaphore_get(&tx_sdriver_input_semaphore,
  TX_WAIT_FOREVER;

  /* Return character from serial RX hardware register. */
  return(*serial_hardware_input_ptr);
}
  VOID tx_sdriver_input_ISR(VOID)
{
  /* See if an input character notification is pending. */
  if (!tx_sdriver_input_semaphore.tx_semaphore_count)
  {
    /* If not, notify thread of an input character. */
    tx_semaphore_put(&tx_sdriver_input_semaphore);
  }
}
```
**FIGURA 10. Input di driver semplice**

### <a name="simple-driver-output"></a>Output di driver semplice

L'elaborazione dell'output usa il semaforo di output per segnalare quando il registro di trasmissione del dispositivo seriale è gratuito. Prima che un carattere di output venga effettivamente scritto nel dispositivo, viene ottenuto il semaforo di output. Se non è disponibile, la trasmissione precedente non è ancora completa.

L'ISR di output è responsabile della gestione dell'interrupt completo di trasmissione. L'elaborazione dell'output ISR equivale a impostare il semaforo di output, consentendo in questo modo l'output di un altro carattere.

> [!NOTE]
> *Solo i thread sono autorizzati a chiamare il*  * **tx_sdriver_output** _ _function. *

Nella figura 11 viene illustrato il codice sorgente associato all'output di un driver semplice.

```c
VOID tx_sdriver_output(UCHAR alpha)
{
  /* Determine if the hardware is ready to transmit a
  character. If not, suspend until the previous output
  completes. */
  tx_semaphore_get(&tx_sdriver_output_semaphore,
                                          TX_WAIT_FOREVER);

  /* Send the character through the hardware. */
  *serial_hardware_output_ptr = alpha;
}
  
VOID tx_sdriver_output_ISR(VOID)
{
  /* Notify thread last character transmit is
  complete. */
  tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
**FIGURA 11. Output di driver semplice**

### <a name="simple-driver-shortcomings"></a>Limitazioni semplici per i driver

Questo semplice esempio di driver di dispositivo illustra l'idea di base di un driver di dispositivo ThreadX. Tuttavia, poiché il driver di dispositivo semplice non risolve il buffer dei dati o problemi di overhead, non rappresenta completamente i driver ThreadX reali. Nella sezione seguente vengono descritti alcuni dei problemi più avanzati associati ai driver di dispositivo.

## <a name="advanced-driver-issues"></a>Problemi relativi ai driver avanzati

Come indicato in precedenza, i driver di dispositivo presentano requisiti univoci come le rispettive applicazioni. Alcune applicazioni possono richiedere una grande quantità di buffer di dati, mentre un'altra applicazione potrebbe richiedere un driver ottimizzato ISRs a causa di interrupt del dispositivo ad alta frequenza.

### <a name="io-buffering"></a>Buffer I/O

Il buffering dei dati nelle applicazioni embedded in tempo reale richiede una pianificazione considerevole. Parte della progettazione è determinata dal dispositivo hardware sottostante. Se il dispositivo fornisce l'I/O di base per i byte, probabilmente si tratta di un semplice buffer circolare. Tuttavia, se il dispositivo fornisce l'I/O a blocchi, DMA o pacchetti, è probabile che venga garantito uno schema di gestione del buffer.

### <a name="circular-byte-buffers"></a>Buffer di byte circolari

I buffer di byte circolari vengono in genere usati nei driver che gestiscono un semplice dispositivo hardware seriale come UART. Due buffer circolari vengono spesso utilizzati in situazioni di questo tipo: uno per l'input e uno per l'output.

Ogni buffer di byte circolari è costituito da un'area di memoria byte (in genere una matrice di **UCHAR**), un puntatore di lettura e un puntatore di scrittura. Un buffer viene considerato vuoto quando il puntatore di lettura e i puntatori di scrittura fanno riferimento alla stessa posizione di memoria nel buffer. L'inizializzazione del driver imposta i puntatori del buffer di lettura e scrittura sull'indirizzo iniziale del buffer.

### <a name="circular-buffer-input"></a>Input del buffer circolare

Il buffer di input viene usato per mantenere i caratteri che arrivano prima che l'applicazione sia pronta. Quando viene ricevuto un carattere di input (in genere in una routine del servizio di interrupt), il nuovo carattere viene recuperato dal dispositivo hardware e inserito nel buffer di input nella posizione a cui punta il puntatore di scrittura. Il puntatore di scrittura viene quindi spostato nella posizione successiva nel buffer. Se la posizione successiva si trova oltre la fine del buffer, il puntatore di scrittura viene impostato sull'inizio del buffer. La condizione della coda completa viene gestita annullando l'avanzamento del puntatore di scrittura se il nuovo puntatore di scrittura è uguale al puntatore di lettura.

Le richieste di byte di input dell'applicazione al driver esaminano prima di tutto i puntatori di lettura e scrittura del buffer di input. Se i puntatori di lettura e scrittura sono identici, il buffer è vuoto. In caso contrario, se il puntatore di lettura non è lo stesso, il byte a cui punta il puntatore di lettura viene copiato dal buffer di input e il puntatore di lettura viene spostato nella posizione del buffer successiva. Se il nuovo puntatore di lettura si trova oltre la fine del buffer, viene reimpostato all'inizio. Nella figura 12 viene illustrata la logica per il buffer di input circolare.

```c
UCHAR   tx_input_buffer[MAX_SIZE];
UCHAR   tx_input_write_ptr;
UCHAR   tx_input_read_ptr;

/* Initialization. */
tx_input_write_ptr =    &tx_input_buffer[0];
tx_input_read_ptr =     &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr = tx_input_write_ptr;
*tx_input_write_ptr++ = alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr = &tx_input_buffer[0]; /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr = save_ptr; /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
  alpha = *tx_input_read_ptr++;
  if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
      tx_input_read_ptr = &tx_input_buffer[0];
}
```
**FIGURA 12. Logica per il buffer di input circolare**

> [!NOTE]
> * Per un'operazione affidabile, potrebbe essere necessario bloccare gli interrupt quando si modificano i puntatori di lettura e scrittura dei buffer circolari di input e di output. *

### <a name="circular-output-buffer"></a>Buffer di output circolare

Il buffer di output viene usato per contenere i caratteri che sono arrivati per l'output prima che il dispositivo hardware abbia terminato di inviare il byte precedente. L'elaborazione del buffer di output è simile all'elaborazione del buffer di input, ad eccezione del fatto che l'elaborazione di interrupt completa di trasmissione manipola il puntatore di lettura dell'output, mentre la richiesta di output dell'applicazione utilizza il puntatore di scrittura di
In caso contrario, l'elaborazione del buffer di output è la stessa. Nella figura 13 viene illustrata la logica per il buffer di output circolare.

```c
UCHAR   tx_output_buffer[MAX_SIZE];
UCHAR   tx_output_write_ptr;
UCHAR   tx_output_read_ptr;

/* Initialization. */
tx_output_write_ptr = &tx_output_buffer[0];
tx_output_read_ptr = &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
  *device_reg = *tx_output_read_ptr++;
  if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
      tx_output_read_ptr = &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr = tx_output_write_ptr;
*tx_output_write_ptr++ = alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr = &tx_output_buffer[0]; /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr = save_ptr; /* Buffer full! */
```
**FIGURA 13. Logica per il buffer di output circolare**

### <a name="buffer-io-management"></a>Gestione I/O del buffer

Per migliorare le prestazioni dei microprocessori incorporati, molti dispositivi dispositivo periferico trasmettono e ricevono dati con i buffer forniti dal software. In alcune implementazioni, è possibile usare più buffer per trasmettere o ricevere singoli pacchetti di dati.

Le dimensioni e la posizione dei buffer di I/O sono determinate dall'applicazione e/o dal software del driver. In genere, i buffer sono di dimensioni fisse e gestiti all'interno di un pool di memoria del blocco ThreadX. La figura 14 descrive un buffer di I/O tipico e un pool di memoria blocco ThreadX che gestisce l'allocazione.

```c
typedef struct TX_IO_BUFFER_STRUCT
{
      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
      struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR tx_buffer_area[TX_MAX_BUFFER_SIZE];
} TX_IO_BUFFER;

TX_BLOCK_POOL tx_io_block_pool;

/* Create a pool of I/O buffers. Assume that the pointer
"free_memory_ptr"points to an available memory area that
is 64 KBytes in size. */
tx_block_pool_create(&tx_io_block_pool,
                  "Sample IO Driver Buffer Pool",
                  free_memory_ptr, 0x10000,
                  sizeof(TX_IO_BUFFER));
```

**FIGURA 14. Buffer I/O**

### <a name="tx_io_buffer"></a>TX_IO_BUFFER

Il typedef TX_IO_BUFFER è costituito da due puntatori. Il puntatore **tx_next_packet** viene usato per collegare più pacchetti nell'elenco di input o output. Il puntatore **tx_next_buffer** viene usato per collegare i buffer che costituiscono un singolo pacchetto di dati dal dispositivo. Entrambi i puntatori vengono impostati su NULL quando il buffer viene allocato dal pool. Inoltre, alcuni dispositivi potrebbero richiedere un altro campo per indicare la quantità di dati effettivamente contenuti nell'area del buffer.

### <a name="buffered-io-advantage"></a>Vantaggio I/O memorizzato nel buffer

Quali sono i vantaggi di uno schema di I/O del buffer? Il vantaggio principale è che i dati non vengono copiati tra i registri dei dispositivi e la memoria dell'applicazione. Al contrario, il driver fornisce al dispositivo una serie di puntatori del buffer. L'I/O del dispositivo fisico utilizza direttamente la memoria buffer fornita.

L'utilizzo del processore per copiare pacchetti di dati di input o di output è estremamente costoso e deve essere evitato in qualsiasi situazione di I/O a velocità effettiva elevata.

Un altro vantaggio dell'approccio i/O memorizzato nel buffer consiste nel fatto che gli elenchi di input e output non dispongono di condizioni complete. Tutti i buffer disponibili possono trovarsi in uno dei due elenchi in qualsiasi momento. Questo è un contrasto con i semplici buffer circolari di byte presentati in precedenza nel capitolo. Ognuna aveva una dimensione fissa determinata in fase di compilazione.

### <a name="buffered-driver-responsibilities"></a>Responsabilità dei driver memorizzati nel buffer

I driver di dispositivo memorizzati nel buffer sono interessati solo alla gestione degli elenchi collegati di buffer di I/O. Per i pacchetti ricevuti prima che il software dell'applicazione sia pronto, viene mantenuto un elenco di buffer di input. Viceversa, un elenco di buffer di output viene mantenuto per i pacchetti inviati più velocemente di quanto possa essere gestito dal dispositivo hardware. La figura 15 Mostra semplici elenchi collegati di input e output di pacchetti di dati e i buffer che compongono ogni pacchetto.

**Elenco di input**

![Elenco di input](./media/user-guide/input-list.png)

**Elenco output**

![Elenco output](./media/user-guide/output-list.png)

**FIGURA 15. Elenchi di Input-Output**

Interfaccia applicazioni con driver memorizzati nel buffer con gli stessi buffer di I/O. Alla trasmissione, il software applicativo fornisce al driver uno o più buffer da trasmettere. Quando il software dell'applicazione richiede l'input, il driver restituisce i dati di input nei buffer di I/O.

> [!NOTE]
> *In alcune applicazioni può essere utile creare un'interfaccia di input del driver che richiede all'applicazione di scambiare un buffer libero per un buffer di input dal driver. Questo potrebbe ridurre l'elaborazione dell'allocazione del buffer all'interno del driver.*

### <a name="interrupt-management"></a>Gestione interrupt

In alcune applicazioni, la frequenza di interrupt del dispositivo può impedire la scrittura dell'ISR in C o l'interazione con ThreadX a ogni interrupt. Se, ad esempio, si accetta 25US per salvare e ripristinare il contesto interrotto, non è consigliabile eseguire un intero contesto di salvataggio se la frequenza di interrupt è 50us. In questi casi, per gestire la maggior parte degli interrupt del dispositivo viene usato un linguaggio ISR (Small assembly language). Questo ISR con overhead ridotto interagisce solo con ThreadX quando è necessario.

Una discussione simile si trova nella discussione sulla gestione degli interrupt alla fine del capitolo 3.

### <a name="thread-suspension"></a>Sospensione thread

Nell'esempio di driver semplice illustrato in precedenza in questo capitolo, il chiamante del servizio di input sospende se un carattere non è disponibile. In alcune applicazioni questo potrebbe non essere accettabile.

Se, ad esempio, il thread responsabile dell'elaborazione dell'input da un driver dispone anche di altre mansioni, la sospensione solo sull'input del driver probabilmente non funzionerà. Al contrario, il driver deve essere personalizzato per richiedere l'elaborazione in modo analogo al modo in cui vengono effettuate altre richieste di elaborazione al thread.

Nella maggior parte dei casi, il buffer di input viene inserito in un elenco collegato e un messaggio di evento di input viene inviato alla coda di input del thread.
