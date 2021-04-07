---
title: Capitolo 5-driver I/O per Azure RTO FileX
description: Questo capitolo contiene una descrizione dei driver I/O per Azure RTO FileX ed è progettato per consentire agli sviluppatori di scrivere driver specifici dell'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f2ef697f68a269b24a34147a4bc076b8a2b1660
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550083"
---
# <a name="chapter-5---io-drivers-for-azure-rtos-filex"></a>Capitolo 5-driver I/O per Azure RTO FileX

Questo capitolo contiene una descrizione dei driver I/O per Azure RTO FileX ed è progettato per consentire agli sviluppatori di scrivere driver specifici dell'applicazione.

## <a name="io-driver-introduction"></a>Introduzione al driver I/O

FileX supporta più dispositivi multimediali. La struttura FX_MEDIA definisce tutti gli elementi necessari per la gestione di un dispositivo multimediale. Questa struttura contiene tutte le informazioni multimediali, inclusi i driver i/O specifici del supporto e i parametri associati per il passaggio di informazioni e stato tra il driver e FileX. Nella maggior parte dei sistemi è presente un driver di I/O univoco per ogni istanza del supporto FileX.

## <a name="io-driver-entry"></a>Voce driver I/O

Ogni driver di I/O FileX dispone di una singola funzione entry definita dalla chiamata al servizio ***fx_media_open*** . La funzione entry driver ha il formato seguente:

```c
void my_driver_entry(FX_MEDIA *media_ptr);
```

FileX chiama la funzione entry driver I/O per richiedere l'accesso a tutti i supporti fisici, inclusa l'inizializzazione e la lettura del settore di avvio. Le richieste effettuate al driver vengono eseguite in sequenza; ad esempio, FileX attende il completamento della richiesta corrente prima che venga inviata un'altra richiesta.

## <a name="io-driver-requests"></a>Richieste driver I/O

Poiché ogni driver di I/O ha una singola funzione entry, FileX esegue richieste specifiche tramite il blocco di controllo multimediale. In particolare, il membro  **fx_media_driver_request** di **FX_MEDIA** viene usato per specificare la richiesta di driver esatta. Il driver di I/O comunica l'esito positivo o negativo della richiesta tramite il membro **fx_media_driver_status** di **FX_MEDIA**. Se la richiesta del driver ha avuto esito positivo, **FX_SUCCESS** viene inserita in questo campo prima che il driver venga restituito. In caso contrario, se viene rilevato un errore, FX_IO_ERROR viene inserito in questo campo.

### <a name="driver-initialization"></a>Inizializzazione driver

Sebbene l'effettivo processo di inizializzazione dei driver sia specifico dell'applicazione, in genere è costituito dall'inizializzazione della struttura dei dati e possibilmente da un'inizializzazione preliminare Questa richiesta è la prima eseguita da FileX e viene eseguita dall'interno del servizio fx_media_open.

Se viene rilevata la protezione da scrittura media, il fx_media_driver_write_protect membro del FX_MEDIA deve essere impostato su FX_TRUE.

Per la richiesta di inizializzazione del driver I/O vengono utilizzati i membri FX_MEDIA seguenti:

|Membro FX_MEDIA|Significato|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_INIT|

FileX fornisce un meccanismo per informare il driver dell'applicazione quando i settori non vengono più utilizzati. Questa operazione è particolarmente utile per i gestori di memoria FLASH che devono gestire tutti i settori logici in uso mappati al FLASH.

Se è necessaria una notifica di settori gratuiti, il driver dell'applicazione imposta semplicemente il campo *fx_media_driver_free_sector_update* nella struttura di **FX_MEDIA** associata a **FX_TRUE**. Dopo l'impostazione, FileX esegue una chiamata al driver di I/O **_FX_DRIVER_RELEASE_SECTORS_** che indica quando uno o più settori consecutivi diventano disponibili.

### <a name="boot-sector-read"></a>Lettura settore di avvio

Invece di usare una richiesta di lettura standard, FileX esegue una richiesta specifica per leggere il settore di avvio del supporto. Per la richiesta di lettura del settore di avvio del driver I/O vengono utilizzati i membri **FX_MEDIA** seguenti:

|Membro FX_MEDIA|Significato|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_BOOT_READ|
|fx_media_driver_buffer| Indirizzo della destinazione per il settore di avvio.|

### <a name="boot-sector-write"></a>Scrittura settore di avvio

Invece di usare una richiesta di scrittura standard, FileX esegue una richiesta specifica per scrivere il settore di avvio del supporto. Per la richiesta di scrittura del settore di avvio del driver I/O vengono utilizzati i membri **FX_MEDIA** seguenti:

|Membro FX_MEDIA|Significato|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_BOOT_WRITE|
|fx_media_driver_buffer| Indirizzo dell'origine per il settore di avvio.|

