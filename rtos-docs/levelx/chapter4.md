---
title: Capitolo 4 - Azure RTOS API NAND LevelX
description: L Azure RTOS API NAND LevelX disponibili per l'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d92b6c10921b4d04345610e139101e93c7a439ff695a89a79245894ad9ef1fec
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790282"
---
# <a name="chapter-4---azure-rtos-levelx-nand-apis"></a>Capitolo 4 - Azure RTOS API NAND LevelX

Le AZURE RTOS NAND LevelX disponibili per l'applicazione sono:

- ***lx_nand_flash_close** _: _Close'istanza flash NAND*
- ***lx_nand_flash_defragment** _: _Defragment'istanza flash NAND*
- ***lx_nand_flash_extended_cache_enable** _: _Enable/disabilitare la cache NAND estesa*
- ***lx_nand_flash_initialize** _: supporto _Initialize flash NAND*
- ***lx_nand_flash_open** _: _Open'istanza flash NAND*
- ***lx_nand_flash_page_ecc_check** _: pagina _Check errori ECC con correzione*
- ***lx_nand_flash_page_ecc_compute** _: _Computes ECC per page*
- ***lx_nand_flash_partial_defragment** _: _Partial deframmentazione dell'istanza flash NAND*
- ***lx_nand_flash_sector_read** _: _Read flash NAND*
- ***lx_nand_flash_sector_release** _: _Release flash NAND*
- ***lx_nand_flash_sector_write** _: _Write flash NAND*

## <a name="lx_nand_flash_close"></a>lx_nand_flash_close

Chiudere l'istanza flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_close(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a>Descrizione

Questo servizio chiude l'istanza flash NAND aperta in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la chiusura dell'istanza flash.

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

Deframmentare l'istanza flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_defragment(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a>Descrizione

Questo servizio deframmenta l'istanza flash NAND aperta in precedenza. Il processo di deframmentazione ottimizza il numero di pagine e blocchi disponibili.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la deframmentazione dell'istanza flash.

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

Abilitare/disabilitare la cache NAND estesa

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_extended_cache_enable(
    LX_NAND_FLASH
    *nand_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a>Descrizione

Questo servizio implementa un livello di cache nella RAM usando la memoria fornita dall'applicazione. La quantità totale di memoria necessaria per l'operazione di cache completa può essere calcolata nel modo seguente:

```c
size (in_bytes) = number_of_blocks (rounded up to be divisible by 4) +  
    ((number_of_blocks * pages_per_block) * 4)  +  
    ((number_of_blocks * (pages_per_block + 1)) * 4)
```

Se la memoria fornita non è sufficientemente grande da contenere la cache NAND completa, questa routine abiliterà la maggior parte possibile della cache flash NAND in base alla memoria fornita.

La cache NAND è disabilitata se l'indirizzo di memoria specificato è NULL. Di conseguenza, la cache NAND può essere usata in modo temporaneo.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.  
- **memory**: indirizzo iniziale per la memoria della cache allineato per l'accesso ULONG. Il valore LX_NULL disabilita la cache.  
- **size**: dimensione in byte della memoria fornita.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR**: (0x01) Memoria insufficiente per un elemento della cache NAND.

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

Inizializzare il supporto flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_initialize(void);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza il supporto flash NAND LevelX. Deve essere chiamato prima di qualsiasi altra API NAND LevelX.

### <a name="input-parameters"></a>Parametri di input

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR**: (0x01) Errore durante l'inizializzazione del supporto flash NAND.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

Aprire l'istanza flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_open(
    LX_NAND_FLASH *nand_flash, 
    CHAR *name,  
    UINT (*nand_driver_initialize) (LX_NAND_FLASH *));
