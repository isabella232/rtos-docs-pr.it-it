---
title: Capitolo 5 - Driver di dispositivo per Azure RTOS ThreadX SMP
description: Questo capitolo contiene una descrizione dei driver di dispositivo per Azure RTOS ThreadX SMP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 706ad47b2c3e7b2979da7262a4de8d681f4fbc53cb1af59a798b34094734060b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792341"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx-smp"></a>Capitolo 5 - Driver di dispositivo per Azure RTOS ThreadX SMP

Questo capitolo contiene una descrizione dei driver di dispositivo per Azure RTOS ThreadX SMP. Le informazioni presentate in questo capitolo sono progettate per consentire agli sviluppatori di scrivere driver specifici dell'applicazione. 

## <a name="device-driver-introduction"></a>Introduzione al driver di dispositivo

La comunicazione con l'ambiente esterno è un componente importante della maggior parte delle applicazioni incorporate. Questa comunicazione viene eseguita tramite dispositivi hardware accessibili al software dell'applicazione incorporato. I componenti software responsabili della gestione di tali dispositivi sono comunemente denominati *Driver di dispositivo*.

I driver di dispositivo nei sistemi incorporati in tempo reale dipendono intrinsecamente dall'applicazione. Questo vale per due motivi principali: la grande diversità dell'hardware di destinazione e i requisiti di prestazioni altrettanto vasti imposti alle applicazioni in tempo reale. Per questo, è praticamente impossibile fornire un set comune di driver che soddisfino i requisiti di ogni applicazione. Per questi motivi, le informazioni contenute in questo capitolo sono progettate per consentire agli utenti di personalizzare i driver di dispositivo *SMP* ThreadX disponibili e scrivere driver specifici.

## <a name="driver-functions"></a>Funzioni del driver

I driver di dispositivo SMP ThreadX sono costituiti da otto aree funzionali di base, come indicato di seguito:

- **Inizializzazione del driver**
- **Controllo driver**
- **Accesso al driver**
- **Driver Input**
- **Driver Output**
- **Interrupt del driver**
- **Stato del driver**
- **Terminazione del driver**

Ad eccezione dell'inizializzazione, ogni area funzionale del driver è facoltativa. Inoltre, l'elaborazione esatta in ogni area è specifica del driver di dispositivo.

### <a name="driver-initialization"></a>Inizializzazione del driver 
Questa area funzionale è responsabile dell'inizializzazione del dispositivo hardware effettivo e delle strutture di dati interne del driver. La chiamata ad altri servizi driver non è consentita fino al completamento dell'inizializzazione.

> [!IMPORTANT]
> Il componente della funzione di inizializzazione del driver viene in genere chiamato dalla **funzione tx_application_define** o da un thread di inizializzazione.

### <a name="driver-control"></a>Controllo driver 
Dopo che il driver è stato inizializzato e pronto per il funzionamento, questa area funzionale è responsabile del controllo in fase di esecuzione. In genere, il controllo in fase di esecuzione consiste nell'apportare modifiche al dispositivo hardware sottostante. Alcuni esempi includono la modifica della velocità in baud di un dispositivo seriale o la ricerca di un nuovo settore su disco.

### <a name="driver-access"></a>Accesso al driver 
Alcuni driver di dispositivo vengono chiamati solo da un singolo thread dell'applicazione. In questi casi, questa area funzionale non è necessaria. Tuttavia, nelle applicazioni in cui più thread necessitano dell'accesso simultaneo al driver, la loro interazione deve essere controllata aggiungendo funzionalità di assegnazione/rilascio nel driver di dispositivo. In alternativa, l'applicazione può usare un semaforo per controllare l'accesso al driver ed evitare sovraccarico aggiuntivo e complicazioni all'interno del driver. 

### <a name="driver-input"></a>Driver Input 
Questa area funzionale è responsabile di tutto l'input del dispositivo. I problemi principali associati all'input del driver comportano in genere il modo in cui l'input viene memorizzato nel buffer e il modo in cui i thread attendono tale input. 

### <a name="driver-output"></a>Driver Output 
Questa area funzionale è responsabile di tutto l'output del dispositivo. I problemi principali associati all'output del driver comportano in genere il modo in cui l'output viene memorizzato nel buffer e il modo in cui i thread attendono di eseguire l'output. 