### <a name="sector-read"></a>Lettura settore

FileX legge uno o più settori nella memoria emettendo una richiesta di lettura al driver di I/O. Per la richiesta di lettura del driver di I/O vengono usati i membri **FX_MEDIA** seguenti:

|Membro FX_MEDIA|Significato|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_READ|
|fx_media_driver_logical_sector|Settore logico da leggere|
|fx_media_driver_sectors|Numero di settori da leggere|
|fx_media_driver_buffer|Buffer di destinazione per i settori letti|
|fx_media_driver_data_sector_read|Impostare su FX_TRUE se viene richiesto un settore di dati di file. In caso contrario, FX_FALSE se viene richiesto un settore di sistema (FAT o directory).|
|fx_media_driver_sector_type|Definisce il tipo esplicito di settore richiesto, come indicato di seguito:<br />FX_FAT_SECTOR (2)<br />FX_DIRECTORY_SECTOR (3)<br />FX_DATA_SECTOR (4)|

### <a name="sector-write"></a>Scrittura settore

FileX scrive uno o più settori nel supporto fisico inviando una richiesta di scrittura al driver di I/O. Per la richiesta di scrittura del driver i/O vengono utilizzati i membri FX_MEDIA seguenti:

|Membro FX_MEDIA| Significato|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_WRITE|
|fx_media_driver_logical_sector|Settore logico da scrivere|
|fx_media_driver_sectors|Numero di settori da scrivere|
|fx_media_driver_buffer|Buffer di origine per i settori da scrivere|
|fx_media_driver_system_write| Impostare su FX_TRUE se viene richiesto un settore di sistema (FAT o settore di directory). In caso contrario, FX_FALSE se viene richiesto un settore di dati di file.|
|fx_media_driver_sector_type|Definisce il tipo esplicito di settore richiesto, come indicato di seguito:<br> <br>FX_FAT_SECTOR (2) <br> FX_DIRECTORY_SECTOR (3) <br>FX_DATA_SECTOR (4).|

### <a name="driver-flush"></a>Scaricamento driver

FileX Scarica tutti i settori attualmente presenti nella cache del settore del driver nel supporto fisico inviando una richiesta di scaricamento al driver di I/O. Naturalmente, se il driver non è la memorizzazione nella cache dei settori, questa richiesta non richiede l'elaborazione del driver. Per la richiesta di scaricamento del driver I/O vengono utilizzati i membri FX_MEDIA seguenti:

|Membro FX_MEDIA| Significato|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_FLUSH|

### <a name="driver-abort"></a>Interruzione driver

FileX indica al driver di interrompere tutte le altre attività di I/O fisiche con i supporti fisici inviando una richiesta di interruzione al driver di I/O. Il driver non deve eseguire nuovamente le operazioni di I/O fino a quando non viene nuovamente inizializzato. Per la richiesta di interruzione del driver I/O vengono utilizzati i membri FX_MEDIA seguenti:

|Membro FX_MEDIA| Significato|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_ABORT|

### <a name="release-sectors"></a>Settori di rilascio

Se selezionato in precedenza dal driver durante l'inizializzazione, FileX informa il driver ogni volta che uno o più settori consecutivi diventano disponibili. Se il driver è effettivamente una gestione FLASH, queste informazioni possono essere usate per indicare a gestione FLASH che questi settori non sono più necessari. Per la richiesta dei settori di rilascio i/O vengono usati i membri **FX_MEDIA** seguenti:

|Membro FX_MEDIA| Significato|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_RELEASE_SECTORS|
|fx_media_driver_logical_sector|Inizio del settore gratuito|
|fx_media_driver_sectors|Numero di settori disponibili|

### <a name="driver-suspension"></a>Sospensione driver

Poiché l'I/O con supporti fisici potrebbe richiedere del tempo, è spesso consigliabile sospendere il thread chiamante. Naturalmente, ciò presuppone che il completamento dell'operazione di I/O sottostante sia basato sull'interrupt. In tal caso, la sospensione dei thread viene facilmente implementata con un semaforo ThreadX. Dopo l'avvio dell'operazione di input o di output, il driver di I/O viene sospeso sul proprio semaforo di I/O interno, creato con un conteggio iniziale pari a zero durante l'inizializzazione del driver. Come parte dell'elaborazione dell'interrupt di completamento i/O del driver, viene impostato lo stesso semaforo di I/O, che a sua volta riattiva il thread sospeso.

### <a name="sector-translation"></a>Conversione settore

Poiché FileX Visualizza i supporti come settori logici lineari, le richieste di I/O effettuate al driver di I/O vengono eseguite con i settori logici. Il conducente è responsabile della conversione tra i settori logici e la geometria fisica del supporto, che può includere testine, tracce e settori fisici. Per i supporti disco FLASH e RAM, i settori logici in genere mappano la directory ai settori fisici. In ogni caso, di seguito sono riportate le formule tipiche per eseguire il mapping logico a settore fisico nel driver I/O:

