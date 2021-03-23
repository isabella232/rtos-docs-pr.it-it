---
title: Capitolo 11-formato del buffer di traccia eventi
description: ThreadX fornisce il supporto predefinito per la traccia degli eventi per tutti i servizi ThreadX di Azure RTO, le modifiche dello stato dei thread e gli eventi definiti dall'utente.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: d11b827558e9c96df44f462329b7807a500a64a4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823480"
---
# <a name="chapter-11---format-of-event-trace-buffer"></a>Capitolo 11-formato del buffer di traccia eventi

Azure RTO ThreadX offre supporto predefinito per la traccia degli eventi per tutti i servizi ThreadX, le modifiche allo stato del thread e gli eventi definiti dall'utente. Per usare la traccia eventi, è sufficiente compilare le librerie ThreadX, NetX e FileX con **TX_ENABLE_EVENT_TRACE** definite e abilitare la traccia chiamando la funzione **_tx_trace_enable_** . In questo capitolo viene descritto il processo.

## <a name="event-trace-format"></a>Formato traccia eventi

Il formato del buffer di traccia dell'evento ThreadX è suddiviso in tre sezioni, ovvero l'intestazione del controllo, il registro oggetti e le voci di traccia. Di seguito viene descritto il layout generale del buffer di traccia dell'evento ThreadX:

**Intestazione del controllo**

**Voce del registro di sistema dell'oggetto 0**

**…**

**Voce del registro oggetti "n"**

**Immissione traccia eventi 0**

**…**

**Voce di traccia eventi "n"**

### <a name="event-trace-control-header"></a>Intestazione controllo traccia eventi

L'intestazione del controllo definisce il layout esatto del buffer di traccia eventi. Ciò include il numero di oggetti ThreadX che è possibile registrare e il numero di eventi che possono essere registrati. Inoltre, l'intestazione del controllo definisce la posizione in cui si trovano tutti gli elementi del buffer di traccia. La struttura dei dati seguente definisce l'intestazione del controllo:

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

### <a name="control-header-id"></a>ID intestazione del controllo

L'ID dell'intestazione del controllo è costituito dal valore ESADECIMALe a 32 bit di 0x54585442, che corrisponde ai caratteri ASCII ***TXTB***. Poiché questo valore viene scritto come variabile senza segno a 32 bit, può essere utilizzato anche per rilevare l'oggetto dell'oggetto buffer di traccia eventi. Se, ad esempio, il valore nei primi quattro addii di memoria è 0x54, 0x58, 0x54, 0x42, il buffer di traccia eventi è stato scritto in formato big endian. In caso contrario, il buffer di traccia eventi è stato scritto in formato little endian.

### <a name="timer-valid-mask"></a>Maschera del timer valida

La maschera timer valida definisce il numero di bit del timestamp nelle voci della traccia eventi effettivi validi. Se, ad esempio, l'origine timestamp dispone di 16 bit, il valore in questo campo dovrebbe essere 0xFFFF. Un'origine timestamp a 32 bit avrà un valore 0xFFFFFFFF. Questo valore è definito dalla costante ***TX_TRACE_TIME_MASK** _ in _ *_tx_port. h_* *.

### <a name="trace-base-address"></a>Indirizzo di base della traccia

L'indirizzo di base del buffer di traccia è l'indirizzo specificato dall'applicazione come inizio del buffer di traccia nella chiamata ***tx_trace_enable*** . Questo indirizzo viene mantenuto per l'utilizzo esclusivo dello strumento di analisi per derivare gli offset bufferrelative per i vari elementi nel buffer. Ad esempio, l'offset relativo del buffer dell'evento corrente nel buffer di traccia viene calcolato dalla semplice sottrazione dell'indirizzo di base dall'indirizzo dell'evento corrente.

### <a name="registry-start-and-end-pointers"></a>Puntatori di inizio e fine del registro di sistema

