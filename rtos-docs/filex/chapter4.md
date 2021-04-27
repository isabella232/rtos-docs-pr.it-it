---
title: Capitolo 4- Descrizione dei Azure RTOS FileX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS FileX in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 948adff65a080649db0870e35bc75ee774775cb7
ms.sourcegitcommit: 4cbe92b337e82124bb5a86d319b787eb05b4ea76
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067013"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a>Capitolo 4- Descrizione dei Azure RTOS FileX

Questo capitolo contiene una descrizione di tutti i Azure RTOS FileX in ordine alfabetico. I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili.

## <a name="fx_directory_attributes_read"></a>fx_directory_attributes_read

Legge gli attributi della directory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio legge gli attributi della directory dal supporto specificato.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name**: puntatore al nome della directory richiesta (il percorso della directory è facoltativo).
- **attributes** _ptr: puntatore alla destinazione per gli attributi della directory da inserire. Gli attributi della directory vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_VOLUME (0x08)
  - FX_DIRECTORY (0x10)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Lettura degli attributi di directory completata
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX _NOT FOUND** (0x04) Directory specificata non trovata nel supporto
- **FX_NOT_DIRECTORY** (0x0E) non è una directory
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_FILE_CORRUPT** 0x08) Il file è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporti non validi
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_attributes_set"></a>fx_directory_attributes_set

Imposta gli attributi della directory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a>Descrizione

Questo servizio imposta gli attributi della directory su quelli specificati dal chiamante.

> [!WARNING]
> *Questa applicazione può modificare solo un subset degli attributi della directory con questo servizio. Qualsiasi tentativo di impostare attributi aggiuntivi restituirà un errore.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name**: puntatore al nome della directory richiesta (il percorso della directory è facoltativo).
- **attributes**: i nuovi attributi di questa directory. Gli attributi di directory validi sono definiti come segue:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Set di attributi della directory riuscito
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NOT_FOUND** (0x04) La directory specificata non è stata trovata nel supporto
- **FX_NOT_DIRECTORY** (0x0E) non è una directory
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura
- **FX_FILE_CORRUPT** file (0x08) è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporti non validi
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido
- **FX_INVALID_ATTR** (0x19) Attributi non validi selezionati.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_create"></a>fx_directory_create

Crea la sottodirectory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a>Descrizione

Questo servizio crea una sottodirectory nella directory predefinita corrente o nel percorso specificato nel nome della directory. A differenza della directory radice, le sottodirectory non hanno un limite al numero di file che possono contenere. La directory radice può contenere solo il numero di voci determinato dal record di avvio.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name**: puntatore al nome della directory da creare (il percorso della directory è facoltativo).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Creazione directory completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NOT_FOUND** (0x04) La directory specificata non è stata trovata nel supporto
- **FX_NOT_DIRECTORY** (0x0E) non è una directory
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_FILE _CORRUPT** file (0x08) è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporti non validi
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido
- **FX_INVALID_ATTR** (0x19) Attributi non validi selezionati.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_default_get"></a>fx_directory_default_get

Ottiene l'ultima directory predefinita

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il puntatore all'ultimo percorso impostato ***da fx_directory_default_set***. Se la directory predefinita non è stata impostata o se la directory predefinita corrente è la directory radice, viene restituito FX_NULL valore .

> [!IMPORTANT]
> *La dimensione predefinita della stringa di percorso interna è di 256 caratteri. Può essere modificato modificando il FX_MAXIMUM_PATH **in** **fx_api.h** e ricompilando l'intera libreria FileX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene usato internamente da FileX.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **return_path_name**: puntatore alla destinazione per l'ultima stringa di directory predefinita. Viene restituito FX_NULL valore se l'impostazione corrente della directory predefinita è la radice. Quando il supporto viene aperto, la radice è l'impostazione predefinita.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Operazione get della directory predefinita riuscita
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_default_set"></a>fx_directory_default_set

Imposta la directory predefinita

### <a name="prototype"></a>Prototipo

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la directory predefinita del supporto. Se viene specificato FX_NULL, la directory predefinita viene impostata sulla directory radice del supporto. Tutte le operazioni sui file successive che non specificano in modo esplicito un percorso verranno impostate per impostazione predefinita su questa directory.

> [!IMPORTANT]
> *La dimensione predefinita della stringa di percorso interna è di 256 caratteri. Può essere modificato modificando il FX_MAXIMUM_PATH **in** **fx_api.h e** ricompilando l'intera libreria FileX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene usato internamente da FileX.*

> [!IMPORTANT]
> *Per i nomi forniti dall'applicazione, FileX supporta sia la barra rovesciata ( ) che la barra (/) per separare directory, sottodirectory e \\ nomi di file. Tuttavia, FileX usa solo il carattere barra rovesciata nei percorsi restituiti all'applicazione.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **new_path_name:** puntatore al nuovo nome di directory predefinito. Se viene specificato FX_NULL, la directory predefinita del supporto viene impostata sulla directory radice del supporto.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Set di directory predefinito riuscito
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_INVALID_PATH** (0x0D) Non è stato possibile trovare la nuova directory
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_delete"></a>fx_directory_delete

Elimina la sottodirectory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a>Descrizione

Questo servizio elimina la directory specificata. Si noti che la directory deve essere vuota per eliminarla.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name:** puntatore al nome della directory da eliminare (il percorso della directory è facoltativo).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Eliminazione della directory completata
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NOT_FOUND** (0x04) Directory specificata non trovata
- **FX_DIR_NOT_EMPTY** (0x10) La directory specificata non è vuota
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura
- **FX_FILE_CORRUPT** file (0x08) è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporti non validi
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory
- **FX_NOT_DIRECTORY** (0x0E) Non è una voce di directory
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_first_entry_find"></a>fx_directory_first_entry_find

Ottiene la prima voce di directory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome della prima voce nella directory predefinita e lo copia nella destinazione specificata.

> [!WARNING]
> *La destinazione specificata deve essere sufficientemente grande da contenere il nome FileX di dimensioni massime, come definito da **FX_MAX_LONG_NAME_LEN.***

> [!WARNING]
> *Se si usa un percorso non locale, è importante impedire (con un semaforo ThreadX, un mutex o una modifica del livello di priorità) altri thread dell'applicazione di modificare questa directory durante l'attraversamento della directory. In caso contrario, è possibile ottenere risultati non validi.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **return_entry_name:** puntatore alla destinazione per il nome della prima voce nella directory predefinita.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca della prima voce di directory riuscita
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_FILE_CORRUPT** file (0x08) è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido
- **FX_CALLER_ERROR** (0x20) Caller non è un thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_first_full_entry_find"></a>fx_directory_first_full_entry_find

Ottiene la prima voce di directory con informazioni complete

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name:** puntatore alla destinazione per il nome di una voce di directory. Deve essere grande almeno quanto FX_MAX_LONG_NAME_LEN.
- **attributes:** se non Null, puntatore alla destinazione per gli attributi della voce da inserire. Gli attributi vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:
  - **FX_READ_ONLY** (0x01)
  - **FX_HIDDEN** (0x02)
  - **FX_SYSTEM** (0x04)
  - **FX_VOLUME** (0x08)
  - **FX_DIRECTORY** (0x10)
  - **FX_ARCHIVE** (0x20)
- **size:** se non Null, puntatore alla destinazione per le dimensioni della voce in byte.
- **year:** se non Null, puntatore alla destinazione per l'anno di modifica della voce.
- **month:** se non Null, puntatore alla destinazione per il mese di modifica della voce.
- **day:** se non Null, puntatore alla destinazione per il giorno di modifica della voce.
- **hour:** se non Null, puntatore alla destinazione per l'ora di modifica della voce.
- **minute:** se non Null, puntatore alla destinazione per il minuto di modifica della voce.
- **second:** se non Null, puntatore alla destinazione per il secondo di modifica della voce.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca della prima voce di directory riuscita
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura
- **FX_FILE _CORRUPT** file (0x08) è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporti non validi
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA     my_media;
UINT         status;
CHAR         entry_name[FX_MAX_LONG_NAME_LEN];
UINT         attributes;
ULONG        size;
UINT         year;
UINT         month;
UINT         day;
UINT         hour;
UINT         minute;
UINT         second;
/* Get the first directory entry in the default directory with full information. */
status = fx_directory_first_full_entry_find(&my_media, entry_name,
    &attributes, &size, &year, &month, &day, &hour, &minute, &second);

/* If status equals FX_SUCCESS, the entry's information is in the local variables. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_information_get"></a>fx_directory_information_get:

Ottiene le informazioni sulle voci di directory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name**: puntatore al nome della voce di directory.
- **attributes:** puntatore alla destinazione per gli attributi.
- **size:** puntatore alla destinazione per le dimensioni.
- **year:** puntatore alla destinazione dell'anno.
- **month:** puntatore alla destinazione del mese.
- **day:** puntatore alla destinazione del giorno.
- **hour:** puntatore alla destinazione per l'ora.
- **minute:** puntatore alla destinazione per il minuto.
- **second:** puntatore alla destinazione per il secondo.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca della prima voce di directory riuscita
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NOT_FOUND** (0x04) La directory specificata non è stata trovata nel supporto
- **FX_IO_ERROR** di I/O del driver 0x90 (0x90)
- **FX_MEDIA_INVALID** (0x02) Supporti non validi
- **FX_FILE _CORRUPT** (0x08) Il file è danneggiato
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA     my_media;
UINT         status; attributes; year; month; day;
CHAR         entry_name[FX_MAX_LONG_NAME_LEN];
ULONG        size;
UINT         hour; minute; second;
/* Retrieve information about the directory entry "myfile.txt".*/
status = fx_directory_information_get(&my_media, "myfile.txt", &attributes, &size,
                                      &year, &month, &day,
                                      &hour, &minute, &second);