```c
media_ptr -> fx_media_driver_physical_sector =
    (media_ptr -> fx_media_driver_logical_sector % media_ptr -> fx_media_sectors_per_track) + 1;

media_ptr -> fx_media_driver_physical_head =
    (media_ptr -> fx_media_driver_logical_sector/ media_ptr ->
    fx_media_sectors_per_track) % media_ptr -> fx_media_heads;

media_ptr -> fx_media_driver_physical_track =(media_ptr ->
    fx_media_driver_logical_sector/ (media_ptr -> fx_media_sectors_per_track *
    media_ptr -> fx_media_heads)));
```

Si noti che i settori fisici iniziano da uno, mentre i settori logici iniziano da zero.

### <a name="hidden-sectors"></a>Settori nascosti

I settori nascosti risiedevano prima del record di avvio sui supporti. Poiché si trovano realmente al di fuori dell'ambito del layout file system FAT, è necessario che siano contabilizzate in ogni operazione di settore logico eseguita dal driver.

### <a name="media-write-protect"></a>Protezione scrittura supporti

Il driver FileX può attivare la protezione da scrittura impostando il campo fx_media_driver_write_protect nel blocco di controllo multimediale. In questo modo verrà restituito un errore se vengono effettuate chiamate FileX durante un tentativo di scrittura nei supporti.

## <a name="sample-ram-driver"></a>Driver RAM di esempio

Il sistema di dimostrazione FileX viene fornito con un piccolo driver di disco RAM, definito nel file fx_ram_driver. c. Il driver presuppone uno spazio di memoria 32K e crea un record di avvio per i settori a 256 128 byte. Questo file fornisce un valido esempio di implementazione di driver di I/O FileX specifici dell'applicazione.