```

### <a name="description"></a>Descrizione

Questo servizio apre un'istanza flash NAND con il blocco di controllo flash NAND e la funzione di inizializzazione del driver specificati. Si noti che la funzione di inizializzazione del driver è responsabile dell'installazione di vari puntatori a funzione per la lettura, la scrittura e la cancellazione di blocchi/pagine dell'hardware NAND associato a questa istanza flash NAND.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **name**: nome dell'istanza flash NAND.
- **nand_driver_initialize:** puntatore a funzione alla funzione di inizializzazione del driver flash NAND. Per altri dettagli sulle responsabilità dei driver flash NAND, vedere il capitolo 3 di questa guida.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS**: (0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante l'apertura dell'istanza flash NAND.
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

Controllare la presenza di errori ECC con correzione

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_page_ecc_check(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a>Descrizione

Questo servizio verifica l'integrità del buffer di pagina NAND fornito con ecc fornito. Si presuppone che le dimensioni della pagina (definite nel puntatore dell'istanza flash NAND) siano un multiplo di 256 byte e che il codice ECC fornito sia in grado di correggere un errore di 1 bit in ogni parte della pagina di 256 byte.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **page_buffer:** puntatore al buffer di pagina flash NAND.
- **ecc_buffer:** puntatore a ECC per la pagina flash NAND. Si noti che sono presenti 3 byte ECC per una parte della pagina di 256 byte.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:** la pagina NAND (0x00) non contiene errori.
- **LX_NAND_ERROR_CORRECTED**: (0x06) Uno o più errori a 1 bit sono stati corretti nella pagina NAND. Le correzioni si trovano nel buffer di pagina.
- **LX_NAND_ERROR_NOT_CORRECTED**: (0x07) Troppi errori da correggere nella pagina NAND.

### <a name="allowed-from"></a>Consentito da

LevelX Driver

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

Ecc di calcolo per la pagina

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_page_ecc_compute(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a>Descrizione

Questo servizio calcola il valore ECC del buffer di pagina NAND fornito e restituisce ecc nel buffer ECC fornito. Si presuppone che le dimensioni della pagina siano un multiplo di 256 byte (definito nel puntatore dell'istanza flash NAND). Il codice ECC viene usato per verificare l'integrità della pagina quando viene letta in un secondo momento.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **page_buffer:** puntatore al buffer di pagina flash NAND.
- **ecc_buffer:** puntatore alla destinazione per ECC della pagina flash NAND. Si noti che devono essere 3 byte di spazio di archiviazione ECC per una parte della pagina di 256 byte. Ad esempio, una pagina di 2048 byte richiederebbe 24 byte per ECC.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:**(0x00) ECC calcolato correttamente.
- **LX_ERROR:**(0x01) Errore durante il calcolo di ECC.

### <a name="allowed-from"></a>Consentito da

LevelX Driver

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

Deframmentazione parziale dell'istanza flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_partial_defragment(
    LX_NAND_FLASH *nand_flash,  
    UINT max_blocks);
```

### <a name="description"></a>Descrizione

Questo servizio deframmenta l'istanza flash NAND aperta in precedenza fino al numero massimo di blocchi specificato. Il processo di deframmentazione ottimizza il numero di pagine e blocchi disponibili.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **max_blocks:** numero massimo di blocchi.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:**(0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la deframmentazione dell'istanza flash.

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

Leggere il settore flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_sector_read(
    LX_NAND_FLASH *nand_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio legge il settore logico dall'istanza flash NAND e, in caso di esito positivo, restituisce il contenuto nel buffer fornito. Si noti che le dimensioni del settore NAND sono sempre le dimensioni della pagina dell'hardware NAND sottostante.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **logical_sector:** settore logico da leggere.
- **buffer**: puntatore alla destinazione per il contenuto del settore logico. Si noti che si presuppone che il buffer sia la dimensione delle dimensioni della pagina flash NAND e allineato per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:**(0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore durante la lettura del settore flash NAND.

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

Rilasciare il settore flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_sector_release(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia il mapping del settore logico nell'istanza flash NAND. Il rilascio di un settore logico quando non viene usato rende più efficiente il livellamento dell'usura LevelX.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **logical_sector:** settore logico da rilasciare.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:**(0x00) Richiesta riuscita.
- **LX_ERROR:**(0x01) Errore di scrittura del settore flash NAND.

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

Scrivere il settore flash NAND

### <a name="prototype"></a>Prototipo

```c
UINT lx_nand_flash_sector_write(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio scrive il settore logico specificato nell'istanza flash NAND.

### <a name="input-parameters"></a>Parametri di input

- **nand_flash:** puntatore di istanza flash NAND.
- **logical_sector:** settore logico da scrivere.
- **buffer**: puntatore al contenuto del settore logico. Si noti che si presuppone che il buffer sia la dimensione delle dimensioni della pagina flash NAND e allineato per l'accesso ULONG.

### <a name="return-values"></a>Valori restituiti

- **LX_SUCCESS:**(0x00) Richiesta riuscita.
- **LX_NO_SECTORS**: (0x02) Non sono disponibili altri settori liberi per eseguire la scrittura.
- **LX_ERROR:**(0x01) Errore durante il rilascio del settore flash NAD.

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