/* If status equals FX_SUCCESS, the directory entry information is available in the local variables. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_clear"></a>fx_directory_local_path_clear:

Cancella il percorso locale predefinito

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella il percorso locale precedente configurato per il thread chiamante.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un supporto aperto in precedenza.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Percorso locale riuscito non crittografato.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è attualmente aperto
- **FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH definito
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_get"></a>fx_directory_local_path_get:

Ottiene la stringa di percorso locale corrente

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il puntatore al percorso locale del supporto specificato. Se non è impostato alcun percorso locale, viene restituito un valore NULL al chiamante.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **return_path_name**: puntatore al puntatore della stringa di destinazione per la stringa di percorso locale da archiviare.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Percorso locale riuscito.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è attualmente aperto
- **FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_restore"></a>fx_directory_local_path_restore:

Ripristina il percorso locale precedente

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio ripristina un percorso locale impostato in precedenza. Viene ripristinata anche la posizione di ricerca della directory effettuata in questo percorso locale, che rende questa routine utile negli attraversamenti di directory ricorsivi da parte dell'applicazione.

> [!IMPORTANT]
> *Ogni percorso locale contiene una stringa di percorso locale **di FX_MAXIMUM_PATH** dimensioni, che per impostazione predefinita è di 256 caratteri. Questa stringa di percorso interna non viene usata da FileX e viene fornita solo per l'uso dell'applicazione. Se **FX_LOCAL_PATH** deve essere dichiarato come variabile locale, gli utenti devono fare attenzione all'aumento dello stack in base alle dimensioni di questa struttura. Gli utenti sono invitati a ridurre le dimensioni **del** FX_MAXIMUM_PATH e ricompilare l'origine della libreria FileX.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **local_path_ptr:** puntatore al percorso locale impostato in precedenza. È molto importante assicurarsi che questo puntatore punti effettivamente a un percorso locale usato in precedenza e ancora intatto.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ripristino del percorso locale riuscito.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è attualmente aperto.
- **FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH definito.
- **FX_PTR_ERROR** (0x18) Supporto non valido o puntatore di percorso locale.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_set"></a>fx_directory_local_path_set

Configura un percorso locale specifico del thread

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a>Descrizione

Questo servizio configura un percorso specifico del thread come specificato da ***new_path_string** _. Al termine di questa routine, le informazioni sul percorso locale archiviate in _ local_path_ptr * avranno la precedenza sul percorso *_multimediale_* globale per tutte le operazioni su file e directory eseguite da questo thread. Questo non avrà alcun impatto su qualsiasi altro thread nel sistema 
> [!IMPORTANT]
> *La dimensione predefinita della stringa di percorso locale è di 256 caratteri. è possibile modificarlo modificando FX_MAXIMUM_PATH **in** **fx_api.h e** ricompilando l'intera libreria FileX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene usato internamente da FileX.*

> [!IMPORTANT]
> *Per i nomi forniti dall'applicazione, FileX supporta sia la barra rovesciata ( ) che i caratteri barra (/) per separare directory, sottodirectory e nomi \\ di file. Tuttavia, FileX usa solo il carattere barra rovesciata nei percorsi restituiti all'applicazione.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al supporto aperto in precedenza.
- **local_path_ptr**: destinazione per contenere le informazioni sul percorso locale specifiche del thread. L'indirizzo di questa struttura può essere fornito alla funzione di ripristino del percorso locale in futuro.
- **new_path_name**: specifica il percorso locale da configurare.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Set di directory predefinito riuscito.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_IMPLEMENTED** (0x22) **FX_NO_LCOAL_PATH
- **FX_INVALID_PATH** (0x0D) Impossibile trovare la nuova directory.
- **FX_NOT_IMPLEMENTED** (0x22) - **FX_NO_LOCAL_PATH definito.
- **FX_PTR_ERROR** (0x18) Supporto non valido o puntatore di percorso locale.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UINT             status;
FX_LOCAL_PATH     my_previous_local_path;
/* Set the local path to \abc\def\ghi. */
status = fx_directory_local_path_set (&my_media,&local_path,"\\abc\\def\\ghi");

/* If status equals FX_SUCCESS, the default directory for this thread
is \abc\def\ghi. All subsequent file operations that do not explicitly
specify a path will default to this directory. Note that the character
"\" serves as an escape character in a string. To represent the
character "\", use the construct "\\".*/
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_long_name_get"></a>fx_directory_long_name_get:

Ottiene il nome lungo dal nome breve

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome lungo (se presente) associato al nome breve (formato 8.3) fornito. Il nome breve può essere un nome file o un nome di directory.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **short_name:** puntatore al nome breve di origine (formato 8.3).
- **long_name:** puntatore alla destinazione per il nome lungo. Se non è presente alcun nome lungo, viene restituito il nome breve. Si noti che la destinazione per il nome lungo deve essere sufficientemente grande da contenere FX_MAX_LONG_NAME_LEN caratteri.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ottenere il nome lungo riuscito
- **FX_NOT_FOUND** (0x04) Nome breve non trovato
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)
- **FX_MEDIA_INVALID** (0x02) Supporto non valido
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato
- **FX_SECTOR_INVALID** (0x89) Settore non valido
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_PTR_ERROR** (0x18) Supporto non valido o puntatore al nome
- **FX_CALLER_ERROR** (0x20) Il chiamante non è un thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_long_name_get_extended"></a>fx_directory_long_name_get_extended

Ottiene il nome lungo dal nome breve

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome lungo (se presente) associato al nome breve (formato 8.3) fornito. Il nome breve può essere un nome file o un nome di directory.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **short_name:** puntatore al nome breve di origine (formato 8.3).
- **long_name:** puntatore alla destinazione per il nome lungo. Se non è presente alcun nome lungo, viene restituito il nome breve. Nota: la destinazione per il nome lungo deve essere sufficientemente grande da **contenere FX_MAX_LONG_NAME_LEN** caratteri.
- **long_file_name_buffer_length**: lunghezza del buffer dei nomi lunghi.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ottiene il nome lungo riuscito.
- **FX_NOT_FOUND** (0x04) Nome breve non trovato.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore al nome non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name), sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_name_test"></a>fx_directory_name_test

Test per la directory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a>Descrizione

Questo servizio verifica se il nome fornito è o meno una directory. In tal caso, viene FX_SUCCESS restituito un oggetto .

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **directory_name:** puntatore al nome della voce di directory.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Nome fornito è una directory.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto
- **FX_NOT_FOUND** (0x04) Impossibile trovare la voce della directory.
- **FX_NOT_DIRECTORY** (0x0E) La voce non è una directory
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore al nome non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create

## <a name="fx_directory_next_entry_find"></a>fx_directory_next_entry_find:

Seleziona la voce di directory successiva

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il nome della voce successiva nella directory predefinita corrente.

> [!WARNING]
> *Se si usa un percorso non locale, è anche importante impedire (con un semaforo ThreadX o un livello di priorità del thread) che altri thread dell'applicazione cambino questa directory durante l'attraversamento di una directory. In caso contrario, è possibile ottenere risultati non validi.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **return_entry_name:** puntatore alla destinazione per il nome della voce successiva nella directory predefinita. Il buffer a cui punta questo puntatore deve essere sufficientemente grande da contenere le dimensioni massime del nome FileX, definite **_da_** FX_MAX_LONG_NAME_LEN .

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca voce successiva riuscita
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_next_full_entry_find"></a>fx_directory_next_full_entry_find:

Ottiene la voce di directory successiva con informazioni complete

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_next_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes, 
    ULONG *size,
    UINT *year, 
    UINT *month, 
    UINT *day,
    UINT *hour, 
    UINT *minute, 
    UINT *second);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome della voce successiva nella directory predefinita e lo copia nella destinazione specificata. Restituisce inoltre informazioni complete sulla voce come specificato dai parametri di input aggiuntivi.

> [!WARNING]
> *La destinazione specificata deve essere sufficientemente grande da contenere il nome FileX di dimensioni massime, come definito da ***FX_MAX_LONG_NAME_LEN****

> [!WARNING]
> *Se si usa un percorso non locale, è importante impedire (con un semaforo ThreadX, un mutex o una modifica del livello di priorità) altri thread dell'applicazione di modificare questa directory durante l'attraversamento della directory. In caso contrario, è possibile ottenere risultati non validi.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **directory_name:** puntatore alla destinazione per il nome di una voce di directory. Deve essere grande almeno quanto **FX_MAX_LONG_NAME_LEN**.
- **attributes:** se non Null, puntatore alla destinazione per gli attributi della voce da inserire. Gli attributi vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:
  - **FX_READ_ONLY** (0x01)
  - **FX_HIDDEN** (0x02)
  - **FX_SYSTEM** (0x04)
  - **FX_VOLUME** (0x08)
  - **FX_DIRECTORY** (0x10)
  - **FX_ARCHIVE** (0x20)
- **size:** se non Null, puntatore alla destinazione per le dimensioni della voce in byte.
- **month:** se non Null, puntatore alla destinazione per il mese di modifica della voce.
- **year:** se non Null, puntatore alla destinazione per l'anno di modifica della voce.
- **day:** se non Null, puntatore alla destinazione per il giorno di modifica della voce.
- **hour:** se non Null, puntatore alla destinazione per l'ora di modifica della voce.
- **minute:** se non Null, puntatore alla destinazione per il minuto di modifica della voce.
- **second:** se non Null, puntatore alla destinazione per il secondo elemento di modifica della voce.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca della voce successiva della directory completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido o tutti i parametri di input sono NULL.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA    my_media;
UINT        status;
CHAR        entry_name[FX_MAX_LONG_NAME_LEN];
UINT        attributes;
ULONG       size;
UINT        year;
UINT        month;
UINT        day;
UINT        hour;
UINT        minute;
UINT        second;

/* Get the next directory entry in the default directory with full information. */
status = fx_directory_next_full_entry_find(&my_media, entry_name, &attributes, &size,
                                           &year, &month, &day,
                                           &hour, &minute, &second);

