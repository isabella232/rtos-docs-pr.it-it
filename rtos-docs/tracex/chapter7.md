---
title: Capitolo 7 - Azure RTOS di traccia FileX
description: Questo capitolo contiene una descrizione degli eventi Azure RTOS FileX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 8668f0867e205afdeab112dfedd257998a5f5b7ff256f27298072dde3e9019b0
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802960"
---
# <a name="chapter-7---azure-rtos-filex-trace-events"></a>Capitolo 7 - Azure RTOS di traccia FileX

Questo capitolo contiene una descrizione degli eventi Azure RTOS FileX. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

**Di seguito è riportato un elenco di eventi FileX visualizzati da TraceX.**

Di seguito viene descritto ogni evento:

| **Icona**                         | **Significato**                               |
| -------------------------------- | ----------------------------------------- |
| ![Icona Internal Logical Sector Cache Miss (Mancata memorizzazione nella cache del settore logico interno)](./media/user-guide/fx-events/image1.png)    | Mancati riscontri nella cache del settore logico interno |
| ![Icona mancata memorizzazione nella cache della directory interna](./media/user-guide/fx-events/image2.png)    | Mancata memorizzazione nella cache della directory interna |
| ![Icona scaricamento supporto interno](./media/user-guide/fx-events/image3.png)    | Scaricamento dei supporti interno |
| ![Icona lettura voce directory interna](./media/user-guide/fx-events/image4.png)    | Lettura voce directory interna |
| ![Icona di scrittura voce di directory interna](./media/user-guide/fx-events/image5.png)    | Internal Directory Entry Write |
| ![Icona di lettura del driver I/O interno](./media/user-guide/fx-events/image6.png)    | Lettura del driver di I/O interno |
| ![Icona di scrittura del driver I/O interno](./media/user-guide/fx-events/image7.png)    | Scrittura del driver di I/O interno |
| ![Icona di scaricamento del driver I/O interno](./media/user-guide/fx-events/image8.png)    | Scaricamento del driver di I/O interno |
| ![Icona di interruzione del driver I/O interno](./media/user-guide/fx-events/image9.png)    | Interruzione interna del driver di I/O |
| ![Icona di inizializzazione del driver I/O interno](./media/user-guide/fx-events/image10.png)    | Inizializzazione del driver di I/O interno |
| ![Icona di lettura di avvio del driver I/O interno](./media/user-guide/fx-events/image11.png)    | Lettura avvio driver I/O interno |
| ![Icona Internal I/O Driver Release Sectors (Settori versione driver I/O interni)](./media/user-guide/fx-events/image12.png)    | Settori di rilascio del driver di I/O interno |
| ![Icona di scrittura di avvio del driver I/O interno](./media/user-guide/fx-events/image13.png)    | Scrittura di avvio del driver di I/O interno |
| ![Icona di annullamento dell'inizializzazione del driver I/O interno](./media/user-guide/fx-events/image14.png)    | Inizializzazione del driver I/O interno |
| ![Icona Lettura attributi directory](./media/user-guide/fx-events/image15.png)    | **Attributi di directory letti** (*fx_directory_attributes_read*) |
| ![Icona Imposta attributi directory](./media/user-guide/fx-events/image16.png)    | **Set di attributi della** directory (*fx_directory_attributes_set*) |
| ![Icona Crea directory](./media/user-guide/fx-events/image17.png)    | **Creazione directory** (*fx_directory_create*) |
| ![Icona Directory Default Get](./media/user-guide/fx-events/image18.png)    | **Directory Default Get** (*fx_directory_default_get*) |
| ![Icona Directory Default Set (Imposta directory predefinita)](./media/user-guide/fx-events/image19.png)    | **Directory Default Set** (*fx_directory_default_set*) |
| ![Icona di eliminazione della directory](./media/user-guide/fx-events/image20.png)    | **Eliminazione directory** (*fx_directory_delete*) |
| ![Icona Directory First Entry Find](./media/user-guide/fx-events/image21.png)    | **Directory First Entry Find** (*fx_directory_first_entry_find*) |
| ![Icona Directory First Full Entry Find](./media/user-guide/fx-events/image22.png)    | **Directory First Full Entry Find** (*fx_directory_first_full_entry_find*) |
| ![Icona Ottieni informazioni directory](./media/user-guide/fx-events/image23.png)    | **Directory Information Get** (*fx_directory_information_get*) |
| ![Icona Directory Local Path Clear (Cancella percorso locale directory)](./media/user-guide/fx-events/image24.png)    | **Cancellazione percorso locale directory** (*fx_directory_local_path_clear*) |
| ![Icona Directory Local Path Get (Ottieni percorso locale directory)](./media/user-guide/fx-events/image25.png)    | **Directory Local Path Get** (*fx_directory_local_path_get*) |
| ![Icona di ripristino del percorso locale della directory](./media/user-guide/fx-events/image26.png)    | **Ripristino del percorso locale della** directory (*fx_directory_local_path_restore*) |
| ![Icona Directory Local Path Set](./media/user-guide/fx-events/image27.png)    | **Directory Local Path Set** (*fx_directory_local_path_set*) |
| ![Icona Directory Long Name Get (Ottieni nome lungo directory)](./media/user-guide/fx-events/image28.png)    | **Directory Long Name Get** (*fx_directory_long_name_get*) |
| ![Icona di test del nome della directory](./media/user-guide/fx-events/image29.png)    | **Test del nome della directory** (*fx_directory_name_test*) |
| ![Icona Directory Next Entry Find (Trova voce successiva directory)](./media/user-guide/fx-events/image30.png)    | **Directory Next Entry Find** (*fx_directory_next_entry_find*) |
| ![Icona Directory Next Full Entry Find](./media/user-guide/fx-events/image31.png)    | **Directory Next Full Entry Find** (*fx_directory_next_full_entry_find*) |
| ![Icona di ridenominazione della directory](./media/user-guide/fx-events/image32.png)    | **Ridenominazione** della directory (*fx_directory_rename*) |
| ![Icona Directory Short Name Get (Ottieni nome breve directory)](./media/user-guide/fx-events/image33.png)    | **Directory Short Name Get** (*fx_directory_short_name_get*) |
| ![Icona Alloca file](./media/user-guide/fx-events/image34.png)    | **Allocazione file** (*fx_file_allocate*) |
| ![Icona Lettura attributi file](./media/user-guide/fx-events/image35.png)    | **Attributi di file letti** (*fx_file_attributes_read*) |
| ![Icona Imposta attributi file](./media/user-guide/fx-events/image36.png)    | **Set di attributi di** file (*fx_file_attributes_set*) |
| ![Icona di allocazione del file con il massimo sforzo](./media/user-guide/fx-events/image37.png)    | **File Best Effort Allocate** (*fx_file_best_effort_allocate*) |
| ![Icona Chiudi file](./media/user-guide/fx-events/image38.png)    | **Chiusura file** (*fx_file_close*) |
| ![Icona Crea file](./media/user-guide/fx-events/image39.png)    | **Creazione file** (*fx_file_create*) |
| ![Icona Set di data e ora file](./media/user-guide/fx-events/image40.png)    | **Set di data e ora del** file (*fx_file_date_time_set*) |
| ![Icona Di eliminazione file](./media/user-guide/fx-events/image41.png)    | **Eliminazione file** (*fx_file_delete*) |
| ![Icona Apri file](./media/user-guide/fx-events/image42.png)    | **File aperto** (*fx_file_open*) |
| ![Icona Di lettura file](./media/user-guide/fx-events/image43.png)    | **Lettura file** (*fx_file_read*) |
| ![Icona Ricerca relativa file](./media/user-guide/fx-events/image44.png)    | **File Relative Seek** (*fx_file_relative_seek*) |
| ![Icona Rinomina file](./media/user-guide/fx-events/image45.png)    | **Ridenominazione** file (*fx_file_rename*) |
| ![Icona Cerca file](./media/user-guide/fx-events/image46.png)    | **File Seek** (*fx_file_seek*) |
| ![Icona Troncamento file](./media/user-guide/fx-events/image47.png)    | **Troncamento file** (*fx_file_truncate*) |
| ![Icona Tronca versione file](./media/user-guide/fx-events/image48.png)    | **Versione troncamento file** (*fx_file_truncate_release*) |
| ![Icona scrittura file](./media/user-guide/fx-events/image49.png)    | **Scrittura file** (*fx_file_write*) |
| ![Icona media abort](./media/user-guide/fx-events/image50.png)    | **Interruzione supporto** (*fx_media_abort*) |
| ![Icona Invalida cache supporti](./media/user-guide/fx-events/image51.png)    | **Invalidazione della cache dei** supporti (*fx_media_cache_invalidate*) |
| ![Icona controllo supporti](./media/user-guide/fx-events/image52.png)    | **Controllo supporti** (*fx_media_check*) |
| ![*Icona Media Close (Chiudi file multimediali)](./media/user-guide/fx-events/image53.png)    | **Media Close** (*fx_media_close*) |
| ![Icona scaricamento supporti](./media/user-guide/fx-events/image54.png)    | **Scaricamento supporti** (*fx_media_flush*) |
| ![Icona Formato multimediale](./media/user-guide/fx-events/image55.png)    | **Formato multimediale** (*fx_media_format*) |
| ![Icona Apri file multimediali](./media/user-guide/fx-events/image56.png)    | **Media Open** (*fx_media_open*) |
| ![Icona Lettura file multimediali](./media/user-guide/fx-events/image57.png)    | **Media Read** (*fx_media_read*) |
| ![Icona Spazio multimediale disponibile](./media/user-guide/fx-events/image58.png)    | **Spazio multimediale disponibile** (*fx_media_space_available*) |
| ![Icona Media Volume Get (Ottieni volume multimediale)](./media/user-guide/fx-events/image59.png)    | **Media Volume Get** (*fx_media_volume_get*) |
| ![Icona del set di volumi multimediali](./media/user-guide/fx-events/image60.png)    | **Set di volumi multimediali** *(fx_media_volume_set*) |
| ![Icona di scrittura multimediale](./media/user-guide/fx-events/image61.png)    | **Media Write** (*fx_media_write*) |
| ![Icona Get data di sistema](./media/user-guide/fx-events/image62.png)    | **System Date Get** (*fx_system_date_get*) |
| ![Icona set di date di sistema](./media/user-guide/fx-events/image63.png)    | **Set di date di** sistema (*fx_system_date_set*) |
| ![Icona di inizializzazione del sistema](./media/user-guide/fx-events/image64.png)    | **Inizializzazione sistema** (*fx_system_initialize*) |
| ![Icona Get dell'ora di sistema](./media/user-guide/fx-events/image65.png)    | **System Time Get** (*fx_system_time_get*) |
| ![Icona set di tempo di sistema](./media/user-guide/fx-events/image66.png)    | **Set di tempo di** sistema (*fx_system_time_set*) |
| ![Icona di creazione directory Unicode](./media/user-guide/fx-events/image67.png)    | **Creazione directory Unicode** (*fx_unicode_directory_create*) |
| ![Icona Rinomina directory Unicode](./media/user-guide/fx-events/image68.png)    | **Ridenominazione della** directory Unicode (*fx_unicode_directory_rename*) |
| ![Icona Di creazione file Unicode](./media/user-guide/fx-events/image69.png)    | **Creazione di file Unicode** (*fx_unicode_file_create*) |
| ![Icona di ridenominazione di file Unicode](./media/user-guide/fx-events/image70.png)    | **Ridenominazione di** file Unicode (*fx_unicode_file_rename*) |
| ![Icona Unicode Lenght Get](./media/user-guide/fx-events/image71.png)    | **Unicode Lenght Get** (*fx_unicode_length_get*) |
| ![Icona Ottieni nome Unicode](./media/user-guide/fx-events/image72.png)    | **Unicode Name Get** (*fx_unicode_name_get*) |
| ![Icona Ottieni nome breve Unicode](./media/user-guide/fx-events/image73.png)    | **Unicode Short Name Get** (*fx_unicode_short_name_get*) |

## <a name="event-descriptions"></a>Descrizioni di eventi

Di seguito viene descritto ogni singolo evento.

### <a name="internal-logical-sector-cache-miss"></a>Mancati riscontri nella cache del settore logico interno 

#### <a name="internal-logical-sector-cache-miss"></a>Mancati riscontri nella cache del settore logico interno

**Icona** ![ Icona mancata memorizzazione nella cache del settore logico interno](./media/user-guide/fx-events/image1.png)

**Descrizione**

Questo evento rappresenta un mancato riscontri nella cache del settore logico FileX interno.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Settore.
- Campo informazioni 3: mancati in totale.
- Campo informazioni 4: dimensioni della cache.

### <a name="internal-directory-cache-miss"></a>Mancata memorizzazione nella cache della directory interna

#### <a name="internal-directory-cache-miss"></a>Mancati riscontri nella cache della directory interna

**Icona** ![ Icona mancata memorizzazione nella cache della directory interna](./media/user-guide/fx-events/image2.png)

**Descrizione** 

Questo evento rappresenta un mancato riscontri nella cache della directory FileX interna.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: mancati in totale.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-media-flush"></a>Scaricamento dei supporti interno 

#### <a name="internal-media-flush"></a>Scaricamento dei supporti interno

**Icona** ![ Icona di scaricamento del supporto interno](./media/user-guide/fx-events/image3.png)

**Descrizione**

Questo evento rappresenta uno scaricamento di supporti FileX interno.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: numero di settori dirty.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.


### <a name="internal-directory-entry-read"></a>Lettura voce directory interna 

#### <a name="internal-directory-entry-read"></a>Lettura della voce della directory interna

**Icona** ![ Icona di lettura voce di directory interna](./media/user-guide/fx-events/image4.png)

**Descrizione**

Questo evento rappresenta un evento interno di lettura della voce di directory FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-directory-entry-write"></a>Internal Directory Entry Write

#### <a name="internal-directory-entry-write"></a>Scrittura di voci di directory interne

**Icona** ![ Icona di scrittura voce di directory interna](./media/user-guide/fx-events/image5.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura interno della voce di directory FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-read"></a>Lettura del driver di I/O interno 

#### <a name="internal-io-driver-read"></a>Lettura del driver di I/O interno 

**Icona** ![ Icona di lettura del driver I/O interno](./media/user-guide/fx-events/image6.png)

**Descrizione** 

Questo evento rappresenta un evento di lettura interno del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Settore.
- Campo informazioni 3: numero di settori.
- Campo informazioni 4: puntatore del buffer.

### <a name="internal-io-driver-write"></a>Scrittura del driver di I/O interno 

#### <a name="internal-io-driver-write"></a>Scrittura del driver di I/O interno 

**Icona** ![ Icona di scrittura del driver I/O interno](./media/user-guide/fx-events/image7.png)

**Descrizione** 

Questo evento rappresenta un evento di scrittura interno del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Settore.
- Campo informazioni 3: numero di settori.
- Campo informazioni 4: puntatore del buffer.

### <a name="internal-io-driver-flush"></a>Scaricamento del driver di I/O interno 

#### <a name="internal-io-driver-flush"></a>Scaricamento del driver di I/O interno 

**Icona** ![ Icona di scaricamento del driver I/O interno](./media/user-guide/fx-events/image8.png)

**Descrizione** 

Questo evento rappresenta un evento di scaricamento interno del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-abort"></a>Interruzione interna del driver di I/O 

#### <a name="internal-io-dirver-abort"></a>Interruzione interna del dirver I/O

**Icona** ![ Icona di interruzione del driver I/O interno](./media/user-guide/fx-events/image9.png)

**Descrizione**

Questo evento rappresenta un evento interno di interruzione del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-initialize"></a>Inizializzazione del driver di I/O interno 

#### <a name="internal-io-driver-initialize"></a>Inizializzazione del driver di I/O interno 

**Icona** ![ Icona di inizializzazione del driver I/O interno](./media/user-guide/fx-events/image10.png)

**Descrizione** 

Questo evento rappresenta un evento di inizializzazione interno del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-boot-sector-read"></a>Lettura del settore di avvio del driver di I/O interno 

#### <a name="internal-io-driver-boot-sector-read"></a>Lettura del settore di avvio del driver di I/O interno 

**Icona** ![ Icona di lettura del settore di avvio del driver I/O interno](./media/user-guide/fx-events/image11.png)

**Descrizione** 

Questo evento rappresenta un evento interno di lettura del settore di avvio del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore del buffer.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-release-sectors"></a>Settori di rilascio del driver di I/O interno 

#### <a name="internal-io-driver-release-sectors"></a>Settori interni di rilascio del driver di I/O 

**Icona** ![ Icona dei settori di rilascio del driver I/O interno](./media/user-guide/fx-events/image12.png)

**Descrizione** 

Questo evento rappresenta un evento interno dei settori di rilascio del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Settore.
- Campo informazioni 3: numero di settori.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-boot-sector-write"></a>Scrittura del settore di avvio del driver di I/O interno

#### <a name="internal-io-driver-boot-sector-write"></a>Scrittura del settore di avvio del driver di I/O interno 

**Icona** ![ Icona di scrittura del settore di avvio del driver I/O interno](./media/user-guide/fx-events/image13.png)

**Descrizione** 

Questo evento rappresenta un evento interno di scrittura del settore di avvio del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore del buffer.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="internal-io-driver-un-initialize"></a>Inizializzazione del driver di I/O interno 

#### <a name="internal-io-driver-un-initialize"></a>Annullamento dell'inizializzazione del driver di I/O interno 

**Icona** ![ Icona di annullamento dell'inizializzazione del driver I/O interno](./media/user-guide/fx-events/image14.png)

**Descrizione** 

Questo evento rappresenta un evento interno di annullamento dell'inizializzazione del driver di I/O FileX.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.
</blockquote></td>

### <a name="directory-attributes-read"></a>Attributi della directory letti 

#### <a name="fx_directory_attributes_read"></a>fx_directory_attributes_read 

**Icona** ![ Icona lettura attributi directory](./media/user-guide/fx-events/image15.png)

**Descrizione** 

Questo evento rappresenta un evento di lettura degli attributi della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Mapping di bit degli attributi:

  | Attributo                         | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | (0x01)  |
  |  Nascosto                           | (0x02)  |
  |  Sistema                           | (0x04)  |
  |  Volume                           | (0x08)  |
  |  Directory                        | (0x10)  |
  |  Archiviazione                          | (0x20)  |
- Campo informazioni 4: Non usato.

### <a name="directory-attributes-set"></a>Set di attributi della directory 

#### <a name="fx_directory_attributes_set"></a>fx_directory_attributes_set 

**Icona** ![ Icona del set di attributi](./media/user-guide/fx-events/image16.png)

**Descrizione** 

Questo evento rappresenta una directory un evento di impostazione degli attributi della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Mapping di bit degli attributi:

  |  Attributo                        | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | (0x01)  |
  |  Nascosto                           | (0x02)  |
  |  Sistema                           | (0x04)  |
  |  Archiviazione                          | (0x20)  |
- Campo informazioni 4: Non usato.

### <a name="directory-create"></a>Creazione directory 

#### <a name="fx_directory_create"></a>fx_directory_create

**Icona** ![ Icona di creazione della directory](./media/user-guide/fx-events/image17.png)

**Descrizione** 

Questo evento rappresenta un evento di creazione directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-default-get"></a>Directory Default Get 

#### <a name="fx_directory_default_get"></a>fx_directory_default_get 

**Icona** ![ Icona ottieni predefinita directory](./media/user-guide/fx-events/image18.png)

**Descrizione** 

Questo evento rappresenta un evento di impostazione predefinito della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome del percorso restituito.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-default-set"></a>Directory Default Set 

#### <a name="fx_directory_default_set"></a>fx_directory_default_set 

**Icona** ![ Icona del set predefinito della directory](./media/user-guide/fx-events/image19.png)

**Descrizione** 

Questo evento rappresenta un evento di impostazione predefinito della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nuovo nome di percorso predefinito.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-delete"></a>Eliminazione directory 

#### <a name="fx_directory_delete"></a>fx_directory_delete

**Icona** ![ Icona di eliminazione della directory](./media/user-guide/fx-events/image20.png)

**Descrizione** 

Questo evento rappresenta un evento di eliminazione della directory.

**Campi di informazioni**
- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-first-entry-find"></a>Directory First Entry Find 

#### <a name="fx_directory_first_entry_find"></a>fx_directory_first_entry_find

**Icona** ![ Icona di ricerca della prima voce della directory](./media/user-guide/fx-events/image21.png)

**Descrizione** 

Questo evento rappresenta un evento di ricerca della prima voce della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-first-full-entry-find"></a>Directory First Full Entry Find 

#### <a name="fx_directory_first_full_entry_find"></a>fx_directory_first_full_entry_find

**Icona** ![ Icona di ricerca della prima voce completa della directory](./media/user-guide/fx-events/image22.png)

**Descrizione** 

Questo evento rappresenta un evento di ricerca della prima voce completa della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-information-get"></a>Ottenere informazioni sulla directory 

#### <a name="fx_directory_information_get"></a>fx_directory_information_get

**Icona** ![ Icona ottieni informazioni directory](./media/user-guide/fx-events/image23.png)

**Descrizione** 

Questo evento rappresenta un evento get di informazioni sulla directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-local-path-clear"></a>Cancellazione percorso locale directory 

#### <a name="fx_directory_local_path_clear"></a>fx_directory_local_path_clear

**Icona** ![ Icona di cancellazione del percorso locale della directory](./media/user-guide/fx-events/image24.png)

**Descrizione** 

Questo evento rappresenta un evento di cancellazione del percorso locale della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-local-path-get"></a>Directory Local Path Get 

#### <a name="fx_directory_local_path_get"></a>fx_directory_local_path_get

**Icona** ![ Icona di get del percorso locale della directory](./media/user-guide/fx-events/image25.png)

**Descrizione** 

Questo evento rappresenta un evento get del percorso locale della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome del percorso restituito.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-local-path-restore"></a>Ripristino del percorso locale della directory 

#### <a name="fx_directory_local_path_restore"></a>fx_directory_local_path_restore

**Icona** ![ Icona di ripristino del percorso locale della directory](./media/user-guide/fx-events/image26.png)

**Descrizione** 

Questo evento rappresenta un evento di ripristino del percorso locale della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore alla struttura del percorso locale.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-local-path-set"></a>Directory Local Path Set 

#### <a name="fx_directory_local_path_set"></a>fx_directory_local_path_set

**Icona** ![ Icona del set di percorsi locali della directory](./media/user-guide/fx-events/image27.png)

**Descrizione** 

Questo evento rappresenta un evento di impostazione del percorso locale della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore alla struttura del percorso locale.
- Campo informazioni 3: puntatore al nuovo nome del percorso.
- Campo informazioni 4: Non usato.

### <a name="directory-long-name-get"></a>Directory Long Name Get 

#### <a name="fx_directory_long_name_get"></a>fx_directory_long_name_get

**Icona** ![ Icona di get del nome lungo della directory](./media/user-guide/fx-events/image28.png)

**Descrizione** 

Questo evento rappresenta un evento get del nome lungo della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome file breve.
- Campo informazioni 3: puntatore al nome file lungo.
- Campo informazioni 4: Non usato.

### <a name="directory-name-test"></a>Test del nome della directory 

#### <a name="fx_directory_name_test"></a>fx_directory_name_test

**Icona** ![ Icona di test del nome della directory](./media/user-guide/fx-events/image29.png)

**Descrizione** 

Questo evento rappresenta un evento di test del nome della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-next-entry-find"></a>Directory Next Entry Find 

#### <a name="fx_directory_next_entry_find"></a>fx_directory_next_entry_find

**Icona** ![ Icona di ricerca della voce successiva della directory](./media/user-guide/fx-events/image30.png)

**Descrizione** 

Questo evento rappresenta un evento di ricerca della voce successiva della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-next-full-entry-find"></a>Directory Next Full Entry Find 

#### <a name="fx_directory_next_full_entry_find"></a>fx_directory_next_full_entry_find

**Icona** ![ Icona di ricerca voce completa della directory successiva](./media/user-guide/fx-events/image31.png)

**Descrizione**

Questo evento rappresenta un evento di ricerca voce completa successivo della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="directory-rename"></a>Ridenominazione della directory 

#### <a name="fx_directory_rename-event"></a>fx_directory_rename evento

**Icona** ![ Icona di ridenominazione della directory](./media/user-guide/fx-events/image32.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione della directory.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome della directory precedente.
- Campo informazioni 3: puntatore al nome della nuova directory.
- Campo informazioni 4: Non usato.

### <a name="directory-short-name-get"></a>Directory Short Name Get 

#### <a name="fx_directory_short_name_get"></a>fx_directory_short_name_get

**Icona** ![ Icona di ricerca del nome breve della directory](./media/user-guide/fx-events/image33.png)

**Descrizione**

Questo evento rappresenta un evento get del nome breve della directory.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome file lungo.
- Campo informazioni 3: puntatore al nome file breve.
- Campo informazioni 4: Non usato.

### <a name="file-allocate"></a>Allocazione file 

#### <a name="fx_file_allocate"></a>fx_file_allocate

**Icona** ![ Icona di allocazione file](./media/user-guide/fx-events/image34.png)

**Descrizione**

Questo evento rappresenta un evento di allocazione file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Campo informazioni 2: dimensioni richieste.
- Campo informazioni 3: dimensioni correnti.
- Campo informazioni 4: nuove dimensioni.

### <a name="file-attributes-read"></a>Attributi di file letti 

#### <a name="fx_file_attributes_read"></a>fx_file_attributes_read

**Icona** ![ Icona lettura attributi file](./media/user-guide/fx-events/image35.png)

**Descrizione**

Questo evento rappresenta un evento di lettura degli attributi di file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto. 
- Campo informazioni 2: Mapping di bit degli attributi:

  |  Attribut                         | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | (0x01)  |
  |  Nascosto                           | (0x02)  |
  |  Sistema                           | (0x04)  |
  |  Volume                           | (0x08)  |
  |  Directory                        | (0x10)  |
  |  Archiviazione                          | (0x20)  |
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="file-attributes-set"></a>Set di attributi di file 

#### <a name="fx_file_attributes_set"></a>fx_file_attributes_set

**Icona** ![ Icona del set di attributi del file](./media/user-guide/fx-events/image36.png)

**Descrizione** 

Questo evento rappresenta un evento set di attributi di file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome del file. 
- Campo informazioni 3: Mapping di bit degli attributi:

  | Attributo                         | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | (0x01)  |
  |  Nascosto                           | (0x02)  |
  |  Sistema                           | (0x04)  |
  |  Archiviazione                          | (0x20)  |
- Campo informazioni 4: Non usato.

### <a name="file-best-effort-allocate"></a>File Best Effort Allocate 

#### <a name="fx_file_best_effort_allocate"></a>fx_file_best_effort_allocate

**Icona** ![ Icona di allocazione del file con il massimo sforzo](./media/user-guide/fx-events/image37.png)

**Descrizione** 

Questo evento rappresenta un evento di allocazione del file con il massimo sforzo.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Campo informazioni 2: dimensioni richieste.
- Campo informazioni 3: dimensioni effettive allocate.
- Campo informazioni 4: Non usato.

### <a name="file-close"></a>Chiusura file 

#### <a name="fx_file_close"></a>fx_file_close

**Icona** ![ Icona di chiusura file](./media/user-guide/fx-events/image38.png)

**Descrizione** 

Questo evento rappresenta un evento di chiusura del file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Campo informazioni 2: dimensioni del file.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="file-create"></a>Creazione di file

#### <a name="fx_file_create"></a>fx_file_create

**Icona** ![ Icona Di creazione file](./media/user-guide/fx-events/image39.png)

**Descrizione**

Questo evento rappresenta un evento di creazione file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome del file.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="file-date-time-set"></a>Set di data e ora del file 

#### <a name="fx_file_date_time_set"></a>fx_file_date_time_set

**Icona** ![ Icona del set di data e ora del file](./media/user-guide/fx-events/image40.png)

**Descrizione**

Questo evento rappresenta un evento del set di data/ora del file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome file.
- Campo informazioni 3: Anno.
- Campo info 4: Mese.

### <a name="file-delete"></a>Eliminazione file 

#### <a name="fx_file_delete"></a>fx_file_delete

**Icona** ![ Icona Di eliminazione file](./media/user-guide/fx-events/image41.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome file.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="file-open"></a>File aperto 

#### <a name="fx_file_open"></a>fx_file_open

**Icona** ![ Icona Apri file](./media/user-guide/fx-events/image42.png)

**Descrizione**

Questo evento rappresenta un evento di apertura file.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al blocco di controllo file.
- Campo informazioni 3: puntatore al nome del file.
- Campo informazioni 4: Tipo di apertura:

  |  Tipo di apertura                        | Valore        |
  |---------------------------------- | --------|
  |  Apri per lettura                    | (0x00)  |
  |  Apri per scrittura                   | (0x01)  |
  |  Apertura rapida per la lettura               | (0x02)  |

### <a name="file-read"></a>Lettura file 

#### <a name="fx_file_read"></a>fx_file_read

**Icona** ![ Icona Di lettura file](./media/user-guide/fx-events/image43.png)

**Descrizione**

Questo evento rappresenta un evento di lettura file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Campo informazioni 2: puntatore del buffer.
- Info Campo 3: Dimensioni della richiesta.
- Info Campo 4: Dimensioni effettive lette.

### <a name="file-relative-seek"></a>Ricerca relativa al file 

#### <a name="fx_file_relative_seek"></a>fx_file_relative_seek

**Icona** ![ Icona di ricerca relativa al file](./media/user-guide/fx-events/image44.png)

**Descrizione**

Questo evento rappresenta un evento di ricerca relativo al file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Info Campo 2: Offset byte.
- Campo informazioni 3: Cercare da:

  | Event                             | Valore        |
  |---------------------------------- | --------|
  |  Dall'inizio                   | (0x00)  |
  |  Da fine                         | (0x01)  | 
  |  Inoltra                          | (0x02)  |
  |  indietro                         | (0x03)  |
- Info Campo 4: offset precedente.

### <a name="file-rename"></a>Ridenominazione file 

#### <a name="fx_file_rename"></a>fx_file_rename

**Icona** ![ Icona di ridenominazione file](./media/user-guide/fx-events/image45.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome file precedente.
- Campo informazioni 3: puntatore al nuovo nome file.
- Campo info 4: Non usato.

### <a name="file-seek"></a>Ricerca file 

#### <a name="fx_file_seek"></a>fx_file_seek

**Icona** ![ Icona Cerca file](./media/user-guide/fx-events/image46.png)

**Descrizione**

Questo evento rappresenta un evento di ricerca file.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al file.
- Info Campo 2: Offset byte.
- Campo informazioni 3: offset precedente.
- Campo info 4: Non usato.

### <a name="file-truncate"></a>Troncamento file 

#### <a name="fx_file_truncate"></a>fx_file_truncate

**Icona** ![ Icona troncamento file](./media/user-guide/fx-events/image47.png)

**Descrizione**

Questo evento rappresenta un evento di troncamento del file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Info Campo 2: Dimensioni richieste.
- Info Campo 3: Dimensioni precedenti.
- Info Campo 4: Nuova dimensione.

### <a name="file-truncate-release"></a>Versione di troncamento file 

#### <a name="fx_file_truncate_release"></a>fx_file_truncate_release 

**Icona** ![ Icona di rilascio troncamento file](./media/user-guide/fx-events/image48.png)

**Descrizione**

Questo evento rappresenta un evento di rilascio di troncamento del file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Info Campo 2: Dimensioni richieste.
- Info Campo 3: Dimensioni precedenti.
- Info Campo 4: Nuova dimensione.

### <a name="file-write"></a>Scrittura file 

#### <a name="fx_file_write"></a>fx_file_write 

**Icona** ![ Icona scrittura file](./media/user-guide/fx-events/image49.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura file.

**Campi di informazioni**

- Campo informazioni 1: puntatore al file.
- Campo informazioni 2: puntatore del buffer.
- Info Campo 3: Dimensioni della richiesta.
- Info Campo 4: Dimensioni effettive scritte.

### <a name="media-abort"></a>Interruzione del supporto 

#### <a name="fx_media_abort"></a>fx_media_abort 

**Icona** ![ Icona interruzione del supporto](./media/user-guide/fx-events/image50.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="media-cache-invalidate"></a>Invalidazione cache supporti

#### <a name="fx_media_cache_invalidate"></a>fx_media_cache_invalidate

**Icona** ![ Icona invalida cache multimediale](./media/user-guide/fx-events/image51.png)

**Descrizione**

Questo evento rappresenta un evento invalidato nella cache multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="media-check"></a>Controllo supporti 

#### <a name="fx_media_check"></a>fx_media_check

**Icona** ![ Icona di controllo dei supporti](./media/user-guide/fx-events/image52.png)

**Descrizione**

Questo evento rappresenta un evento di controllo dei supporti.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: Puntatore di memoria scratch.
- Info Campo 3: Dimensioni memoria scratch.
- Campo informazioni 4: Mappa di bit degli errori:

  | Tipo di errore                        | Valore        |
  |---------------------------------- | --------|
  |  Errore della catena FAT                  | (0x01)  |
  |  Errore di directory                  | (0x02)  |
  |  Errore del cluster perso               | (0x04)  |
  |  Errore di dimensione del file                  | (0x08)  |

### <a name="media-close"></a>Chiusura dei supporti 

#### <a name="fx_media_close"></a>fx_media_close

**Icona** ![ Icona Di chiusura del supporto](./media/user-guide/fx-events/image53.png)

**Descrizione**

Questo evento rappresenta un evento di chiusura dei supporti.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="media-flush"></a>Scaricamento dei supporti 

#### <a name="fx_media_flush"></a>fx_media_flush

**Icona** ![ Icona scaricamento supporti](./media/user-guide/fx-events/image54.png)

**Descrizione**

Questo evento rappresenta un evento di scaricamento dei supporti.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="media-format"></a>Formato multimediale 

#### <a name="fx_media_format"></a>fx_media_format

**Icona** ![ Icona formato multimediale](./media/user-guide/fx-events/image55.png)

**Descrizione**

Questo evento rappresenta un evento di formato multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Info Campo 2: numero di voci radice.
- Campo informazioni 3: Settori.
- Campo informazioni 4: Settori per cluster.

### <a name="media-open"></a>File multimediali aperti 

#### <a name="fx_media_open"></a>fx_media_open

**Icona** ![ Icona Apri file multimediali](./media/user-guide/fx-events/image56.png)

**Descrizione**

Questo evento rappresenta un evento di apertura multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore alla voce del driver multimediale.
- Campo informazioni 3: puntatore alla memoria.
- Info Campo 4: Dimensioni della memoria.

### <a name="media-read-media-read"></a>Media Read Media Read 

#### <a name="fx_media_read"></a>fx_media_read

**Icona** ![ Icona lettura file multimediali](./media/user-guide/fx-events/image57.png)

**Descrizione**

Questo evento rappresenta un evento di lettura multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: settore logico.
- Campo informazioni 3: puntatore del buffer.
- Campo informazioni 4: Byte letti.

### <a name="media-space-available"></a>Spazio multimediale disponibile 

#### <a name="fx_media_space_available"></a>fx_media_space_available

**Icona** ![ Icona Spazio multimediale disponibile](./media/user-guide/fx-events/image58.png)

**Descrizione**

Questo evento rappresenta un evento disponibile nello spazio multimediale.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore byte disponibili.
- Campo informazioni 3: numero di cluster gratuiti.
- Campo informazioni 4: Non usato.

### <a name="media-volume-get"></a>Volume multimediale Get 

#### <a name="fx_media_volume_get"></a>fx_media_volume_get

**Icona** ![ Icona ottieni volume multimediale](./media/user-guide/fx-events/image59.png)

**Descrizione**

Questo evento rappresenta un evento get del volume multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome del volume.
- Campo informazioni 3: Origine volume.
- Campo informazioni 4: Non usato.

### <a name="media-volume-set"></a>Set di volumi multimediali 

#### <a name="fx_media_volume_set"></a>fx_media_volume_set

**Icona** ![ Icona del set di volumi multimediali](./media/user-guide/fx-events/image60.png)

**Descrizione**

Questo evento rappresenta un evento del set di volumi multimediali.

**Campi di informazioni** 
- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome del volume.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="media-write"></a>Scrittura supporti 

#### <a name="fx_media_write"></a>fx_media_write

**Icona** ![ Icona di scrittura multimediale](./media/user-guide/fx-events/image61.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura multimediale.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: settore logico.
- Campo informazioni 3: puntatore del buffer.
- Campo informazioni 4: byte scritti.

### <a name="system-date-get"></a>System Date Get 

#### <a name="fx_system_date_get"></a>fx_system_date_get 

**Icona** ![ Icona di ripristino della data di sistema](./media/user-guide/fx-events/image62.png)

**Descrizione**

Questo evento rappresenta un evento get della data di sistema.

**Campi di informazioni**

- Campo informazioni 1: Anno.
- Campo informazioni 2: Mese.
- Campo informazioni 3: Giorno.
- Campo informazioni 4: Non usato.

### <a name="system-date-set"></a>Set di date di sistema 

#### <a name="fx_system_date_set"></a>fx_system_date_set 

**Icona** ![ Icona del set di date di sistema](./media/user-guide/fx-events/image63.png)

**Descrizione**

Questo evento rappresenta un evento del set di date di sistema.

**Campi di informazioni**

- Campo informazioni 1: Anno.
- Campo informazioni 2: Mese.
- Campo informazioni 3: Giorno.
- Campo informazioni 4: Non usato.

### <a name="system-initialize"></a>Inizializzazione del sistema 

#### <a name="fx_system_initialize"></a>fx_system_initialize 

**Icona** ![ Icona di inizializzazione del sistema](./media/user-guide/fx-events/image64.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione del sistema.

**Campi di informazioni**

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="system-time-get"></a>System Time Get 

#### <a name="fx_system_time_get"></a>fx_system_time_get 

**Icona** ![ Icona di ripristino dell'ora di sistema](./media/user-guide/fx-events/image65.png)

**Descrizione**

Questo evento rappresenta un evento di get dell'ora di sistema.

**Campi di informazioni** 

- Campo informazioni 1: Ora.
- Campo informazioni 2: Minuto.
- Campo informazioni 3: secondo.
- Campo informazioni 4: Non usato.

### <a name="system-time-set"></a>Set di tempo di sistema 

#### <a name="fx_system_time_set"></a>fx_system_time_set 

**Icona** ![ Icona del set di tempo di sistema](./media/user-guide/fx-events/image66.png)

**Descrizione**

Questo evento rappresenta un evento del set di tempo di sistema.

**Campi di informazioni**

- Campo informazioni 1: Ora.
- Campo informazioni 2: Minuto.
- Campo informazioni 3: secondo.
- Campo informazioni 4: Non usato.

### <a name="unicode-directory-create"></a>Creazione directory Unicode 

#### <a name="fx_unicode_directory_create"></a>fx_unicode_directory_create 

**Icona** ![ Icona di creazione directory Unicode](./media/user-guide/fx-events/image67.png)

**Descrizione**

Questo evento rappresenta un evento di creazione directory Unicode.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome Unicode.
- Campo informazioni 3: dimensioni del nome Unicode.
- Campo informazioni 4: puntatore al nome breve.

### <a name="unicode-directory-rename"></a>Ridenominazione della directory Unicode 

#### <a name="fx_unicode_directory_rename"></a>fx_unicode_directory_rename

**Icona** ![ Icona di ridenominazione della directory Unicode](./media/user-guide/fx-events/image68.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione di directory Unicode.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome Unicode.
- Campo informazioni 3: dimensioni del nome Unicode.
- Campo informazioni 4: puntatore al nome breve.

### <a name="unicode-file-create"></a>Creazione di file Unicode 

#### <a name="fx_unicode_file_create"></a>fx_unicode_file_create

**Icona** ![ Icona per la creazione di file Unicode](./media/user-guide/fx-events/image69.png)

**Descrizione**

Questo evento rappresenta un evento di creazione di file Unicode.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Info Field 2: puntatore al nome Unicode.
- Campo informazioni 3: dimensioni del nome Unicode.
- Campo informazioni 4: puntatore al nome breve.

### <a name="unicode-file-rename"></a>Ridenominazione di file Unicode 

#### <a name="fx_unicode_file_rename"></a>fx_unicode_file_rename

**Icona** ![ Icona di ridenominazione di file Unicode](./media/user-guide/fx-events/image70.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione di file Unicode.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome Unicode.
- Campo informazioni 3: dimensioni del nome Unicode.
- Campo informazioni 4: puntatore al nome breve.

### <a name="unicode-length-get"></a>Unicode Length Get 

#### <a name="fx_unicode_length_get"></a>fx_unicode_length_get

**Icona** ![ Icona di get della lunghezza Unicode](./media/user-guide/fx-events/image71.png)

**Descrizione**

Questo evento rappresenta un evento Get di lunghezza Unicode.

**Campi di informazioni**

- Info Field 1: puntatore al nome Unicode.
- Campo informazioni 2: Lunghezza.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="unicode-name-get"></a>Unicode Name Get 

#### <a name="fx_unicode_name_get"></a>fx_unicode_name_get

**Icona** ![ Icona di get del nome Unicode](./media/user-guide/fx-events/image72.png)

**Descrizione**

Questo evento rappresenta un evento get del nome Unicode.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: nome breve dell'origine.
- Campo informazioni 3: puntatore del nome Unicode di destinazione.
- Campo informazioni 4: lunghezza del nome Unicode di destinazione.

### <a name="unicode-short-name-get"></a>Unicode Short Name Get 

#### <a name="fx_unicode_short_name_get"></a>fx_unicode_short_name_get

**Icona** ![ Icona get del nome breve Unicode](./media/user-guide/fx-events/image73.png)

**Descrizione**

Questo evento rappresenta un evento get del nome breve Unicode.

**Campi di informazioni**

- Campo informazioni 1: puntatore al supporto.
- Campo informazioni 2: puntatore al nome Unicode di origine.
- Info Field 3: lunghezza del nome Unicode.
- Campo informazioni 4: puntatore al nome breve.