Il puntatore di avvio del registro di sistema punta all'indirizzo della prima voce del registro di sistema dell'oggetto, mentre il puntatore di fine del registro di sistema punta all'indirizzo im. /mediately dopo l'ultima voce di registro. Questi valori vengono impostati durante l'elaborazione del *tx_trace_enable* e non vengono modificati durante la durata della traccia.

### <a name="registry-name-size"></a>Dimensioni Nome registro

Le dimensioni del nome del registro di sistema definiscono le dimensioni massime in byte per ogni nome di oggetto nella voce del registro di sistema ed è definito dal simbolo ***TX_TRACE_OBJECT_REGISTRY_NAME** _. Il valore predefinito è 32 ed è definito in _*_tx_trace. h_*_. Il nome dell'oggetto corrisponde al nome assegnato dall'applicazione al momento della creazione dell'oggetto. Ad esempio, il nome del registro di sistema dell'oggetto per un thread è il nome fornito dall'applicazione alla chiamata _ *_tx_thread_create_* *.

### <a name="buffer-start-and-end-pointers"></a>Puntatori di inizio e fine del buffer

Il puntatore di avvio del buffer di traccia eventi punta all'indirizzo della prima voce di traccia, mentre il puntatore finale del registro di sistema punta all'indirizzo im. /mediately che segue l'ultima voce di traccia. Questi valori vengono impostati durante l' ***tx_trace_enable</*** elaborazione e non vengono modificati durante la durata della traccia.

### <a name="current-buffer-pointer"></a>Puntatore al buffer corrente

Il puntatore corrente del buffer di traccia eventi punta all'indirizzo della voce di traccia meno recente. Poiché le voci di traccia vengono mantenute in un elenco circolare, il puntatore al buffer corrente rappresenta anche la voce di traccia successiva da scrivere. |

## <a name="event-trace-object-registry"></a>Registro oggetti traccia eventi

Il registro degli oggetti di traccia eventi contiene le voci del registro di sistema dell'oggetto ***n** che corrispondono agli oggetti creati dall'applicazione. Lo scopo principale del registro oggetti è per gli strumenti di analisi esterna correlare i nomi di oggetto effettivi con gli indirizzi degli oggetti delle voci del buffer di traccia. Il numero di voci del registro di sistema viene specificato dall'applicazione nella chiamata _ *_tx_trace_enable_**.

Ogni voce del registro oggetti contiene informazioni su un oggetto ThreadX specifico creato in precedenza dall'applicazione. La struttura dei dati seguente definisce la voce del registro di sistema di ogni oggetto:

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

### <a name="object-available-flag"></a>Flag oggetto disponibile

Il flag oggetto disponibile viene impostato su 1 se è disponibile la voce del registro di sistema dell'oggetto. In caso contrario, se il valore non è 1, la voce del registro di sistema dell'oggetto non è disponibile. Si noti che la voce potrebbe ancora contenere informazioni valide anche se disponibile.

### <a name="object-entry-type"></a>Tipo voce oggetto

Il tipo di voce dell'oggetto identifica il tipo di oggetto in questa voce. Di seguito è riportato un elenco dei tipi di oggetto validi:

| **Valore** | **Tipo oggetto** |
|---------- | --------------- |
| 0         | Non valido       |
| 1         | Thread          |
| 2         | Timer |
| 3         | Coda |
| 4         | Semaphore |
| 5         | Mutex |
| 6         | Gruppo flag di evento |
| 7         | Blocca pool |
| 8         | Pool di byte |
| 9         | .. /media |
| 10        | File |
| 11        | IP |
| 12        | Pool di pacchetti |
| 13        | Socket TCP |
| 14        | Socket UDP |
| 15-20     | Riservato |  
| 21        | Dispositivo stack host USB |
| 22        | Interfaccia stack host USB |
| 23        | Endpoint host USB |
| 24        | Classe host USB |
| 25        | Dispositivo USB |
| 26        | Interfaccia del dispositivo USB |
| 27        | Endpoint dispositivo USB |
| 28        | Classe dispositivo USB |

### <a name="object-pointer"></a>Puntatore all'oggetto

Il puntatore all'oggetto specifica l'indirizzo dell'oggetto usato per accedere all'oggetto usando l'API ThreadX.

### <a name="object-reserved-fields"></a>Campi riservati oggetto

Per tutti gli oggetti diversi dai thread, questi campi riservati devono essere 0. Per i thread, la priorità del thread nel momento in cui viene immessa nel registro di sistema viene inserita in questi due campi riservati.

### <a name="object-parameters"></a>Parametri oggetto

I parametri dell'oggetto contengono informazioni aggiuntive sull'oggetto. Di seguito vengono descritte le informazioni aggiuntive per ogni oggetto ThreadX:

| **Tipo oggetto**        | **Parametro 1**  | **Parametro 2** |
|----------------------- | ---------------- | --------------- |
| Thread                 | Inizio dello stack      | Dimensioni dello stack |
| Timer                  | Cicli iniziali | Ripianificazione di cicli |
| Coda                  | Dimensione della coda | Dimensioni del messaggio |
| Semaphore              | Istanze iniziali | - |
| Mutex                  | Flag ereditarietà | - |
| Gruppo flag di evento      | - | - |
| Blocca pool             | Blocchi totali | Dimensione blocco |
| Pool di byte              | Total Bytes | - |
| .. /media                  | Dimensioni cache FAT | Dimensioni della cache del settore |
| File                   | - | - |
| IP                     | Inizio dello stack | Dimensioni dello stack |
| Pool di pacchetti            | Dimensione pacchetti | Numero di pacchetti |
| Socket TCP             | Indirizzo IP | Dimensioni della finestra |
| Socket UDP             | Indirizzo IP | Massimo coda RX |

### <a name="object-name"></a>Nome oggetto

Il nome dell'oggetto contiene il nome dell'oggetto ThreadX. Il nome è il nome fornito a ThreadX al momento della creazione dell'oggetto. Per impostazione predefinita, il nome dell'oggetto è costituito da un massimo di 32 caratteri. I nomi effettivi maggiori di 32 caratteri vengono troncati.

## <a name="event-trace-entries"></a>Voci di traccia eventi

Le voci della traccia eventi si trovano nella parte inferiore del buffer di traccia eventi. Le voci vengono mantenute in un elenco circolare, con il puntatore alla voce corrente che punta alla voce meno recente. Il numero di voci nell'elenco viene calcolato dalla chiamata ***tx_trace_enable*** .

Ogni voce del registro oggetti contiene informazioni su un evento di traccia ThreadX specifico. La struttura dei dati seguente definisce ogni voce dell'evento di traccia:

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

Il puntatore al thread contiene l'indirizzo del thread in esecuzione al momento dell'evento. Se l'evento si è verificato durante l'inizializzazione (nessun thread in esecuzione), il valore di questo puntatore è 0xF0F0F0F0. Se l'evento si è verificato durante una routine del servizio di interrupt (ISR), il valore di questo puntatore è 0xFFFFFFFF. Se la voce non è ancora stata utilizzata, il valore di questo puntatore è 0.

### <a name="thread-priority"></a>Priorità thread

Il campo priorità thread contiene la priorità del thread e la soglia di precedenza del thread che era in esecuzione al momento dell'evento. Se è presente un contesto di interrupt (puntatore al thread è 0xFFFFFFFF), il valore di questo campo non è la priorità, ma il valore di ***_tx_thread_current_ptr*** al momento dell'evento. In caso contrario, il valore di questo campo è 0.

### <a name="event-id"></a>ID evento

L'ID evento specifica l'evento che ha avuto luogo. Gli ID evento di traccia ThreadX validi sono compresi tra 1 e 1024. I valori a partire da 1025 e versioni successive sono riservati per gli eventi specifici dell'utente. Per la definizione completa degli ID evento ThreadX, vedere il file ***tx_trace. h*** .</td>

### <a name="information-fields-1-4"></a>Campi informazioni (1-4)

I campi informativi contengono informazioni aggiuntive sull'evento specifico. Per una descrizione completa dei campi di informazioni per ogni ID evento ThreadX definito, vedere il file ***tx_trace. h*** .