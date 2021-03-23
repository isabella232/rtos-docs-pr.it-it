---
title: Capitolo 4-API NAND LevelX di Azure RTO
description: API di Azure RTO LevelX NAND disponibili per l'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 73bb94768396b4b8461791a164a102d1f8ef159f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822967"
---
# <a name="chapter-4---azure-rtos-levelx-nand-apis"></a>Capitolo 4-API NAND LevelX di Azure RTO

Le API di Azure RTO LevelX NAND disponibili per l'applicazione sono:

- ***lx_nand_flash_close** _: _Close istanza Flash NAND *
- ***lx_nand_flash_defragment** _: _Defragment istanza Flash NAND *
- ***lx_nand_flash_extended_cache_enable** _: _Enable/Disable della cache NAND estesa *
- ***lx_nand_flash_initialize** _: _Initialize supporto Flash NAND *
- ***lx_nand_flash_open** _: _Open istanza Flash NAND *
- ***lx_nand_flash_page_ecc_check** _: _Check pagina per gli errori ecc con correzione *
- ***lx_nand_flash_page_ecc_compute** _: _Computes ecc per la pagina *
- ***lx_nand_flash_partial_defragment** _: _Partial deframmentazione dell'istanza Flash NAND *
- ***lx_nand_flash_sector_read** _: _Read settore Flash NAND *
- ***lx_nand_flash_sector_release** _: _Release settore Flash NAND *
- ***lx_nand_flash_sector_write** _: _Write settore Flash NAND *

## <a name="lx_nand_flash_close"></a>lx_nand_flash_close

