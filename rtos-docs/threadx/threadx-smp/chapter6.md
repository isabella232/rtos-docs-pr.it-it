---
title: Capitolo 6 - Sistema dimostrativo per Azure RTOS ThreadX SMP
description: Questo capitolo contiene una descrizione del sistema dimostrativo fornito con tutti i Azure RTOS di supporto del processore ThreadX SMP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5da4c12cf3c035e59dcd1abef063d5ae40a657d6fd91bbd29f51cf7d46813154
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784054"
---
# <a name="chapter-6---demonstration-system-for-azure-rtos-threadx-smp"></a>Capitolo 6 - Sistema dimostrativo per Azure RTOS ThreadX SMP

Questo capitolo contiene una descrizione del sistema dimostrativo fornito con tutti i Azure RTOS di supporto del processore ThreadX SMP. 

## <a name="overview"></a>Panoramica

Ogni distribuzione del prodotto ThreadX SMP contiene un sistema dimostrativo che viene eseguito su tutti i microprocessori supportati.

Questo sistema di esempio è definito nel file di ***distribuzione demo_threadx.c*** ed è progettato per illustrare l'uso di ThreadX SMP in un ambiente multithread incorporato. La dimostrazione è costituita da inizializzazione, otto thread, un pool di byte, un pool di blocchi, una coda, un semaforo, un mutex e un gruppo di flag di evento.

> [!IMPORTANT]
> Fatta eccezione per le dimensioni dello stack del thread, l'applicazione dimostrativa è identica in tutti i processori supportati da ThreadX SMP.

L'elenco completo ***di demo_threadx.c,*** inclusi i numeri di riga a cui si fa riferimento nel resto di questo capitolo, viene visualizzato a pagina 324 e successiva.

## <a name="application-define"></a>Definizione dell'applicazione

La ***tx_application_define*** viene eseguita dopo il completamento dell'inizializzazione SMP ThreadX di base. È responsabile della configurazione di tutte le risorse di sistema iniziali, inclusi thread, code, semafori, mutex, flag di eventi e pool di memoria.

Il sistema dimostrativo ***tx_application_define** _ (numeri _line 60-164*) crea gli oggetti dimostrativi nell'ordine seguente:

```C
byte_pool_0
thread_0
thread_1
thread_2
thread_3
thread_4
thread_5
thread_6
thread_7
queue_0
semaphore_0
event_flags_0
mutex_0
block_pool_0
```
Il sistema dimostrativo non crea altri oggetti SMP ThreadX aggiuntivi. Tuttavia, un'applicazione effettiva può creare oggetti di sistema durante il runtime all'interno dei thread in esecuzione.

### <a name="initial-execution"></a>Esecuzione iniziale 
Tutti i thread vengono creati con **l'TX_AUTO_START** predefinita. Questo li rende inizialmente pronti per l'esecuzione. Al **_tx_application_define,_** il controllo viene trasferito all'utilità di pianificazione dei thread e da qui a ogni singolo thread.

L'ordine di esecuzione dei thread è determinato dalla priorità e dall'ordine in cui sono stati creati. Nel sistema dimostrativo ***thread_0** _ viene eseguito per primo perché ha la priorità più alta ( è stato creato con una priorità _di 1*). Dopo la_ sospensione di * thread_0, viene eseguito _*_thread_5,_*_ seguito dall'esecuzione di _*_thread_3_*_, _*_thread_4_*_, _*_thread_6_*_, _*_thread_7_*_, _*_thread_1_*_ e infine _*_thread_2_**.

> [!IMPORTANT]
> Anche se **thread_3** e **thread_4** hanno la stessa priorità (entrambe create con priorità 8), thread_3 viene eseguita per prima.  Ciò è dovuto **al thread_3** stato creato e pronto **prima thread_4**. I thread con uguale priorità vengono eseguiti in modo FIFO.

## <a name="thread-0"></a>Thread 0

La funzione ***thread_0_entry** _ contrassegna il punto di ingresso del thread _(righe 167-190*). ***Thread_0**_ è il primo thread del sistema dimostrativo da eseguire. L'elaborazione è semplice: incrementa il contatore, viene inattiva per 10 tick timer, imposta un flag di evento per la riattivazione _*_thread_5_**, quindi ripete la sequenza.