### <a name="driver-interrupts"></a>Interrupt del driver 
La maggior parte dei sistemi in tempo reale si basa su interrupt hardware per notificare al driver gli eventi di input, output, controllo ed errore del dispositivo. Gli interrupt forniscono un tempo di risposta garantito a tali eventi esterni. Anziché interrompere, il software del driver può controllare periodicamente l'hardware esterno per tali eventi. Questa tecnica è detta *polling.* È meno in tempo reale rispetto agli interrupt, ma il polling può avere senso per alcune applicazioni meno in tempo reale. 

### <a name="driver-status"></a>Stato del driver 
Questa area di funzione è responsabile di fornire lo stato di runtime e le statistiche associate all'operazione del driver. Le informazioni gestite da questa area di funzione includono in genere quanto segue: 
- Stato corrente del dispositivo
- Byte di input
- Byte di output
- Conteggi degli errori del dispositivo

### <a name="driver-termination"></a>Terminazione del driver 
Questa area funzionale è facoltativa. È necessario solo se è necessario arrestare il driver e/o il dispositivo hardware fisico. Dopo essere stato terminato, il driver non deve essere chiamato di nuovo fino a quando non viene inizializzato nuovamente. 

## <a name="simple-driver-example"></a>Esempio di driver semplice

Un esempio è il modo migliore per descrivere un driver di dispositivo. In questo esempio il driver presuppone un semplice dispositivo hardware seriale con un registro di configurazione, un registro di input e un registro di output. Questo semplice esempio di driver illustra le aree funzionali di inizializzazione, input, output e interrupt.

### <a name="simple-driver-initialization"></a>Inizializzazione del driver semplice 
La ***tx_sdriver_initialize*** del driver semplice crea due semafori di conteggio usati per gestire l'operazione di input e output del driver. Il semaforo di input viene impostato dall'ISR di input quando un carattere viene ricevuto dal dispositivo hardware seriale. Per questo scopo, il semaforo di input viene creato con un conteggio iniziale pari a zero.

Al contrario, il semaforo di output indica la disponibilità del registro di trasmissione hardware seriale. Viene creato con un valore pari a uno per indicare che il registro di trasmissione è inizialmente disponibile.

La funzione di inizializzazione è anche responsabile dell'installazione dei gestori del vettore di interrupt di basso livello per le notifiche di input e output. Come altre routine del servizio di interrupt SMP ThreadX, il gestore di basso livello deve chiamare ***_tx_thread_context_save** _ prima di chiamare il driver SEMPLICE ISR. Al termine dell'ISR del driver, il gestore di basso livello deve chiamare _*_ _tx_thread_context_restore_**.

> [!IMPORTANT]
> È importante che l'inizializzazione venga chiamata prima di qualsiasi altra funzione del driver. In genere, l'inizializzazione del driver viene chiamata **da tx_application_define**.

Vedere la figura 9 a pagina 306 per il codice sorgente di inizializzazione del driver semplice.