/* If status equals FX_SUCCESS, the entry's information is in the local variables. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_rename"></a>fx_directory_rename

Rinomina la directory

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a>Descrizione

Questo servizio modifica il nome della directory con il nuovo nome di directory specificato. La ridenominazione viene eseguita anche in relazione al percorso specificato o al percorso predefinito. Se viene specificato un percorso nel nuovo nome di directory, la directory rinominata viene effettivamente spostata nel percorso specificato. Se non viene specificato alcun percorso, la directory rinominata viene inserita nel percorso predefinito corrente.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **old_directory_name:** puntatore al nome della directory corrente.
- **new_directory_name:** puntatore al nuovo nome di directory.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ridenominazione della directory completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** impossibile trovare 0x04 directory (0x04).
- **FX_NOT_DIRECTORY** (0x0E) non è una directory.
- **FX_INVALID_NAME** (0x0C) Nuovo nome di directory non valido.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory.
- **FX_INVALID_PATH** (0x0D) Percorso non valido specificato con il nome della directory.
- **FX_ALREADY_CREATED** (0x0B) La directory specificata è già stata creata.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_short_name_get"></a>fx_directory_short_name_get:

Ottiene il nome breve da un nome lungo

### <a name="prototype"></a>Prototipo

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome breve (formato 8.3) associato al nome lungo fornito. Il nome lungo può essere un nome di file o un nome di directory.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **long_name:** puntatore al nome lungo di origine.
- **short_name:** puntatore al nome breve di destinazione (formato 8.3). Si noti che la destinazione per il nome breve deve essere sufficientemente grande da contenere 14 caratteri.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Get nome breve riuscito.
- **FX_NOT_FOUND** (0x04) Nome lungo non trovato.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore del nome non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_short_name_get_extended"></a>fx_directory_short_name_get_extended

Ottiene il nome breve da un nome lungo

### <a name="prototype"></a>Prototipo

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome breve (formato 8.3) associato al nome lungo fornito. Il nome lungo può essere un nome di file o un nome di directory.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **long_name:** puntatore al nome lungo di origine.
- **short_name:** puntatore al nome breve di destinazione (formato 8.3). Nota: la destinazione per il nome breve deve essere sufficientemente grande da contenere 14 caratteri.
- **short_file_name_length**: lunghezza del buffer dei nomi brevi.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Get nome breve riuscito.
- **FX_NOT_FOUND** (0x04) Nome lungo non trovato.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore del nome non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_fault_tolerant_enable"></a>fx_fault_tolerant_enable

Abilita il servizio a tolleranza di errore

### <a name="prototype"></a>Prototipo

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il modulo a tolleranza di errore. All'avvio, il modulo a tolleranza di errore rileva se il file system è sotto protezione a tolleranza di errore FileX. In caso contrario, il servizio trova i settori disponibili nel file system per archiviare i log file system transazioni. Se il file system è con protezione a tolleranza di errore FileX, applica i log al file system per mantenerne l'integrità.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **memory_ptr**: puntatore a un blocco di memoria usato dal modulo a tolleranza di errore come memoria scratch.
- **memory_size**: dimensioni della memoria scratch. Per il corretto funzionamento della tolleranza di errore, le dimensioni della memoria scratch devono essere di almeno 3072 byte e devono essere multiple di dimensioni di settore.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Abilitata correttamente a tolleranza di errore.
- **FX_NOT_ENOUGH_MEMORY** dimensioni della memoria 0x91 (0x91) troppo piccole.
- **FX_BOOT_ERROR** (0x01) Errore del settore di avvio.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più disponibili cluster gratuiti.
- **FX_NO_MORE_SPACE** (0x0A) il supporto associato a questo file non dispone di un numero sufficiente di cluster disponibili.
- **FX_SECTOR_INVALID** (0x89) Non è valido
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a>Vedere anche

- fx_system_initialize
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write

## <a name="fx_file_allocate"></a>fx_file_allocate

Alloca spazio per un file

### <a name="prototype"></a>Prototipo

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a>Descrizione

Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato. FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster. Il risultato viene quindi arrotondato all'intero cluster successivo.

Per allocare spazio oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_allocate*.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **size:** numero di byte da allocare per il file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Allocazione file riuscita.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_FAT_READ_ERROR** (0x03) Non è stato possibile leggere la voce FAT.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più disponibili cluster gratuiti.
- **FX_NO_MORE_SPACE** (0x0A) il supporto associato a questo file non dispone di un numero sufficiente di cluster disponibili.
- **FX_SECTOR_INVALID** (0x89) Non è valido
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open- fx_file_read
- fx_file_relative_seek
- fx_file_rename- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_attributes_read"></a>fx_file_attributes_read

Legge gli attributi del file

### <a name="prototype"></a>Prototipo

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio legge gli attributi del file dal supporto specificato.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **file_name**: puntatore al nome del file richiesto (il percorso della directory è facoltativo).
- **attributes_ptr**: puntatore alla destinazione per gli attributi del file da inserire. Gli attributi del file vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_VOLUME (0x08)
  - FX_DIRECTORY (0x10)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Lettura dell'attributo riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) Il file specificato non è stato trovato nel supporto.
- **FX_NOT_A_FILE** (0x05) Il file specificato è una directory.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto o puntatore attributi non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_attributes_set"></a>fx_file_attributes_set

Imposta gli attributi del file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a>Descrizione

Questo servizio imposta gli attributi del file su quelli specificati dal chiamante.

> [!WARNING]
> *L'applicazione può modificare solo un subset degli attributi del file con questo servizio. Qualsiasi tentativo di impostare attributi aggiuntivi restituirà un errore.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **file_name**: puntatore al nome del file richiesto** (il percorso della directory è facoltativo).
- **attributes:** nuovi attributi per il file. Gli attributi di file validi sono definiti come segue:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Set di attributi riuscito.
- **FX_ACCESS_ERROR** (0x06) Il file è aperto e non può avere i relativi attributi impostati.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti altre voci nella tabella FAT o nella mappa del cluster exFAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_NOT_FOUND** (0x04) File specificato non trovato nel supporto.
- **FX_NOT_A_FILE** (0x05) Il file specificato è una directory.
- **FX_SECTOR_INVALID** (0x89) Il settore non è valido
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_INVALID_ATTR** (0x19) Attributi non validi selezionati.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_best_effort_allocate"></a>fx_file_best_effort_allocate

Sforzo ottimale per allocare spazio per un file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a>Descrizione

Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato. FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster. Il risultato viene quindi arrotondato all'intero cluster successivo. Se non sono disponibili cluster consecutivi sufficienti nei supporti, questo servizio collega il blocco più grande disponibile di cluster consecutivi al file. La quantità di spazio effettivamente allocato al file viene restituita al chiamante.

Per allocare spazio oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_best_effort_allocate*.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **size**: numero di byte da allocare per il file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Allocazione dei file ottimale.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_NO_MORE_SPACE** (0x0A) I supporti associati a questo file non hanno un numero sufficiente di cluster disponibili.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore di file o destinazione non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_close"></a>fx_file_close

Chiude il file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio chiude il file specificato. Se il file è stato aperto per la scrittura e se è stato modificato, questo servizio completa il processo di modifica del file aggiornando la voce di directory con le nuove dimensioni e l'ora e la data correnti del sistema.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Chiusura del file completata.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di attributi non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_create"></a>fx_file_create

Crea un file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a>Descrizione

Questo servizio crea il file specificato nella directory predefinita o nel percorso della directory fornito con il nome del file.

> [!WARNING]
> *Questo servizio crea un file di lunghezza zero, ad esempio nessun cluster allocato. L'allocazione viene eseguita automaticamente nelle scritture di file successive o può essere eseguita in anticipo con il servizio fx_file_allocate o fx_file_extended_allocate per lo spazio oltre i 4 GB).*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **file_name:** puntatore al nome del file da creare (il percorso della directory è facoltativo).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Creazione del file completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_ALREADY_CREATED** (0x0B) Il file specificato è già stato creato.
- **FX_NO_MORE_SPACE** (0x0A) Non sono presenti altre voci nella directory radice o non sono disponibili altri cluster.
- **FX_INVALID_PATH** (0x0D) Percorso non valido specificato con il nome file.
- **FX_INVALID_NAME** (0x0C) Nome file non valido.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_MEDIA_INVALID** (0x02)Supporti non validi.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore del nome file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a>Vedere anche
- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_date_time_set"></a>fx_file_date_time_set

### <a name="sets-file-date-and-time"></a>Imposta la data e l'ora del file

Impostazione di data e ora del file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_date_time_set(
    FX_MEDIA *media_ptr, 
    CHAR *file_name,
    UINT year, 
    UINT month, 
    UINT day,
    UINT hour, 
    UINT minute, 
    UINT second);
```
### <a name="description"></a>Descrizione

Questo servizio imposta la data e l'ora del file specificato.

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **file_name**: puntatore al nome del file.
- **year:** valore dell'anno (1980-2107 inclusi).
- **month:** valore del mese (1-12 inclusi).
- **day:** valore del giorno (da 1 a 31 inclusi).
- **hour**: valore di hour (0-23 inclusi).
- **minute:** valore di minute (0-59 inclusi).
- **second:** valore di second (0-59 inclusi).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Data/ora riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** file (0x04) non trovato.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore al nome non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.
- **FX_INVALID_YEAR** (0x12) Year non è valido.
- **FX_INVALID_MONTH** (0x13) Month non è valido.
- **FX_INVALID_DAY** (0x14) Day non è valido.
- **FX_INVALID_HOUR** (0x15) L'ora non è valida.
- **FX_INVALID_MINUTE** minuto (0x16) non è valido.
- **FX_INVALID_SECOND** (0x17) Second non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_delete"></a>fx_file_delete

### <a name="deletes-file"></a>Elimina il file

Eliminazione di file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il file specificato.


### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **file_name:** puntatore al nome del file da eliminare (il percorso della directory è facoltativo).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Eliminazione del file completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) File specificato non trovato.
- **FX_NOT_A_FILE** (0x05) Il nome file specificato è una directory o un volume.
- **FX_ACCESS_ERROR** (0x06) Il file specificato è attualmente aperto.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_allocate"></a>fx_file_extended_allocate

Alloca spazio per un file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a>Descrizione

Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato. FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster. Il risultato viene quindi arrotondato all'intero cluster successivo.

Questo servizio è progettato per exFAT. Il *parametro size* accetta un valore intero a 64 bit, che consente al chiamante di preallocare spazio oltre l'intervallo di 4 GB.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **size**: numero di byte da allocare per il file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Corretta allocazione dei file.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_NO_MORE_SPACE** (0x0A) il supporto associato a questo file non dispone di un numero sufficiente di cluster disponibili.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_best_effort_allocate"></a>fx_file_extended_best_effort_allocate

Sforzo ottimale per allocare spazio per un file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a>Descrizione

Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato. FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster. Il risultato viene quindi arrotondato all'intero cluster successivo. Se nel supporto non sono disponibili cluster consecutivi sufficienti, questo servizio collega il blocco più grande disponibile di cluster consecutivi al file . La quantità di spazio effettivamente allocato al file viene restituita al chiamante.

Questo servizio è progettato per exFAT. Il *parametro size* accetta un valore intero a 64 bit, che consente al chiamante di preallocare spazio oltre l'intervallo di 4 GB.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **size:** numero di byte da allocare per il file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Allocazione file riuscita.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_NO_MORE_SPACE** (0x0A) il supporto associato a questo file non dispone di un numero sufficiente di cluster disponibili.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

FX_FILE my_file;
UINT             status;
ULONG64         actual_allocation;

/* Attempt to allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_best_effort_allocate(&my_file,
    0x100000000, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_relative_seek"></a>fx_file_extended_relative_seek

Posizioni in base a un offset di byte relativo

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il puntatore interno di lettura/scrittura del file all'offset di byte relativo specificato. Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.

Questo servizio è progettato per exFAT. Il *byte_offset* accetta un valore intero a 64 bit, che consente al chiamante di riposizionare il puntatore di lettura/scrittura oltre l'intervallo di 4 GB.

> [!IMPORTANT]
> *Se l'operazione di ricerca tenta di cercare oltre la fine del file, il puntatore di lettura/scrittura del file viene posizionato alla fine del file. Viceversa, se l'operazione di ricerca tenta di posizionarsi oltre l'inizio del file, il puntatore di lettura/scrittura del file viene posizionato all'inizio del file.*

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **byte_offset:** offset dei byte relativo desiderato nel file.
- **seek_from**: direzione e posizione della posizione da cui eseguire la ricerca relativa. Le opzioni di ricerca valide sono definite come segue:
  - FX_SEEK_BEGIN (0x00)
  - FX_SEEK_END (0x01)
  - FX_SEEK_FORWARD (0x02)
  - FX_SEEK_BACK (0x03) Se FX_SEEK_BEGIN specificato, l'operazione di ricerca viene eseguita dall'inizio del file. Se FX_SEEK_END specificato, l'operazione di ricerca viene eseguita all'indietro dalla fine del file. Se FX_SEEK_FORWARD specificato, l'operazione di ricerca viene eseguita in avanti dalla posizione corrente del file. Se FX_SEEK_BACK specificato, l'operazione di ricerca viene eseguita all'indietro dalla posizione corrente del file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca relativa al file completata.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_seek"></a>fx_file_extended_seek

Posizioni all'offset di byte

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il puntatore di lettura/scrittura del file interno all'offset di byte specificato. Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.

Questo servizio è progettato per exFAT. Il *byte_offset* accetta un valore intero a 64 bit, che consente al chiamante di riposizionare il puntatore di lettura/scrittura oltre l'intervallo di 4 GB.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **byte_offset:** offset di byte desiderato nel file. Un valore pari a zero posizionerà il puntatore in lettura/scrittura all'inizio del file, mentre un valore maggiore delle dimensioni del file posizionerà il puntatore di lettura/scrittura alla fine del file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca di file riuscita.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_truncate"></a>fx_file_extended_truncate

Tronca il file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a>Descrizione

Questo servizio tronca le dimensioni del file alle dimensioni specificate. Se le dimensioni fornite sono maggiori delle dimensioni effettive del file, questo servizio non fa nulla. Nessuno dei cluster multimediali associati al file viene rilasciato.

> [!WARNING]
> *Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*

Questo servizio è progettato per exFAT. Il *parametro size* accetta un valore intero a 64 bit, che consente al chiamante di operare oltre l'intervallo di 4 GB.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **size:** nuove dimensioni del file. I byte oltre le nuove dimensioni del file vengono eliminati.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Troncamento del file riuscito.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_truncate_release"></a>fx_file_extended_truncate_release

Tronca i file e rilascia i cluster

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a>Descrizione

Questo servizio tronca le dimensioni del file alle dimensioni specificate. Se le dimensioni specificate sono maggiori delle dimensioni effettive del file, questo servizio non esegue alcun'operazione. A differenza ***del fx_file_extended_truncate,*** questo servizio rilascia tutti i cluster inutilizzati.

> [!WARNING]
> *Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*

Questo servizio è progettato per exFAT. Il *parametro size* accetta un valore intero a 64 bit, che consente al chiamante di operare oltre l'intervallo di 4 GB.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **size:** nuove dimensioni del file. I byte oltre questa nuova dimensione di file vengono eliminati.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Troncamento del file riuscito.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_open"></a>fx_file_open

Apre il file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a>Descrizione

Questo servizio apre il file specificato per la lettura o la scrittura. Un file può essere aperto per la lettura più volte, mentre un file può essere aperto per la scrittura una sola volta fino a quando il writer non chiude il file.

> [!IMPORTANT]
> *È necessario fare attenzione se un file è aperto simultaneamente per la lettura e la scrittura. La scrittura di file eseguita quando un file viene aperto simultaneamente per la lettura potrebbe non essere visibile dal lettore, a meno che il lettore non chiuda e riapre il file per la lettura. Analogamente, il writer di file deve prestare attenzione quando si usano servizi di troncamento dei file. Se un file viene troncato dal writer, i lettori dello stesso file potrebbero restituire dati non validi.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **file_ptr:** puntatore al blocco di controllo file.
- **file_name**: puntatore al nome del file da aprire (il percorso della directory è facoltativo).
- **open_type**: tipo di file aperto. Le opzioni valide per il tipo aperto sono:
  - FX_OPEN_FOR_READ (0x00)
  - FX_OPEN_FOR_WRITE (0x01)
  - FX_OPEN_FOR_READ_FAST (0x02)

L'apertura di file FX_OPEN_FOR_READ e FX_OPEN_FOR_READ_FAST è simile:

- FX_OPEN_FOR_READ verifica che l'elenco collegato dei cluster che costituiscono il file sia intatto e FX_OPEN_FOR_READ_FAST non esegue questa verifica, il che lo rende più veloce.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Il file è stato aperto correttamente.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) Il file specificato non è stato trovato.
- **FX_NOT_A_FILE** (0x05) Il nome file specificato è una directory o un volume.
- **FX_FILE_CORRUPT** (0x08) Il file specificato è danneggiato e l'apertura non è riuscita.
- **FX_ACCESS_ERROR** (0x06) Il file specificato è già aperto o il tipo open non è valido.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_MEDIA_INVALID** (0x02) Supporto non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_read"></a>fx_file_read

Legge i byte dal file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a>Descrizione

Questo servizio legge i byte dal file e li archivia nel buffer fornito. Al termine della lettura, il puntatore di lettura interno del file viene regolato in modo che punti al byte successivo nel file. Se nella richiesta sono rimasti meno byte, nel buffer vengono archiviati solo i byte rimanenti. In ogni caso, il numero totale di byte inseriti nel buffer viene restituito al chiamante.

> [!WARNING]
> *L'applicazione deve assicurarsi che il buffer fornito sia in grado di archiviare il numero specificato di byte richiesti.*

> [!WARNING]
> *Si ottiene prestazioni più veloci se il buffer di destinazione si trova su un limite di parole lunghe e le dimensioni richieste sono divisibile in modo uniforme in base a sizeof(**ULONG**).*

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **buffer_ptr:** puntatore al buffer di destinazione per la lettura.
- **request_size**: numero massimo di byte da leggere.
- **actual_size:** puntatore alla variabile per contenere il numero effettivo di byte letti nel buffer fornito.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Lettura del file completata.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_FILE_CORRUPT** (0x08) Il file specificato è danneggiato e la lettura non è riuscita.
- **FX_END_OF_FILE** (0x09) È stata raggiunta la fine del file.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Puntatore al file o al buffer non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE                 my_file;
unsigned char           my_buffer[1024];
ULONG                   actual_bytes;
UINT                    status;

/* Read up to 1024 bytes into "my_buffer." */
status = fx_file_read(&my_file, my_buffer, 1024, &actual_bytes);