***Thread_0*** è il thread con la priorità più alta nel sistema. Alla scadenza della sospensione richiesta, verrà eseguito qualsiasi altro thread in esecuzione nella dimostrazione.

## <a name="thread-1"></a>Thread 1

La funzione ***thread_1_entry** _ contrassegna il punto di ingresso del thread _(righe 193-216*). ***Thread_1**_ è il secondo all'ultimo thread del sistema dimostrativo da eseguire. L'elaborazione consiste nell'incremento del contatore, nell'invio di un messaggio _*_thread_2_*_ (_da * ***queue_0**_) e nella ripetizione della sequenza. Si noti _*_che thread_1_*_ viene sospesa _*_ogni queue_0_*_ completa (_line 207*).

## <a name="thread-2"></a>Thread 2

La funzione ***thread_2_entry** _ contrassegna il punto di ingresso del thread _(righe 219-243*). ***Thread_2**_ è l'ultimo thread del sistema dimostrativo da eseguire. L'elaborazione consiste nell'incremento del contatore, nel recupero di un messaggio _*_thread_1_*_ (tramite _*_queue_0_*_) e nella ripetizione della sequenza. Si noti _*_che thread_2_*_ viene sospesa _*_ogni queue_0_*_ vuoto (_line 233*).

Anche se *** thread_1** _ _*_e thread_2_*_ condividono la priorità più bassa nel sistema dimostrativo (_priority 16), sono anche gli unici thread pronti per l'esecuzione nella maggior parte dei *casi. Sono anche gli unici thread creati con la sezione temporale (righe* 87 e 93*). Ogni thread può essere eseguito per un massimo di 4 tick timer prima dell'esecuzione dell'altro thread.

## <a name="threads-3-and-4"></a>Thread 3 e 4

La funzione ***thread_3_and_4_entry** _ contrassegna _**_ il punto di ingresso di thread_3 e _*_thread_4_*_ _(righe 246-280*). Entrambi i thread hanno una priorità di 8, che li rende il terzo e il quarto thread del sistema dimostrativo da eseguire. L'elaborazione_ per ogni thread è la stessa: incremento del contatore, recupero di * semaphore_0 , sospensione per 2 tick timer, rilascio _*_semaphore_0_*_ e ripetizione della sequenza. Si noti che ogni thread viene sospeso _*_ogni semaphore_0_*_ non è disponibile (_line 264*).

Entrambi i thread usano anche la stessa funzione per l'elaborazione principale. Questo non presenta problemi perché entrambi hanno un proprio stack univoco e C è naturalmente rientrante. Ogni thread determina quale si tratta verificando il parametro di input del thread ( riga *258*), che viene impostato al momento della creazione ( righe *102 e 109*).

> [!IMPORTANT]
> È anche ragionevole ottenere il punto di thread corrente durante l'esecuzione del thread e confrontarlo con l'indirizzo del blocco di controllo per determinare l'identità del thread.

## <a name="thread-5"></a>Thread 5

La funzione ***thread_5_entry** _ contrassegna il punto di ingresso del thread _(righe 283-305*). ***Thread_5**_ è il secondo thread del sistema dimostrativo da eseguire. L'elaborazione consiste nell'incrementare il contatore, ottenere un flag di evento _*_da_*_ thread_0 (tramite _*_event_flags_0_*_) e ripetere la sequenza. Si noti _*_thread_5_*_ ogni volta che il flag di evento _*_event_flags_0_*_ non è disponibile (_line 298*).

## <a name="threads-6-and-7"></a>Thread 6 e 7

La funzione ***thread_6_and_7_entry** _ contrassegna il punto di ingresso thread_6 _*_e_*_ _*_thread_7_*_ _(righe 307-358*). Entrambi i thread hanno una priorità di 8, che li rende il quinto e il sesto thread del sistema dimostrativo da eseguire._ L'elaborazione per ogni thread è la stessa: incremento del contatore, recupero di * mutex_0 due volte, sospensione per 2 tick timer, rilascio _*_mutex_0_*_ due volte e ripetizione della sequenza. Si noti che ogni thread viene sospeso _*_ogni mutex_0_*_ non è disponibile (_line 325*).