```C
VOID     tx_sdriver_initialize(VOID)
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
**FIGURA 9. Inizializzazione del driver semplice**

### <a name="simple-driver-input"></a>Input del driver semplice 
L'input per il driver semplice è al centro del semaforo di input. Quando viene ricevuto un interrupt di input del dispositivo seriale, viene impostato il semaforo di input. Se uno o più thread sono in attesa di un carattere dal driver, il thread in attesa più lungo viene ripreso. Se nessun thread è in attesa, il semaforo rimane impostato finché un thread non chiama la funzione di input dell'unità.

Esistono diverse limitazioni per la gestione dell'input del driver semplice. Il più significativo è la possibilità di eliminare i caratteri di input. Ciò è possibile perché non è possibile inserire nel buffer i caratteri di input che arrivano prima dell'elaborazione del carattere precedente. Questa operazione viene gestita facilmente aggiungendo un buffer di caratteri di input.

> [!IMPORTANT]
> Solo i thread possono chiamare la **tx_sdriver_input** funzione.

La figura 10 mostra il codice sorgente associato all'input del driver semplice.

```C
UCHAR     tx_sdriver_input(VOID)
{

    /* Determine if there is a character waiting. If not,
        suspend. */
    tx_semaphore_get(&tx_sdriver_input_semaphore,
                                             TX_WAIT_FOREVER;
    /* Return character from serial RX hardware register. */
    return(*serial_hardware_input_ptr);
}

VOID     tx_sdriver_input_ISR(VOID)
{
    /* See if an input character notification is pending. */
    if (!tx_sdriver_input_semaphore.tx_semaphore_count)
    {
        /* If not, notify thread of an input character. */
        tx_semaphore_put(&tx_sdriver_input_semaphore);
    }
}
```
**FIGURA 10. Input del driver semplice**

### <a name="simple-driver-output"></a>Output del driver semplice 
L'elaborazione dell'output usa il semaforo di output per segnalare quando il registro di trasmissione del dispositivo seriale è gratuito. Prima che un carattere di output venga effettivamente scritto nel dispositivo, viene ottenuto il semaforo di output. Se non è disponibile, la trasmissione precedente non è ancora completa.

L'ISR di output è responsabile della gestione dell'interrupt completo di trasmissione. L'elaborazione dell'ISR di output è l'impostazione del semaforo di output, consentendo l'output di un altro carattere.

> [!IMPORTANT]
> Solo i thread possono chiamare la **tx_sdriver_output** funzione.

La figura 11 mostra il codice sorgente associato all'output del driver semplice.

```C
VOID     tx_sdriver_output(UCHAR alpha)
{

    /* Determine if the hardware is ready to transmit a
       character. If not, suspend until the previous output
        completes. */
    tx_semaphore_get(&tx_sdriver_output_semaphore,
                                            TX_WAIT_FOREVER);
    /* Send the character through the hardware. */
    *serial_hardware_output_ptr = alpha;
}

VOID     tx_sdriver_output_ISR(VOID)
{
    /* Notify thread last character transmit is
        complete. */
    tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
**FIGURA 11. Output del driver semplice**

### <a name="simple-driver-shortcomings"></a>Lacune del driver semplice 
Questo semplice esempio di driver di dispositivo illustra l'idea di base di un driver di dispositivo ThreadX SMP. Tuttavia, poiché il driver di dispositivo semplice non consente di risolvere i problemi di buffering dei dati o di sovraccarico, non rappresenta completamente i driver SMP ThreadX reali. La sezione seguente descrive alcuni dei problemi più avanzati associati ai driver di dispositivo.

## <a name="advanced-driver-issues"></a>Problemi avanzati del driver

Come accennato in precedenza, i driver di dispositivo hanno requisiti univoci come le applicazioni. Alcune applicazioni possono richiedere un'enorme quantità di buffer dei dati, mentre un'altra applicazione potrebbe richiedere isr di driver ottimizzati a causa di interrupt del dispositivo ad alta frequenza.

### <a name="io-buffering"></a>Memorizzazione nel buffer di I/O 
Il buffering dei dati nelle applicazioni incorporate in tempo reale richiede una pianificazione considerevole. Parte della progettazione è dettata dal dispositivo hardware sottostante. Se il dispositivo fornisce operazioni di I/O di byte di base, è probabile che sia disponibile un buffer circolare semplice. Tuttavia, se il dispositivo fornisce blocchi, DMA o I/O di pacchetti, è probabilmente giustificato uno schema di gestione del buffer. 

### <a name="circular-byte-buffers"></a>Buffer di byte circolari 
I buffer di byte circolari vengono in genere usati nei driver che gestiscono un dispositivo hardware seriale semplice, ad esempio un UART. In queste situazioni vengono usati più spesso due buffer circolari, uno per l'input e uno per l'output.

Ogni buffer di byte circolare è costituito da un'area di memoria di byte (in genere una matrice di UCHAR), un puntatore di lettura e un puntatore di scrittura. Un buffer viene considerato vuoto quando il puntatore di lettura e i puntatori di scrittura fanno riferimento alla stessa posizione di memoria nel buffer. L'inizializzazione del driver imposta i puntatori del buffer di lettura e scrittura all'indirizzo iniziale del buffer.

### <a name="circular-buffer-input"></a>Input buffer circolare 
Il buffer di input viene usato per contenere i caratteri che arrivano prima che l'applicazione sia pronta per loro. Quando viene ricevuto un carattere di input (in genere in una routine del servizio di interrupt), il nuovo carattere viene recuperato dal dispositivo hardware e inserito nel buffer di input nella posizione a cui punta il puntatore di scrittura. Il puntatore di scrittura viene quindi avanzato alla posizione successiva nel buffer. Se la posizione successiva è oltre la fine del buffer, il puntatore di scrittura viene impostato sull'inizio del buffer. La condizione completa della coda viene gestita annullando l'avanzamento del puntatore di scrittura se il nuovo puntatore di scrittura è lo stesso del puntatore di lettura.

Le richieste di byte di input dell'applicazione al driver esaminano innanzitutto i puntatori di lettura e scrittura del buffer di input. Se i puntatori di lettura e scrittura sono identici, il buffer è vuoto. In caso contrario, se il puntatore di lettura non è lo stesso, il byte a cui punta il puntatore di lettura viene copiato dal buffer di input e il puntatore di lettura viene avanzato alla posizione successiva del buffer. Se il nuovo puntatore di lettura è oltre la fine del buffer, viene reimpostato all'inizio. La figura 12 illustra la logica per il buffer di input circolare.

```C
UCHAR     tx_input_buffer[MAX_SIZE];
UCHAR     tx_input_write_ptr;
UCHAR     tx_input_read_ptr;

/* Initialization.  */
tx_input_write_ptr =  &tx_input_buffer[0];
tx_input_read_ptr =    &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr =  tx_input_write_ptr;
*tx_input_write_ptr++ =  alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr =  &tx_input_buffer[0];  /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr =  save_ptr;  /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
    alpha =  *tx_input_read_ptr++;
    if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
        tx_input_read_ptr =  &tx_input_buffer[0];
}
```
**FIGURA 12. Logica per il buffer di input circolare**

> [!IMPORTANT]
> Per un'operazione affidabile, potrebbe essere necessario bloccare gli interrupt quando si modificano i puntatori di lettura e scrittura dei buffer circolari di input e di output.

### <a name="circular-output-buffer"></a>Buffer di output circolare 
Il buffer di output viene usato per contenere i caratteri che sono arrivati per l'output prima che il dispositivo hardware abbia terminato l'invio del byte precedente. L'elaborazione del buffer di output è simile all'elaborazione del buffer di input, ma l'elaborazione dell'interrupt di trasmissione completa modifica il puntatore di lettura dell'output, mentre la richiesta di output dell'applicazione usa il puntatore di scrittura di output. In caso contrario, l'elaborazione del buffer di output è la stessa. La figura 13 mostra la logica per il buffer di output circolare.

```C
UCHAR     tx_output_buffer[MAX_SIZE];
UCHAR     tx_output_write_ptr;
UCHAR     tx_output_read_ptr;

/* Initialization.  */
tx_output_write_ptr =  &tx_output_buffer[0];
tx_output_read_ptr =   &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
    *device_reg =  *tx_output_read_ptr++;
    if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
    tx_output_read_ptr =  &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr =  tx_output_write_ptr;
*tx_output_write_ptr++ =  alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr =  &tx_output_buffer[0];  /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr =  save_ptr;  /* Buffer full!  */
```
**FIGURA 13. Logica per il buffer di output circolare**

### <a name="buffer-io-management"></a>Gestione I/O del buffer 
Per migliorare le prestazioni dei microprocessori incorporati, molti dispositivi periferici trasmettono e ricevono dati con buffer forniti dal software. In alcune implementazioni è possibile usare più buffer per trasmettere o ricevere singoli pacchetti di dati. 

Le dimensioni e la posizione dei buffer di I/O sono determinate dal software dell'applicazione e/o del driver. In genere, le dimensioni dei buffer sono fisse e vengono gestite all'interno di un pool di memoria a blocchi ThreadX SMP. La figura 14 indica un buffer di I/O tipico e un pool di memoria a blocchi ThreadX SMP che ne gestisce l'allocazione.

```C
typedef struct TX_IO_BUFFER_STRUCT
{

      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
    struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR  tx_buffer_area[TX_MAX_BUFFER_SIZE];
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
**FIGURA 14. I/O Buffer**

### <a name="tx_io_buffer"></a>TX_IO_BUFFER 
Il typedef TX_IO_BUFFER costituito da due puntatori. Il **puntatore * tx_next_packet** _ viene usato per collegare più pacchetti nell'elenco di input o di output. Il *_puntatore_* _ tx_next_buffer * viene usato per collegare tra loro i buffer che costituiscono un singolo pacchetto di dati dal dispositivo. Entrambi questi puntatori sono impostati su NULL quando il buffer viene allocato dal pool. Alcuni dispositivi possono anche richiedere un altro campo per indicare la quantità di dati effettivamente contenuta nell'area del buffer.

### <a name="buffered-io-advantage"></a>Vantaggio di I/O memorizzato nel buffer 
Quali sono i vantaggi di uno schema di I/O del buffer? Il vantaggio principale è che i dati non vengono copiati tra i registri del dispositivo e la memoria dell'applicazione. Al contrario, il driver fornisce al dispositivo una serie di puntatori al buffer. L'I/O del dispositivo fisico usa direttamente la memoria buffer fornita.

L'uso del processore per copiare pacchetti di informazioni di input o di output è estremamente diss costose e deve essere evitato in qualsiasi situazione di I/O con velocità effettiva elevata.

Un altro vantaggio dell'approccio di I/O memorizzato nel buffer è che gli elenchi di input e output non hanno condizioni complete. Tutti i buffer disponibili possono essere presenti in qualsiasi elenco in qualsiasi momento. Ciò è in contrasto con i buffer circolari di byte semplici presentati in precedenza nel capitolo. Ognuna aveva una dimensione fissa determinata in fase di compilazione.

### <a name="buffered-driver-responsibilities"></a>Responsabilità dei driver memorizzati nel buffer 
I driver di dispositivo memorizzati nel buffer riguardano solo la gestione di elenchi collegati di buffer di I/O. Viene mantenuto un elenco di buffer di input per i pacchetti ricevuti prima che il software dell'applicazione sia pronto. Al contrario, viene mantenuto un elenco di buffer di output per i pacchetti inviati più velocemente di quanto il dispositivo hardware possa gestirli. La figura 15 a pagina 314 mostra semplici elenchi collegati di input e output di pacchetti di dati e dei buffer che costituiscono ogni pacchetto.

![Responsabilità dei driver memorizzati nel buffer](media/image11.png)

**FIGURA 15. Input-Output elenchi**

Le applicazioni si interfacciano con i driver memorizzati nel buffer con gli stessi buffer di I/O. Durante la trasmissione, il software dell'applicazione fornisce al driver uno o più buffer da trasmettere. Quando il software dell'applicazione richiede l'input, il driver restituisce i dati di input nei buffer di I/O.

> [!IMPORTANT]
> In alcune applicazioni può essere utile creare un'interfaccia di input del driver che richiede all'applicazione di scambiare un buffer libero per un buffer di input dal driver. Ciò potrebbe elaborare l'allocazione del buffer all'interno del driver.

### <a name="interrupt-management"></a>Gestione degli interrupt 
In alcune applicazioni, la frequenza di interrupt del dispositivo può impedire la scrittura dell'ISR in C o l'interazione con ThreadX SMP su ogni interrupt. Ad esempio, se sono necessari 25us per salvare e ripristinare il contesto interrotto, non è consigliabile eseguire un salvataggio completo del contesto se la frequenza di interrupt è 50us. In questi casi, viene usato un ISR in linguaggio assembly di piccole dimensioni per gestire la maggior parte degli interrupt del dispositivo. Questo ISR lowoverhead interagirebbe con ThreadX SMP solo quando necessario.

Una discussione simile è disponibile nella discussione sulla gestione delle interruzioni alla fine del capitolo 3.

> [!NOTE]
> Se il blocco di interrupt deve essere usato per proteggere le sezioni critiche del codice del driver dal codice ISR del driver, il codice del driver a livello di thread deve sempre essere eseguito nello stesso core in cui viene elaborato l'ISR. In caso contrario, è necessario usare primitive SMP ThreadX interne come TX_DISABLE e TX_RESTORE che hanno anche la protezione inter-core predefinita.

### <a name="thread-suspension"></a>Sospensione dei thread 
Nell'esempio di driver semplice presentato in precedenza in questo capitolo, il chiamante del servizio di input viene sospeso se non è disponibile un carattere. In alcune applicazioni potrebbe non essere accettabile.

Ad esempio, se il thread responsabile dell'elaborazione dell'input da un driver ha anche altri compiti, la sospensione solo sull'input del driver probabilmente non funzionerà. Al contrario, il driver deve essere personalizzato per richiedere l'elaborazione in modo simile al modo in cui vengono effettuate altre richieste di elaborazione al thread.

Nella maggior parte dei casi, il buffer di input viene inserito in un elenco collegato e un messaggio di evento di input viene inviato alla coda di input del thread.