/* If status equals FX_SUCCESS, "my_buffer" contains the bytes
    read from the file. The total number of bytes read is in "actual_bytes." */
```
### <a name="see-also"></a>Vedere anche

- fx_file_allocate,
- fx_file_attributes_read,
- fx_file_attributes_set,
- fx_file_best_effort_allocate,
- fx_file_close,
- fx_file_create,
- fx_file_date_time_set,
- fx_file_delete,
- fx_file_extended_allocate,
- fx_file_extended_best_effort_allocate,
- fx_file_extended_relative_seek,
- fx_file_extended_seek,
- fx_file_extended_truncate,
- fx_file_extended_truncate_release,
- fx_file_open,
- fx_file_relative_seek,
- fx_file_rename,
- fx_file_seek,
- fx_file_truncate,
- fx_file_truncate_release,
- fx_file_write,
- fx_file_write_notify_set,
- fx_unicode_file_create,
- fx_unicode_file_rename,
- fx_unicode_name_get,
- fx_unicode_short_name_get

## <a name="fx_file_relative_seek"></a>fx_file_relative_seek

Posizioni a un offset di byte relativo

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il puntatore di lettura/scrittura del file interno all'offset di byte relativo specificato. Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.

> [!IMPORTANT]
> *Se l'operazione di ricerca tenta di cercare oltre la fine del file, il puntatore di lettura/scrittura del file viene posizionato alla fine del file. Al contrario, se l'operazione di ricerca tenta di posizionarsi oltre l'inizio del file, il puntatore di lettura/scrittura del file viene posizionato all'inizio del file.*

Per cercare con un valore di offset superiore a 4 GB, l'applicazione deve usare il *servizio* fx_file_extended_relative_seek .

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **byte_offset:** offset di byte relativo desiderato nel file.
- **seek_from**: direzione e posizione della posizione da cui eseguire la ricerca relativa. Le opzioni di ricerca valide sono definite nel modo seguente:
  - FX_SEEK_BEGIN (0x00)
  - FX_SEEK_END (0x01)
  - FX_SEEK_FORWARD (0x02)
  - FX_SEEK_BACK (0x03)

Se FX_SEEK_BEGIN specificato, l'operazione di ricerca viene eseguita dall'inizio del file. Se FX_SEEK_END specificato, l'operazione di ricerca viene eseguita all'indietro dalla fine del file. Se FX_SEEK_FORWARD specificato, l'operazione di ricerca viene eseguita in avanti dalla posizione corrente del file. Se FX_SEEK_BACK specificato, l'operazione di ricerca viene eseguita all'indietro dalla posizione corrente del file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca relativa del file completata.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_rename"></a>fx_file_rename

Rinomina il file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a>Descrizione

Questo servizio modifica il nome del file specificato *da* old_file_name . La ridenominazione viene eseguita anche in relazione al percorso specificato o al percorso predefinito. Se viene specificato un percorso nel nuovo nome file, il file rinominato viene spostato nel percorso specificato. Se non viene specificato alcun percorso, il file rinominato viene inserito nel percorso predefinito corrente.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un blocco di controllo multimediale.
- **old_file_name**: puntatore al nome del file da rinominare (il percorso della directory è facoltativo).
- **new_file_name**: puntatore al nuovo nome file. Il percorso della directory non è consentito.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) La ridenominazione del file è riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) Il file specificato non è stato trovato.
- **FX_NOT_A_FILE** (0x05) Il file specificato è una directory.
- **FX_ACCESS_ERROR** (0x06) Il file specificato è già aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_INVALID_NAME** (0x0C) Il nuovo nome file specificato non è un nome file valido.
- **FX_INVALID_PATH** (0x0D) non è valido.
- **FX_ALREADY_CREATED** (0x0B) Viene usato il nuovo nome file.
- **FX_MEDIA_INVALID** (0x02) non è valido.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_seek"></a>fx_file_seek

Posizioni per l'offset dei byte

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il puntatore interno di lettura/scrittura del file all'offset di byte specificato. Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.

Per eseguire la ricerca con un valore di offset superiore a 4 GB, l'applicazione deve usare il *fx_file_extended_seek*.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **byte_offset:** offset di byte desiderato nel file. Il valore zero posiziona il puntatore di lettura/scrittura all'inizio del file, mentre un valore maggiore delle dimensioni del file posiziona il puntatore di lettura/scrittura alla fine del file.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Ricerca di file riuscita.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_truncate"></a>fx_file_truncate

Tronca il file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a>Descrizione

Questo servizio tronca le dimensioni del file alle dimensioni specificate. Se le dimensioni fornite sono maggiori delle dimensioni effettive del file, questo servizio non fa nulla. Nessuno dei cluster di supporti associati al file viene rilasciato.

> [!WARNING]
> *Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*

Per operare oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_truncate*.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **size:** nuove dimensioni del file. I byte oltre le nuove dimensioni del file vengono eliminati.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Troncamento del file riuscito.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_truncate_release"></a>fx_file_truncate_release

Tronca i file e rilascia i cluster

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a>Descrizione

Questo servizio tronca le dimensioni del file alle dimensioni specificate. Se le dimensioni specificate sono maggiori delle dimensioni effettive del file, questo servizio non esegue alcun'operazione. A differenza ***del fx_file_truncate,*** questo servizio rilascia tutti i cluster inutilizzati.

> [!WARNING]
> *Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*

Per operare oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_truncate_release*.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore a un file aperto in precedenza.
- **size:** nuove dimensioni del file. I byte oltre le nuove dimensioni del file vengono eliminati.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Troncamento del file riuscito.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.
- **FX_PTR_ERROR** (0x18) Puntatore di file non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_write"></a>fx_file_write

Scrive byte nel file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a>Descrizione

Questo servizio scrive byte dal buffer specificato a partire dalla posizione corrente del file. Al termine della scrittura, il puntatore di lettura interno del file viene regolato in modo che punti al byte successivo nel file.

> [!WARNING]
> *Si ottiene prestazioni più veloci se il buffer di origine si trova su un limite di parole lunghe e le dimensioni richieste sono divisibile in modo uniforme in base a sizeof(**ULONG**).*

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **buffer_ptr:** puntatore al buffer di origine per la scrittura.
- **size**: numero di byte da scrivere.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Scrittura file riuscita.
- **FX_NOT_OPEN** (0x07) Il file specificato non è aperto.
- **FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.
- **FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio nel supporto per eseguire la scrittura.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.
- **FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.
- **FX_PTR_ERROR** (0x18) Puntatore a file o buffer non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate,
- fx_file_attributes_read,
- fx_file_attributes_set,
- fx_file_best_effort_allocate,
- fx_file_close,
- fx_file_create,
- fx_file_date_time_set,
- fx_file_delete,
- fx_file_extended_allocate,
- fx_file_extended_best_effort_allocate,
- fx_file_extended_relative_seek,
- fx_file_extended_seek,
- fx_file_extended_truncate,
- fx_file_extended_truncate_release,
- fx_file_open,
- fx_file_read,
- fx_file_relative_seek,
- fx_file_rename,
- fx_file_seek,
- fx_file_truncate,
- fx_file_truncate_release,
- fx_file_write_notify_set,
- fx_unicode_file_create,
- fx_unicode_file_rename,
- fx_unicode_name_get,
- fx_unicode_short_name_get

## <a name="fx_file_write_notify_set"></a>fx_file_write_notify_set

Imposta la funzione di notifica della scrittura di file

### <a name="prototype"></a>Prototipo

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a>Descrizione

Questo servizio installa la funzione di callback richiamata dopo un'operazione di scrittura di file riuscita.

### <a name="input-parameters"></a>Parametri di input

- **file_ptr:** puntatore al blocco di controllo file.
- **file_write_notify:** funzione di callback di scrittura file da installare. Impostare la funzione di callback su NULL per disabilitare la funzione di callback.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) La funzione di callback è stata installata correttamente.
- **FX_PTR_ERROR** (0x18) file_ptr è NULL.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_media_abort"></a>fx_media_abort

Interrompe le attività multimediali

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio interrompe tutte le attività correnti associate al supporto, inclusa la chiusura di tutti i file aperti, l'invio di una richiesta di interruzione al driver associato e il posizionamento dei supporti in uno stato interrotto. Questo servizio viene in genere chiamato quando vengono rilevati errori di I/O.

> [!WARNING]
> *Il supporto deve essere riaperto per usarlo nuovamente dopo l'esecuzione di un'operazione di interruzione.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Interruzione supporto riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_cache_invalidate"></a>fx_media_cache_invalidate

Invalida la cache del settore logico

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio scarica tutti i settori dirty nella cache e quindi invalida l'intera cache del settore logico.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** Puntatore al blocco di controllo multimediale

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Invalidazione della cache multimediale riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto non valido o puntatore scratch.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_check"></a>fx_media_check

Verifica la presenza di errori nei supporti

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio controlla i supporti specificati per verificare la presenza di errori strutturali di base, tra cui collegamenti incrociati di file/directory, catene FAT non valide e cluster persi. Questo servizio offre anche la possibilità di correggere gli errori rilevati.

Il fx_media_check richiede memoria scratch per l'analisi approfondita delle directory e dei file nei supporti. In particolare, la memoria scratch fornita al servizio di controllo dei supporti deve essere sufficientemente grande da contenere diverse voci di directory, una struttura di dati per "impilare" la posizione corrente delle voci di directory prima di entrare nelle sottodirectory e infine la mappa di bit FAT logica. La memoria scratch deve essere di almeno 512-1024 byte più memoria per la mappa di bit FAT logica, che richiede tutti i bit quanti sono i cluster nei supporti. Ad esempio, un dispositivo con 8000 cluster richiederebbe 1000 byte per rappresentare e quindi un'area scratch totale nell'ordine di 2048 byte.

> [!WARNING]
> *Questo servizio deve essere chiamato solo immediatamente dopo fx_media_open e senza altre file system attività.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **scratch_memory_ptr:** puntatore all'inizio della memoria scratch.
- **scratch_memory_size:** dimensioni della memoria scratch in byte.
- **error_correction_option:** bit dell'opzione di correzione degli errori, quando il bit è impostato, viene eseguita la correzione degli errori. I bit dell'opzione di correzione degli errori sono definiti come segue:
  - FX_FAT_CHAIN_ERROR (0x01)
  - FX_DIRECTORY_ERROR (0x02)
  - FX_LOST_CLUSTER_ERROR (0x04) Semplicemente O insieme alle opzioni di correzione degli errori necessarie. Se non è necessaria alcuna correzione degli errori, deve essere specificato il valore 0.
- **errors_detected_ptr**: destinazione per i bit di rilevamento degli errori, come definito di seguito:
  - FX_FAT_CHAIN_ERROR (0x01)
  - FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)
  - FX_FILE_SIZE_ERROR (0x08)

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Controllo dei supporti riuscito, visualizzare la destinazione degli errori rilevati per informazioni dettagliate.
- **FX_ACCESS_ERROR** (0x06) Impossibile eseguire il controllo con i file aperti.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NO_MORE_SPACE** (0x0A) Nessun altro spazio sul supporto.
- **FX_NOT_ENOUGH_MEMORY** (0x91) La memoria scratch fornita non è sufficientemente grande.
- **FX_ERROR_NOT_FIXED** (0x93) Danneggiamento della directory radice FAT32 che non è stato possibile correzione.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_SECTOR_INVALID** (0x89) Sector non è valido.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore scratch non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
ULONG             detected_errors;
UCHAR             sratch_memory[4096];

/* Check the media and correct all errors. */

status = fx_media_check(&my_media, sratch_memory, 4096,
                        FX_FAT_CHAIN_ERROR |
                        FX_DIRECTORY_ERROR |
                        FX_LOST_CLUSTER_ERROR, &detected_errors);

/* If status is FX_SUCCESS and detected_errors is 0,
    the media was successfully checked and found to be error free. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_close"></a>fx_media_close

Chiude i supporti

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio chiude il supporto specificato. Durante la chiusura del supporto, tutti i file aperti vengono chiusi e tutti i buffer rimanenti vengono scaricati nel supporto fisico.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Chiusura dei supporti completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_close_notify_set"></a>fx_media_close_notify_set

Imposta la funzione media close notify

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a>Descrizione

Questo servizio imposta una funzione di callback di notifica che verrà richiamata dopo la chiusura corretta di un supporto.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **media_close_notify:** la funzione di callback di notifica della chiusura dei supporti deve essere installata. Il passaggio di NULL come funzione di callback disabilita il callback di chiusura del supporto.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) La funzione di callback è stata installata correttamente.
- **FX_PTR_ERROR** (0x18) media_ptr è NULL.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_exfat_format"></a>fx_media_exFAT_format

Formatta i supporti

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_exFAT_format(
    FX_MEDIA *media_ptr,
    VOID (*driver)(FX_MEDIA *media),
    VOID *driver_info_ptr, 
    UCHAR *memory_ptr,
    UINT memory_size, 
    CHAR *volume_name,
    UINT number_of_fats,
    ULONG64 hidden_sectors, 
    ULONG64 total_sectors,
    UINT bytes_per_sector, 
    UINT sectors_per_cluster,
    UINT volume_serial_number, 
    UINT boundary_unit);
```
### <a name="description"></a>Descrizione