```c
/*FUNCTION: _fx_ram_driver
RELEASE: PORTABLE C 5.7
AUTHOR: William E. Lamie, Microsoft, Inc.
DESCRIPTION: This function is the entry point to the generic
    RAM disk driver that is delivered with all versions of FileX.
    The format of the RAM disk is easily modified by calling fx_media_format prior to opening the media.

    This driver also serves as a template for developing FileX drivers
    for actual devices. Simply replace the read/write sector logic
    with calls to read/write from the appropriate physical device.

FileX RAM/FLASH structures look like the following:
Physical Sector             Contents
    0                         Boot record
    1                         FAT Area Start
    +FAT Sectors             Root Directory Start
    +Directory Sectors         Data Sector Start

INPUT: media_ptr Media control block pointer
OUTPUT: None
CALLS:     _fx_utility_memory_copy Copy sector memory
        _fx_utility_16_unsigned_read Read 16-bit unsigned
CALLED BY: FileX System Functions
RELEASE HISTORY:

    DATE         NAME         DESCRIPTION
    12-12-2005     William E.     Lamie Initial Version 5.0
    07-18-2007     William E.     Lamie Modified comment(s),
                                resulting in version 5.1
    03-01-2009     William E.     Lamie Modified comment(s),
                                resulting in version 5.2
    11-01-2015     William E.     Lamie Modified comment(s),
                                resulting in version 5.3
    04-15-2016     William E.     Lamie Modified comment(s),
                                resulting in version 5.4
    04-03-2017     William E.     Lamie Modified comment(s),
                                fixed compiler warnings,
                                resulting in version 5.5
    12-01-2018     William E.     Lamie Modified comment(s),
                                checked buffer overflow,
                                resulting in version 5.6
    08-15-2019     William E.     Lamie Modified comment(s),
                                resulting in version 5.7
*/

VOID _fx_ram_driver(FX_MEDIA *media_ptr) { UCHAR *source_buffer;
                                           UCHAR *destination_buffer;
                                           UINT bytes_per_sector;

    /* There are several useful/important pieces of information contained
        in the media structure, some of which are supplied by FileX and
        others are for the driver to setup. The following
        is a summary of the necessary FX_MEDIA structure members:
    FX_MEDIA Member                     Meaning

    fx_media_driver_request             FileX request type.
        Valid requests from FileX are as follows:
        FX_DRIVER_READ
        FX_DRIVER_WRITE
        FX_DRIVER_FLUSH
        FX_DRIVER_ABORT
        FX_DRIVER_INIT
        FX_DRIVER_BOOT_READ
        FX_DRIVER_RELEASE_SECTORS
        FX_DRIVER_BOOT_WRITE FX_DRIVER_UNINIT

    fx_media_driver_status              This value is RETURNED by the driver.
        If the operation is successful, this field should be set to FX_SUCCESS
        for before returning. Otherwise, if an error occurred, this field should be set to FX_IO_ERROR.

    fx_media_driver_buffer              Pointer to buffer to read or write sector data. This is supplied by FileX.

    fx_media_driver_logical_sector      Logical sector FileX is requesting.
    fx_media_driver_sectors             Number of sectors FileX is requesting.

    The following is a summary of the optional FX_MEDIA structure members: FX_MEDIA Member Meaning

    fx_media_driver_info                Pointer to any additional information or memory.
        This is optional for the driver use and is setup from the fx_media_open call.
        The RAM disk uses this pointer for the RAM disk memory itself.

    fx_media_driver_write_protect       The DRIVER sets this to FX_TRUE when media is write protected.
        This is typically done in initialization, but can be done anytime.

    fx_media_driver_free_sector_update  The DRIVER sets this to FX_TRUE when it needs
        to know when clusters are released. This is important for FLASH wear-leveling drivers.

    fx_media_driver_system_write        FileX sets this flag to FX_TRUE if the sector
        being written is a system sector, e.g., a boot, FAT, or directory sector.
        The driver may choose to use this to initiate error recovery logic for greater fault
        tolerance. fx_media_driver_data_sector_read FileX sets this flag to FX_TRUE
        if the sector(s) being read are file data sectors, i.e., NOT system sectors.

    fx_media_driver_sector_type         FileX sets this variable to the specific type of
        sector being read or written. The following sector types are identified:
            FX_UNKNOWN_SECTOR
            FX_BOOT_SECTOR
            FX_FAT_SECTOR
            FX_DIRECTORY_SECTOR
            FX_DATA_SECTOR */

    /* Process the driver request specified in the media control block. */

    switch (media_ptr -> fx_media_driver_request){

        case FX_DRIVER_READ: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
            is pointed to by the fx_media_driver_info pointer, which is supplied
            by the application in the call to fx_media_open. */

            source_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the RAM sector into the destination. */

             _fx_utility_memory_copy(source_buffer,
                media_ptr -> fx_media_driver_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_WRITE: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
                is pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */

            destination_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the source to the RAM sector. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_FLUSH: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_ABORT: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_INIT: {

            /* FLASH drivers are responsible for setting several fields
                in the media structure, as follows:
                media_ptr -> fx_media_driver_free_sector_update media_ptr ->
                fx_media_driver_write_protect
                The fx_media_driver_free_sector_update flag is used to instruct
                FileX to inform the driver whenever sectors are not being used.
                This is especially useful for FLASH managers so they don't have
                maintain mapping for sectors no longer in use.
                The fx_media_driver_write_protect flag can be set anytime by
                the driver to indicate the media is not writable. Write attempts
                made when this flag is set are returned as errors. */
            /* Perform basic initialization here... since the boot record is going
                to be read subsequently and again for volume name requests. */
            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

         case FX_DRIVER_UNINIT: {

            /* There is nothing to do in this case for the RAM driver.
                For actual devices some shutdown processing may be necessary. */

            /* Successful driver request. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_READ: {
            /* Read the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is pointed
                to by the fx_media_driver_info pointer, which is supplied by the
                application in the call to fx_media_open. */

            source_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* For RAM driver, determine if the boot record is valid. */

            if ((source_buffer[0] != (UCHAR)0xEB) ||

            ((source_buffer[1] != (UCHAR)0x34) &&

            (source_buffer[1] != (UCHAR)0x76)) || /* exFAT jump code. */

            (source_buffer[2] != (UCHAR)0x90)) {

            /* Invalid boot record, return an error! */
            media_ptr -> fx_media_driver_status = FX_MEDIA_INVALID; return; }

            /* For RAM disk only, pickup the bytes per sector. */

            bytes_per_sector =
                _fx_utility_16_unsigned_read(&source_buffer[FX_BYTES_SECTOR]); #ifdef FX_ENABLE_EXFAT

            /* if byte per sector is zero, then treat it as exFAT volume. */

            if (bytes_per_sector == 0 && (source_buffer[1] == (UCHAR)0x76)) {

            /* Pickup the byte per sector shift, and calculate byte per sector. */ 
            bytes_per_sector = (UINT)(1 << source_buffer[FX_EF_BYTE_PER_SECTOR_SHIFT]);

            }

            #endif /* FX_ENABLE_EXFAT */

            /* Ensure this is less than the media memory size. */
            if (bytes_per_sector \media_ptr -> fx_media_memory_size) {

            media_ptr -> fx_media_driver_status = FX_BUFFER_ERROR; break; }

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(source_buffer, media_ptr -> fx_media_driver_buffer, bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_WRITE: {

            /* Write the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is
                pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */ 
            destination_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        default: {
            /* Invalid driver request. */
            media_ptr -> fx_media_driver_status = FX_IO_ERROR; break;}
    }
}
```
