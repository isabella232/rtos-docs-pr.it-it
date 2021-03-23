---
title: Capitolo 6-Azure RTO LevelX o API
description: LevelX o API RTO di Azure disponibili per l'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3ab7d3a7e431d7c8f49ef4f5cab9216dc77c8d33
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822955"
---
# <a name="chapter-6---azure-rtos-levelx-nor-apis"></a>Capitolo 6-Azure RTO LevelX o API

Le funzioni API o LevelX di Azure RTO non sono disponibili per l'applicazione, come indicato di seguito.

- ***lx_nor_flash_close** _: _Close o l'istanza Flash *
- ***lx_nor_flash_defragment** _: _Defragment o l'istanza Flash *
- ***lx_nor_flash_extended_cache_enable** _: _Enable/Disable esteso o cache *
- ***lx_nor_flash_initialize** _: _Initialize o supporto Flash *
- ***lx_nor_flash_open** _: _Open o l'istanza Flash *
- ***lx_nor_flash_partial_defragment** _: _Partial deframmentazione di o di un'istanza Flash *
- ***lx_nor_flash_sector_read** _: _Read o settore Flash *
- ***lx_nor_flash_sector_release** _: _Release o settore Flash *
- ***lx_nor_flash_sector_write** _: _Write o settore Flash *

## <a name="lx_nor_flash_close"></a>lx_nor_flash_close

