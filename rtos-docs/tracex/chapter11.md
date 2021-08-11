---
title: Capitolo 11 - Formato del buffer di traccia eventi
description: ThreadX fornisce il supporto predefinito della traccia eventi per tutti i Azure RTOS ThreadX, le modifiche dello stato dei thread e gli eventi definiti dall'utente.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: b230a6207cec3a0968d88b197455896881e5ef7a0d8b93d4b1fb5a37696a7b6c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802142"
---
# <a name="chapter-11---format-of-event-trace-buffer"></a>Capitolo 11 - Formato del buffer di traccia eventi

Azure RTOS ThreadX fornisce il supporto predefinito della traccia eventi per tutti i servizi ThreadX, le modifiche dello stato dei thread e gli eventi definiti dall'utente. Per usare la traccia eventi, è sufficiente compilare le librerie ThreadX, NetX e FileX con TX_ENABLE_EVENT_TRACE definito **e** abilitare la traccia chiamando la **_tx_trace_enable_** funzione . Questo capitolo descrive tale processo.

## <a name="event-trace-format"></a>Formato traccia eventi

Il formato del buffer di traccia degli eventi ThreadX è suddiviso in tre sezioni: l'intestazione del controllo, il registro oggetti e le voci di traccia. Di seguito viene descritto il layout generale del buffer di traccia degli eventi ThreadX:

**Intestazione del controllo**

**Voce del Registro di sistema dell'oggetto 0**

**…**

**Voce registro oggetti "n"**

**Voce di traccia eventi 0**

**…**

**Voce di traccia eventi "n"**

### <a name="event-trace-control-header"></a>Intestazione del controllo Traccia eventi

L'intestazione del controllo definisce il layout esatto del buffer di traccia eventi. Sono inclusi il numero di oggetti ThreadX che è possibile registrare e il numero di eventi che è possibile registrare. Inoltre, l'intestazione del controllo definisce la posizione in cui risiede ogni elemento del buffer di traccia. La struttura di dati seguente definisce l'intestazione del controllo:

```c
typedef struct TX_TRACE_CONTROL_HEADER_STRUCT
{
    ULONG    tx_trace_control_header_id;
    ULONG    tx_trace_control_header_timer_valid_mask;
    ULONG    tx_trace_control_header_trace_base_address;
    ULONG    tx_trace_control_header_object_registry_start_pointer;
    USHORT   tx_trace_control_header_reserved1;
    USHORT   tx_trace_control_header_object_registry_name_size;
    ULONG    tx_trace_control_header_object_registry_end_pointer;
    ULONG    tx_trace_control_header_buffer_start_pointer;
    ULONG    tx_trace_control_header_buffer_end_pointer;
    ULONG    tx_trace_control_header_buffer_current_pointer;
    ULONG    tx_trace_control_header_reserved2;
    ULONG    tx_trace_control_header_reserved3;
    ULONG    tx_trace_control_header_reserved4;
} TX_TRACE_CONTROL_HEADER;
```

### <a name="control-header-id"></a>ID intestazione controllo

L'ID dell'intestazione del controllo è costituito dal valore HEX a 32 bit di 0x54585442, che corrisponde ai caratteri ASCII ***TXTB.*** Poiché questo valore viene scritto come variabile senza segno a 32 bit, può essere usato anche per rilevare l'endianness del buffer di traccia eventi. Ad esempio, se il valore nei primi quattro byte della memoria è 0x54, 0x58, 0x54, 0x42, il buffer di traccia degli eventi è stato scritto in big endian formato. In caso contrario, il buffer di traccia degli eventi è stato little endian formato.

### <a name="timer-valid-mask"></a>Maschera valida timer

La maschera valida del timer definisce il numero di bit del timestamp nelle voci di traccia eventi effettive valide. Ad esempio, se l'origine timestamp ha 16 bit, il valore in questo campo deve essere 0xFFFF. Un'origine timestamp a 32 bit avrebbe un valore di 0xFFFFFFFF. Questo valore è definito dalla costante ***TX_TRACE_TIME_MASK** _ in _*_tx_port.h_**.

### <a name="trace-base-address"></a>Indirizzo di base della traccia

L'indirizzo di base del buffer di traccia è l'indirizzo specificato dall'applicazione come inizio del buffer di traccia ***nella tx_trace_enable*** chiamata. Questo indirizzo viene mantenuto per l'unico uso dello strumento di analisi per derivare offset bufferrelative per i vari elementi nel buffer. Ad esempio, l'offset relativo del buffer dell'evento corrente nel buffer di traccia viene calcolato dalla semplice sottrazione dell'indirizzo di base dall'indirizzo dell'evento corrente.

### <a name="registry-start-and-end-pointers"></a>Puntatori all'inizio e alla fine del Registro di sistema