Questo servizio formatta i supporti forniti in modo compatibile con exFAT in base ai parametri forniti. Questo servizio deve essere chiamato prima di aprire il supporto.

> [!WARNING]
> *La formattazione di un supporto già formattato cancella in modo efficace tutti i file e le directory presenti nel supporto.*

> [!IMPORTANT]
> *Le dimensioni del volume exFAT devono corrispondere alle dimensioni della partizione (se è presente un layout MBR o GPT) o alle dimensioni dell'intero dispositivo se non è presente alcun layout di partizione (nessun MBR o GPT). In Windows esiste una limitazione per cui il disco exFAT non verrà ricoginato se formattato con alcuni valori dei settori totali inferiori ai settori avialibili*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale. Viene usato solo per fornire alcune informazioni di base necessarie per il funzionamento del driver.
- **driver**: puntatore al driver di I/O per questo supporto. Si tratta in genere dello stesso driver fornito alla chiamata fx_media_open successiva.
- **driver_info_ptr:** puntatore a informazioni facoltative che possono essere utilizzate dal driver di I/O.
- **memory_ptr**: puntatore alla memoria di lavoro per il supporto. memory_size specifica le dimensioni della memoria dei supporti di lavoro. Le dimensioni devono essere almeno le dimensioni del settore del supporto.
- **volume_name**: puntatore alla stringa del nome del volume, che può avere un massimo di 11 caratteri.
- **number_of_fats**: numero di fat nel supporto. L'implementazione corrente supporta un fat sul supporto.
- **hidden_sectors**: numero di settori nascosti prima del settore di avvio del supporto. Questo è tipico quando sono presenti più partizioni.
- **total_sectors**: numero totale di settori nei supporti.
- **bytes_per_sector**: numero di byte per settore, che in genere è 512. FileX richiede che sia un multiplo di 32.
- **sectors_per_cluster**: numero di settori in ogni cluster. Il cluster è l'unità di allocazione minima in un file system FAT.
- **volumne_serial_number:** numero di serie da usare per questo volume.
- **boundary_unit:** dimensioni di allineamento dell'area dati fisica, in numero di settori.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Formato multimediale riuscito.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto, driver o puntatore di memoria non valido.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             sd_card;
UCHAR                 media_memory[512];