Entrambi i thread usano anche la stessa funzione per l'elaborazione principale. Questo non presenta problemi perché entrambi hanno un proprio stack univoco e C è naturalmente rientrante. Ogni thread determina quale si tratta verificando il parametro di input del thread ( riga *319*), che viene impostato al momento della creazione ( righe *126 e 133*).

## <a name="observing-the-demonstration"></a>Osservazione della dimostrazione

Ognuno dei thread dimostrativi incrementa il proprio contatore univoco. I contatori seguenti possono essere esaminati per verificare l'operazione della demo:

```C
thread_0_counter
thread_1_counter
thread_2_counter
thread_3_counter
thread_4_counter
thread_5_counter
thread_6_counter
thread_7_counter
```

Ognuno di questi contatori dovrebbe continuare ad aumentare durante l'esecuzione della dimostrazione, con ***thread_1_counter** _ e _ *_thread_2_counter_** che aumentano alla velocità più rapida.

## <a name="distribution-file-demo_threadxc"></a>File di distribuzione: demo_threadx.c

In questa sezione viene visualizzato l'elenco completo ***di demo_threadx.c***, inclusi i numeri di riga a cui si fa riferimento in questo capitolo.

```C
000 /* This is a small demo of the high-performance ThreadX SMP kernel. It includes examples of eight
001 threads of different priorities, using a message queue, semaphore, mutex, event flags group,
002 byte pool, and block pool. */
003
004 #include "tx_api.h"
005
006 #define DEMO_STACK_SIZE         1024
007 #define DEMO_BYTE_POOL_SIZE     9120
008 #define DEMO_BLOCK_POOL_SIZE    100
009 #define DEMO_QUEUE_SIZE         100
010
011 /* Define the ThreadX SMP object control blocks...  */
012
013 TX_THREAD               thread_0;
014 TX_THREAD               thread_1;
015 TX_THREAD               thread_2;
016 TX_THREAD               thread_3;
017 TX_THREAD               thread_4;
018 TX_THREAD               thread_5;
019 TX_THREAD               thread_6;
020 TX_THREAD               thread_7;
021 TX_QUEUE                queue_0;
022 TX_SEMAPHORE            semaphore_0;
023 TX_MUTEX                mutex_0;
024 TX_EVENT_FLAGS_GROUP    event_flags_0;
025 TX_BYTE_POOL            byte_pool_0;
026 TX_BLOCK_POOL           block_pool_0;
027
028 /* Define the counters used in the demo application...  */
029
030 ULONG                    thread_0_counter;
031 ULONG                    thread_1_counter;
032 ULONG                    thread_1_messages_sent;
033 ULONG                    thread_2_counter;
034 ULONG                    thread_2_messages_received;
035 ULONG                    thread_3_counter;
036 ULONG                    thread_4_counter;
037 ULONG                    thread_5_counter;
038 ULONG                    thread_6_counter;
039 ULONG                    thread_7_counter;
040
041 /* Define thread prototypes.  */
042
043 void    thread_0_entry(ULONG thread_input);
044 void    thread_1_entry(ULONG thread_input);
045 void    thread_2_entry(ULONG thread_input);
046 void    thread_3_and_4_entry(ULONG thread_input);
047 void    thread_5_entry(ULONG thread_input);
048 void    thread_6_and_7_entry(ULONG thread_input);
049
050
051 /* Define main entry point.  */
052
053 int main()
054 {
055
056     /* Enter the ThreadX SMP kernel. */
057     tx_kernel_enter();
058 }
059
060 /* Define what the initial system looks like. */
061 void    tx_application_define(void *first_unused_memory)
062 {
063
064 CHAR    *pointer;
065
066    /* Create a byte memory pool from which to allocate the thread stacks. */
067    tx_byte_pool_create(&byte_pool_0, "byte pool 0", first_unused_memory,
068                               DEMO_BYTE_POOL_SIZE);
069
070    /* Put system definition stuff in here, e.g., thread creates and other assorted
071       create information. */
072
073    /* Allocate the stack for thread 0. */
074    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
075
076    /* Create the main thread. */
077    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
078                               pointer, DEMO_STACK_SIZE,
079                               1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
080
081    /* Allocate the stack for thread 1. */
082    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
083
084    /* Create threads 1 and 2. These threads pass information through a ThreadX SMP
085       message queue. It is also interesting to note that these threads have a time
086       slice. */
087    tx_thread_create(&thread_1, "thread 1", thread_1_entry, 1,
088                              pointer, DEMO_STACK_SIZE,
089                              16, 16, 4, TX_AUTO_START);
090
091    /* Allocate the stack for thread 2. */
092    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
093    tx_thread_create(&thread_2, "thread 2", thread_2_entry, 2,
094                              pointer, DEMO_STACK_SIZE,
095                              16, 16, 4, TX_AUTO_START);
096
097    /* Allocate the stack for thread 3. */
098    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
099
100    /* Create threads 3 and 4. These threads compete for a ThreadX SMP counting semaphore.
101       An interesting thing here is that both threads share the same instruction area. */
102    tx_thread_create(&thread_3, "thread 3", thread_3_and_4_entry, 3,
103                              pointer, DEMO_STACK_SIZE,
104                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
105
106    /* Allocate the stack for thread 4. */
107    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
108
109    tx_thread_create(&thread_4, "thread 4", thread_3_and_4_entry, 4,
110                              pointer, DEMO_STACK_SIZE,
111                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
112
113    /* Allocate the stack for thread 5. */
114    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
115
116    /* Create thread 5. This thread simply pends on an event flag, which will be set
117       by thread_0. */
118    tx_thread_create(&thread_5, "thread 5", thread_5_entry, 5,
119                              pointer, DEMO_STACK_SIZE,
120                              4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
121
122    /* Allocate the stack for thread 6. */
123    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
124
125    /* Create threads 6 and 7. These threads compete for a ThreadX SMP mutex. */
126    tx_thread_create(&thread_6, "thread 6", thread_6_and_7_entry, 6,
127                              pointer, DEMO_STACK_SIZE,
128                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
129
130    /* Allocate the stack for thread 7. */
131    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
132
133    tx_thread_create(&thread_7, "thread 7", thread_6_and_7_entry, 7,
134                              pointer, DEMO_STACK_SIZE,
135                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
136
137    /* Allocate the message queue. */
138    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_QUEUE_SIZE*sizeof(ULONG), TX_NO_WAIT);
139
140    /* Create the message queue shared by threads 1 and 2. */
141    tx_queue_create(&queue_0, "queue 0", TX_1_ULONG, pointer, DEMO_QUEUE_SIZE*sizeof(ULONG));
142
143    /* Create the semaphore used by threads 3 and 4. */
144    tx_semaphore_create(&semaphore_0, "semaphore 0", 1);
145
146    /* Create the event flags group used by threads 1 and 5. */
147    tx_event_flags_create(&event_flags_0, "event flags 0");
148
149    /* Create the mutex used by thread 6 and 7 without priority inheritance. */
150    tx_mutex_create(&mutex_0, "mutex 0", TX_NO_INHERIT);
151
152    /* Allocate the memory for a small block pool. */
153    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_BLOCK_POOL_SIZE, TX_NO_WAIT);
154
155    /* Create a block memory pool to allocate a message buffer from. */
156    tx_block_pool_create(&block_pool_0, "block pool 0", sizeof(ULONG), pointer,
157                 DEMO_BLOCK_POOL_SIZE);
158
159    /* Allocate a block and release the block memory. */
160    tx_block_allocate(&block_pool_0, &pointer, TX_NO_WAIT);
161
162    /* Release the block back to the pool. */
163    tx_block_release(pointer);
164 }
165
166    /* Define the test threads. */
167    void thread_0_entry(ULONG thread_input)
168 {
169
170 UINT status;
171
172
173    /* This thread simply sits in while-forever-sleep loop. */
174     while(1)
175    {
176
177    /* Increment the thread counter. */
178    thread_0_counter++;
179
180    /* Sleep for 10 ticks. */
181    tx_thread_sleep(10);
182
183    /* Set event flag 0 to wakeup thread 5. */
184    status = tx_event_flags_set(&event_flags_0, 0x1, TX_OR);
185
186    /* Check status. */
187    if (status != TX_SUCCESS)
188       break;
189    }
190 }
191
192
193 void    thread_1_entry(ULONG thread_input)
194 {
195
196 UINT    status;
197
198
199    /* This thread simply sends messages to a queue shared by thread 2. */
200    while(1)
201    {
202
203         /* Increment the thread counter. */
204         thread_1_counter++;
205
206         /* Send message to queue 0. */
207         status = tx_queue_send(&queue_0, &thread_1_messages_sent, TX_WAIT_FOREVER);
208
209         /* Check completion status. */
210         if (status != TX_SUCCESS)
211            break;
212
213         /* Increment the message sent. */
214         thread_1_messages_sent++;
215    }
216 }
217
218
219 void     thread_2_entry(ULONG thread_input)
220 {
221
222 ULONG     received_message;
223 UINT      status;
224
225     /* This thread retrieves messages placed on the queue by thread 1. */
226     while(1)
227     {
228
229         /* Increment the thread counter. */
230         thread_2_counter++;
231
232         /* Retrieve a message from the queue. */
233         status = tx_queue_receive(&queue_0, &received_message, TX_WAIT_FOREVER);
234
235         /* Check completion status and make sure the message is what we
236            expected. */
237         if ((status != TX_SUCCESS) || (received_message != thread_2_messages_received))
238            break;
239
240         /* Otherwise, all is okay. Increment the received message count. */
241         thread_2_messages_received++;
242      }
243 }
244
245
246 void     thread_3_and_4_entry(ULONG thread_input)
247 {
248
249 UINT     status;
250
251
252     /* This function is executed from thread 3 and thread 4. As the loop
253        below shows, these function compete for ownership of semaphore_0. */
254     while(1)
255     {
256
257         /* Increment the thread counter. */
258         if (thread_input == 3)
259            thread_3_counter++;
260         else
261            thread_4_counter++;
262
263         /* Get the semaphore with suspension. */
264         status = tx_semaphore_get(&semaphore_0, TX_WAIT_FOREVER);
265
266         /* Check status. */
267         if (status != TX_SUCCESS)
268            break;
269
270         /* Sleep for 2 ticks to hold the semaphore. */
271         tx_thread_sleep(2);
272
273         /* Release the semaphore. */
274         status = tx_semaphore_put(&semaphore_0);
275
276         /* Check status. */
277         if (status != TX_SUCCESS)
278             break;
279     }
280 }
281
282
283 void     thread_5_entry(ULONG thread_input)
284 {
285
286 UINT     status;
287 ULONG    actual_flags;
288
289
290     /* This thread simply waits for an event in a forever loop. */
291     while(1)
292     {
293
294         /* Increment the thread counter. */
295         thread_5_counter++;
296
297         /* Wait for event flag 0. */
298         status = tx_event_flags_get(&event_flags_0, 0x1, TX_OR_CLEAR,
299                                &actual_flags, TX_WAIT_FOREVER);
300
301         /* Check status. */
302         if ((status != TX_SUCCESS) || (actual_flags != 0x1))
303            break;
304     }
305 }
306
307 void     thread_6_and_7_entry(ULONG thread_input)
308 {
309
310 UINT     status;
311
312
313     /* This function is executed from thread 6 and thread 7. As the loop
314         below shows, these function compete for ownership of mutex_0. */
315     while(1)
316     {
317
318         /* Increment the thread counter. */
319         if (thread_input == 6)
320            thread_6_counter++;
321         else
322            thread_7_counter++;
323
324         /* Get the mutex with suspension. */
325         status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);
326
327         /* Check status. */
328         if (status != TX_SUCCESS)
329            break;
330
331         /* Get the mutex again with suspension. This shows
332            that an owning thread may retrieve the mutex it
333            owns multiple times. */
334         status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);
335
336         /* Check status. */
337         if (status != TX_SUCCESS)
338             break;
339
340         /* Sleep for 2 ticks to hold the mutex. */
341         tx_thread_sleep(2);
342
343         /* Release the mutex. */
344         status = tx_mutex_put(&mutex_0);
345
346         /* Check status. */
347         if (status != TX_SUCCESS)
348            break;
349
350         /* Release the mutex again. This will actually
351            release ownership since it was obtained twice. */
352         status = tx_mutex_put(&mutex_0);
353
354         /* Check status. */
355         if (status != TX_SUCCESS)
356            break;
357     }
358 }
```