Il puntatore di avvio del Registro di sistema punta all'indirizzo della prima voce del Registro di sistema dell'oggetto, mentre il puntatore finale del Registro di sistema punta all'indirizzo im.. /mediamente dopo l'ultima voce di registro. Questi valori vengono specificati durante *l'tx_trace_enable* e non vengono modificati per tutta la durata della traccia.

### <a name="registry-name-size"></a>Dimensioni del nome del Registro di sistema

La dimensione del nome del Registro di sistema definisce le dimensioni massime in byte per ogni nome di oggetto nella voce del Registro di sistema ed è definita dal simbolo ***TX_TRACE_OBJECT_REGISTRY_NAME** _. Il valore predefinito è 32 ed è definito in _*_tx_trace.h._*_ Il nome dell'oggetto corrisponde al nome specificato dall'applicazione al momento della creazione dell'oggetto. Ad esempio, il nome del Registro di sistema dell'oggetto per un thread è il nome fornito dall'applicazione alla chiamata _*_tx_thread_create_**.

### <a name="buffer-start-and-end-pointers"></a>Puntatori di inizio ed fine del buffer

Il puntatore iniziale del buffer di traccia eventi punta all'indirizzo della prima voce di traccia, mentre il puntatore finale del Registro di sistema punta all'indirizzo im.. /mediamente dopo l'ultima voce di traccia. Questi valori vengono specificati durante il ***tx_trace_enable</elaborazione*** e non vengono modificati per tutta la durata della traccia.

### <a name="current-buffer-pointer"></a>Puntatore del buffer corrente

Il puntatore corrente del buffer di traccia eventi punta all'indirizzo della voce di traccia meno recente. Poiché le voci di traccia vengono mantenute in un elenco circolare, il puntatore del buffer corrente rappresenta anche la voce di traccia successiva da scrivere. |

## <a name="event-trace-object-registry"></a>Registro oggetti traccia eventi

Il Registro di sistema dell'oggetto traccia eventi contiene ***n** _ voci del Registro di sistema dell'oggetto che corrispondono agli oggetti creati dall'applicazione. Lo scopo principale del Registro di sistema degli oggetti è quello di mettere in correlazione i nomi degli oggetti effettivi con gli indirizzi degli oggetti delle voci del buffer di traccia. Il numero di voci del Registro di sistema viene specificato dall'applicazione nella chiamata _ *_tx_trace_enable_** .

Ogni voce del registro oggetti contiene informazioni su un oggetto ThreadX specifico creato in precedenza dall'applicazione. La struttura di dati seguente definisce ogni voce del Registro di sistema dell'oggetto:

```c
typedef struct TX_TRACE_OBJECT_REGISTRY_ENTRY_STRUCT
{
    UCHAR    tx_trace_object_registry_entry_object_available**;
    UCHAR    tx_trace_object_registry_entry_object_type**;
    UCHAR    tx_trace_object_registry_entry_object_reserved1;
    UCHAR    tx_trace_object_registry_entry_object_reserved2;
    ULONG    tx_trace_thread_registry_entry_object_pointer;
    ULONG    tx_trace_object_registry_entry_object_parameter_1;
    ULONG    tx_trace_object_registry_entry_object_parameter_2;
    UCHAR    tx_trace_thread_registry_entry_object_name[TX_TRACE_OBJECT_REGISTRY_NAME];

} TX_TRACE_OBJECT_REGISTRY_ENTRY;
```

### <a name="object-available-flag"></a>Flag disponibile per gli oggetti

Il flag object available è impostato su 1 se la voce del Registro di sistema dell'oggetto è disponibile. In caso contrario, se il valore non è 1, la voce del Registro di sistema dell'oggetto non è disponibile. Si noti che la voce potrebbe comunque contenere informazioni valide anche se è disponibile.

### <a name="object-entry-type"></a>Tipo di voce dell'oggetto

Il tipo di voce dell'oggetto identifica il tipo di oggetto in questa voce. Di seguito è riportato un elenco dei tipi di oggetto validi:

| **Valore** | **Tipo oggetto** |
|---------- | --------------- |
| 0         | Non valido       |
| 1         | Thread          |
| 2         | Timer |
| 3         | Coda |
| 4         | Semaphore |
| 5         | Mutex |
| 6         | Gruppo di flag di eventi |
| 7         | Pool a blocchi |
| 8         | Byte Pool |
| 9         | .. /media |
| 10        | File |
| 11        | IP |
| 12        | Pool di pacchetti |
| 13        | TCP Socket |
| 14        | UDP Socket |
| 15-20     | Riservato |  
| 21        | Dispositivo stack host USB |
| 22        | Interfaccia stack host USB |
| 23        | USB Host Endpoint |
| 24        | Classe host USB |
| 25        | Dispositivo USB |
| 26        | Interfaccia dispositivo USB |
| 27        | Endpoint dispositivo USB |
| 28        | Classe dispositivo USB |

### <a name="object-pointer"></a>Puntatore a oggetto