/* Format a 64GB SD card with exFAT file system. The media has
    been properly partitioned, with the partition starts from sector 32768.
    For 64GB, there are total of 120913920 sectors, each sector 512 bytes. */

status = fx_media_exFAT_format(&sd_card, _fx_sd_driver,
                                driver_information, media_memory,
                                sizeof(media_memory),
                                "exFAT_DISK" /* Volume Name */,
                                1 /* Number of FATs */,
                                32768 /* Hidden sectors */,
                                120913920 /* Total sectors */,
                                512 /* Sector size */,
                                256 /* Sectors per cluster */,
                                12345 /* Volume ID */,
                                8192 /* Boundary unit */);

/* If status is FX_SUCCESS, the media was successfully formatted. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_extended_space_available"></a>fx_media_extended_space_available

Restituisce lo spazio multimediale disponibile

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio restituisce il numero di byte disponibili nel supporto.

Questo servizio è progettato per exFAT. Il puntatore *available_bytes* parametro accetta un valore integer a 64 bit, che consente al chiamante di usare supporti oltre l'intervallo di 4 GB.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un supporto aperto in precedenza.
- **available_bytes_ptr:** byte disponibili rimasti nel supporto.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) È stato recuperato lo spazio disponibile nel supporto.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido o puntatore byte disponibili è NULL.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_flush"></a>fx_media_flush

Scarica i dati nei supporti fisici

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio scarica tutti i settori memorizzati nella cache e le voci di directory di tutti i file modificati nel supporto fisico.

> [!WARNING]
> *Questa routine può essere chiamata periodicamente dall'applicazione per ridurre il rischio di danneggiamento dei file e/o perdita di dati in caso di perdita improvvisa di alimentazione nella destinazione.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Scaricamento dei supporti riuscito.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_FILE_CORRUPT**    file (0x08) è danneggiato.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_format"></a>fx_media_format

Formatta i supporti

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_format(
    FX_MEDIA *media_ptr,
    VOID (*driver)(FX_MEDIA *media),
    VOID *driver_info_ptr,
    UCHAR *memory_ptr, 
    UINT memory_size,
    CHAR *volume_name, 
    UINT number_of_fats,
    UINT directory_entries, 
    UINT hidden_sectors,
    ULONG total_sectors, 
    UINT bytes_per_sector,
    UINT sectors_per_cluster,
    UINT heads,
    UINT sectors_per_track);
```
### <a name="description"></a>Descrizione

Questo servizio formatta i supporti forniti in modo compatibile con FAT 16/16/32 in base ai parametri forniti. Questo servizio deve essere chiamato prima di aprire il supporto.

> [!WARNING]
> *La formattazione di un supporto già formattato cancella in modo efficace tutti i file e le directory presenti nel supporto.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale. Viene usato solo per fornire alcune informazioni di base necessarie per il funzionamento del driver.
- **driver:** puntatore al driver di I/O per questo supporto. Si tratta in genere dello stesso driver fornito alla chiamata fx_media_open successiva.
- **driver_info_ptr:** puntatore a informazioni facoltative che possono essere utilizzate dal driver di I/O.
- **memory_ptr:** puntatore alla memoria di lavoro per il supporto.
- **memory_size**: specifica le dimensioni della memoria del supporto di lavoro. Le dimensioni devono essere almeno le dimensioni del settore del supporto.
- **volume_name:** puntatore alla stringa del nome del volume, che contiene un massimo di 11 caratteri.
- **number_of_fats**: numero di fat nei supporti. Il valore minimo è 1 per la fat primaria. I valori maggiori di 1 comportano la manutenzione di copie FAT aggiuntive in fase di esecuzione.
- **directory_entries**: numero di voci di directory nella directory radice.
- **hidden_sectors**: numero di settori nascosti prima del settore di avvio del supporto. Questo è tipico quando sono presenti più partizioni.
- **total_sectors**: numero totale di settori nei supporti.
- **bytes_per_sector**: numero di byte per settore, che in genere è 512. FileX richiede che sia un multiplo di 32.
- **sectors_per_cluster**: numero di settori in ogni cluster. Il cluster è l'unità di allocazione minima in un file system FAT.
- **heads:** numero di teste fisiche.
- **sectors_per_track**: numero di settori per traccia.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Formato multimediale riuscito.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto, driver o puntatore di memoria non valido.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         ram_disk;
UCHAR             media_memory[512];
UCHAR             ram_disk_memory[32768];

/* Format a RAM disk with 32768 bytes and 512 bytes per sector. */

status = fx_media_format(&ram_disk, _fx_ram_driver,
                         ram_disk_memory, media_memory,
                         sizeof(media_memory),
                         "MY_RAM_DISK" /* Volume Name */,
                         1 /* Number of FATs */,
                         32 /* Directory Entries */,
                         0 /* Hidden sectors */,
                         64 /* Total sectors */,
                         512 /* Sector size */,
                         1 /* Sectors per cluster */,
                         1 /* Heads */,
                         1 /* Sectors per track */);

/* If status is FX_SUCCESS, the media was successfully formatted
    and can now be opened with the following call: */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_open"></a>fx_media_open

Apre i supporti per l'accesso ai file

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a>Descrizione

Questo servizio apre un supporto per l'accesso ai file usando il driver di I/O fornito.

> [!WARNING]
> *La memoria fornita a questo servizio viene usata per implementare una cache del settore logico interno, di conseguenza, maggiore sarà la quantità di memoria fornita, maggiore sarà l'I/O fisico. FileX richiede una cache di almeno un settore logico (byte per settore del supporto).*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **media_name:** puntatore al nome del supporto.
- **media_driver:** puntatore al driver di I/O per questo supporto. Il driver di I/O deve essere conforme ai requisiti del driver FileX definiti nel capitolo 5.
- **driver_info_ptr**: puntatore a informazioni facoltative che possono essere utilizzate dal driver di I/O fornito.
- **memory_ptr**: puntatore alla memoria di lavoro per il supporto.
- **memory_size**: specifica le dimensioni della memoria dei supporti di lavoro. Le dimensioni devono essere grandi quanto le dimensioni del settore dei supporti (in genere 512 byte).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) I supporti sono stati aperti correttamente.
- **FX_BOOT_ERROR** (0x01) Errore durante la lettura del settore di avvio del supporto.
- **FX_MEDIA_INVALID** (0x02) Il settore di avvio del supporto specificato è danneggiato o non valido. Inoltre, questo codice restituito viene usato per indicare che la dimensione della cache del settore logico o la dimensione della voce FAT non è una potenza di 2.
- **FX_FAT_READ_ERROR** (0x03) Errore durante la lettura del file fat multimediale.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Uno o più puntatori sono NULL.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_open_notify_set"></a>fx_media_open_notify_set

Imposta la funzione di notifica dell'apertura dei supporti

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a>Descrizione

Questo servizio imposta una funzione di callback di notifica che verrà richiamata dopo l'apertura di un supporto.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **media_open_notify:** funzione di callback di notifica dell'apertura dei supporti da installare. Il passaggio di NULL come funzione di callback disabilita il callback di apertura dei supporti.

### <a name="return-values"></a>Valori restituiti


- **FX_SUCCESS** (0x00) Correttamente installata la funzione di callback.
- **FX_PTR_ERROR** (0x18) media_ptr è NULL.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_read"></a>fx_media_read

Legge il settore logico dai supporti

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio legge un settore logico dal supporto e lo inserisce nel buffer fornito.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un supporto aperto in precedenza.
- **logical_sector**: settore logico da leggere.
- **buffer_ptr:** puntatore alla destinazione per il settore logico letto.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Lettura dei supporti riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore al buffer non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_space_available"></a>fx_media_space_available

Restituisce lo spazio multimediale disponibile

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il numero di byte disponibili nel supporto.

Per usare supporti di dimensioni superiori a 4 GB, l'applicazione deve usare il *fx_media_extended_space_available*.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un supporto aperto in precedenza.
- **available_bytes_ptr:** byte disponibili rimasti nel supporto.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) È stato restituito spazio disponibile nel supporto.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido o puntatore byte disponibili è NULL.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_volume_get"></a>fx_media_volume_get

Ottiene il nome del volume multimediale

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il nome del volume del supporto aperto in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **volume_name:** puntatore alla destinazione per il nome del volume. Si noti che la destinazione deve essere almeno sufficientemente grande da contenere 12 caratteri.
- **volume_source**: indica dove recuperare il nome, dal settore di avvio o dalla directory radice. I valori validi per questo parametro sono:
  - FX_BOOT_SECTOR
  - FX_DIRECTORY_SECTOR

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Volume multimediale riuscito.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** volume (0x04) non trovato.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione del volume non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_volume_get_extended"></a>fx_media_volume_get_extended

Ottiene il nome del volume multimediale dei supporti aperti in precedenza

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il nome del volume del supporto aperto in precedenza.

> [!IMPORTANT]
> Questo servizio è identico a ***fx_media_volume_get()** _ ad eccezione del fatto che il chiamante passa le dimensioni del buffer _ *volume_name** .

### <a name="input-parameters"></a>Parametri di input


- **media_ptr:** puntatore al blocco di controllo multimediale.
- **volume_name:** puntatore alla destinazione per il nome del volume. Si noti che la destinazione deve essere sufficientemente grande da contenere 12 caratteri.
- **volume_name_buffer_length**: dimensioni del buffer volume_name buffer.
- **volume_source**: indica dove recuperare il nome, dal settore di avvio o dalla directory radice. I valori validi per questo parametro sono:
  - FX_BOOT_SECTOR
  - FX_DIRECTORY_SECTOR

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Volume multimediale riuscito.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** volume (0x04) non trovato.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione del volume non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_volume_set"></a>fx_media_volume_set

Imposta il nome del volume multimediale

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a>Descrizione

Questo servizio imposta il nome del volume del supporto aperto in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **volume_name:** puntatore al nome del volume.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Set di volumi multimediali riuscito.
- **FX_INVALID_NAME** (0x0C) Volume_name non è valido.
- **FX_MEDIA_INVALID** (0x02) Impossibile impostare il nome del volume.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Supporto o puntatore nome volume non valido.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_write
- fx_system_initialize

## <a name="fx_media_write"></a>fx_media_write

Scrive un settore logico

