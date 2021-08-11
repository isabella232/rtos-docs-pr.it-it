---
title: Capitolo 6 - Azure RTOS API LevelX NOR
description: Le Azure RTOS LEVELX NOR disponibili per l'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2e109f5916a9e903aa3341f2855ade085e9d9a22b80ec7cb2e0c310e43ff3eac
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790242"
---
# <a name="chapter-6---azure-rtos-levelx-nor-apis"></a>Capitolo 6 - Azure RTOS API LevelX NOR

Le Azure RTOS'API LevelX NOR disponibili per l'applicazione sono le seguenti.

- ***lx_nor_flash_close** _: _Close'istanza flash NOR*
- ***lx_nor_flash_defragment** _: _Defragment'istanza flash NOR*
- ***lx_nor_flash_extended_cache_enable** _: _Enable/disabilitare la cache NOR estesa*
- ***lx_nor_flash_initialize** _: _Initialize supporto flash NOR*
- ***lx_nor_flash_open** _: _Open'istanza flash NOR*
- ***lx_nor_flash_partial_defragment** _: _Partial deframmentazione dell'istanza flash NOR*
- ***lx_nor_flash_sector_read** _: _Read SETTORE FLASH NOR*
- ***lx_nor_flash_sector_release** _: _Release SETTORE FLASH NOR*
- ***lx_nor_flash_sector_write** _: _Write SETTORE FLASH NOR*

## <a name="lx_nor_flash_close"></a>lx_nor_flash_close

Chiudere l'istanza flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_close(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a>Descrizione

Questo servizio chiude l'istanza flash NOR aperta in precedenza.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash:* puntatore dell'istanza flash NOR.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la chiusura dell'istanza flash.

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

Deframmentare l'istanza flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_defragment(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a>Descrizione

Questo servizio deframmenta l'istanza flash NOR aperta in precedenza. Il processo di deframmentazione ottimizza il numero di settori e blocchi liberi.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash:* puntatore dell'istanza flash NOR.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la deframmentazione dell'istanza flash.

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

Abilitare/disabilitare la cache NOR estesa

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_extended_cache_enable(
    LX_NOR_FLASH *nor_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a>Descrizione

Questo servizio implementa un livello di cache del settore NOR nella RAM usando la memoria fornita dall'applicazione. Ogni 512 byte di memoria forniti si traduce in un settore NOR che può essere memorizzato nella cache. I settori memorizzati nella cache sono quelli che contengono le informazioni sul controllo dei blocchi, ad esempio il conteggio delle cancellazioni, la mappa dei settori liberi e le informazioni sul mapping dei settori. I settori di dati non vengono archiviati in questa cache.

### <a name="input-parameters"></a>Parametri di input

- **nor_flash:** puntatore dell'istanza flash NOR.  
- **memory:** indirizzo iniziale per la memoria cache, allineato per l'accesso ULONG. Il valore LX_NULL disabilita la cache.  
- **size:** dimensione in byte della memoria fornita (deve essere multiplo di 512 byte).

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR**: (0x01) Memoria insufficiente per un settore NOR.
- **LX_DISABLED:**(0x09) CACHE estesa NOR disabilitata dall'opzione di configurazione .

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

Inizializzare il supporto flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_initialize(void);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza il supporto flash LevelX NOR. Deve essere chiamato prima di qualsiasi altra API LevelX NOR.

### <a name="input-parameters"></a>Parametri di input

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante l'inizializzazione del supporto flash NOR.

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

Aprire l'istanza flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_open(
    LX_NOR_FLASH *nor_flash, 
    CHAR *name,  
    UINT (*nor_driver_initialize) (LX_NOR_FLASH *));
```

### <a name="description"></a>Descrizione

Questo servizio apre un'istanza flash NOR con il blocco di controllo flash NOR specificato e la funzione di inizializzazione del driver. Si noti che la funzione di inizializzazione del driver è responsabile dell'installazione di vari puntatori a funzione per la lettura, la scrittura e la cancellazione di blocchi dell'hardware NOR associato a questa istanza flash NOR.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash:* puntatore dell'istanza flash NOR.
- *name:* nome dell'istanza flash NOR.
- *nor_driver_initialize:* puntatore a funzione alla funzione di inizializzazione del driver flash NOR. Per altre informazioni sulle responsabilità dei driver FLASH NOR, vedere il capitolo 5 di questa guida.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante l'apertura dell'istanza flash NOR.
- **LX_NO_MEMORY:** il driver (0x08) non ha fornito buffer per la lettura di nessun settore nella RAM.

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

Deframmentazione parziale dell'istanza flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_partial_defragment(
    LX_NOR_FLASH *nor_flash, 
    UINT max_blocks);
```

### <a name="description"></a>Descrizione

Questo servizio deframmenta l'istanza flash NOR aperta in precedenza fino al numero massimo di blocchi specificato. Il processo di deframmentazione ottimizza il numero di settori e blocchi liberi.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash:* puntatore dell'istanza flash NOR.
- *max_blocks:* numero massimo di blocchi.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la deframmentazione dell'istanza flash.

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

Read NOR flash sector

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_sector_read(
    LX_NOR_FLASH *nor_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio legge il settore logico dall'istanza flash NOR e, in caso di esito positivo, restituisce il contenuto nel buffer fornito. Si noti che le dimensioni del settore NOR sono sempre di 512 byte.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash* Puntatore dell'istanza flash NOR.
- *logical_sector:* settore logico da leggere.
- *buffer:* puntatore alla destinazione per il contenuto del settore logico. Si noti che si presuppone che il buffer sia di 512 byte e allineato per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la lettura del settore FLASH NOR.

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

Rilasciare il settore flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_sector_release(
    LX_NOR_FLASH *nor_flash,
    ULONG logical_sector);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia il mapping del settore logico nell'istanza flash NOR. Il rilascio di un settore logico quando non viene usato rende più efficiente il livellamento dell'usura LevelX.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash:* puntatore dell'istanza flash NOR.
- *logical_sector:* settore logico da rilasciare.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore O scrittura settore flash.

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

Scrivere il settore flash NOR

### <a name="prototype"></a>Prototipo

```c
UINT lx_nor_flash_sector_write(
    LX_nor_FLASH *NOR_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio scrive il settore logico specificato nell'istanza flash NOR.

### <a name="input-parameters"></a>Parametri di input

- *nor_flash*: puntatore dell'istanza flash NOR.
- *logical_sector:* settore logico da scrivere.
- *buffer*: puntatore al contenuto del settore logico. Si noti che si presuppone che il buffer sia allineato a 512 byte per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:**(0x00) Richiesta riuscita.
- **LX_NO_SECTORS**: (0x02) Non sono disponibili altri settori gratuiti per eseguire la scrittura.
- **LX_ERROR:**(0x01) Errore durante il rilascio del settore FLASH NOR.

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
