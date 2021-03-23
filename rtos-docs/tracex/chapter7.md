---
title: 'Capitolo 7: eventi di traccia di Azure RTO FileX'
description: Questo capitolo contiene una descrizione degli eventi FileX di Azure RTO.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: c3cbc945e33b87b6759c56ec1429d6bf57259bd9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823396"
---
# <a name="chapter-7---azure-rtos-filex-trace-events"></a>Capitolo 7: eventi di traccia di Azure RTO FileX

Questo capitolo contiene una descrizione degli eventi FileX di Azure RTO. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

**Di seguito è riportato un elenco di eventi FileX visualizzati da TraceX.**

Di seguito viene descritto ogni evento:

| **Icona**                         | **Significato**                               |
| -------------------------------- | ----------------------------------------- |
| ![Icona di mancata memorizzazione nella cache del settore logico interno](./media/user-guide/fx-events/image1.png)    | Mancato riscontro nella cache del settore logico interno |
| ![Icona di mancata memorizzazione nella cache della directory interna](./media/user-guide/fx-events/image2.png)    | Mancata memorizzazione nella cache della directory interna |
| ![Icona di svuotamento supporti interni](./media/user-guide/fx-events/image3.png)    | Scaricamento multimediale interno |
| ![Icona di lettura della voce di directory interna](./media/user-guide/fx-events/image4.png)    | Lettura voce directory interna |
| ![Icona di scrittura della voce di directory interna](./media/user-guide/fx-events/image5.png)    | Scrittura voce directory interna |
| ![Icona lettura driver I/O interno](./media/user-guide/fx-events/image6.png)    | Lettura driver I/O interno |
| ![Icona scrittura driver I/O interno](./media/user-guide/fx-events/image7.png)    | Scrittura driver I/O interno |
| ![Icona di svuotamento driver I/O interno](./media/user-guide/fx-events/image8.png)    | Scaricamento driver I/O interno |
| ![Icona di interruzione del driver I/O interno](./media/user-guide/fx-events/image9.png)    | Interruzione driver I/O interno |
| ![Icona di inizializzazione del driver I/O interno](./media/user-guide/fx-events/image10.png)    | Inizializzazione driver I/O interno |
| ![Icona di lettura avvio driver I/O interno](./media/user-guide/fx-events/image11.png)    | Lettura avvio driver I/O interno |
| ![Icona settori di rilascio driver I/O interno](./media/user-guide/fx-events/image12.png)    | Settori di rilascio driver I/O interni |
| ![Icona di scrittura avvio driver I/O interno](./media/user-guide/fx-events/image13.png)    | Scrittura di avvio driver I/O interno |
| ![Icona di annullamento inizializzatore driver I/O interno](./media/user-guide/fx-events/image14.png)    | Annulla inizializzazione driver driver I/O interno |
| ![Icona di lettura attributi directory](./media/user-guide/fx-events/image15.png)    | **Attributi di directory letti** (*fx_directory_attributes_read*) |
| ![Icona set di attributi di directory](./media/user-guide/fx-events/image16.png)    | **Set di attributi di directory** (*fx_directory_attributes_set*) |
| ![Icona Crea directory](./media/user-guide/fx-events/image17.png)    | **Creazione directory** (*fx_directory_create*) |
| ![Icona di Get predefinita della directory](./media/user-guide/fx-events/image18.png)    | **Get** (*fx_directory_default_get*) predefinito della directory |
| ![Icona set predefinito directory](./media/user-guide/fx-events/image19.png)    | **Set predefinito directory** (*fx_directory_default_set*) |
| ![Icona di eliminazione directory](./media/user-guide/fx-events/image20.png)    | **Eliminazione directory** (*fx_directory_delete*) |
| ![Icona trova della prima voce di directory](./media/user-guide/fx-events/image21.png)    | **Ricerca nella prima voce di directory** (*fx_directory_first_entry_find*) |
| ![Icona di ricerca della prima voce completa della directory](./media/user-guide/fx-events/image22.png)    | **Ricerca della prima voce completa directory** (*fx_directory_first_full_entry_find*) |
| ![Icona delle informazioni di directory Get](./media/user-guide/fx-events/image23.png)    | **Informazioni di directory Get** (*fx_directory_information_get*) |
| ![Icona Cancella percorso locale directory](./media/user-guide/fx-events/image24.png)    | **Cancellazione percorso locale directory** (*fx_directory_local_path_clear*) |
| ![Icona di Get percorso locale della directory](./media/user-guide/fx-events/image25.png)    | **Percorso locale della directory Get** (*fx_directory_local_path_get*) |
| ![Icona di ripristino del percorso locale della directory](./media/user-guide/fx-events/image26.png)    | **Ripristino percorso locale directory** (*fx_directory_local_path_restore*) |
| ![Icona del set di percorsi locali della directory](./media/user-guide/fx-events/image27.png)    | **Set di percorsi locali della directory** (*fx_directory_local_path_set*) |
| ![Icona Ottieni nome lungo directory](./media/user-guide/fx-events/image28.png)    | **Nome lungo directory Get** (*fx_directory_long_name_get*) |
| ![Icona di test nome directory](./media/user-guide/fx-events/image29.png)    | **Test nome directory** (*fx_directory_name_test*) |
| ![Icona di ricerca voce successiva directory](./media/user-guide/fx-events/image30.png)    | **Ricerca voce successiva directory** (*fx_directory_next_entry_find*) |
| ![Icona di ricerca voce completa successiva alla directory](./media/user-guide/fx-events/image31.png)    | **Ricerca voce completa successiva directory** (*fx_directory_next_full_entry_find*) |
| ![Icona Rinomina Directory](./media/user-guide/fx-events/image32.png)    | **Ridenominazione directory** (*fx_directory_rename*) |
| ![Icona di Get nome breve directory](./media/user-guide/fx-events/image33.png)    | **Nome breve directory Get** (*fx_directory_short_name_get*) |
| ![Icona alloca file](./media/user-guide/fx-events/image34.png)    | **Alloca file** (*fx_file_allocate*) |
| ![Icona di lettura attributi file](./media/user-guide/fx-events/image35.png)    | **Attributi di file letti** (*fx_file_attributes_read*) |
| ![Icona set di attributi file](./media/user-guide/fx-events/image36.png)    | **Attributi file impostati** (*fx_file_attributes_set*) |
| ![Icona di allocazione file per il massimo sforzo](./media/user-guide/fx-events/image37.png)    | **File per il massimo sforzo allocato** (*fx_file_best_effort_allocate*) |
| ![Icona di chiusura file](./media/user-guide/fx-events/image38.png)    | **Chiusura file** (*fx_file_close*) |
| ![Icona Crea file](./media/user-guide/fx-events/image39.png)    | **Creazione file** (*fx_file_create*) |
| ![Icona del set di data e ora del file](./media/user-guide/fx-events/image40.png)    | **Data/ora file** (*fx_file_date_time_set*) |
| ![Icona Elimina file](./media/user-guide/fx-events/image41.png)    | **Eliminazione file** (*fx_file_delete*) |
| ![Icona Apri file](./media/user-guide/fx-events/image42.png)    | **Apertura file** (*fx_file_open*) |
| ![Icona lettura file](./media/user-guide/fx-events/image43.png)    | **Lettura file** (*fx_file_read*) |
| ![Icona di ricerca relativa ai file](./media/user-guide/fx-events/image44.png)    | **Ricerca relativa ai file** (*fx_file_relative_seek*) |
| ![Icona Rinomina file](./media/user-guide/fx-events/image45.png)    | **Ridenominazione file** (*fx_file_rename*) |
| ![Icona di ricerca file](./media/user-guide/fx-events/image46.png)    | **Ricerca file** (*fx_file_seek*) |
| ![Icona troncamento file](./media/user-guide/fx-events/image47.png)    | **Troncamento file** (*fx_file_truncate*) |
| ![Icona versione troncamento file](./media/user-guide/fx-events/image48.png)    | **Versione troncamento file** (*fx_file_truncate_release*) |
| ![Icona scrittura file](./media/user-guide/fx-events/image49.png)    | **Scrittura file** (*fx_file_write*) |
| ![Icona Interrompi supporto](./media/user-guide/fx-events/image50.png)    | **Interruzione supporto** (*fx_media_abort*) |
| ![Icona di invalidamento della cache multimediale](./media/user-guide/fx-events/image51.png)    | **Media cache invalidata** (*fx_media_cache_invalidate*) |
| ![Icona del controllo del supporto](./media/user-guide/fx-events/image52.png)    | **Controllo supporto** (*fx_media_check*) |
| ![* Icona di chiusura del supporto](./media/user-guide/fx-events/image53.png)    | **Chiusura media** (*fx_media_close*) |
| ![Icona di scaricamento supporti](./media/user-guide/fx-events/image54.png)    | **Scaricamento supporti** (*fx_media_flush*) |
| ![Icona formato supporto](./media/user-guide/fx-events/image55.png)    | **Formato supporto** (*fx_media_format*) |
| ![Icona del supporto aperto](./media/user-guide/fx-events/image56.png)    | **Supporto aperto** (*fx_media_open*) |
| ![Icona di lettura del supporto](./media/user-guide/fx-events/image57.png)    | **Media Read** (*fx_media_read*) |
| ![Icona spazio multimediale disponibile](./media/user-guide/fx-events/image58.png)    | **Spazio multimediale disponibile** (*fx_media_space_available*) |
| ![Icona Ottieni volume multimediale](./media/user-guide/fx-events/image59.png)    | **Volume multimediale Get** (*fx_media_volume_get*) |
| ![Icona del set di volumi multimediali](./media/user-guide/fx-events/image60.png)    | **Set di volumi multimediali** (*fx_media_volume_set*) |
| ![Icona scrittura supporti](./media/user-guide/fx-events/image61.png)    | **Scrittura supporti** (*fx_media_write*) |
| ![Icona Data di sistema Get](./media/user-guide/fx-events/image62.png)    | **Data di sistema Get** (*fx_system_date_get*) |
| ![Icona del set di dati di sistema](./media/user-guide/fx-events/image63.png)    | **Set di date di sistema** (*fx_system_date_set*) |
| ![Icona Inizializzazione sistema](./media/user-guide/fx-events/image64.png)    | **Inizializzazione sistema** (*fx_system_initialize*) |
| ![Icona dell'ora di sistema Get](./media/user-guide/fx-events/image65.png)    | **Tempo di sistema Get** (*fx_system_time_get*) |
| ![Icona del set di impostazioni dell'ora di sistema](./media/user-guide/fx-events/image66.png)    | **Impostazione dell'ora di sistema** (*fx_system_time_set*) |
| ![Icona di creazione directory Unicode](./media/user-guide/fx-events/image67.png)    | **Creazione directory Unicode** (*fx_unicode_directory_create*) |
| ![Icona Rinomina Directory Unicode](./media/user-guide/fx-events/image68.png)    | **Ridenominazione directory Unicode** (*fx_unicode_directory_rename*) |
| ![Icona di creazione file Unicode](./media/user-guide/fx-events/image69.png)    | **Creazione di file Unicode** (*fx_unicode_file_create*) |
| ![Icona Rinomina file Unicode](./media/user-guide/fx-events/image70.png)    | **Ridenominazione di file Unicode** (*fx_unicode_file_rename*) |
| ![Icona di ottenere la lunghezza Unicode](./media/user-guide/fx-events/image71.png)    | **Lunghezza Unicode get** (*fx_unicode_length_get*) |
| ![Icona Ottieni nome Unicode](./media/user-guide/fx-events/image72.png)    | **Nome Unicode get** (*fx_unicode_name_get*) |
| ![Icona di Get con nome breve Unicode](./media/user-guide/fx-events/image73.png)    | **Nome breve Unicode get** (*fx_unicode_short_name_get*) |

## <a name="event-descriptions"></a>Descrizioni di eventi

Di seguito viene descritto ogni singolo evento.

### <a name="internal-logical-sector-cache-miss"></a>Mancato riscontro nella cache del settore logico interno 

#### <a name="internal-logical-sector-cache-miss"></a>Mancato riscontro nella cache del settore logico interno

**Icona** ![ di Icona di mancata memorizzazione nella cache del settore logico interno](./media/user-guide/fx-events/image1.png)

**Descrizione**

Questo evento rappresenta un mancato riscontro nella cache del settore logico FileX interno.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: settore.
- Campo info 3: Totale mancati riscontri.
- Informazioni sul campo 4: dimensioni della cache.

### <a name="internal-directory-cache-miss"></a>Mancata memorizzazione nella cache della directory interna

#### <a name="internal-directory-cache-miss"></a>Mancata memorizzazione nella cache della directory interna

**Icona** ![ di Icona di mancata memorizzazione nella cache della directory interna](./media/user-guide/fx-events/image2.png)

**Descrizione** 

Questo evento rappresenta un mancato riscontro nella cache della directory FileX interna.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: Totale mancati riscontri.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-media-flush"></a>Scaricamento multimediale interno 

#### <a name="internal-media-flush"></a>Scaricamento multimediale interno

**Icona** ![ di Icona di svuotamento supporti interni](./media/user-guide/fx-events/image3.png)

**Descrizione**

Questo evento rappresenta uno scaricamento multimediale FileX interno.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: numero di settori modificati.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.


### <a name="internal-directory-entry-read"></a>Lettura voce directory interna 

#### <a name="internal-directory-entry-read"></a>Lettura voce directory interna

**Icona** ![ di Icona di lettura della voce di directory interna](./media/user-guide/fx-events/image4.png)

**Descrizione**

Questo evento rappresenta un evento di lettura della voce di directory FileX interna.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-directory-entry-write"></a>Scrittura voce directory interna

#### <a name="internal-directory-entry-write"></a>Scrittura voce directory interna

**Icona** ![ di Icona di scrittura della voce di directory interna](./media/user-guide/fx-events/image5.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura della voce della directory FileX interna.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-read"></a>Lettura driver I/O interno 

#### <a name="internal-io-driver-read"></a>Lettura driver I/O interno 

**Icona** ![ di Icona lettura driver I/O interno](./media/user-guide/fx-events/image6.png)

**Descrizione** 

Questo evento rappresenta un evento di lettura del driver I/O interno di FileX.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: settore.
- Campo info 3: numero di settori.
- Informazioni sul campo 4: puntatore del buffer.

### <a name="internal-io-driver-write"></a>Scrittura driver I/O interno 

#### <a name="internal-io-driver-write"></a>Scrittura driver I/O interno 

**Icona** ![ di Icona scrittura driver I/O interno](./media/user-guide/fx-events/image7.png)

**Descrizione** 

Questo evento rappresenta un evento di scrittura driver I/O interno di FileX.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: settore.
- Campo info 3: numero di settori.
- Informazioni sul campo 4: puntatore del buffer.

### <a name="internal-io-driver-flush"></a>Scaricamento driver I/O interno 

#### <a name="internal-io-driver-flush"></a>Scaricamento driver I/O interno 

**Icona** ![ di Icona di svuotamento driver I/O interno](./media/user-guide/fx-events/image8.png)

**Descrizione** 

Questo evento rappresenta un evento di scaricamento del driver I/O interno di FileX.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-abort"></a>Interruzione driver I/O interno 

#### <a name="internal-io-dirver-abort"></a>Interruzione I/O interna dirver

**Icona** ![ di Icona di interruzione del driver I/O interno](./media/user-guide/fx-events/image9.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del driver I/O interno di FileX.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-initialize"></a>Inizializzazione driver I/O interno 

#### <a name="internal-io-driver-initialize"></a>Inizializzazione driver I/O interno 

**Icona** ![ di Icona di inizializzazione del driver I/O interno](./media/user-guide/fx-events/image10.png)

**Descrizione** 

Questo evento rappresenta un evento di inizializzazione del driver I/O interno di FileX.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-boot-sector-read"></a>Lettura settore di avvio driver I/O interno 

#### <a name="internal-io-driver-boot-sector-read"></a>Lettura settore di avvio driver I/O interno 

**Icona** ![ di Icona di lettura del settore di avvio del driver I/O interno](./media/user-guide/fx-events/image11.png)

**Descrizione** 

Questo evento rappresenta un evento di lettura del settore di avvio del driver di I/O FileX interno.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore del buffer.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-release-sectors"></a>Settori di rilascio driver I/O interni 

#### <a name="internal-io-driver-release-sectors"></a>Settori di rilascio driver I/O interni 

**Icona** ![ di Icona settori di rilascio driver I/O interno](./media/user-guide/fx-events/image12.png)

**Descrizione** 

Questo evento rappresenta un evento Internal FileX I/O driver release sectors.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: settore.
- Campo info 3: numero di settori.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-boot-sector-write"></a>Scrittura settore di avvio driver I/O interno

#### <a name="internal-io-driver-boot-sector-write"></a>Scrittura settore di avvio driver I/O interno 

**Icona** ![ di Icona di scrittura del settore di avvio del driver I/O interno](./media/user-guide/fx-events/image13.png)

**Descrizione** 

Questo evento rappresenta un evento di scrittura del settore di avvio del driver di I/O FileX interno.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore del buffer.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="internal-io-driver-un-initialize"></a>Annulla inizializzazione del driver di I/O interno 

#### <a name="internal-io-driver-un-initialize"></a>Annulla inizializzazione del driver di I/O interno 

**Icona** ![ di Icona di annullamento inizializzazione del driver I/O interno](./media/user-guide/fx-events/image14.png)

**Descrizione** 

Questo evento rappresenta un evento di annullamento inizializzazione del driver di I/O FileX interno.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.
</blockquote></td>

### <a name="directory-attributes-read"></a>Attributi di directory letti 

#### <a name="fx_directory_attributes_read"></a>fx_directory_attributes_read 

**Icona** ![ di Icona di lettura attributi directory](./media/user-guide/fx-events/image15.png)

**Descrizione** 

Questo evento rappresenta un evento di lettura degli attributi della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Informazioni sul campo 3: attributi mappa di bit:

  | Attributo                         | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | 0x01  |
  |  Nascosto                           | 0x02  |
  |  Sistema                           | 0x04  |
  |  Volume                           | 0x08  |
  |  Directory                        | 0x10  |
  |  Archiviazione                          | 0x20  |
- Campo informazioni 4: non utilizzato.

### <a name="directory-attributes-set"></a>Attributi di directory impostati 

#### <a name="fx_directory_attributes_set"></a>fx_directory_attributes_set 

**Icona** ![ di Icona set attributi](./media/user-guide/fx-events/image16.png)

**Descrizione** 

Questo evento rappresenta una directory di un evento set di attributi di directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Informazioni sul campo 3: attributi mappa di bit:

  |  Attributo                        | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | 0x01  |
  |  Nascosto                           | 0x02  |
  |  Sistema                           | 0x04  |
  |  Archiviazione                          | 0x20  |
- Campo informazioni 4: non utilizzato.

### <a name="directory-create"></a>Creazione Directory 

#### <a name="fx_directory_create"></a>fx_directory_create

**Icona** ![ di Icona Crea directory](./media/user-guide/fx-events/image17.png)

**Descrizione** 

Questo evento rappresenta un evento di creazione della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-default-get"></a>Impostazione predefinita directory Get 

#### <a name="fx_directory_default_get"></a>fx_directory_default_get 

**Icona** ![ di Icona di Get predefinita della directory](./media/user-guide/fx-events/image18.png)

**Descrizione** 

Questo evento rappresenta un evento set predefinito di directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome del percorso restituito.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-default-set"></a>Set predefinito directory 

#### <a name="fx_directory_default_set"></a>fx_directory_default_set 

**Icona** ![ di Icona set predefinito directory](./media/user-guide/fx-events/image19.png)

**Descrizione** 

Questo evento rappresenta un evento set predefinito di directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nuovo nome di percorso predefinito.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-delete"></a>Eliminazione directory 

#### <a name="fx_directory_delete"></a>fx_directory_delete

**Icona** ![ di Icona di eliminazione directory](./media/user-guide/fx-events/image20.png)

**Descrizione** 

Questo evento rappresenta un evento di eliminazione della directory.

**Campi informazioni**
- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-first-entry-find"></a>Ricerca nella prima voce della directory 

#### <a name="fx_directory_first_entry_find"></a>fx_directory_first_entry_find

**Icona** ![ di Icona trova della prima voce di directory](./media/user-guide/fx-events/image21.png)

**Descrizione** 

Questo evento rappresenta un evento di ricerca della prima voce di directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-first-full-entry-find"></a>Ricerca della prima voce completa directory 

#### <a name="fx_directory_first_full_entry_find"></a>fx_directory_first_full_entry_find

**Icona** ![ di Icona di ricerca della prima voce completa della directory](./media/user-guide/fx-events/image22.png)

**Descrizione** 

Questo evento rappresenta un evento di ricerca della prima voce completa della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-information-get"></a>Informazioni di directory Get 

#### <a name="fx_directory_information_get"></a>fx_directory_information_get

**Icona** ![ di Icona delle informazioni di directory Get](./media/user-guide/fx-events/image23.png)

**Descrizione** 

Questo evento rappresenta un evento di ottenere informazioni sulla directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-local-path-clear"></a>Cancellazione percorso locale directory 

#### <a name="fx_directory_local_path_clear"></a>fx_directory_local_path_clear

**Icona** ![ di Icona Cancella percorso locale directory](./media/user-guide/fx-events/image24.png)

**Descrizione** 

Questo evento rappresenta un evento di cancellazione del percorso locale della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-local-path-get"></a>Percorso locale di directory Get 

#### <a name="fx_directory_local_path_get"></a>fx_directory_local_path_get

**Icona** ![ di Icona di Get percorso locale della directory](./media/user-guide/fx-events/image25.png)

**Descrizione** 

Questo evento rappresenta un evento di Get percorso locale della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome del percorso restituito.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-local-path-restore"></a>Ripristino del percorso locale della directory 

#### <a name="fx_directory_local_path_restore"></a>fx_directory_local_path_restore

**Icona** ![ di Icona di ripristino del percorso locale della directory](./media/user-guide/fx-events/image26.png)

**Descrizione** 

Questo evento rappresenta un evento di ripristino del percorso locale della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore alla struttura del percorso locale.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-local-path-set"></a>Set di percorsi locali della directory 

#### <a name="fx_directory_local_path_set"></a>fx_directory_local_path_set

**Icona** ![ di Icona del set di percorsi locali della directory](./media/user-guide/fx-events/image27.png)

**Descrizione** 

Questo evento rappresenta un evento del set di percorsi locali della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore alla struttura del percorso locale.
- Informazioni sul campo 3: puntatore al nuovo nome del percorso.
- Campo informazioni 4: non utilizzato.

### <a name="directory-long-name-get"></a>Nome lungo directory Get 

#### <a name="fx_directory_long_name_get"></a>fx_directory_long_name_get

**Icona** ![ di Icona Ottieni nome lungo directory](./media/user-guide/fx-events/image28.png)

**Descrizione** 

Questo evento rappresenta un evento di Get con nome lungo di directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome file breve.
- Informazioni sul campo 3: puntatore al nome file lungo.
- Campo informazioni 4: non utilizzato.

### <a name="directory-name-test"></a>Test nome directory 

#### <a name="fx_directory_name_test"></a>fx_directory_name_test

**Icona** ![ di Icona di test nome directory](./media/user-guide/fx-events/image29.png)

**Descrizione** 

Questo evento rappresenta un evento di test del nome di directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-next-entry-find"></a>Ricerca voce successiva directory 

#### <a name="fx_directory_next_entry_find"></a>fx_directory_next_entry_find

**Icona** ![ di Icona di ricerca voce successiva directory](./media/user-guide/fx-events/image30.png)

**Descrizione** 

Questo evento rappresenta un evento di ricerca voce successiva della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-next-full-entry-find"></a>Ricerca voce completa successiva alla directory 

#### <a name="fx_directory_next_full_entry_find"></a>fx_directory_next_full_entry_find

**Icona** ![ di Icona di ricerca voce completa successiva alla directory](./media/user-guide/fx-events/image31.png)

**Descrizione**

Questo evento rappresenta una directory che segue l'evento di ricerca full entry.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome della directory.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="directory-rename"></a>Ridenominazione directory 

#### <a name="fx_directory_rename-event"></a>evento fx_directory_rename

**Icona** ![ di Icona Rinomina Directory](./media/user-guide/fx-events/image32.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione della directory.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome di directory precedente.
- Informazioni sul campo 3: puntatore al nuovo nome della directory.
- Campo informazioni 4: non utilizzato.

### <a name="directory-short-name-get"></a>Nome breve directory Get 

#### <a name="fx_directory_short_name_get"></a>fx_directory_short_name_get

**Icona** ![ di Icona di Get nome breve directory](./media/user-guide/fx-events/image33.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento del nome breve della directory.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome file lungo.
- Informazioni sul campo 3: puntatore al nome file breve.
- Campo informazioni 4: non utilizzato.

### <a name="file-allocate"></a>Alloca file 

#### <a name="fx_file_allocate"></a>fx_file_allocate

**Icona** ![ di Icona alloca file](./media/user-guide/fx-events/image34.png)

**Descrizione**

Questo evento rappresenta un evento di allocazione di file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Campo informazioni 2: dimensione richiesta.
- Informazioni sul campo 3: dimensioni correnti.
- Campo informazioni 4: nuove dimensioni.

### <a name="file-attributes-read"></a>Lettura attributi file 

#### <a name="fx_file_attributes_read"></a>fx_file_attributes_read

**Icona** ![ di Icona di lettura attributi file](./media/user-guide/fx-events/image35.png)

**Descrizione**

Questo evento rappresenta un evento di lettura degli attributi del file.

**Campi informazioni**

- Info Field 1: puntatore al supporto. 
- Informazioni sul campo 2: attributi mappa di bit:

  |  Attribut                         | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | 0x01  |
  |  Nascosto                           | 0x02  |
  |  Sistema                           | 0x04  |
  |  Volume                           | 0x08  |
  |  Directory                        | 0x10  |
  |  Archiviazione                          | 0x20  |
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="file-attributes-set"></a>Attributi file impostati 

#### <a name="fx_file_attributes_set"></a>fx_file_attributes_set

**Icona** ![ di Icona set di attributi file](./media/user-guide/fx-events/image36.png)

**Descrizione** 

Questo evento rappresenta un evento del set di attributi di file.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome file. 
- Informazioni sul campo 3: attributi mappa di bit:

  | Attributo                         | Valore        |
  |---------------------------------- | --------|
  |  Sola lettura                        | 0x01  |
  |  Nascosto                           | 0x02  |
  |  Sistema                           | 0x04  |
  |  Archiviazione                          | 0x20  |
- Campo informazioni 4: non utilizzato.

### <a name="file-best-effort-allocate"></a>Allocazione di file per il massimo sforzo 

#### <a name="fx_file_best_effort_allocate"></a>fx_file_best_effort_allocate

**Icona** ![ di Icona di allocazione file per il massimo sforzo](./media/user-guide/fx-events/image37.png)

**Descrizione** 

Questo evento rappresenta un evento di allocazione del Best effort di file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Campo informazioni 2: dimensione richiesta.
- Info Field 3: dimensioni effettive allocate.
- Campo informazioni 4: non utilizzato.

### <a name="file-close"></a>Chiusura file 

#### <a name="fx_file_close"></a>fx_file_close

**Icona** ![ di Icona di chiusura file](./media/user-guide/fx-events/image38.png)

**Descrizione** 

Questo evento rappresenta un evento di chiusura del file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Informazioni sul campo 2: dimensioni del file.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="file-create"></a>Creazione file

#### <a name="fx_file_create"></a>fx_file_create

**Icona** ![ di Icona Crea file](./media/user-guide/fx-events/image39.png)

**Descrizione**

Questo evento rappresenta un evento di creazione di file.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome file.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="file-date-time-set"></a>Data/ora file impostato 

#### <a name="fx_file_date_time_set"></a>fx_file_date_time_set

**Icona** ![ di Icona del set di data e ora del file](./media/user-guide/fx-events/image40.png)

**Descrizione**

Questo evento rappresenta un evento del set di data/ora del file.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome file.
- Campo informazioni 3: anno.
- Campo informazioni 4: mese.

### <a name="file-delete"></a>Eliminazione file 

#### <a name="fx_file_delete"></a>fx_file_delete

**Icona** ![ di Icona Elimina file](./media/user-guide/fx-events/image41.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione di file.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome file.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="file-open"></a>Apertura file 

#### <a name="fx_file_open"></a>fx_file_open

**Icona** ![ di Icona Apri file](./media/user-guide/fx-events/image42.png)

**Descrizione**

Questo evento rappresenta un evento di apertura del file.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al blocco di controllo file.
- Info Field 3: puntatore al nome file.
- Campo informazioni 4: tipo aperto:

  |  Tipo aperto                        | Valore        |
  |---------------------------------- | --------|
  |  Apri per la lettura                    | 0x00  |
  |  Apri per scrittura                   | 0x01  |
  |  Apertura rapida per la lettura               | 0x02  |

### <a name="file-read"></a>Lettura file 

#### <a name="fx_file_read"></a>fx_file_read

**Icona** ![ di Icona lettura file](./media/user-guide/fx-events/image43.png)

**Descrizione**

Questo evento rappresenta un evento di lettura del file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Informazioni sul campo 2: puntatore del buffer.
- Informazioni sul campo 3: dimensioni della richiesta.
- Campo dati 4: dimensioni effettive lette.

### <a name="file-relative-seek"></a>Ricerca relativa ai file 

#### <a name="fx_file_relative_seek"></a>fx_file_relative_seek

**Icona** ![ di Icona di ricerca relativa ai file](./media/user-guide/fx-events/image44.png)

**Descrizione**

Questo evento rappresenta un evento di ricerca relativo al file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Informazioni sul campo 2: offset di byte.
- Campo informazioni 3: cerca da:

  | Evento                             | Valore        |
  |---------------------------------- | --------|
  |  Dall'inizio                   | 0x00  |
  |  Da fine                         | 0x01  | 
  |  Inoltra                          | 0x02  |
  |  indietro                         | 0x03  |
- Campo informazioni 4: offset precedente.

### <a name="file-rename"></a>Ridenominazione file 

#### <a name="fx_file_rename"></a>fx_file_rename

**Icona** ![ di Icona Rinomina file](./media/user-guide/fx-events/image45.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione del file.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome del file precedente.
- Info Field 3: puntatore al nuovo nome file.
- Campo informazioni 4: non utilizzato.

### <a name="file-seek"></a>Ricerca file 

#### <a name="fx_file_seek"></a>fx_file_seek

**Icona** ![ di Icona di ricerca file](./media/user-guide/fx-events/image46.png)

**Descrizione**

Questo evento rappresenta un evento di ricerca di file.

**Campi informazioni** 

- Info Field 1: puntatore al file.
- Informazioni sul campo 2: offset di byte.
- Informazioni sul campo 3: offset precedente.
- Campo informazioni 4: non utilizzato.

### <a name="file-truncate"></a>Troncamento file 

#### <a name="fx_file_truncate"></a>fx_file_truncate

**Icona** ![ di Icona troncamento file](./media/user-guide/fx-events/image47.png)

**Descrizione**

Questo evento rappresenta un evento di troncamento del file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Campo informazioni 2: dimensione richiesta.
- Informazioni sul campo 3: dimensioni precedenti.
- Campo informazioni 4: nuove dimensioni.

### <a name="file-truncate-release"></a>Versione troncamento file 

#### <a name="fx_file_truncate_release"></a>fx_file_truncate_release 

**Icona** ![ di Icona versione troncamento file](./media/user-guide/fx-events/image48.png)

**Descrizione**

Questo evento rappresenta un evento di rilascio troncato del file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Campo informazioni 2: dimensione richiesta.
- Informazioni sul campo 3: dimensioni precedenti.
- Campo informazioni 4: nuove dimensioni.

### <a name="file-write"></a>Scrittura file 

#### <a name="fx_file_write"></a>fx_file_write 

**Icona** ![ di Icona scrittura file](./media/user-guide/fx-events/image49.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura di file.

**Campi informazioni**

- Info Field 1: puntatore al file.
- Informazioni sul campo 2: puntatore del buffer.
- Informazioni sul campo 3: dimensioni della richiesta.
- Informazioni campo 4: dimensioni effettive scritte.

### <a name="media-abort"></a>Interruzione supporto 

#### <a name="fx_media_abort"></a>fx_media_abort 

**Icona** ![ di Icona Interrompi supporto](./media/user-guide/fx-events/image50.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del supporto.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="media-cache-invalidate"></a>Media cache invalidata

#### <a name="fx_media_cache_invalidate"></a>fx_media_cache_invalidate

**Icona** ![ di Icona di invalidamento della cache multimediale](./media/user-guide/fx-events/image51.png)

**Descrizione**

Questo evento rappresenta un evento di invalidamento della cache multimediale.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="media-check"></a>Controllo dei supporti 

#### <a name="fx_media_check"></a>fx_media_check

**Icona** ![ di Icona del controllo del supporto](./media/user-guide/fx-events/image52.png)

**Descrizione**

Questo evento rappresenta un evento di controllo del supporto.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore di memoria Scratch.
- Informazioni sul campo 3: dimensioni della memoria Scratch.
- Informazioni sul campo 4: errori mappa di bit:

  | Tipo di errore                        | Valore        |
  |---------------------------------- | --------|
  |  Errore catena FAT                  | 0x01  |
  |  Errore directory                  | 0x02  |
  |  Errore del cluster perso               | 0x04  |
  |  Errore dimensioni file                  | 0x08  |

### <a name="media-close"></a>Chiusura supporti 

#### <a name="fx_media_close"></a>fx_media_close

**Icona** ![ di Icona di chiusura supporti](./media/user-guide/fx-events/image53.png)

**Descrizione**

Questo evento rappresenta un evento di chiusura dei supporti.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="media-flush"></a>Scaricamento supporti 

#### <a name="fx_media_flush"></a>fx_media_flush

**Icona** ![ di Icona di scaricamento supporti](./media/user-guide/fx-events/image54.png)

**Descrizione**

Questo evento rappresenta un evento di scaricamento dei supporti.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="media-format"></a>Formato multimediale 

#### <a name="fx_media_format"></a>fx_media_format

**Icona** ![ di Icona formato supporto](./media/user-guide/fx-events/image55.png)

**Descrizione**

Questo evento rappresenta un evento di formato multimediale.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: numero di voci radice.
- Campo info 3: settori.
- Campo dati 4: settori per cluster.

### <a name="media-open"></a>Supporto aperto 

#### <a name="fx_media_open"></a>fx_media_open

**Icona** ![ di Icona del supporto aperto](./media/user-guide/fx-events/image56.png)

**Descrizione**

Questo evento rappresenta un evento di apertura del supporto.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore alla voce del driver multimediale.
- Campo info 3: puntatore di memoria.
- Informazioni sul campo 4: dimensioni della memoria.

### <a name="media-read-media-read"></a>Media lettura media lettura 

#### <a name="fx_media_read"></a>fx_media_read

**Icona** ![ di Icona di lettura del supporto](./media/user-guide/fx-events/image57.png)

**Descrizione**

Questo evento rappresenta un evento di lettura del supporto.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: settore logico.
- Campo info 3: puntatore del buffer.
- Campo informazioni 4: byte letti.

### <a name="media-space-available"></a>Spazio multimediale disponibile 

#### <a name="fx_media_space_available"></a>fx_media_space_available

**Icona** ![ di Icona spazio multimediale disponibile](./media/user-guide/fx-events/image58.png)

**Descrizione**

Questo evento rappresenta un evento di spazio multimediale disponibile.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore byte disponibili.
- Campo info 3: numero di cluster disponibili.
- Campo informazioni 4: non utilizzato.

### <a name="media-volume-get"></a>Volume multimediale Get 

#### <a name="fx_media_volume_get"></a>fx_media_volume_get

**Icona** ![ di Icona Ottieni volume multimediale](./media/user-guide/fx-events/image59.png)

**Descrizione**

Questo evento rappresenta un evento media volume Get.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome del volume.
- Informazioni sul campo 3: origine del volume.
- Campo informazioni 4: non utilizzato.

### <a name="media-volume-set"></a>Set di volumi multimediali 

#### <a name="fx_media_volume_set"></a>fx_media_volume_set

**Icona** ![ di Icona del set di volumi multimediali](./media/user-guide/fx-events/image60.png)

**Descrizione**

Questo evento rappresenta un evento del set di volumi multimediali.

**Campi informazioni** 
- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome del volume.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="media-write"></a>Scrittura supporti 

#### <a name="fx_media_write"></a>fx_media_write

**Icona** ![ di Icona scrittura supporti](./media/user-guide/fx-events/image61.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura del supporto.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Campo informazioni 2: settore logico.
- Campo info 3: puntatore del buffer.
- Campo informazioni 4: byte scritti.

### <a name="system-date-get"></a>Data di sistema Get 

#### <a name="fx_system_date_get"></a>fx_system_date_get 

**Icona** ![ di Icona Data di sistema Get](./media/user-guide/fx-events/image62.png)

**Descrizione**

Questo evento rappresenta un evento System Date Get.

**Campi informazioni**

- Campo informazioni 1: anno.
- Campo informazioni 2: mese.
- Campo informazioni 3: giorno.
- Campo informazioni 4: non utilizzato.

### <a name="system-date-set"></a>Set di date di sistema 

#### <a name="fx_system_date_set"></a>fx_system_date_set 

**Icona** ![ di Icona del set di dati di sistema](./media/user-guide/fx-events/image63.png)

**Descrizione**

Questo evento rappresenta un evento di data set di sistema.

**Campi informazioni**

- Campo informazioni 1: anno.
- Campo informazioni 2: mese.
- Campo informazioni 3: giorno.
- Campo informazioni 4: non utilizzato.

### <a name="system-initialize"></a>Inizializzazione sistema 

#### <a name="fx_system_initialize"></a>fx_system_initialize 

**Icona** ![ di Icona Inizializzazione sistema](./media/user-guide/fx-events/image64.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione del sistema.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="system-time-get"></a>Ora di sistema Get 

#### <a name="fx_system_time_get"></a>fx_system_time_get 

**Icona** ![ di Icona dell'ora di sistema Get](./media/user-guide/fx-events/image65.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento dell'ora di sistema.

**Campi informazioni** 

- Campo informazioni 1: ora.
- Campo informazioni 2: minuti.
- Campo informazioni 3: secondo.
- Campo informazioni 4: non utilizzato.

### <a name="system-time-set"></a>Impostazione dell'ora di sistema 

#### <a name="fx_system_time_set"></a>fx_system_time_set 

**Icona** ![ di Icona del set di impostazioni dell'ora di sistema](./media/user-guide/fx-events/image66.png)

**Descrizione**

Questo evento rappresenta un evento di impostazione dell'ora di sistema.

**Campi informazioni**

- Campo informazioni 1: ora.
- Campo informazioni 2: minuti.
- Campo informazioni 3: secondo.
- Campo informazioni 4: non utilizzato.

### <a name="unicode-directory-create"></a>Creazione directory Unicode 

#### <a name="fx_unicode_directory_create"></a>fx_unicode_directory_create 

**Icona** ![ di Icona di creazione directory Unicode](./media/user-guide/fx-events/image67.png)

**Descrizione**

Questo evento rappresenta un evento di creazione della directory Unicode.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome Unicode.
- Info Field 3: dimensioni del nome Unicode.
- Informazioni sul campo 4: puntatore al nome breve.

### <a name="unicode-directory-rename"></a>Ridenominazione della directory Unicode 

#### <a name="fx_unicode_directory_rename"></a>fx_unicode_directory_rename

**Icona** ![ di Icona Rinomina Directory Unicode](./media/user-guide/fx-events/image68.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione della directory Unicode.

**Campi informazioni** 

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome Unicode.
- Info Field 3: dimensioni del nome Unicode.
- Informazioni sul campo 4: puntatore al nome breve.

### <a name="unicode-file-create"></a>Creazione file Unicode 

#### <a name="fx_unicode_file_create"></a>fx_unicode_file_create

**Icona** ![ di Icona di creazione file Unicode](./media/user-guide/fx-events/image69.png)

**Descrizione**

Questo evento rappresenta un evento di creazione di file Unicode.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Info Field 2: puntatore al nome Unicode.
- Info Field 3: dimensioni del nome Unicode.
- Informazioni sul campo 4: puntatore al nome breve.

### <a name="unicode-file-rename"></a>Ridenominazione file Unicode 

#### <a name="fx_unicode_file_rename"></a>fx_unicode_file_rename

**Icona** ![ di Icona Rinomina file Unicode](./media/user-guide/fx-events/image70.png)

**Descrizione**

Questo evento rappresenta un evento di ridenominazione di file Unicode.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome Unicode.
- Info Field 3: dimensioni del nome Unicode.
- Informazioni sul campo 4: puntatore al nome breve.

### <a name="unicode-length-get"></a>Get lunghezza Unicode 

#### <a name="fx_unicode_length_get"></a>fx_unicode_length_get

**Icona** ![ di Icona Ottieni lunghezza Unicode](./media/user-guide/fx-events/image71.png)

**Descrizione**

Questo evento rappresenta un evento Get di lunghezza Unicode.

**Campi informazioni**

- Info Field 1: puntatore al nome Unicode.
- Campo informazioni 2: lunghezza.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="unicode-name-get"></a>Get nome Unicode 

#### <a name="fx_unicode_name_get"></a>fx_unicode_name_get

**Icona** ![ di Icona Ottieni nome Unicode](./media/user-guide/fx-events/image72.png)

**Descrizione**

Questo evento rappresenta un evento Get del nome Unicode.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: nome breve di origine.
- Informazioni sul campo 3: puntatore al nome Unicode di destinazione.
- Informazioni campo 4: lunghezza del nome Unicode di destinazione.

### <a name="unicode-short-name-get"></a>Get nome breve Unicode 

#### <a name="fx_unicode_short_name_get"></a>fx_unicode_short_name_get

**Icona** ![ di Icona di Get con nome breve Unicode](./media/user-guide/fx-events/image73.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento nome breve Unicode.

**Campi informazioni**

- Info Field 1: puntatore al supporto.
- Informazioni sul campo 2: puntatore al nome Unicode di origine.
- Info Field 3: lunghezza del nome Unicode.
- Informazioni sul campo 4: puntatore al nome breve.