Il puntatore a oggetto specifica l'indirizzo dell'oggetto usato per accedere all'oggetto tramite l'API ThreadX.

### <a name="object-reserved-fields"></a>Campi riservati dell'oggetto

Per tutti gli oggetti diversi da thread, questi campi riservati devono essere 0. Per i thread, la priorità del thread al momento dell'immissione nel Registro di sistema viene inserita in questi due campi riservati.

### <a name="object-parameters"></a>Parametri dell'oggetto

I parametri dell'oggetto contengono informazioni supplementari sull'oggetto. Di seguito vengono descritte le informazioni supplementari per ogni oggetto ThreadX:

| **Tipo oggetto**        | **Parametro 1**  | **Parametro 2** |
|----------------------- | ---------------- | --------------- |
| Thread                 | Avvio dello stack      | Dimensioni dello stack |
| Timer                  | Tick iniziali | Ripianificare i tick |
| Coda                  | Dimensione della coda | Dimensioni del messaggio |
| Semaphore              | Istanze iniziali | - |
| Mutex                  | Flag di ereditarietà | - |
| Gruppo di flag di eventi      | - | - |
| Pool a blocchi             | Totale blocchi | Dimensione blocco |
| Byte Pool              | Total Bytes | - |
| .. /media                  | Dimensioni cache fat | Dimensioni della cache di settore |
| File                   | - | - |
| IP                     | Avvio dello stack | Dimensioni dello stack |
| Pool di pacchetti            | Dimensione pacchetti | Numero di pacchetti |
| TCP Socket             | Indirizzo IP | Dimensioni della finestra |
| UDP Socket             | Indirizzo IP | RX Queue Max |

### <a name="object-name"></a>Nome oggetto

Il nome dell'oggetto contiene il nome dell'oggetto ThreadX. Il nome è il nome fornito a ThreadX al momento della creazione dell'oggetto. Per impostazione predefinita, il nome dell'oggetto ha un massimo di 32 caratteri. I nomi effettivi maggiori di 32 caratteri vengono troncati.

## <a name="event-trace-entries"></a>Voci di Traccia eventi

Le voci di traccia eventi si trovano nella parte inferiore del buffer di traccia eventi. Le voci vengono mantenute in un elenco circolare, con il puntatore di ingresso corrente che punta alla voce meno recente. Il numero di voci nell'elenco viene calcolato dalla ***tx_trace_enable*** chiamata.

Ogni voce del registro oggetti contiene informazioni su un evento di traccia ThreadX specifico. La struttura di dati seguente definisce ogni voce di evento di traccia:

```c
typedef struct TX_TRACE_BUFFER_ENTRY_STRUCT
{
    ULONG     tx_trace_buffer_entry_thread_pointer;
    ULONG     tx_trace_buffer_entry_thread_priority;
    ULONG     tx_trace_buffer_entry_event_id;
    ULONG     tx_trace_buffer_entry_time_stamp;
    ULONG     tx_trace_buffer_entry_information_field_1;
    ULONG     tx_trace_buffer_entry_information_field_2;
    ULONG     tx_trace_buffer_entry_information_field_3;
    ULONG     tx_trace_buffer_entry_information_field_4;
} TX_TRACE_BUFFER_ENTRY;
```

### <a name="thread-pointer"></a>Puntatore thread

Il puntatore del thread contiene l'indirizzo del thread in esecuzione al momento dell'evento. Se l'evento si è verificato durante l'inizializzazione (nessun thread in esecuzione), il valore di questo puntatore viene 0xF0F0F0F0. Se l'evento si è verificato durante un'istruzione ISR (Interrupt Service Routine), il valore di questo puntatore viene 0xFFFFFFFF. Se la voce non è ancora stata usata, il valore di questo puntatore è 0.

### <a name="thread-priority"></a>Priorità thread

Il campo priorità thread contiene la priorità del thread e la soglia di precedenza del thread in esecuzione al momento dell'evento. Se è presente un contesto di interrupt (il puntatore del thread è 0xFFFFFFFF), il valore di questo campo non è la priorità, ma il valore di ***_tx_thread_current_ptr*** al momento dell'evento. In caso contrario, il valore di questo campo è 0.

### <a name="event-id"></a>ID evento

L'ID evento specifica l'evento che ha avuto luogo. Gli ID di evento di traccia ThreadX validi sono compreso tra 1 e 1024. I valori a partire da 1025 e superiori sono riservati per gli eventi specifici dell'utente. Fare riferimento al file ***tx_trace.h per*** la definizione completa degli ID evento ThreadX.</td>

### <a name="information-fields-1-4"></a>Campi informazioni (1-4)

I campi di informazioni contengono informazioni aggiuntive sull'evento specifico. Fare riferimento al file ***tx_trace.h per*** la descrizione completa dei campi di informazioni per ogni ID evento ThreadX definito.