### <a name="prototype"></a>Prototipo

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio scrive il buffer fornito nel settore logico specificato.

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore a un supporto aperto in precedenza.
- **logical_sector:** settore logico da scrivere.
- **buffer_ptr:** puntatore all'origine per la scrittura del settore logico.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Scrittura di supporti riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.
- **FX_CALLER_ERROR**    (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             my_media;
UCHAR                 my_buffer[128];
UINT                 status;

/* Write logical sector 22 from "my_buffer" assuming
    the physical media has a sector size of 128. */

status = fx_media_write(&my_media, 22, my_buffer);

/* If status equals FX_SUCCESS, the contents of logical
    sector 22 are now the same as "my_buffer." */
```

### <a name="see-also"></a>Vedere anche

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_system_initialize

## <a name="fx_system_date_get"></a>fx_system_date_get

Ottiene file system data

### <a name="prototype"></a>Prototipo

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a>Descrizione

Questo servizio restituisce la data di sistema corrente.

### <a name="input-parameters"></a>Parametri di input

- **year:** puntatore alla destinazione per l'anno.
- **month:** puntatore alla destinazione per month.
- **day:** puntatore alla destinazione per il giorno.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero data riuscito.
- **FX_PTR_ERROR** (0x18) Uno o più parametri di input sono NULL.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT            status;
UINT            year;
UINT            month;
UINT            day;
/* Retrieve the current system date. */

status = fx_system_date_get(&year, &month, &day);

/* If status equals FX_SUCCESS, the year, month,
    and day parameters now have meaningful information. */
```

### <a name="see-also"></a>Vedere anche

- fx_system_date_set
- fx_system_initialize
- fx_system_time_get
- fx_system_time_set

## <a name="fx_system_date_set"></a>fx_system_date_set

Imposta la data di sistema

### <a name="prototype"></a>Prototipo

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la data di sistema come specificato.

> [!WARNING]
> *Questo servizio deve essere  chiamato subito dopo l'fx_system_initialize per impostare la data di sistema iniziale. Per impostazione predefinita, la data di sistema è quella dell'ultima versione generica di FileX.*

### <a name="input-parameters"></a>Parametri di input

- **year:** anno nuovo. L'intervallo valido è compreso tra il 1980 e l'anno 2107.
- **month:** nuovo mese. L'intervallo valido è compreso tra 1 e 12.
- **day**: nuovo giorno. L'intervallo valido è compreso tra 1 e 31, a seconda delle condizioni del mese e dell'anno bisestile.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Data riuscita.
- **FX_INVALID_YEAR** (0x12) Anno non valido specificato.
- **FX_INVALID_MONTH** (0x13) Mese non valido specificato.
- **FX_INVALID_DAY** (0x14) Giorno non valido specificato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a>Vedere anche

- fx_system_date_get
- fx_system_initialize
- fx_system_time_get
- fx_system_time_set

## <a name="fx_system_initialize"></a>fx_system_initialize

Inizializza l'intero sistema

### <a name="prototype"></a>Prototipo

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza tutte le principali strutture di dati FileX. Deve essere chiamato  in tx_application_define o possibilmente da un thread di inizializzazione e deve essere chiamato prima di usare qualsiasi altro servizio FileX.

> [!WARNING]
> *Una volta inizializzata da questa chiamata, l'applicazione deve chiamare fx_system_date_set _ e _ fx_system_time_set * per iniziare con una data e un'ora *di sistema accurate.*

### <a name="input-parameters"></a>Parametri di input

Nessuno

### <a name="return-values"></a>Valori restituiti

Nessuno.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
void tx_application_define(VOID *free_memory)
{
    UINT status;
    /* Initialize the FileX system. */
    fx_system_initialize();
    /* Set the file system date. */
    fx_system_date_set(my_year, my_month, my_day);

    /* Set the file system time. */
    fx_system_time_set(my_hour, my_minute, my_second);

    /* Now perform all other initialization and possibly FileX media
        open calls if the corresponding driver does not block on the boot sector read. */

    ...

}
```

### <a name="see-also"></a>Vedere anche

- fx_system_date_get
- fx_system_date_set
- fx_system_time_get
- fx_system_time_set

## <a name="fx_system_time_get"></a>fx_system_time_get

Ottiene l'ora di sistema corrente

### <a name="prototype"></a>Prototipo

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'ora di sistema corrente.

### <a name="input-parameters"></a>Parametri di input

- **hour:** puntatore alla destinazione per hour.
- **minute:** puntatore alla destinazione per minute.
- **second:** puntatore alla destinazione per second.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero dell'ora di sistema riuscito.
- **FX_PTR_ERROR** (0x18) Uno o più parametri di input

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT             status;
UINT             hour;
UINT             minute;
UINT             second;

/* Retrieve the current system time. */

status = fx_system_time_get(&hour, &minute, &second);

/* If status equals FX_SUCCESS, the current system time
    is in the hour, minute, and second variables. */
```

### <a name="see-also"></a>Vedere anche

- fx_system_date_get
- fx_system_date_set
- fx_system_initialize
- fx_system_time_set

## <a name="fx_system_time_set"></a>fx_system_time_set

Imposta l'ora di sistema corrente

### <a name="prototype"></a>Prototipo

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'ora di sistema corrente su quella specificata dai parametri di input.

> [!WARNING]
> *Questo servizio deve essere chiamato subito dopo **l'fx_system_initialize** per impostare l'ora di sistema iniziale. Per impostazione predefinita, l'ora di sistema è 0:0:0.*

### <a name="input-parameters"></a>Parametri di input

- **hour**: nuova ora (0-23).
- **minute**: nuovo minuto (0-59).
- **second**: nuovo secondo (0-59).

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero dell'ora di sistema riuscito.
- **FX_INVALID_HOUR**    (0x15) Nuova ora non è valida.
- **FX_INVALID_MINUTE** (0x16) Nuovo minuto non valido.
- **FX_INVALID_SECOND** (0x17) Nuovo secondo non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a>Vedere anche

- fx_system_date_get
- fx_system_date_set
- fx_system_initialize
- fx_system_time_get

## <a name="fx_unicode_directory_create"></a>fx_unicode_directory_create

Crea una directory Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a>Descrizione

Questo servizio crea una sottodirectory con nome Unicode nella directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome di origine Unicode. In caso di esito positivo, il nome breve (formato 8.3) della sottodirectory Unicode appena creata viene restituito dal servizio.

> [!WARNING]
> *Tutte le operazioni sulla sottodirectory Unicode (che lo rende il percorso predefinito, l'eliminazione e così via) devono essere eseguite fornendo il nome breve restituito (formato 8.3) ai servizi directory FileX standard.*

> [!IMPORTANT]
> *Questo servizio non è supportato nei supporti exFAT.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **source_unicode_name**: puntatore al nome Unicode per la nuova sottodirectory.
- **source_unicode_length**: lunghezza del nome Unicode.
- **short_name**: puntatore alla destinazione per il nome breve (formato 8.3) per la nuova sottodirectory Unicode.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Creazione della directory Unicode riuscita.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_ALREADY_CREATED** (0x0B) La directory specificata esiste già.
- **FX_NO_MORE_SPACE** (0x0A) Nessun altro cluster disponibile nel supporto per la nuova voce di directory.
- **FX_NOT_IMPLEMENTED** (0x22) non implementato per le file system exFAT.
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Supporti o puntatori del nome non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.
- **FX_IO_ERROR (0x90)** Errore di I/O del driver.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             ram_disk;
UCHAR                 my_short_name[13];
UCHAR                 my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                         0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                         0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                         0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                         0x63,0x00, 0x00,0x00};

/* Create a Unicode subdirectory with the name contained in "my_unicode_name". */

length = fx_unicode_directory_create(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the Unicode subdirectory is created and "my_short_name"
    contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_rename

## <a name="fx_unicode_directory_rename"></a>fx_unicode_directory_rename

Rinomina la directory usando una stringa Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a>Descrizione

Questo servizio modifica una sottodirectory con nome Unicode nel nuovo nome Unicode specificato nella directory di lavoro corrente. I parametri del nome Unicode non devono contenere informazioni sul percorso.

> [!IMPORTANT]
> *Questo servizio non è supportato nei supporti exFAT.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **old_unicode_name**: puntatore al nome Unicode per il file corrente.
- **old_unicode_name_length**: lunghezza del nome Unicode corrente.
- **new_unicode_name**: puntatore al nuovo nome file Unicode.
- **old_unicode_name_length**: lunghezza del nuovo nome Unicode.
- **new_short_name**: puntatore alla destinazione per il nome breve (formato 8.3) per il file Unicode rinominato. Rinominare la directory con Unicode

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) I supporti sono stati aperti correttamente.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_ALREADY_CREATED** (0x0B) Il nome di directory specificato esiste già.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Uno o più puntatori sono NULL.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             my_media;
UINT                 status;
UCHAR                 my_short_name[13];
UCHAR                 my_old_unicode_name[] = {'a', '\0', 'b', '\0', 'c', '\0', '\0', '\0'};
UCHAR                 my_new_unicode_name[] = {'d', '\0', 'e', '\0', 'f', '\0', '\0', '\0'};

/* Change the Unicode-named file "abc" to "def". */

status = fx_unicode_directory_rename(&my_media, my_old_unicode_name,
    3, my_new_unicode_name, 3, my_short_name);

/* If status equals FX_SUCCESS, the directory was changed to "def" and
    "my_short_name" contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a>Vedere anche

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create

## <a name="fx_unicode_file_create"></a>fx_unicode_file_create

Crea un file Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a>Descrizione

Questo servizio crea un file con nome Unicode nella directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome di origine Unicode. In caso di esito positivo, il servizio restituire il nome breve (formato 8.3) del file Unicode appena creato.

> [!WARNING]
> *Tutte le operazioni sul file Unicode (apertura, scrittura, lettura, chiusura e così via) devono essere eseguite fornendo il nome breve restituito (formato 8.3) ai servizi file FileX standard.*

### <a name="input-parameters"></a>Parametri di input


- **media_ptr:** puntatore al blocco di controllo multimediale.
- **source_unicode_name**: puntatore al nome Unicode per il nuovo file.
- **source_unicode_length**: lunghezza del nome Unicode.
- **short_name:** puntatore alla destinazione per il nome breve (formato 8.3) per il nuovo file Unicode.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Creazione del file completata.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_ALREADY_CREATED** (0x0B) Il file specificato esiste già.
- **FX_NO_MORE_SPACE** (0x0A) Nessun altro cluster disponibile nel supporto per la nuova voce di file.
- **FX_NOT_IMPLEMENTED** (0x22) non implementato per le file system exFAT.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.
- **FX_PTR_ERROR** (0x18) Supporti o puntatori di nome non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         ram_disk;
UCHAR             my_short_name[13];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Create a Unicode file with the name contained in "my_unicode_name". */

length = fx_unicode_file_create(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the Unicode file is created and "my_short_name"
    contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_file_rename"></a>fx_unicode_file_rename

Rinomina un file usando una stringa Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a>Descrizione

Questo servizio modifica il nome di un file con nome Unicode nel nuovo nome Unicode specificato nella directory predefinita corrente. I parametri del nome Unicode non devono contenere informazioni sul percorso.

> [!IMPORTANT]
> *Questo servizio non è supportato nei supporti exFAT.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **old_unicode_name**: puntatore al nome Unicode per il file corrente.
- **old_unicode_name_length**: lunghezza del nome Unicode corrente.
- **new_unicode_name**: puntatore al nuovo nome file Unicode.
- **new_unicode_name_length**: lunghezza del nuovo nome Unicode.
- **new_short_name**: puntatore alla destinazione per il nome breve (formato 8.3) per il file Unicode rinominato.

### <a name="return-values"></a>Valori restituiti


- **FX_SUCCESS** (0x00) I supporti sono stati aperti correttamente.
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_ALREADY_CREATED** (0x0B) Il nome file specificato esiste già.
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_PTR_ERROR** (0x18) Uno o più puntatori sono NULL.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.
- **FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             my_media;
UINT                 status;
UCHAR                 my_short_name[13];
UCHAR                 my_old_unicode_name[] = {'a', '\0', 'b', '\0', 'c', '\0', '\0', '\0'};
UCHAR                 my_new_unicode_name[] = {'d', '\0', 'e', '\0', 'f', '\0', '\0', '\0'};

/* Change the Unicode-named file "abc" to "def". */

status = fx_unicode_file_rename(&my_media, my_old_unicode_name,
    3, my_new_unicode_name, 3, my_short_name);

/* If status equals FX_SUCCESS, the file name was changed to "def" and
    "my_short_name" contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_length_get"></a>fx_unicode_length_get

Ottiene la lunghezza del nome Unicode

### <a name="prototype"></a>Prototipo

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a>Descrizione

Questo servizio determina la lunghezza del nome Unicode fornito. Un carattere Unicode è rappresentato da due byte. Un nome Unicode è una serie di caratteri Unicode a due byte terminati da due byte NULL (due byte con valore 0).

### <a name="input-parameters"></a>Parametri di input

**unicode_name:** puntatore al nome Unicode.

### <a name="return-values"></a>Valori restituiti

**length:** lunghezza del nome Unicode (numero di caratteri Unicode nel nome).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UCHAR     my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                           0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                           0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                           0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                           0x63,0x00, 0x00,0x00};

UINT     length;

/* Get the length of "my_unicode_name". */

length = fx_unicode_length_get(my_unicode_name);

/* A value of 17 will be returned for the length of the "my_unicode_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_length_get_extended"></a>fx_unicode_length_get_extended

Ottiene la lunghezza del nome Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a>Descrizione

Questo servizio ottiene la lunghezza del nome Unicode fornito. Un carattere Unicode è rappresentato da due byte. Un nome Unicode è una serie di caratteri Unicode di duebyte terminati da due byte NULL (due byte con valore 0).

> [!IMPORTANT]
> *Questo servizio è identico **a fx_unicode_length_get(),** ad eccezione del fatto che il chiamante passa le dimensioni del buffer **unicode_name,** inclusi i due caratteri NULL.*

### <a name="input-parameters"></a>Parametri di input

- **unicode_name:** puntatore al nome Unicode.
- **buffer_length**: dimensioni del buffer dei nomi Unicode.

### <a name="return-values"></a>Valori restituiti

**length:** lunghezza del nome Unicode (numero di caratteri Unicode nel nome).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UCHAR         my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                 0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                 0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                 0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                 0x63,0x00, 0x00,0x00};

UINT         length;

/* Get the length of "my_unicode_name". */

length = fx_unicode_length_get_extended(my_unicode_name, sizeof(my_unicode_name));

/* A value of 17 will be returned for the length of the "my_unicode_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_name_get"></a>fx_unicode_name_get

Ottiene il nome Unicode dal nome breve

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome Unicode associato al nome breve fornito (formato 8.3) all'interno della directory predefinita corrente. Nel parametro nome breve non sono consentite informazioni sul percorso. In caso di esito positivo, il nome Unicode associato al nome breve viene restituito dal servizio.

> [!IMPORTANT]
> *Questo servizio può essere usato per ottenere nomi Unicode sia per i file che per le sottodirectory.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **short_name** Puntatore al nome breve (formato 8.3).
- **destination_unicode_name**: puntatore alla destinazione per il nome Unicode associato al nome breve fornito.
- **destination_unicode_length:** puntatore alla lunghezza del nome Unicode restituita.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero del nome Unicode riuscito.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.
- **FX_FILE_CORRUPT** file (0x08) è danneggiato
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) Nome breve non trovato o dimensioni di destinazione Unicode troppo piccole.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_PTR_ERROR** (0x18) Supporti o puntatori di nome non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA             ram_disk;
UCHAR                 my_unicode_name[256*2];
ULONG                 unicode_name_length;

/* Get the Unicode name associated with the short name "ABC0~111.TXT".
    Note that the Unicode destination must have 2 times the
    number of maximum characters in the name. */

length = fx_unicode_name_get(&ram_disk, "ABC0~111.TXT", my_unicode_name, unicode_name_length);

/* If successful, the Unicode name is returned in "my_unicode_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_short_name_get

## <a name="fx_unicode_name_get_extended"></a>fx_unicode_name_get_extended

Ottiene il nome Unicode dal nome breve

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il nome Unicode associato al nome breve fornito (formato 8.3) all'interno della directory predefinita corrente. Nel parametro nome breve non sono consentite informazioni sul percorso. In caso di esito positivo, il nome Unicode associato al nome breve viene restituito dal servizio.

> [!IMPORTANT]
> *Questo servizio è identico a ***fx_unicode_name_get**, ad eccezione del fatto che il chiamante fornisce le dimensioni del buffer Unicode di destinazione _come argomento di input. Ciò consente al servizio di garantire che non sovrascriverà il buffer Unicode di destinazione_

> [!IMPORTANT]
> *Questo servizio può essere usato per ottenere nomi Unicode sia per i file che per le sottodirectory.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **short_name:** puntatore al nome breve (formato 8.3).
- **destination_unicode_name**: puntatore alla destinazione per il nome Unicode associato al nome breve fornito.
- **destination_unicode_length:** puntatore alla lunghezza del nome Unicode restituita.
- **unicode_name_buffer_length**: dimensioni del buffer dei nomi Unicode. Nota: è necessario un carattere di terminazione NULL, che crea un byte aggiuntivo.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero del nome Unicode riuscito.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) Nome breve non trovato o dimensioni di destinazione Unicode troppo piccole.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_PTR_ERROR** (0x18) Supporti o puntatori nome non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         ram_disk;
UCHAR             my_unicode_name[256*2];
ULONG             unicode_name_length;

/* Get the Unicode name associated with the short name "ABC0~111.TXT".
    Note that the Unicode destination must have 2 times the number of maximum characters in the name. */

length = fx_unicode_name_get_extended(&ram_disk, "ABC0~111.TXT",
    my_unicode_name,&unicode_name_length, sizeof(ny_unicode_name));

/* If successful, the Unicode name is returned in "my_unicode_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_short_name_get

## <a name="fx_unicode_short_name_get"></a>fx_unicode_short_name_get

Ottiene il nome breve dal nome Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

Questo servizio recupera il nome breve (formato 8.3) associato al nome Unicode all'interno della directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome Unicode. In caso di esito positivo, il nome breve associato al nome Unicode viene restituito dal servizio.

> [!IMPORTANT]
> *Questo servizio può essere usato per ottenere nomi brevi sia per i file che per le sottodirectory.*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **source_unicode_name:** puntatore al nome Unicode.
- **source_unicode_length**: lunghezza del nome Unicode.
- **destination_short_name:** puntatore alla destinazione per il nome breve (formato 8.3). Deve avere dimensioni di almeno 13 byte.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero del nome breve riuscito.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) nome Unicode non trovato.
- **FX_NOT_IMPLEMENTED** (0x22) non implementato per l'file system exFAT.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_PTR_ERROR** (0x18) Supporti o puntatori nome non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
FX_MEDIA         ram_disk;
UCHAR             my_short_name[13];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Get the short name associated with the Unicode name contained in the array "my_unicode_name". */

length = fx_unicode_short_name_get(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the short name is returned in "my_short_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get

## <a name="fx_unicode_short_name_get_extended"></a>fx_unicode_short_name_get_extended

Ottiene il nome breve dal nome Unicode

### <a name="prototype"></a>Prototipo

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome breve (formato 8.3) associato al nome Unicode all'interno della directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome Unicode. In caso di esito positivo, il nome breve associato al nome Unicode viene restituito dal servizio.

> [!IMPORTANT]
> *Questo servizio è identico **a fx_unicode_short_name_get(),** ad eccezione del fatto che il chiamante fornisce le dimensioni del buffer di destinazione come argomento di input. Ciò consente al servizio di garantire che il nome breve non superi il buffer di destinazione.*

*Questo servizio può essere usato per ottenere nomi brevi sia per i file che per le sottodirectory*

### <a name="input-parameters"></a>Parametri di input

- **media_ptr:** puntatore al blocco di controllo multimediale.
- **source_unicode_name:** puntatore al nome Unicode.
- **source_unicode_length**: lunghezza del nome Unicode.
- **destination_short_name:** puntatore alla destinazione per il nome breve (formato 8.3). Deve avere dimensioni di almeno 13 byte.
- **short_name_buffer_length**: dimensione del buffer di destinazione. Le dimensioni del buffer devono essere di almeno 14 byte.

### <a name="return-values"></a>Valori restituiti

- **FX_SUCCESS** (0x00) Recupero del nome breve riuscito.
- **FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.
- **FX_FILE_CORRUPT** (0x08) Il file è danneggiato
- **FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).
- **FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.
- **FX_NOT_FOUND** (0x04) nome Unicode non trovato.
- **FX_NOT_IMPLEMENTED** (0x22) non implementato per le file system exFAT.
- **FX_SECTOR_INVALID** (0x89) Settore non valido.
- **FX_PTR_ERROR** (0x18) Supporti o puntatori del nome non validi.
- **FX_CALLER_ERROR** (0x20) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define         SHORT_NAME_BUFFER_SIZE 13
FX_MEDIA         ram_disk;
UCHAR             my_short_name[SHORT_NAME_BUFFER_SIZE];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Get the short name associated with the Unicode name contained in the array "my_unicode_name". */

length = fx_unicode_short_name_get_extended(&ram_disk,
    my_unicode_name, 17, my_short_name,SHORT_NAME_BUFFER_SIZE);

/* If successful, the short name is returned in "my_short_name". */
```

### <a name="see-also"></a>Vedere anche

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get