Istanza Close o Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_close(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a>Descrizione

Questo servizio chiude l'istanza precedentemente aperta o Flash.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: né puntatore all'istanza Flash.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la chiusura dell'istanza Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Close NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_close(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_defragment"></a>lx_nor_flash_defragment

Deframmenta o istanza Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_defragment(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a>Descrizione

Questo servizio Deframmenta l'istanza precedentemente aperta o Flash. Il processo di deframmentazione ottimizza il numero di settori e blocchi liberi.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: né puntatore all'istanza Flash.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Defragment NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_defragment(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_extended_cache_enable"></a>lx_nor_flash_extended_cache_enable

Abilita/Disabilita esteso o cache

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_extended_cache_enable(
    LX_NOR_FLASH *nor_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a>Descrizione

Questo servizio implementa un livello di cache del settore o nella RAM usando la memoria fornita dall'applicazione. Ogni 512 byte di memoria fornita si traduce in uno o più settori che possono essere memorizzati nella cache. I settori memorizzati nella cache sono quelli che contengono le informazioni sul controllo del blocco, ad esempio il conteggio delle cancellazioni, la mappa del settore gratuito e le informazioni sul mapping del settore. I settori dati non vengono archiviati in questa cache.

### <a name="input-parameters"></a>Parametri di input

- **nor_flash**: né puntatore all'istanza Flash.  
- **Memory**: indirizzo iniziale per la memoria cache, allineato per l'accesso ULONG. Il valore LX_NULL Disabilita la cache.  
- **size**: dimensione in byte della memoria fornita (deve essere un multiplo di 512 byte).

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) memoria insufficiente per uno o più settori.
- **LX_DISABLED**: (0x09) o la cache estesa disabilitata dall'opzione di configurazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Enable the NOR flash cache for the instance "my_nor_flash". */  
status = lx_nor_flash_extended_cache_enable(&my_nor_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_initialize"></a>lx_nor_flash_initialize

Inizializzazione o supporto Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_initialize(void);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza LevelX o il supporto Flash. Deve essere chiamato prima di qualsiasi altro LevelX o API.

### <a name="input-parameters"></a>Parametri di input

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante l'INIZIALIZZAzione o il supporto Flash.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Initialize NOR flash support. */  
status = lx_nor_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_partial_defragment
- lx_nor_flash_open
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_open"></a>lx_nor_flash_open

Apri o istanza Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_open(
    LX_NOR_FLASH *nor_flash, 
    CHAR *name,  
    UINT (*nor_driver_initialize) (LX_NOR_FLASH *));
```

### <a name="description"></a>Descrizione

Questo servizio apre un'istanza di o Flash con la funzione di inizializzazione del driver e del blocco di controllo flash specificata. Si noti che la funzione di inizializzazione del driver è responsabile dell'installazione di diversi puntatori a funzione per la lettura, la scrittura e la cancellazione dei blocchi dell'hardware o dell'hardware associato a questa istanza di o Flash.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: né puntatore all'istanza Flash.
- *nome*: nome dell'istanza di o Flash.
- *nor_driver_initialize*: puntatore a funzione o funzione di inizializzazione del driver Flash. Vedere il capitolo 5 di questa guida per altre informazioni sulle responsabilità dei driver di o Flash.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante l'apertura o l'istanza Flash.
- **LX_NO_MEMORY**: il driver (0x08) non ha fornito il buffer per la lettura di nessun settore nella RAM.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Open NOR flash instance "my_nor_flash" with the driver "my_nor_driver_initialize". */  
status = lx_nor_flash_open(&my_nor_flash,"my NOR flash",  
    my_nor_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_partial_defragment"></a>lx_nor_flash_partial_defragment

Deframmentazione parziale dell'istanza di o di Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_partial_defragment(
    LX_NOR_FLASH *nor_flash, 
    UINT max_blocks);
```

### <a name="description"></a>Descrizione

Questo servizio Deframmenta l'istanza precedentemente aperta o flash fino al numero massimo di blocchi specificato. Il processo di deframmentazione ottimizza il numero di settori e blocchi liberi.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: né puntatore all'istanza Flash.
- *max_blocks*: numero massimo di blocchi.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Defragment of one block in NOR flash instance* *"my_nor_flash". */  
status = lx_nor_flash_partial_defragment(&my_nor_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_sector_read"></a>lx_nor_flash_sector_read

Lettura e settore Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_sector_read(
    LX_NOR_FLASH *nor_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio legge il settore logico dall'istanza di o Flash e, se ha esito positivo, restituisce il contenuto nel buffer fornito. Si noti che la dimensione del settore è sempre di 512 byte.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash* O puntatore all'istanza Flash.
- *logical_sector*: settore logico da leggere.
- *buffer*: puntatore alla destinazione per il contenuto del settore logico. Si presuppone che il buffer sia 512 byte e che sia allineato per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la lettura o il settore Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Read logical sector 20 of the NOR flash instance "my_nor_flash" and place contents in "buffer". */ 
status = lx_nor_flash_sector_read(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contents of logical sector 20. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_sector_release"></a>lx_nor_flash_sector_release

Versione o settore Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_sector_release(
    LX_NOR_FLASH *nor_flash,
    ULONG logical_sector);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia il mapping del settore logico nell'istanza di o di Flash. Il rilascio di un settore logico quando non viene usato rende più efficiente il livellamento del LevelX.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: né puntatore all'istanza Flash.
- *logical_sector*: settore logico da rilasciare.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore o scrittura nel settore Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Release logical sector 20 of the NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_sector_release(&my_nor_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_sector_write"></a>lx_nor_flash_sector_write

Settore della scrittura e del flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_sector_write(
    LX_nor_FLASH *NOR_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio scrive il settore logico specificato nell'istanza di o Flash.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: né puntatore all'istanza Flash.
- *logical_sector*: settore logico da scrivere.
- *buffer*: puntatore al contenuto del settore logico. Si presuppone che il buffer sia allineato a 512 byte per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_NO_SECTORS**: (0x02) non sono più disponibili settori gratuiti per eseguire la scrittura.
- **LX_ERROR**: (0x01) errore durante il rilascio o il settore Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Write logical sector 20 of the NOR flash instance "my_nor_flash" with the contents pointed to by "buffer". */ 
status = lx_nor_flash_sector_write(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a>Vedere anche

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