Chiudi istanza Flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_close(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a>Descrizione

Questo servizio chiude l'istanza Flash NAND precedentemente aperta.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la chiusura dell'istanza Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Close NAND flash instance "my_nand_flash". */
status = lx_nand_flash_close(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_defragment"></a>lx_nand_flash_defragment

Deframmenta istanza Flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_defragment(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a>Descrizione

Questo servizio Deframmenta l'istanza Flash NAND precedentemente aperta. Il processo di deframmentazione ottimizza il numero di pagine e blocchi liberi.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Defragment NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_defragment(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_extended_cache_enable"></a>lx_nand_flash_extended_cache_enable

Abilita/Disabilita cache NAND estesa

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_extended_cache_enable(
    LX_NAND_FLASH
    *nand_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a>Descrizione

Questo servizio implementa un livello di cache nella RAM usando la memoria fornita dall'applicazione. La quantità totale di memoria necessaria per l'operazione Full cache può essere calcolata nel modo seguente:

```c
size (in_bytes) = number_of_blocks (rounded up to be divisible by 4) +  
    ((number_of_blocks * pages_per_block) * 4)  +  
    ((number_of_blocks * (pages_per_block + 1)) * 4)
```

Se la memoria fornita non è sufficientemente grande da contenere la cache NAND completa, questa routine consentirà la maggior parte della cache del flash NAND in base alla memoria fornita.

La cache NAND è disabilitata se l'indirizzo di memoria specificato è NULL. La cache NAND potrebbe quindi essere utilizzata in modo temporaneo.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.  
- **Memory**: indirizzo iniziale per la memoria cache allineata per l'accesso ULONG. Il valore LX_NULL Disabilita la cache.  
- **size**: dimensione in byte della memoria fornita.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) memoria insufficiente per un elemento della cache NAND.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Enable the NAND flash cache for the instance "my_nand_flash". */
status = lx_nand_flash_extended_cache_enable(&my_nand_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_initialize"></a>lx_nand_flash_initialize

Inizializza supporto Flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_initialize(void);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza il supporto Flash NAND LevelX. Deve essere chiamato prima di qualsiasi altra API LevelX NAND.

### <a name="input-parameters"></a>Parametri di input

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante l'inizializzazione del supporto Flash NAND.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Initialize NAND flash support. */
status = lx_nand_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_open"></a>lx_nand_flash_open

Apri istanza Flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_open(
    LX_NAND_FLASH *nand_flash, 
    CHAR *name,  
    UINT (*nand_driver_initialize) (LX_NAND_FLASH *));
```

### <a name="description"></a>Descrizione

Questo servizio apre un'istanza di Flash NAND con il blocco di controllo flash NAND specificato e la funzione di inizializzazione del driver. Si noti che la funzione di inizializzazione del driver è responsabile dell'installazione di diversi puntatori a funzione per la lettura, la scrittura e la cancellazione di blocchi/pagine dell'hardware NAND associato a questa istanza di Flash NAND.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **nome**: nome dell'istanza di Flash NAND.
- **nand_driver_initialize**: puntatore a funzione per la funzione di inizializzazione del driver Flash NAND. Per ulteriori informazioni sulle responsabilità dei driver Flash NAND, vedere il capitolo 3 di questa guida.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante l'apertura dell'istanza NAND Flash.
- **LX_NO_MEMORY**: il driver (0x08) non ha fornito il buffer per la lettura di una pagina nella RAM.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Open NAND flash instance "my_nand_flash" with the driver "my_nand_driver_initialize". */ 
status = lx_nand_flash_open(&my_nand_flash,"my nand flash",  
    my_nand_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_page_ecc_check"></a>lx_nand_flash_page_ecc_check

Pagina di controllo degli errori ECC con correzione

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_page_ecc_check(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a>Descrizione

Questo servizio verifica l'integrità del buffer di pagine NAND fornito con l'ECC fornito. Si presuppone che le dimensioni della pagina (definite nel puntatore dell'istanza Flash NAND) siano un multiplo di 256 byte e che il codice ECC fornito sia in grado di correggere un errore a 1 bit in ogni porzione di 256 byte della pagina.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **page_buffer**: puntatore al buffer della pagina Flash NAND.
- **ecc_buffer**: puntatore ad ecc per la pagina Flash NAND. Si noti che ci sono 3 byte ECC per parte della pagina a 256 byte.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la pagina NAND non contiene errori.
- **LX_NAND_ERROR_CORRECTED**: (0x06) uno o più errori a 1 bit sono stati corretti nella pagina NAND: le correzioni si trovano nel buffer di pagina.
- **LX_NAND_ERROR_NOT_CORRECTED**: (0x07) troppi errori da correggere nella pagina NAND.

### <a name="allowed-from"></a>Consentito da

Driver LevelX

### <a name="example"></a>Esempio

```c
/* Check the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash" . */
status = lx_nand_flash_page_ecc_check(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the page is valid. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_page_ecc_compute"></a>lx_nand_flash_page_ecc_compute

Calcolo ECC per la pagina

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_page_ecc_compute(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a>Descrizione

Questo servizio calcola l'ECC del buffer di pagine NAND fornito e restituisce il ECC nel buffer di ECC fornito. Si presuppone che le dimensioni della pagina siano un multiplo di 256 byte (definito nel puntatore dell'istanza Flash NAND). Il codice ECC viene usato per verificare l'integrità della pagina quando viene letta in un secondo momento.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **page_buffer**: puntatore al buffer della pagina Flash NAND.
- **ecc_buffer**: puntatore alla destinazione per ecc della pagina Flash NAND. Si noti che deve essere di 3 byte di spazio di archiviazione ECC per parte della pagina a 256 byte. Ad esempio, una pagina di 2048 byte richiede 24 byte per l'ECC.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) ecc calcolato correttamente.
- **LX_ERROR**: (0x01) errore durante il calcolo ecc.

### <a name="allowed-from"></a>Consentito da

Driver LevelX

### <a name="example"></a>Esempio

```c
/* Compute ECC for the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_page_ecc_compute(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the ECC was calculated and Can be found in the memory pointed to by "ecc_pointer." */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_partial_defragment"></a>lx_nand_flash_partial_defragment

Deframmentazione parziale dell'istanza di Flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_partial_defragment(
    LX_NAND_FLASH *nand_flash,  
    UINT max_blocks);
```

### <a name="description"></a>Descrizione

Questo servizio Deframmenta l'istanza Flash NAND precedentemente aperta fino al numero massimo di blocchi specificato. Il processo di deframmentazione ottimizza il numero di pagine e blocchi liberi.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **max_blocks**: numero massimo di blocchi.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Defragment 1 block of NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_partial_defragment(&my_nand_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_sector_read"></a>lx_nand_flash_sector_read

Leggi il settore NAND Flash

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_sector_read(
    LX_NAND_FLASH *nand_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio legge il settore logico dall'istanza Flash NAND e, in caso di esito positivo, restituisce il contenuto del buffer fornito. Si noti che le dimensioni del settore NAND sono sempre le dimensioni di pagina dell'hardware NAND sottostante.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **logical_sector**: settore logico da leggere.
- **buffer**: puntatore alla destinazione per il contenuto del settore logico. Si presuppone che il buffer corrisponda alle dimensioni della pagina Flash NAND e allineato per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la lettura del settore NAND Flash.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Read logical sector 20 of the NAND flash instance "my_nand_flash" and place contents in "buffer". */
status = lx_nand_flash_sector_read(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contentsnof logical sector 20. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_sector_release"></a>lx_nand_flash_sector_release

Settore Flash NAND versione

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_sector_release(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia il mapping del settore logico nell'istanza del flash NAND. Il rilascio di un settore logico quando non viene usato rende più efficiente il livellamento del LevelX.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **logical_sector**: settore logico da rilasciare.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_ERROR**: (0x01) errore durante la scrittura del settore Flash NAND.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Release logical sector 20 of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_sector_release(&my_nand_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_sector_write"></a>lx_nand_flash_sector_write

Scrivi settore Flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_sector_write(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio scrive il settore logico specificato nell'istanza di Flash NAND.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash**: puntatore all'istanza Flash NAND.
- **logical_sector**: settore logico da scrivere.
- **buffer**: puntatore al contenuto del settore logico. Si presuppone che il buffer corrisponda alle dimensioni della pagina Flash NAND e allineato per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) la richiesta è riuscita.
- **LX_NO_SECTORS**: (0x02) non sono più disponibili settori gratuiti per eseguire la scrittura.
- **LX_ERROR**: (0x01) errore durante il rilascio del settore Flash NAND.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Write logical sector 20 of the NAND flash instance "my_nand_flash" with the contents pointed to by "buffer". */  
status = lx_nand_flash_sector_write(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a>Vedere anche

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
