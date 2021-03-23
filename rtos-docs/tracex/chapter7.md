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
# <a name="chapter-7---azure-rtos-filex-trace-events"></a><span data-ttu-id="65129-103">Capitolo 7: eventi di traccia di Azure RTO FileX</span><span class="sxs-lookup"><span data-stu-id="65129-103">Chapter 7 - Azure RTOS FileX trace events</span></span>

<span data-ttu-id="65129-104">Questo capitolo contiene una descrizione degli eventi FileX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="65129-104">This chapter contains a description of the Azure RTOS FileX events.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="65129-105">Elenco di eventi e icone</span><span class="sxs-lookup"><span data-stu-id="65129-105">List of Events and Icons</span></span>

<span data-ttu-id="65129-106">**Di seguito è riportato un elenco di eventi FileX visualizzati da TraceX.**</span><span class="sxs-lookup"><span data-stu-id="65129-106">**The following is a list of FileX events displayed by TraceX.**</span></span>

<span data-ttu-id="65129-107">Di seguito viene descritto ogni evento:</span><span class="sxs-lookup"><span data-stu-id="65129-107">The following describes each event:</span></span>

| <span data-ttu-id="65129-108">**Icona**</span><span class="sxs-lookup"><span data-stu-id="65129-108">**Icon**</span></span>                         | <span data-ttu-id="65129-109">**Significato**</span><span class="sxs-lookup"><span data-stu-id="65129-109">**Meaning**</span></span>                               |
| -------------------------------- | ----------------------------------------- |
| ![Icona di mancata memorizzazione nella cache del settore logico interno](./media/user-guide/fx-events/image1.png)    | <span data-ttu-id="65129-111">Mancato riscontro nella cache del settore logico interno</span><span class="sxs-lookup"><span data-stu-id="65129-111">Internal Logical Sector Cache Miss</span></span> |
| ![Icona di mancata memorizzazione nella cache della directory interna](./media/user-guide/fx-events/image2.png)    | <span data-ttu-id="65129-113">Mancata memorizzazione nella cache della directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-113">Internal Directory Cache Miss</span></span> |
| ![Icona di svuotamento supporti interni](./media/user-guide/fx-events/image3.png)    | <span data-ttu-id="65129-115">Scaricamento multimediale interno</span><span class="sxs-lookup"><span data-stu-id="65129-115">Internal Media Flush</span></span> |
| ![Icona di lettura della voce di directory interna](./media/user-guide/fx-events/image4.png)    | <span data-ttu-id="65129-117">Lettura voce directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-117">Internal Directory Entry Read</span></span> |
| ![Icona di scrittura della voce di directory interna](./media/user-guide/fx-events/image5.png)    | <span data-ttu-id="65129-119">Scrittura voce directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-119">Internal Directory Entry Write</span></span> |
| ![Icona lettura driver I/O interno](./media/user-guide/fx-events/image6.png)    | <span data-ttu-id="65129-121">Lettura driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-121">Internal I/O Driver Read</span></span> |
| ![Icona scrittura driver I/O interno](./media/user-guide/fx-events/image7.png)    | <span data-ttu-id="65129-123">Scrittura driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-123">Internal I/O Driver Write</span></span> |
| ![Icona di svuotamento driver I/O interno](./media/user-guide/fx-events/image8.png)    | <span data-ttu-id="65129-125">Scaricamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-125">Internal I/O Driver Flush</span></span> |
| ![Icona di interruzione del driver I/O interno](./media/user-guide/fx-events/image9.png)    | <span data-ttu-id="65129-127">Interruzione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-127">Internal I/O Driver Abort</span></span> |
| ![Icona di inizializzazione del driver I/O interno](./media/user-guide/fx-events/image10.png)    | <span data-ttu-id="65129-129">Inizializzazione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-129">Internal I/O Driver Initialize</span></span> |
| ![Icona di lettura avvio driver I/O interno](./media/user-guide/fx-events/image11.png)    | <span data-ttu-id="65129-131">Lettura avvio driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-131">Internal I/O Driver Boot Read</span></span> |
| ![Icona settori di rilascio driver I/O interno](./media/user-guide/fx-events/image12.png)    | <span data-ttu-id="65129-133">Settori di rilascio driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="65129-133">Internal I/O Driver Release Sectors</span></span> |
| ![Icona di scrittura avvio driver I/O interno](./media/user-guide/fx-events/image13.png)    | <span data-ttu-id="65129-135">Scrittura di avvio driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-135">Internal I/O Driver Boot Write</span></span> |
| ![Icona di annullamento inizializzatore driver I/O interno](./media/user-guide/fx-events/image14.png)    | <span data-ttu-id="65129-137">Annulla inizializzazione driver driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-137">Internal I / O Driver Driver Un-initialize</span></span> |
| ![Icona di lettura attributi directory](./media/user-guide/fx-events/image15.png)    | <span data-ttu-id="65129-139">**Attributi di directory letti** (*fx_directory_attributes_read*)</span><span class="sxs-lookup"><span data-stu-id="65129-139">**Directory Attributes Read** (*fx_directory_attributes_read*)</span></span> |
| ![Icona set di attributi di directory](./media/user-guide/fx-events/image16.png)    | <span data-ttu-id="65129-141">**Set di attributi di directory** (*fx_directory_attributes_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-141">**Directory Attributes Set** (*fx_directory_attributes_set*)</span></span> |
| ![Icona Crea directory](./media/user-guide/fx-events/image17.png)    | <span data-ttu-id="65129-143">**Creazione directory** (*fx_directory_create*)</span><span class="sxs-lookup"><span data-stu-id="65129-143">**Directory Create** (*fx_directory_create*)</span></span> |
| ![Icona di Get predefinita della directory](./media/user-guide/fx-events/image18.png)    | <span data-ttu-id="65129-145">**Get** (*fx_directory_default_get*) predefinito della directory</span><span class="sxs-lookup"><span data-stu-id="65129-145">**Directory Default Get** (*fx_directory_default_get*)</span></span> |
| ![Icona set predefinito directory](./media/user-guide/fx-events/image19.png)    | <span data-ttu-id="65129-147">**Set predefinito directory** (*fx_directory_default_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-147">**Directory Default Set** (*fx_directory_default_set*)</span></span> |
| ![Icona di eliminazione directory](./media/user-guide/fx-events/image20.png)    | <span data-ttu-id="65129-149">**Eliminazione directory** (*fx_directory_delete*)</span><span class="sxs-lookup"><span data-stu-id="65129-149">**Directory Delete** (*fx_directory_delete*)</span></span> |
| ![Icona trova della prima voce di directory](./media/user-guide/fx-events/image21.png)    | <span data-ttu-id="65129-151">**Ricerca nella prima voce di directory** (*fx_directory_first_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="65129-151">**Directory First Entry Find** (*fx_directory_first_entry_find*)</span></span> |
| ![Icona di ricerca della prima voce completa della directory](./media/user-guide/fx-events/image22.png)    | <span data-ttu-id="65129-153">**Ricerca della prima voce completa directory** (*fx_directory_first_full_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="65129-153">**Directory First Full Entry Find** (*fx_directory_first_full_entry_find*)</span></span> |
| ![Icona delle informazioni di directory Get](./media/user-guide/fx-events/image23.png)    | <span data-ttu-id="65129-155">**Informazioni di directory Get** (*fx_directory_information_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-155">**Directory Information Get** (*fx_directory_information_get*)</span></span> |
| ![Icona Cancella percorso locale directory](./media/user-guide/fx-events/image24.png)    | <span data-ttu-id="65129-157">**Cancellazione percorso locale directory** (*fx_directory_local_path_clear*)</span><span class="sxs-lookup"><span data-stu-id="65129-157">**Directory Local Path Clear** (*fx_directory_local_path_clear*)</span></span> |
| ![Icona di Get percorso locale della directory](./media/user-guide/fx-events/image25.png)    | <span data-ttu-id="65129-159">**Percorso locale della directory Get** (*fx_directory_local_path_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-159">**Directory Local Path Get** (*fx_directory_local_path_get*)</span></span> |
| ![Icona di ripristino del percorso locale della directory](./media/user-guide/fx-events/image26.png)    | <span data-ttu-id="65129-161">**Ripristino percorso locale directory** (*fx_directory_local_path_restore*)</span><span class="sxs-lookup"><span data-stu-id="65129-161">**Directory Local Path Restore** (*fx_directory_local_path_restore*)</span></span> |
| ![Icona del set di percorsi locali della directory](./media/user-guide/fx-events/image27.png)    | <span data-ttu-id="65129-163">**Set di percorsi locali della directory** (*fx_directory_local_path_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-163">**Directory Local Path Set** (*fx_directory_local_path_set*)</span></span> |
| ![Icona Ottieni nome lungo directory](./media/user-guide/fx-events/image28.png)    | <span data-ttu-id="65129-165">**Nome lungo directory Get** (*fx_directory_long_name_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-165">**Directory Long Name Get** (*fx_directory_long_name_get*)</span></span> |
| ![Icona di test nome directory](./media/user-guide/fx-events/image29.png)    | <span data-ttu-id="65129-167">**Test nome directory** (*fx_directory_name_test*)</span><span class="sxs-lookup"><span data-stu-id="65129-167">**Directory Name Test** (*fx_directory_name_test*)</span></span> |
| ![Icona di ricerca voce successiva directory](./media/user-guide/fx-events/image30.png)    | <span data-ttu-id="65129-169">**Ricerca voce successiva directory** (*fx_directory_next_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="65129-169">**Directory Next Entry Find** (*fx_directory_next_entry_find*)</span></span> |
| ![Icona di ricerca voce completa successiva alla directory](./media/user-guide/fx-events/image31.png)    | <span data-ttu-id="65129-171">**Ricerca voce completa successiva directory** (*fx_directory_next_full_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="65129-171">**Directory Next Full Entry Find** (*fx_directory_next_full_entry_find*)</span></span> |
| ![Icona Rinomina Directory](./media/user-guide/fx-events/image32.png)    | <span data-ttu-id="65129-173">**Ridenominazione directory** (*fx_directory_rename*)</span><span class="sxs-lookup"><span data-stu-id="65129-173">**Directory Rename** (*fx_directory_rename*)</span></span> |
| ![Icona di Get nome breve directory](./media/user-guide/fx-events/image33.png)    | <span data-ttu-id="65129-175">**Nome breve directory Get** (*fx_directory_short_name_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-175">**Directory Short Name Get** (*fx_directory_short_name_get*)</span></span> |
| ![Icona alloca file](./media/user-guide/fx-events/image34.png)    | <span data-ttu-id="65129-177">**Alloca file** (*fx_file_allocate*)</span><span class="sxs-lookup"><span data-stu-id="65129-177">**File Allocate** (*fx_file_allocate*)</span></span> |
| ![Icona di lettura attributi file](./media/user-guide/fx-events/image35.png)    | <span data-ttu-id="65129-179">**Attributi di file letti** (*fx_file_attributes_read*)</span><span class="sxs-lookup"><span data-stu-id="65129-179">**File Attributes Read** (*fx_file_attributes_read*)</span></span> |
| ![Icona set di attributi file](./media/user-guide/fx-events/image36.png)    | <span data-ttu-id="65129-181">**Attributi file impostati** (*fx_file_attributes_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-181">**File Attributes Set** (*fx_file_attributes_set*)</span></span> |
| ![Icona di allocazione file per il massimo sforzo](./media/user-guide/fx-events/image37.png)    | <span data-ttu-id="65129-183">**File per il massimo sforzo allocato** (*fx_file_best_effort_allocate*)</span><span class="sxs-lookup"><span data-stu-id="65129-183">**File Best Effort Allocate** (*fx_file_best_effort_allocate*)</span></span> |
| ![Icona di chiusura file](./media/user-guide/fx-events/image38.png)    | <span data-ttu-id="65129-185">**Chiusura file** (*fx_file_close*)</span><span class="sxs-lookup"><span data-stu-id="65129-185">**File Close** (*fx_file_close*)</span></span> |
| ![Icona Crea file](./media/user-guide/fx-events/image39.png)    | <span data-ttu-id="65129-187">**Creazione file** (*fx_file_create*)</span><span class="sxs-lookup"><span data-stu-id="65129-187">**File Create** (*fx_file_create*)</span></span> |
| ![Icona del set di data e ora del file](./media/user-guide/fx-events/image40.png)    | <span data-ttu-id="65129-189">**Data/ora file** (*fx_file_date_time_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-189">**File Date Time Set** (*fx_file_date_time_set*)</span></span> |
| ![Icona Elimina file](./media/user-guide/fx-events/image41.png)    | <span data-ttu-id="65129-191">**Eliminazione file** (*fx_file_delete*)</span><span class="sxs-lookup"><span data-stu-id="65129-191">**File Delete** (*fx_file_delete*)</span></span> |
| ![Icona Apri file](./media/user-guide/fx-events/image42.png)    | <span data-ttu-id="65129-193">**Apertura file** (*fx_file_open*)</span><span class="sxs-lookup"><span data-stu-id="65129-193">**File Open** (*fx_file_open*)</span></span> |
| ![Icona lettura file](./media/user-guide/fx-events/image43.png)    | <span data-ttu-id="65129-195">**Lettura file** (*fx_file_read*)</span><span class="sxs-lookup"><span data-stu-id="65129-195">**File Read** (*fx_file_read*)</span></span> |
| ![Icona di ricerca relativa ai file](./media/user-guide/fx-events/image44.png)    | <span data-ttu-id="65129-197">**Ricerca relativa ai file** (*fx_file_relative_seek*)</span><span class="sxs-lookup"><span data-stu-id="65129-197">**File Relative Seek** (*fx_file_relative_seek*)</span></span> |
| ![Icona Rinomina file](./media/user-guide/fx-events/image45.png)    | <span data-ttu-id="65129-199">**Ridenominazione file** (*fx_file_rename*)</span><span class="sxs-lookup"><span data-stu-id="65129-199">**File Rename** (*fx_file_rename*)</span></span> |
| ![Icona di ricerca file](./media/user-guide/fx-events/image46.png)    | <span data-ttu-id="65129-201">**Ricerca file** (*fx_file_seek*)</span><span class="sxs-lookup"><span data-stu-id="65129-201">**File Seek** (*fx_file_seek*)</span></span> |
| ![Icona troncamento file](./media/user-guide/fx-events/image47.png)    | <span data-ttu-id="65129-203">**Troncamento file** (*fx_file_truncate*)</span><span class="sxs-lookup"><span data-stu-id="65129-203">**File Truncate** (*fx_file_truncate*)</span></span> |
| ![Icona versione troncamento file](./media/user-guide/fx-events/image48.png)    | <span data-ttu-id="65129-205">**Versione troncamento file** (*fx_file_truncate_release*)</span><span class="sxs-lookup"><span data-stu-id="65129-205">**File Truncate Release** (*fx_file_truncate_release*)</span></span> |
| ![Icona scrittura file](./media/user-guide/fx-events/image49.png)    | <span data-ttu-id="65129-207">**Scrittura file** (*fx_file_write*)</span><span class="sxs-lookup"><span data-stu-id="65129-207">**File Write** (*fx_file_write*)</span></span> |
| ![Icona Interrompi supporto](./media/user-guide/fx-events/image50.png)    | <span data-ttu-id="65129-209">**Interruzione supporto** (*fx_media_abort*)</span><span class="sxs-lookup"><span data-stu-id="65129-209">**Media Abort** (*fx_media_abort*)</span></span> |
| ![Icona di invalidamento della cache multimediale](./media/user-guide/fx-events/image51.png)    | <span data-ttu-id="65129-211">**Media cache invalidata** (*fx_media_cache_invalidate*)</span><span class="sxs-lookup"><span data-stu-id="65129-211">**Media Cache Invalidate** (*fx_media_cache_invalidate*)</span></span> |
| ![Icona del controllo del supporto](./media/user-guide/fx-events/image52.png)    | <span data-ttu-id="65129-213">**Controllo supporto** (*fx_media_check*)</span><span class="sxs-lookup"><span data-stu-id="65129-213">**Media Check** (*fx_media_check*)</span></span> |
| ![\* Icona di chiusura del supporto](./media/user-guide/fx-events/image53.png)    | <span data-ttu-id="65129-215">**Chiusura media** (*fx_media_close*)</span><span class="sxs-lookup"><span data-stu-id="65129-215">**Media Close** (*fx_media_close*)</span></span> |
| ![Icona di scaricamento supporti](./media/user-guide/fx-events/image54.png)    | <span data-ttu-id="65129-217">**Scaricamento supporti** (*fx_media_flush*)</span><span class="sxs-lookup"><span data-stu-id="65129-217">**Media Flush** (*fx_media_flush*)</span></span> |
| ![Icona formato supporto](./media/user-guide/fx-events/image55.png)    | <span data-ttu-id="65129-219">**Formato supporto** (*fx_media_format*)</span><span class="sxs-lookup"><span data-stu-id="65129-219">**Media Format** (*fx_media_format*)</span></span> |
| ![Icona del supporto aperto](./media/user-guide/fx-events/image56.png)    | <span data-ttu-id="65129-221">**Supporto aperto** (*fx_media_open*)</span><span class="sxs-lookup"><span data-stu-id="65129-221">**Media Open** (*fx_media_open*)</span></span> |
| ![Icona di lettura del supporto](./media/user-guide/fx-events/image57.png)    | <span data-ttu-id="65129-223">**Media Read** (*fx_media_read*)</span><span class="sxs-lookup"><span data-stu-id="65129-223">**Media Read** (*fx_media_read*)</span></span> |
| ![Icona spazio multimediale disponibile](./media/user-guide/fx-events/image58.png)    | <span data-ttu-id="65129-225">**Spazio multimediale disponibile** (*fx_media_space_available*)</span><span class="sxs-lookup"><span data-stu-id="65129-225">**Media Space Available** (*fx_media_space_available*)</span></span> |
| ![Icona Ottieni volume multimediale](./media/user-guide/fx-events/image59.png)    | <span data-ttu-id="65129-227">**Volume multimediale Get** (*fx_media_volume_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-227">**Media Volume Get** (*fx_media_volume_get*)</span></span> |
| ![Icona del set di volumi multimediali](./media/user-guide/fx-events/image60.png)    | <span data-ttu-id="65129-229">**Set di volumi multimediali** (*fx_media_volume_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-229">**Media Volume Set** (*fx_media_volume_set*)</span></span> |
| ![Icona scrittura supporti](./media/user-guide/fx-events/image61.png)    | <span data-ttu-id="65129-231">**Scrittura supporti** (*fx_media_write*)</span><span class="sxs-lookup"><span data-stu-id="65129-231">**Media Write** (*fx_media_write*)</span></span> |
| ![Icona Data di sistema Get](./media/user-guide/fx-events/image62.png)    | <span data-ttu-id="65129-233">**Data di sistema Get** (*fx_system_date_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-233">**System Date Get** (*fx_system_date_get*)</span></span> |
| ![Icona del set di dati di sistema](./media/user-guide/fx-events/image63.png)    | <span data-ttu-id="65129-235">**Set di date di sistema** (*fx_system_date_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-235">**System Date Set** (*fx_system_date_set*)</span></span> |
| ![Icona Inizializzazione sistema](./media/user-guide/fx-events/image64.png)    | <span data-ttu-id="65129-237">**Inizializzazione sistema** (*fx_system_initialize*)</span><span class="sxs-lookup"><span data-stu-id="65129-237">**System Initialize** (*fx_system_initialize*)</span></span> |
| ![Icona dell'ora di sistema Get](./media/user-guide/fx-events/image65.png)    | <span data-ttu-id="65129-239">**Tempo di sistema Get** (*fx_system_time_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-239">**System Time Get** (*fx_system_time_get*)</span></span> |
| ![Icona del set di impostazioni dell'ora di sistema](./media/user-guide/fx-events/image66.png)    | <span data-ttu-id="65129-241">**Impostazione dell'ora di sistema** (*fx_system_time_set*)</span><span class="sxs-lookup"><span data-stu-id="65129-241">**System Time Set** (*fx_system_time_set*)</span></span> |
| ![Icona di creazione directory Unicode](./media/user-guide/fx-events/image67.png)    | <span data-ttu-id="65129-243">**Creazione directory Unicode** (*fx_unicode_directory_create*)</span><span class="sxs-lookup"><span data-stu-id="65129-243">**Unicode Directory Create** (*fx_unicode_directory_create*)</span></span> |
| ![Icona Rinomina Directory Unicode](./media/user-guide/fx-events/image68.png)    | <span data-ttu-id="65129-245">**Ridenominazione directory Unicode** (*fx_unicode_directory_rename*)</span><span class="sxs-lookup"><span data-stu-id="65129-245">**Unicode Directory Rename** (*fx_unicode_directory_rename*)</span></span> |
| ![Icona di creazione file Unicode](./media/user-guide/fx-events/image69.png)    | <span data-ttu-id="65129-247">**Creazione di file Unicode** (*fx_unicode_file_create*)</span><span class="sxs-lookup"><span data-stu-id="65129-247">**Unicode File Create** (*fx_unicode_file_create*)</span></span> |
| ![Icona Rinomina file Unicode](./media/user-guide/fx-events/image70.png)    | <span data-ttu-id="65129-249">**Ridenominazione di file Unicode** (*fx_unicode_file_rename*)</span><span class="sxs-lookup"><span data-stu-id="65129-249">**Unicode File Rename** (*fx_unicode_file_rename*)</span></span> |
| ![Icona di ottenere la lunghezza Unicode](./media/user-guide/fx-events/image71.png)    | <span data-ttu-id="65129-251">**Lunghezza Unicode get** (*fx_unicode_length_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-251">**Unicode Lenght Get** (*fx_unicode_length_get*)</span></span> |
| ![Icona Ottieni nome Unicode](./media/user-guide/fx-events/image72.png)    | <span data-ttu-id="65129-253">**Nome Unicode get** (*fx_unicode_name_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-253">**Unicode Name Get** (*fx_unicode_name_get*)</span></span> |
| ![Icona di Get con nome breve Unicode](./media/user-guide/fx-events/image73.png)    | <span data-ttu-id="65129-255">**Nome breve Unicode get** (*fx_unicode_short_name_get*)</span><span class="sxs-lookup"><span data-stu-id="65129-255">**Unicode Short Name Get** (*fx_unicode_short_name_get*)</span></span> |

## <a name="event-descriptions"></a><span data-ttu-id="65129-256">Descrizioni di eventi</span><span class="sxs-lookup"><span data-stu-id="65129-256">Event Descriptions</span></span>

<span data-ttu-id="65129-257">Di seguito viene descritto ogni singolo evento.</span><span class="sxs-lookup"><span data-stu-id="65129-257">The following describes each individual event.</span></span>

### <a name="internal-logical-sector-cache-miss"></a><span data-ttu-id="65129-258">Mancato riscontro nella cache del settore logico interno</span><span class="sxs-lookup"><span data-stu-id="65129-258">Internal Logical Sector Cache Miss</span></span> 

#### <a name="internal-logical-sector-cache-miss"></a><span data-ttu-id="65129-259">Mancato riscontro nella cache del settore logico interno</span><span class="sxs-lookup"><span data-stu-id="65129-259">Internal logical sector cache miss</span></span>

<span data-ttu-id="65129-260">**Icona** ![ di Icona di mancata memorizzazione nella cache del settore logico interno](./media/user-guide/fx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="65129-260">**Icon** ![Internal logical sector cache miss icon](./media/user-guide/fx-events/image1.png)</span></span>

<span data-ttu-id="65129-261">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-261">**Description**</span></span>

<span data-ttu-id="65129-262">Questo evento rappresenta un mancato riscontro nella cache del settore logico FileX interno.</span><span class="sxs-lookup"><span data-stu-id="65129-262">This event represents an internal FileX logical sector cache miss.</span></span>

<span data-ttu-id="65129-263">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-263">**Information Fields**</span></span>

- <span data-ttu-id="65129-264">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-264">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-265">Informazioni sul campo 2: settore.</span><span class="sxs-lookup"><span data-stu-id="65129-265">Info Field 2: Sector.</span></span>
- <span data-ttu-id="65129-266">Campo info 3: Totale mancati riscontri.</span><span class="sxs-lookup"><span data-stu-id="65129-266">Info Field 3: Total misses.</span></span>
- <span data-ttu-id="65129-267">Informazioni sul campo 4: dimensioni della cache.</span><span class="sxs-lookup"><span data-stu-id="65129-267">Info Field 4: Cache size.</span></span>

### <a name="internal-directory-cache-miss"></a><span data-ttu-id="65129-268">Mancata memorizzazione nella cache della directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-268">Internal Directory Cache Miss</span></span>

#### <a name="internal-directory-cache-miss"></a><span data-ttu-id="65129-269">Mancata memorizzazione nella cache della directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-269">Internal directory cache miss</span></span>

<span data-ttu-id="65129-270">**Icona** ![ di Icona di mancata memorizzazione nella cache della directory interna](./media/user-guide/fx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="65129-270">**Icon** ![Internal directory cache miss icon](./media/user-guide/fx-events/image2.png)</span></span>

<span data-ttu-id="65129-271">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-271">**Description**</span></span> 

<span data-ttu-id="65129-272">Questo evento rappresenta un mancato riscontro nella cache della directory FileX interna.</span><span class="sxs-lookup"><span data-stu-id="65129-272">This event represents an internal FileX directory cache miss.</span></span>

<span data-ttu-id="65129-273">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-273">**Information Fields**</span></span>

- <span data-ttu-id="65129-274">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-274">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-275">Campo informazioni 2: Totale mancati riscontri.</span><span class="sxs-lookup"><span data-stu-id="65129-275">Info Field 2: Total misses.</span></span>
- <span data-ttu-id="65129-276">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-276">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-277">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-277">Info Field 4: Not used.</span></span>

### <a name="internal-media-flush"></a><span data-ttu-id="65129-278">Scaricamento multimediale interno</span><span class="sxs-lookup"><span data-stu-id="65129-278">Internal Media Flush</span></span> 

#### <a name="internal-media-flush"></a><span data-ttu-id="65129-279">Scaricamento multimediale interno</span><span class="sxs-lookup"><span data-stu-id="65129-279">Internal media flush</span></span>

<span data-ttu-id="65129-280">**Icona** ![ di Icona di svuotamento supporti interni](./media/user-guide/fx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="65129-280">**Icon** ![Internal media flush icon](./media/user-guide/fx-events/image3.png)</span></span>

<span data-ttu-id="65129-281">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-281">**Description**</span></span>

<span data-ttu-id="65129-282">Questo evento rappresenta uno scaricamento multimediale FileX interno.</span><span class="sxs-lookup"><span data-stu-id="65129-282">This event represents an internal FileX media flush.</span></span>

<span data-ttu-id="65129-283">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-283">**Information Fields**</span></span>

- <span data-ttu-id="65129-284">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-284">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-285">Campo informazioni 2: numero di settori modificati.</span><span class="sxs-lookup"><span data-stu-id="65129-285">Info Field 2: Number of dirty sectors.</span></span>
- <span data-ttu-id="65129-286">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-286">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-287">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-287">Info Field 4: Not used.</span></span>


### <a name="internal-directory-entry-read"></a><span data-ttu-id="65129-288">Lettura voce directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-288">Internal Directory Entry Read</span></span> 

#### <a name="internal-directory-entry-read"></a><span data-ttu-id="65129-289">Lettura voce directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-289">Internal directory entry read</span></span>

<span data-ttu-id="65129-290">**Icona** ![ di Icona di lettura della voce di directory interna](./media/user-guide/fx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="65129-290">**Icon** ![Internal directory entry read icon](./media/user-guide/fx-events/image4.png)</span></span>

<span data-ttu-id="65129-291">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-291">**Description**</span></span>

<span data-ttu-id="65129-292">Questo evento rappresenta un evento di lettura della voce di directory FileX interna.</span><span class="sxs-lookup"><span data-stu-id="65129-292">This event represents an internal FileX directory entry read event.</span></span>

<span data-ttu-id="65129-293">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-293">**Information Fields**</span></span>

- <span data-ttu-id="65129-294">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-294">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-295">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-295">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-296">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-296">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-297">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-297">Info Field 4: Not used.</span></span>

### <a name="internal-directory-entry-write"></a><span data-ttu-id="65129-298">Scrittura voce directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-298">Internal Directory Entry Write</span></span>

#### <a name="internal-directory-entry-write"></a><span data-ttu-id="65129-299">Scrittura voce directory interna</span><span class="sxs-lookup"><span data-stu-id="65129-299">Internal directory entry write</span></span>

<span data-ttu-id="65129-300">**Icona** ![ di Icona di scrittura della voce di directory interna](./media/user-guide/fx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="65129-300">**Icon** ![Internal directory entry write icon](./media/user-guide/fx-events/image5.png)</span></span>

<span data-ttu-id="65129-301">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-301">**Description**</span></span>

<span data-ttu-id="65129-302">Questo evento rappresenta un evento di scrittura della voce della directory FileX interna.</span><span class="sxs-lookup"><span data-stu-id="65129-302">This event represents an internal FileX directory entry write event.</span></span>

<span data-ttu-id="65129-303">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-303">**Information Fields**</span></span>

- <span data-ttu-id="65129-304">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-304">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-305">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-305">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-306">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-306">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-307">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-307">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-read"></a><span data-ttu-id="65129-308">Lettura driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-308">Internal I/O Driver Read</span></span> 

#### <a name="internal-io-driver-read"></a><span data-ttu-id="65129-309">Lettura driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-309">Internal I/O driver read</span></span> 

<span data-ttu-id="65129-310">**Icona** ![ di Icona lettura driver I/O interno](./media/user-guide/fx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="65129-310">**Icon** ![Internal I / O driver read icon](./media/user-guide/fx-events/image6.png)</span></span>

<span data-ttu-id="65129-311">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-311">**Description**</span></span> 

<span data-ttu-id="65129-312">Questo evento rappresenta un evento di lettura del driver I/O interno di FileX.</span><span class="sxs-lookup"><span data-stu-id="65129-312">This event represents an internal FileX I/O driver read event.</span></span>

<span data-ttu-id="65129-313">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-313">**Information Fields**</span></span>

- <span data-ttu-id="65129-314">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-314">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-315">Informazioni sul campo 2: settore.</span><span class="sxs-lookup"><span data-stu-id="65129-315">Info Field 2: Sector.</span></span>
- <span data-ttu-id="65129-316">Campo info 3: numero di settori.</span><span class="sxs-lookup"><span data-stu-id="65129-316">Info Field 3: Number of sectors.</span></span>
- <span data-ttu-id="65129-317">Informazioni sul campo 4: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-317">Info Field 4: Buffer pointer.</span></span>

### <a name="internal-io-driver-write"></a><span data-ttu-id="65129-318">Scrittura driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-318">Internal I/O Driver Write</span></span> 

#### <a name="internal-io-driver-write"></a><span data-ttu-id="65129-319">Scrittura driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-319">Internal I/O driver write</span></span> 

<span data-ttu-id="65129-320">**Icona** ![ di Icona scrittura driver I/O interno](./media/user-guide/fx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="65129-320">**Icon** ![Internal I / O driver write icon](./media/user-guide/fx-events/image7.png)</span></span>

<span data-ttu-id="65129-321">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-321">**Description**</span></span> 

<span data-ttu-id="65129-322">Questo evento rappresenta un evento di scrittura driver I/O interno di FileX.</span><span class="sxs-lookup"><span data-stu-id="65129-322">This event represents an internal FileX I/O driver write event.</span></span>

<span data-ttu-id="65129-323">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-323">**Information Fields**</span></span>

- <span data-ttu-id="65129-324">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-324">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-325">Informazioni sul campo 2: settore.</span><span class="sxs-lookup"><span data-stu-id="65129-325">Info Field 2: Sector.</span></span>
- <span data-ttu-id="65129-326">Campo info 3: numero di settori.</span><span class="sxs-lookup"><span data-stu-id="65129-326">Info Field 3: Number of sectors.</span></span>
- <span data-ttu-id="65129-327">Informazioni sul campo 4: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-327">Info Field 4: Buffer pointer.</span></span>

### <a name="internal-io-driver-flush"></a><span data-ttu-id="65129-328">Scaricamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-328">Internal I/O Driver Flush</span></span> 

#### <a name="internal-io-driver-flush"></a><span data-ttu-id="65129-329">Scaricamento driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-329">Internal I/O driver flush</span></span> 

<span data-ttu-id="65129-330">**Icona** ![ di Icona di svuotamento driver I/O interno](./media/user-guide/fx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="65129-330">**Icon** ![Internal I / O driver flush icon](./media/user-guide/fx-events/image8.png)</span></span>

<span data-ttu-id="65129-331">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-331">**Description**</span></span> 

<span data-ttu-id="65129-332">Questo evento rappresenta un evento di scaricamento del driver I/O interno di FileX.</span><span class="sxs-lookup"><span data-stu-id="65129-332">This event represents an internal FileX I/O driver flush event.</span></span>

<span data-ttu-id="65129-333">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-333">**Information Fields**</span></span>

- <span data-ttu-id="65129-334">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-334">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-335">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-335">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-336">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-336">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-337">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-337">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-abort"></a><span data-ttu-id="65129-338">Interruzione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-338">Internal I/O Driver Abort</span></span> 

#### <a name="internal-io-dirver-abort"></a><span data-ttu-id="65129-339">Interruzione I/O interna dirver</span><span class="sxs-lookup"><span data-stu-id="65129-339">Internal I/O dirver abort</span></span>

<span data-ttu-id="65129-340">**Icona** ![ di Icona di interruzione del driver I/O interno](./media/user-guide/fx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="65129-340">**Icon** ![Internal I / O driver abort icon](./media/user-guide/fx-events/image9.png)</span></span>

<span data-ttu-id="65129-341">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-341">**Description**</span></span>

<span data-ttu-id="65129-342">Questo evento rappresenta un evento di interruzione del driver I/O interno di FileX.</span><span class="sxs-lookup"><span data-stu-id="65129-342">This event represents an internal FileX I/O driver abort event.</span></span>

<span data-ttu-id="65129-343">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-343">**Information Fields**</span></span>

- <span data-ttu-id="65129-344">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-344">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-345">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-345">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-346">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-346">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-347">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-347">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-initialize"></a><span data-ttu-id="65129-348">Inizializzazione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-348">Internal I/O Driver Initialize</span></span> 

#### <a name="internal-io-driver-initialize"></a><span data-ttu-id="65129-349">Inizializzazione driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-349">Internal I/O driver initialize</span></span> 

<span data-ttu-id="65129-350">**Icona** ![ di Icona di inizializzazione del driver I/O interno](./media/user-guide/fx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="65129-350">**Icon** ![Internal I / O driver initialize icon](./media/user-guide/fx-events/image10.png)</span></span>

<span data-ttu-id="65129-351">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-351">**Description**</span></span> 

<span data-ttu-id="65129-352">Questo evento rappresenta un evento di inizializzazione del driver I/O interno di FileX.</span><span class="sxs-lookup"><span data-stu-id="65129-352">This event represents an internal FileX I/O driver initialize event.</span></span>

<span data-ttu-id="65129-353">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-353">**Information Fields**</span></span>

- <span data-ttu-id="65129-354">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-354">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-355">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-355">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-356">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-356">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-357">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-357">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-boot-sector-read"></a><span data-ttu-id="65129-358">Lettura settore di avvio driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-358">Internal I/O Driver Boot Sector Read</span></span> 

#### <a name="internal-io-driver-boot-sector-read"></a><span data-ttu-id="65129-359">Lettura settore di avvio driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-359">Internal I/O driver boot sector read</span></span> 

<span data-ttu-id="65129-360">**Icona** ![ di Icona di lettura del settore di avvio del driver I/O interno](./media/user-guide/fx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="65129-360">**Icon** ![Internal I / O driver boot sector read icon](./media/user-guide/fx-events/image11.png)</span></span>

<span data-ttu-id="65129-361">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-361">**Description**</span></span> 

<span data-ttu-id="65129-362">Questo evento rappresenta un evento di lettura del settore di avvio del driver di I/O FileX interno.</span><span class="sxs-lookup"><span data-stu-id="65129-362">This event represents an internal FileX I/O driver boot sector read event.</span></span>

<span data-ttu-id="65129-363">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-363">**Information Fields**</span></span>

- <span data-ttu-id="65129-364">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-364">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-365">Informazioni sul campo 2: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-365">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="65129-366">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-366">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-367">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-367">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-release-sectors"></a><span data-ttu-id="65129-368">Settori di rilascio driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="65129-368">Internal I/O Driver Release Sectors</span></span> 

#### <a name="internal-io-driver-release-sectors"></a><span data-ttu-id="65129-369">Settori di rilascio driver I/O interni</span><span class="sxs-lookup"><span data-stu-id="65129-369">Internal I/O driver release sectors</span></span> 

<span data-ttu-id="65129-370">**Icona** ![ di Icona settori di rilascio driver I/O interno](./media/user-guide/fx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="65129-370">**Icon** ![Internal I / O driver release sectors icon](./media/user-guide/fx-events/image12.png)</span></span>

<span data-ttu-id="65129-371">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-371">**Description**</span></span> 

<span data-ttu-id="65129-372">Questo evento rappresenta un evento Internal FileX I/O driver release sectors.</span><span class="sxs-lookup"><span data-stu-id="65129-372">This event represents an internal FileX I/O driver release sectors event.</span></span>

<span data-ttu-id="65129-373">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-373">**Information Fields**</span></span>

- <span data-ttu-id="65129-374">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-374">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-375">Informazioni sul campo 2: settore.</span><span class="sxs-lookup"><span data-stu-id="65129-375">Info Field 2: Sector.</span></span>
- <span data-ttu-id="65129-376">Campo info 3: numero di settori.</span><span class="sxs-lookup"><span data-stu-id="65129-376">Info Field 3: Number of sectors.</span></span>
- <span data-ttu-id="65129-377">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-377">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-boot-sector-write"></a><span data-ttu-id="65129-378">Scrittura settore di avvio driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-378">Internal I/O Driver Boot Sector Write</span></span>

#### <a name="internal-io-driver-boot-sector-write"></a><span data-ttu-id="65129-379">Scrittura settore di avvio driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-379">Internal I/O driver boot sector write</span></span> 

<span data-ttu-id="65129-380">**Icona** ![ di Icona di scrittura del settore di avvio del driver I/O interno](./media/user-guide/fx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="65129-380">**Icon** ![Internal I / O driver boot sector write icon](./media/user-guide/fx-events/image13.png)</span></span>

<span data-ttu-id="65129-381">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-381">**Description**</span></span> 

<span data-ttu-id="65129-382">Questo evento rappresenta un evento di scrittura del settore di avvio del driver di I/O FileX interno.</span><span class="sxs-lookup"><span data-stu-id="65129-382">This event represents an internal FileX I/O driver boot sector write event.</span></span>

<span data-ttu-id="65129-383">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-383">**Information Fields**</span></span>

- <span data-ttu-id="65129-384">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-384">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-385">Informazioni sul campo 2: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-385">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="65129-386">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-386">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-387">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-387">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="65129-388">Annulla inizializzazione del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-388">Internal I/O Driver Un-initialize</span></span> 

#### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="65129-389">Annulla inizializzazione del driver di I/O interno</span><span class="sxs-lookup"><span data-stu-id="65129-389">Internal I/O driver un-initialize</span></span> 

<span data-ttu-id="65129-390">**Icona** ![ di Icona di annullamento inizializzazione del driver I/O interno](./media/user-guide/fx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="65129-390">**Icon** ![Internal I / O driver un-initialize icon](./media/user-guide/fx-events/image14.png)</span></span>

<span data-ttu-id="65129-391">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-391">**Description**</span></span> 

<span data-ttu-id="65129-392">Questo evento rappresenta un evento di annullamento inizializzazione del driver di I/O FileX interno.</span><span class="sxs-lookup"><span data-stu-id="65129-392">This event represents an internal FileX I/O driver un-initialize event.</span></span>

<span data-ttu-id="65129-393">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-393">**Information Fields**</span></span>

- <span data-ttu-id="65129-394">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-394">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-395">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-395">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-396">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-396">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-397">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-397">Info Field 4: Not used.</span></span>
</blockquote></td>

### <a name="directory-attributes-read"></a><span data-ttu-id="65129-398">Attributi di directory letti</span><span class="sxs-lookup"><span data-stu-id="65129-398">Directory Attributes Read</span></span> 

#### <a name="fx_directory_attributes_read"></a><span data-ttu-id="65129-399">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="65129-399">fx_directory_attributes_read</span></span> 

<span data-ttu-id="65129-400">**Icona** ![ di Icona di lettura attributi directory](./media/user-guide/fx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="65129-400">**Icon** ![Directory attributes read icon](./media/user-guide/fx-events/image15.png)</span></span>

<span data-ttu-id="65129-401">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-401">**Description**</span></span> 

<span data-ttu-id="65129-402">Questo evento rappresenta un evento di lettura degli attributi della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-402">This event represents a directory attributes read event.</span></span>

<span data-ttu-id="65129-403">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-403">**Information Fields**</span></span>

- <span data-ttu-id="65129-404">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-404">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-405">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-405">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-406">Informazioni sul campo 3: attributi mappa di bit:</span><span class="sxs-lookup"><span data-stu-id="65129-406">Info Field 3: Attributes bit map:</span></span>

  | <span data-ttu-id="65129-407">Attributo</span><span class="sxs-lookup"><span data-stu-id="65129-407">Attribute</span></span>                         | <span data-ttu-id="65129-408">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-408">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-409">Sola lettura</span><span class="sxs-lookup"><span data-stu-id="65129-409">Read Only</span></span>                        | <span data-ttu-id="65129-410">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-410">(0x01)</span></span>  |
  |  <span data-ttu-id="65129-411">Nascosto</span><span class="sxs-lookup"><span data-stu-id="65129-411">Hidden</span></span>                           | <span data-ttu-id="65129-412">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-412">(0x02)</span></span>  |
  |  <span data-ttu-id="65129-413">Sistema</span><span class="sxs-lookup"><span data-stu-id="65129-413">System</span></span>                           | <span data-ttu-id="65129-414">0x04</span><span class="sxs-lookup"><span data-stu-id="65129-414">(0x04)</span></span>  |
  |  <span data-ttu-id="65129-415">Volume</span><span class="sxs-lookup"><span data-stu-id="65129-415">Volume</span></span>                           | <span data-ttu-id="65129-416">0x08</span><span class="sxs-lookup"><span data-stu-id="65129-416">(0x08)</span></span>  |
  |  <span data-ttu-id="65129-417">Directory</span><span class="sxs-lookup"><span data-stu-id="65129-417">Directory</span></span>                        | <span data-ttu-id="65129-418">0x10</span><span class="sxs-lookup"><span data-stu-id="65129-418">(0x10)</span></span>  |
  |  <span data-ttu-id="65129-419">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="65129-419">Archive</span></span>                          | <span data-ttu-id="65129-420">0x20</span><span class="sxs-lookup"><span data-stu-id="65129-420">(0x20)</span></span>  |
- <span data-ttu-id="65129-421">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-421">Info Field 4: Not used.</span></span>

### <a name="directory-attributes-set"></a><span data-ttu-id="65129-422">Attributi di directory impostati</span><span class="sxs-lookup"><span data-stu-id="65129-422">Directory Attributes Set</span></span> 

#### <a name="fx_directory_attributes_set"></a><span data-ttu-id="65129-423">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="65129-423">fx_directory_attributes_set</span></span> 

<span data-ttu-id="65129-424">**Icona** ![ di Icona set attributi](./media/user-guide/fx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="65129-424">**Icon** ![Attributes set icon](./media/user-guide/fx-events/image16.png)</span></span>

<span data-ttu-id="65129-425">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-425">**Description**</span></span> 

<span data-ttu-id="65129-426">Questo evento rappresenta una directory di un evento set di attributi di directory.</span><span class="sxs-lookup"><span data-stu-id="65129-426">This event represents a directory a directory attributes set event.</span></span>

<span data-ttu-id="65129-427">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-427">**Information Fields**</span></span>

- <span data-ttu-id="65129-428">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-428">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-429">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-429">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-430">Informazioni sul campo 3: attributi mappa di bit:</span><span class="sxs-lookup"><span data-stu-id="65129-430">Info Field 3: Attributes bit map:</span></span>

  |  <span data-ttu-id="65129-431">Attributo</span><span class="sxs-lookup"><span data-stu-id="65129-431">Attribute</span></span>                        | <span data-ttu-id="65129-432">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-432">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-433">Sola lettura</span><span class="sxs-lookup"><span data-stu-id="65129-433">Read Only</span></span>                        | <span data-ttu-id="65129-434">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-434">(0x01)</span></span>  |
  |  <span data-ttu-id="65129-435">Nascosto</span><span class="sxs-lookup"><span data-stu-id="65129-435">Hidden</span></span>                           | <span data-ttu-id="65129-436">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-436">(0x02)</span></span>  |
  |  <span data-ttu-id="65129-437">Sistema</span><span class="sxs-lookup"><span data-stu-id="65129-437">System</span></span>                           | <span data-ttu-id="65129-438">0x04</span><span class="sxs-lookup"><span data-stu-id="65129-438">(0x04)</span></span>  |
  |  <span data-ttu-id="65129-439">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="65129-439">Archive</span></span>                          | <span data-ttu-id="65129-440">0x20</span><span class="sxs-lookup"><span data-stu-id="65129-440">(0x20)</span></span>  |
- <span data-ttu-id="65129-441">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-441">Info Field 4: Not used.</span></span>

### <a name="directory-create"></a><span data-ttu-id="65129-442">Creazione Directory</span><span class="sxs-lookup"><span data-stu-id="65129-442">Directory Create</span></span> 

#### <a name="fx_directory_create"></a><span data-ttu-id="65129-443">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="65129-443">fx_directory_create</span></span>

<span data-ttu-id="65129-444">**Icona** ![ di Icona Crea directory](./media/user-guide/fx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="65129-444">**Icon** ![Directory create icon](./media/user-guide/fx-events/image17.png)</span></span>

<span data-ttu-id="65129-445">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-445">**Description**</span></span> 

<span data-ttu-id="65129-446">Questo evento rappresenta un evento di creazione della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-446">This event represents a directory create event.</span></span>

<span data-ttu-id="65129-447">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-447">**Information Fields**</span></span>

- <span data-ttu-id="65129-448">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-448">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-449">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-449">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-450">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-450">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-451">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-451">Info Field 4: Not used.</span></span>

### <a name="directory-default-get"></a><span data-ttu-id="65129-452">Impostazione predefinita directory Get</span><span class="sxs-lookup"><span data-stu-id="65129-452">Directory Default Get</span></span> 

#### <a name="fx_directory_default_get"></a><span data-ttu-id="65129-453">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="65129-453">fx_directory_default_get</span></span> 

<span data-ttu-id="65129-454">**Icona** ![ di Icona di Get predefinita della directory](./media/user-guide/fx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="65129-454">**Icon** ![Directory default get icon](./media/user-guide/fx-events/image18.png)</span></span>

<span data-ttu-id="65129-455">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-455">**Description**</span></span> 

<span data-ttu-id="65129-456">Questo evento rappresenta un evento set predefinito di directory.</span><span class="sxs-lookup"><span data-stu-id="65129-456">This event represents a directory default set event.</span></span>

<span data-ttu-id="65129-457">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-457">**Information Fields**</span></span>

- <span data-ttu-id="65129-458">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-458">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-459">Informazioni sul campo 2: puntatore al nome del percorso restituito.</span><span class="sxs-lookup"><span data-stu-id="65129-459">Info Field 2: Pointer to return path name.</span></span>
- <span data-ttu-id="65129-460">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-460">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-461">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-461">Info Field 4: Not used.</span></span>

### <a name="directory-default-set"></a><span data-ttu-id="65129-462">Set predefinito directory</span><span class="sxs-lookup"><span data-stu-id="65129-462">Directory Default Set</span></span> 

#### <a name="fx_directory_default_set"></a><span data-ttu-id="65129-463">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="65129-463">fx_directory_default_set</span></span> 

<span data-ttu-id="65129-464">**Icona** ![ di Icona set predefinito directory](./media/user-guide/fx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="65129-464">**Icon** ![Directory default set icon](./media/user-guide/fx-events/image19.png)</span></span>

<span data-ttu-id="65129-465">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-465">**Description**</span></span> 

<span data-ttu-id="65129-466">Questo evento rappresenta un evento set predefinito di directory.</span><span class="sxs-lookup"><span data-stu-id="65129-466">This event represents a directory default set event.</span></span>

<span data-ttu-id="65129-467">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-467">**Information Fields**</span></span>

- <span data-ttu-id="65129-468">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-468">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-469">Informazioni sul campo 2: puntatore al nuovo nome di percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="65129-469">Info Field 2: Pointer to new default path name.</span></span>
- <span data-ttu-id="65129-470">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-470">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-471">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-471">Info Field 4: Not used.</span></span>

### <a name="directory-delete"></a><span data-ttu-id="65129-472">Eliminazione directory</span><span class="sxs-lookup"><span data-stu-id="65129-472">Directory Delete</span></span> 

#### <a name="fx_directory_delete"></a><span data-ttu-id="65129-473">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="65129-473">fx_directory_delete</span></span>

<span data-ttu-id="65129-474">**Icona** ![ di Icona di eliminazione directory](./media/user-guide/fx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="65129-474">**Icon** ![Directory delete icon](./media/user-guide/fx-events/image20.png)</span></span>

<span data-ttu-id="65129-475">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-475">**Description**</span></span> 

<span data-ttu-id="65129-476">Questo evento rappresenta un evento di eliminazione della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-476">This event represents a directory delete event.</span></span>

<span data-ttu-id="65129-477">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-477">**Information Fields**</span></span>
- <span data-ttu-id="65129-478">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-478">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-479">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-479">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-480">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-480">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-481">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-481">Info Field 4: Not used.</span></span>

### <a name="directory-first-entry-find"></a><span data-ttu-id="65129-482">Ricerca nella prima voce della directory</span><span class="sxs-lookup"><span data-stu-id="65129-482">Directory First Entry Find</span></span> 

#### <a name="fx_directory_first_entry_find"></a><span data-ttu-id="65129-483">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="65129-483">fx_directory_first_entry_find</span></span>

<span data-ttu-id="65129-484">**Icona** ![ di Icona trova della prima voce di directory](./media/user-guide/fx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="65129-484">**Icon** ![Directory first entry find icon](./media/user-guide/fx-events/image21.png)</span></span>

<span data-ttu-id="65129-485">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-485">**Description**</span></span> 

<span data-ttu-id="65129-486">Questo evento rappresenta un evento di ricerca della prima voce di directory.</span><span class="sxs-lookup"><span data-stu-id="65129-486">This event represents a directory first entry find event.</span></span>

<span data-ttu-id="65129-487">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-487">**Information Fields**</span></span>

- <span data-ttu-id="65129-488">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-488">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-489">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-489">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-490">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-490">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-491">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-491">Info Field 4: Not used.</span></span>

### <a name="directory-first-full-entry-find"></a><span data-ttu-id="65129-492">Ricerca della prima voce completa directory</span><span class="sxs-lookup"><span data-stu-id="65129-492">Directory First Full Entry Find</span></span> 

#### <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="65129-493">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="65129-493">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="65129-494">**Icona** ![ di Icona di ricerca della prima voce completa della directory](./media/user-guide/fx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="65129-494">**Icon** ![Directory first full entry find icon](./media/user-guide/fx-events/image22.png)</span></span>

<span data-ttu-id="65129-495">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-495">**Description**</span></span> 

<span data-ttu-id="65129-496">Questo evento rappresenta un evento di ricerca della prima voce completa della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-496">This event represents a directory first full entry find event.</span></span>

<span data-ttu-id="65129-497">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-497">**Information Fields**</span></span>

- <span data-ttu-id="65129-498">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-498">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-499">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-499">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-500">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-500">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-501">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-501">Info Field 4: Not used.</span></span>

### <a name="directory-information-get"></a><span data-ttu-id="65129-502">Informazioni di directory Get</span><span class="sxs-lookup"><span data-stu-id="65129-502">Directory Information Get</span></span> 

#### <a name="fx_directory_information_get"></a><span data-ttu-id="65129-503">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="65129-503">fx_directory_information_get</span></span>

<span data-ttu-id="65129-504">**Icona** ![ di Icona delle informazioni di directory Get](./media/user-guide/fx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="65129-504">**Icon** ![Directory information get icon](./media/user-guide/fx-events/image23.png)</span></span>

<span data-ttu-id="65129-505">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-505">**Description**</span></span> 

<span data-ttu-id="65129-506">Questo evento rappresenta un evento di ottenere informazioni sulla directory.</span><span class="sxs-lookup"><span data-stu-id="65129-506">This event represents a directory information get event.</span></span>

<span data-ttu-id="65129-507">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-507">**Information Fields**</span></span>

- <span data-ttu-id="65129-508">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-508">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-509">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-509">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-510">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-510">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-511">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-511">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-clear"></a><span data-ttu-id="65129-512">Cancellazione percorso locale directory</span><span class="sxs-lookup"><span data-stu-id="65129-512">Directory Local Path Clear</span></span> 

#### <a name="fx_directory_local_path_clear"></a><span data-ttu-id="65129-513">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="65129-513">fx_directory_local_path_clear</span></span>

<span data-ttu-id="65129-514">**Icona** ![ di Icona Cancella percorso locale directory](./media/user-guide/fx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="65129-514">**Icon** ![Directory local path clear icon](./media/user-guide/fx-events/image24.png)</span></span>

<span data-ttu-id="65129-515">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-515">**Description**</span></span> 

<span data-ttu-id="65129-516">Questo evento rappresenta un evento di cancellazione del percorso locale della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-516">This event represents a directory local path clear event.</span></span>

<span data-ttu-id="65129-517">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-517">**Information Fields**</span></span>

- <span data-ttu-id="65129-518">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-518">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-519">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-519">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-520">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-520">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-521">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-521">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-get"></a><span data-ttu-id="65129-522">Percorso locale di directory Get</span><span class="sxs-lookup"><span data-stu-id="65129-522">Directory Local Path Get</span></span> 

#### <a name="fx_directory_local_path_get"></a><span data-ttu-id="65129-523">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="65129-523">fx_directory_local_path_get</span></span>

<span data-ttu-id="65129-524">**Icona** ![ di Icona di Get percorso locale della directory](./media/user-guide/fx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="65129-524">**Icon** ![Directory local path get icon](./media/user-guide/fx-events/image25.png)</span></span>

<span data-ttu-id="65129-525">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-525">**Description**</span></span> 

<span data-ttu-id="65129-526">Questo evento rappresenta un evento di Get percorso locale della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-526">This event represents a directory local path get event.</span></span>

<span data-ttu-id="65129-527">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-527">**Information Fields**</span></span>

- <span data-ttu-id="65129-528">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-528">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-529">Informazioni sul campo 2: puntatore al nome del percorso restituito.</span><span class="sxs-lookup"><span data-stu-id="65129-529">Info Field 2: Pointer to return path name.</span></span>
- <span data-ttu-id="65129-530">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-530">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-531">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-531">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-restore"></a><span data-ttu-id="65129-532">Ripristino del percorso locale della directory</span><span class="sxs-lookup"><span data-stu-id="65129-532">Directory Local Path Restore</span></span> 

#### <a name="fx_directory_local_path_restore"></a><span data-ttu-id="65129-533">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="65129-533">fx_directory_local_path_restore</span></span>

<span data-ttu-id="65129-534">**Icona** ![ di Icona di ripristino del percorso locale della directory](./media/user-guide/fx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="65129-534">**Icon** ![Directory local path restore icon](./media/user-guide/fx-events/image26.png)</span></span>

<span data-ttu-id="65129-535">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-535">**Description**</span></span> 

<span data-ttu-id="65129-536">Questo evento rappresenta un evento di ripristino del percorso locale della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-536">This event represents a directory local path restore event.</span></span>

<span data-ttu-id="65129-537">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-537">**Information Fields**</span></span>

- <span data-ttu-id="65129-538">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-538">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-539">Informazioni sul campo 2: puntatore alla struttura del percorso locale.</span><span class="sxs-lookup"><span data-stu-id="65129-539">Info Field 2: Pointer to local path structure.</span></span>
- <span data-ttu-id="65129-540">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-540">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-541">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-541">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-set"></a><span data-ttu-id="65129-542">Set di percorsi locali della directory</span><span class="sxs-lookup"><span data-stu-id="65129-542">Directory Local Path Set</span></span> 

#### <a name="fx_directory_local_path_set"></a><span data-ttu-id="65129-543">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="65129-543">fx_directory_local_path_set</span></span>

<span data-ttu-id="65129-544">**Icona** ![ di Icona del set di percorsi locali della directory](./media/user-guide/fx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="65129-544">**Icon** ![Directory local path set icon](./media/user-guide/fx-events/image27.png)</span></span>

<span data-ttu-id="65129-545">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-545">**Description**</span></span> 

<span data-ttu-id="65129-546">Questo evento rappresenta un evento del set di percorsi locali della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-546">This event represents a directory local path set event.</span></span>

<span data-ttu-id="65129-547">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-547">**Information Fields**</span></span>

- <span data-ttu-id="65129-548">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-548">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-549">Informazioni sul campo 2: puntatore alla struttura del percorso locale.</span><span class="sxs-lookup"><span data-stu-id="65129-549">Info Field 2: Pointer to local path structure.</span></span>
- <span data-ttu-id="65129-550">Informazioni sul campo 3: puntatore al nuovo nome del percorso.</span><span class="sxs-lookup"><span data-stu-id="65129-550">Info Field 3: Pointer to new path name.</span></span>
- <span data-ttu-id="65129-551">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-551">Info Field 4: Not used.</span></span>

### <a name="directory-long-name-get"></a><span data-ttu-id="65129-552">Nome lungo directory Get</span><span class="sxs-lookup"><span data-stu-id="65129-552">Directory Long Name Get</span></span> 

#### <a name="fx_directory_long_name_get"></a><span data-ttu-id="65129-553">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="65129-553">fx_directory_long_name_get</span></span>

<span data-ttu-id="65129-554">**Icona** ![ di Icona Ottieni nome lungo directory](./media/user-guide/fx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="65129-554">**Icon** ![Directory long name get icon](./media/user-guide/fx-events/image28.png)</span></span>

<span data-ttu-id="65129-555">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-555">**Description**</span></span> 

<span data-ttu-id="65129-556">Questo evento rappresenta un evento di Get con nome lungo di directory.</span><span class="sxs-lookup"><span data-stu-id="65129-556">This event represents a directory long name get event.</span></span>

<span data-ttu-id="65129-557">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-557">**Information Fields**</span></span>

- <span data-ttu-id="65129-558">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-558">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-559">Informazioni sul campo 2: puntatore al nome file breve.</span><span class="sxs-lookup"><span data-stu-id="65129-559">Info Field 2: Pointer to short file name.</span></span>
- <span data-ttu-id="65129-560">Informazioni sul campo 3: puntatore al nome file lungo.</span><span class="sxs-lookup"><span data-stu-id="65129-560">Info Field 3: Pointer to long file name.</span></span>
- <span data-ttu-id="65129-561">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-561">Info Field 4: Not used.</span></span>

### <a name="directory-name-test"></a><span data-ttu-id="65129-562">Test nome directory</span><span class="sxs-lookup"><span data-stu-id="65129-562">Directory Name Test</span></span> 

#### <a name="fx_directory_name_test"></a><span data-ttu-id="65129-563">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="65129-563">fx_directory_name_test</span></span>

<span data-ttu-id="65129-564">**Icona** ![ di Icona di test nome directory](./media/user-guide/fx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="65129-564">**Icon** ![Directory name test icon](./media/user-guide/fx-events/image29.png)</span></span>

<span data-ttu-id="65129-565">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-565">**Description**</span></span> 

<span data-ttu-id="65129-566">Questo evento rappresenta un evento di test del nome di directory.</span><span class="sxs-lookup"><span data-stu-id="65129-566">This event represents a directory name test event.</span></span>

<span data-ttu-id="65129-567">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-567">**Information Fields**</span></span>

- <span data-ttu-id="65129-568">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-568">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-569">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-569">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-570">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-570">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-571">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-571">Info Field 4: Not used.</span></span>

### <a name="directory-next-entry-find"></a><span data-ttu-id="65129-572">Ricerca voce successiva directory</span><span class="sxs-lookup"><span data-stu-id="65129-572">Directory Next Entry Find</span></span> 

#### <a name="fx_directory_next_entry_find"></a><span data-ttu-id="65129-573">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="65129-573">fx_directory_next_entry_find</span></span>

<span data-ttu-id="65129-574">**Icona** ![ di Icona di ricerca voce successiva directory](./media/user-guide/fx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="65129-574">**Icon** ![Directory next entry find icon](./media/user-guide/fx-events/image30.png)</span></span>

<span data-ttu-id="65129-575">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-575">**Description**</span></span> 

<span data-ttu-id="65129-576">Questo evento rappresenta un evento di ricerca voce successiva della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-576">This event represents a directory next entry find event.</span></span>

<span data-ttu-id="65129-577">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-577">**Information Fields**</span></span>

- <span data-ttu-id="65129-578">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-578">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-579">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-579">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-580">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-580">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-581">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-581">Info Field 4: Not used.</span></span>

### <a name="directory-next-full-entry-find"></a><span data-ttu-id="65129-582">Ricerca voce completa successiva alla directory</span><span class="sxs-lookup"><span data-stu-id="65129-582">Directory Next Full Entry Find</span></span> 

#### <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="65129-583">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="65129-583">fx_directory_next_full_entry_find</span></span>

<span data-ttu-id="65129-584">**Icona** ![ di Icona di ricerca voce completa successiva alla directory](./media/user-guide/fx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="65129-584">**Icon** ![Directory next full entry find icon](./media/user-guide/fx-events/image31.png)</span></span>

<span data-ttu-id="65129-585">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-585">**Description**</span></span>

<span data-ttu-id="65129-586">Questo evento rappresenta una directory che segue l'evento di ricerca full entry.</span><span class="sxs-lookup"><span data-stu-id="65129-586">This event represents a directory next full entry find event.</span></span>

<span data-ttu-id="65129-587">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-587">**Information Fields**</span></span>

- <span data-ttu-id="65129-588">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-588">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-589">Informazioni sul campo 2: puntatore al nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-589">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="65129-590">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-590">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-591">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-591">Info Field 4: Not used.</span></span>

### <a name="directory-rename"></a><span data-ttu-id="65129-592">Ridenominazione directory</span><span class="sxs-lookup"><span data-stu-id="65129-592">Directory Rename</span></span> 

#### <a name="fx_directory_rename-event"></a><span data-ttu-id="65129-593">evento fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="65129-593">fx_directory_rename event</span></span>

<span data-ttu-id="65129-594">**Icona** ![ di Icona Rinomina Directory](./media/user-guide/fx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="65129-594">**Icon** ![Directory rename icon](./media/user-guide/fx-events/image32.png)</span></span>

<span data-ttu-id="65129-595">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-595">**Description**</span></span>

<span data-ttu-id="65129-596">Questo evento rappresenta un evento di ridenominazione della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-596">This event represents a directory rename event.</span></span>

<span data-ttu-id="65129-597">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-597">**Information Fields**</span></span>

- <span data-ttu-id="65129-598">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-598">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-599">Informazioni sul campo 2: puntatore al nome di directory precedente.</span><span class="sxs-lookup"><span data-stu-id="65129-599">Info Field 2: Pointer to old directory name.</span></span>
- <span data-ttu-id="65129-600">Informazioni sul campo 3: puntatore al nuovo nome della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-600">Info Field 3: Pointer to new directory name.</span></span>
- <span data-ttu-id="65129-601">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-601">Info Field 4: Not used.</span></span>

### <a name="directory-short-name-get"></a><span data-ttu-id="65129-602">Nome breve directory Get</span><span class="sxs-lookup"><span data-stu-id="65129-602">Directory Short Name Get</span></span> 

#### <a name="fx_directory_short_name_get"></a><span data-ttu-id="65129-603">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="65129-603">fx_directory_short_name_get</span></span>

<span data-ttu-id="65129-604">**Icona** ![ di Icona di Get nome breve directory](./media/user-guide/fx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="65129-604">**Icon** ![Directory short name get icon](./media/user-guide/fx-events/image33.png)</span></span>

<span data-ttu-id="65129-605">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-605">**Description**</span></span>

<span data-ttu-id="65129-606">Questo evento rappresenta un evento di ottenimento del nome breve della directory.</span><span class="sxs-lookup"><span data-stu-id="65129-606">This event represents a directory short name get event.</span></span>

<span data-ttu-id="65129-607">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-607">**Information Fields**</span></span> 

- <span data-ttu-id="65129-608">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-608">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-609">Informazioni sul campo 2: puntatore al nome file lungo.</span><span class="sxs-lookup"><span data-stu-id="65129-609">Info Field 2: Pointer to long file name.</span></span>
- <span data-ttu-id="65129-610">Informazioni sul campo 3: puntatore al nome file breve.</span><span class="sxs-lookup"><span data-stu-id="65129-610">Info Field 3: Pointer to short file name.</span></span>
- <span data-ttu-id="65129-611">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-611">Info Field 4: Not used.</span></span>

### <a name="file-allocate"></a><span data-ttu-id="65129-612">Alloca file</span><span class="sxs-lookup"><span data-stu-id="65129-612">File Allocate</span></span> 

#### <a name="fx_file_allocate"></a><span data-ttu-id="65129-613">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="65129-613">fx_file_allocate</span></span>

<span data-ttu-id="65129-614">**Icona** ![ di Icona alloca file](./media/user-guide/fx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="65129-614">**Icon** ![File allocate icon](./media/user-guide/fx-events/image34.png)</span></span>

<span data-ttu-id="65129-615">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-615">**Description**</span></span>

<span data-ttu-id="65129-616">Questo evento rappresenta un evento di allocazione di file.</span><span class="sxs-lookup"><span data-stu-id="65129-616">This event represents a file allocate event.</span></span>

<span data-ttu-id="65129-617">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-617">**Information Fields**</span></span>

- <span data-ttu-id="65129-618">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-618">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-619">Campo informazioni 2: dimensione richiesta.</span><span class="sxs-lookup"><span data-stu-id="65129-619">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="65129-620">Informazioni sul campo 3: dimensioni correnti.</span><span class="sxs-lookup"><span data-stu-id="65129-620">Info Field 3: Current size.</span></span>
- <span data-ttu-id="65129-621">Campo informazioni 4: nuove dimensioni.</span><span class="sxs-lookup"><span data-stu-id="65129-621">Info Field 4: New size.</span></span>

### <a name="file-attributes-read"></a><span data-ttu-id="65129-622">Lettura attributi file</span><span class="sxs-lookup"><span data-stu-id="65129-622">File Attributes Read</span></span> 

#### <a name="fx_file_attributes_read"></a><span data-ttu-id="65129-623">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="65129-623">fx_file_attributes_read</span></span>

<span data-ttu-id="65129-624">**Icona** ![ di Icona di lettura attributi file](./media/user-guide/fx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="65129-624">**Icon** ![File attributes read icon](./media/user-guide/fx-events/image35.png)</span></span>

<span data-ttu-id="65129-625">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-625">**Description**</span></span>

<span data-ttu-id="65129-626">Questo evento rappresenta un evento di lettura degli attributi del file.</span><span class="sxs-lookup"><span data-stu-id="65129-626">This event represents a file attributes read event.</span></span>

<span data-ttu-id="65129-627">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-627">**Information Fields**</span></span>

- <span data-ttu-id="65129-628">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-628">Info Field 1: Pointer to the media.</span></span> 
- <span data-ttu-id="65129-629">Informazioni sul campo 2: attributi mappa di bit:</span><span class="sxs-lookup"><span data-stu-id="65129-629">Info Field 2: Attributes bit map:</span></span>

  |  <span data-ttu-id="65129-630">Attribut</span><span class="sxs-lookup"><span data-stu-id="65129-630">Attribut</span></span>                         | <span data-ttu-id="65129-631">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-631">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-632">Sola lettura</span><span class="sxs-lookup"><span data-stu-id="65129-632">Read Only</span></span>                        | <span data-ttu-id="65129-633">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-633">(0x01)</span></span>  |
  |  <span data-ttu-id="65129-634">Nascosto</span><span class="sxs-lookup"><span data-stu-id="65129-634">Hidden</span></span>                           | <span data-ttu-id="65129-635">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-635">(0x02)</span></span>  |
  |  <span data-ttu-id="65129-636">Sistema</span><span class="sxs-lookup"><span data-stu-id="65129-636">System</span></span>                           | <span data-ttu-id="65129-637">0x04</span><span class="sxs-lookup"><span data-stu-id="65129-637">(0x04)</span></span>  |
  |  <span data-ttu-id="65129-638">Volume</span><span class="sxs-lookup"><span data-stu-id="65129-638">Volume</span></span>                           | <span data-ttu-id="65129-639">0x08</span><span class="sxs-lookup"><span data-stu-id="65129-639">(0x08)</span></span>  |
  |  <span data-ttu-id="65129-640">Directory</span><span class="sxs-lookup"><span data-stu-id="65129-640">Directory</span></span>                        | <span data-ttu-id="65129-641">0x10</span><span class="sxs-lookup"><span data-stu-id="65129-641">(0x10)</span></span>  |
  |  <span data-ttu-id="65129-642">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="65129-642">Archive</span></span>                          | <span data-ttu-id="65129-643">0x20</span><span class="sxs-lookup"><span data-stu-id="65129-643">(0x20)</span></span>  |
- <span data-ttu-id="65129-644">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-644">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-645">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-645">Info Field 4: Not used.</span></span>

### <a name="file-attributes-set"></a><span data-ttu-id="65129-646">Attributi file impostati</span><span class="sxs-lookup"><span data-stu-id="65129-646">File Attributes Set</span></span> 

#### <a name="fx_file_attributes_set"></a><span data-ttu-id="65129-647">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="65129-647">fx_file_attributes_set</span></span>

<span data-ttu-id="65129-648">**Icona** ![ di Icona set di attributi file](./media/user-guide/fx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="65129-648">**Icon** ![File attributes set icon](./media/user-guide/fx-events/image36.png)</span></span>

<span data-ttu-id="65129-649">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-649">**Description**</span></span> 

<span data-ttu-id="65129-650">Questo evento rappresenta un evento del set di attributi di file.</span><span class="sxs-lookup"><span data-stu-id="65129-650">This event represents a file attributes set event.</span></span>

<span data-ttu-id="65129-651">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-651">**Information Fields**</span></span>

- <span data-ttu-id="65129-652">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-652">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-653">Informazioni sul campo 2: puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="65129-653">Info Field 2: Pointer to file name.</span></span> 
- <span data-ttu-id="65129-654">Informazioni sul campo 3: attributi mappa di bit:</span><span class="sxs-lookup"><span data-stu-id="65129-654">Info Field 3: Attributes bit map:</span></span>

  | <span data-ttu-id="65129-655">Attributo</span><span class="sxs-lookup"><span data-stu-id="65129-655">Attribute</span></span>                         | <span data-ttu-id="65129-656">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-656">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-657">Sola lettura</span><span class="sxs-lookup"><span data-stu-id="65129-657">Read Only</span></span>                        | <span data-ttu-id="65129-658">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-658">(0x01)</span></span>  |
  |  <span data-ttu-id="65129-659">Nascosto</span><span class="sxs-lookup"><span data-stu-id="65129-659">Hidden</span></span>                           | <span data-ttu-id="65129-660">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-660">(0x02)</span></span>  |
  |  <span data-ttu-id="65129-661">Sistema</span><span class="sxs-lookup"><span data-stu-id="65129-661">System</span></span>                           | <span data-ttu-id="65129-662">0x04</span><span class="sxs-lookup"><span data-stu-id="65129-662">(0x04)</span></span>  |
  |  <span data-ttu-id="65129-663">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="65129-663">Archive</span></span>                          | <span data-ttu-id="65129-664">0x20</span><span class="sxs-lookup"><span data-stu-id="65129-664">(0x20)</span></span>  |
- <span data-ttu-id="65129-665">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-665">Info Field 4: Not used.</span></span>

### <a name="file-best-effort-allocate"></a><span data-ttu-id="65129-666">Allocazione di file per il massimo sforzo</span><span class="sxs-lookup"><span data-stu-id="65129-666">File Best Effort Allocate</span></span> 

#### <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="65129-667">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="65129-667">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="65129-668">**Icona** ![ di Icona di allocazione file per il massimo sforzo](./media/user-guide/fx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="65129-668">**Icon** ![File best effort allocate icon](./media/user-guide/fx-events/image37.png)</span></span>

<span data-ttu-id="65129-669">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-669">**Description**</span></span> 

<span data-ttu-id="65129-670">Questo evento rappresenta un evento di allocazione del Best effort di file.</span><span class="sxs-lookup"><span data-stu-id="65129-670">This event represents a file best effort allocate event.</span></span>

<span data-ttu-id="65129-671">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-671">**Information Fields**</span></span>

- <span data-ttu-id="65129-672">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-672">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-673">Campo informazioni 2: dimensione richiesta.</span><span class="sxs-lookup"><span data-stu-id="65129-673">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="65129-674">Info Field 3: dimensioni effettive allocate.</span><span class="sxs-lookup"><span data-stu-id="65129-674">Info Field 3: Actual size allocated.</span></span>
- <span data-ttu-id="65129-675">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-675">Info Field 4: Not used.</span></span>

### <a name="file-close"></a><span data-ttu-id="65129-676">Chiusura file</span><span class="sxs-lookup"><span data-stu-id="65129-676">File Close</span></span> 

#### <a name="fx_file_close"></a><span data-ttu-id="65129-677">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="65129-677">fx_file_close</span></span>

<span data-ttu-id="65129-678">**Icona** ![ di Icona di chiusura file](./media/user-guide/fx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="65129-678">**Icon** ![File close icon](./media/user-guide/fx-events/image38.png)</span></span>

<span data-ttu-id="65129-679">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-679">**Description**</span></span> 

<span data-ttu-id="65129-680">Questo evento rappresenta un evento di chiusura del file.</span><span class="sxs-lookup"><span data-stu-id="65129-680">This event represents a file close event.</span></span>

<span data-ttu-id="65129-681">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-681">**Information Fields**</span></span>

- <span data-ttu-id="65129-682">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-682">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-683">Informazioni sul campo 2: dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="65129-683">Info Field 2: File size.</span></span>
- <span data-ttu-id="65129-684">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-684">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-685">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-685">Info Field 4: Not used.</span></span>

### <a name="file-create"></a><span data-ttu-id="65129-686">Creazione file</span><span class="sxs-lookup"><span data-stu-id="65129-686">File Create</span></span>

#### <a name="fx_file_create"></a><span data-ttu-id="65129-687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="65129-687">fx_file_create</span></span>

<span data-ttu-id="65129-688">**Icona** ![ di Icona Crea file](./media/user-guide/fx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="65129-688">**Icon** ![File create icon](./media/user-guide/fx-events/image39.png)</span></span>

<span data-ttu-id="65129-689">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-689">**Description**</span></span>

<span data-ttu-id="65129-690">Questo evento rappresenta un evento di creazione di file.</span><span class="sxs-lookup"><span data-stu-id="65129-690">This event represents a file create event.</span></span>

<span data-ttu-id="65129-691">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-691">**Information Fields**</span></span>

- <span data-ttu-id="65129-692">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-692">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-693">Informazioni sul campo 2: puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="65129-693">Info Field 2: Pointer to file name.</span></span>
- <span data-ttu-id="65129-694">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-694">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-695">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-695">Info Field 4: Not used.</span></span>

### <a name="file-date-time-set"></a><span data-ttu-id="65129-696">Data/ora file impostato</span><span class="sxs-lookup"><span data-stu-id="65129-696">File Date Time Set</span></span> 

#### <a name="fx_file_date_time_set"></a><span data-ttu-id="65129-697">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="65129-697">fx_file_date_time_set</span></span>

<span data-ttu-id="65129-698">**Icona** ![ di Icona del set di data e ora del file](./media/user-guide/fx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="65129-698">**Icon** ![File date time set icon](./media/user-guide/fx-events/image40.png)</span></span>

<span data-ttu-id="65129-699">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-699">**Description**</span></span>

<span data-ttu-id="65129-700">Questo evento rappresenta un evento del set di data/ora del file.</span><span class="sxs-lookup"><span data-stu-id="65129-700">This event represents a file date/time set event.</span></span>

<span data-ttu-id="65129-701">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-701">**Information Fields**</span></span>

- <span data-ttu-id="65129-702">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-702">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-703">Informazioni sul campo 2: puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="65129-703">Info Field 2: Pointer to file name.</span></span>
- <span data-ttu-id="65129-704">Campo informazioni 3: anno.</span><span class="sxs-lookup"><span data-stu-id="65129-704">Info Field 3: Year.</span></span>
- <span data-ttu-id="65129-705">Campo informazioni 4: mese.</span><span class="sxs-lookup"><span data-stu-id="65129-705">Info Field 4: Month.</span></span>

### <a name="file-delete"></a><span data-ttu-id="65129-706">Eliminazione file</span><span class="sxs-lookup"><span data-stu-id="65129-706">File Delete</span></span> 

#### <a name="fx_file_delete"></a><span data-ttu-id="65129-707">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="65129-707">fx_file_delete</span></span>

<span data-ttu-id="65129-708">**Icona** ![ di Icona Elimina file](./media/user-guide/fx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="65129-708">**Icon** ![File delete icon](./media/user-guide/fx-events/image41.png)</span></span>

<span data-ttu-id="65129-709">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-709">**Description**</span></span>

<span data-ttu-id="65129-710">Questo evento rappresenta un evento di eliminazione di file.</span><span class="sxs-lookup"><span data-stu-id="65129-710">This event represents a file delete event.</span></span>

<span data-ttu-id="65129-711">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-711">**Information Fields**</span></span>

- <span data-ttu-id="65129-712">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-712">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-713">Informazioni sul campo 2: puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="65129-713">Info Field 2: Pointer to file name.</span></span>
- <span data-ttu-id="65129-714">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-714">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-715">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-715">Info Field 4: Not used.</span></span>

### <a name="file-open"></a><span data-ttu-id="65129-716">Apertura file</span><span class="sxs-lookup"><span data-stu-id="65129-716">File Open</span></span> 

#### <a name="fx_file_open"></a><span data-ttu-id="65129-717">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="65129-717">fx_file_open</span></span>

<span data-ttu-id="65129-718">**Icona** ![ di Icona Apri file](./media/user-guide/fx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="65129-718">**Icon** ![File open icon](./media/user-guide/fx-events/image42.png)</span></span>

<span data-ttu-id="65129-719">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-719">**Description**</span></span>

<span data-ttu-id="65129-720">Questo evento rappresenta un evento di apertura del file.</span><span class="sxs-lookup"><span data-stu-id="65129-720">This event represents a file open event.</span></span>

<span data-ttu-id="65129-721">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-721">**Information Fields**</span></span> 

- <span data-ttu-id="65129-722">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-722">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-723">Informazioni sul campo 2: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="65129-723">Info Field 2: Pointer to the file control block.</span></span>
- <span data-ttu-id="65129-724">Info Field 3: puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="65129-724">Info Field 3: Pointer to file name.</span></span>
- <span data-ttu-id="65129-725">Campo informazioni 4: tipo aperto:</span><span class="sxs-lookup"><span data-stu-id="65129-725">Info Field 4: Open type:</span></span>

  |  <span data-ttu-id="65129-726">Tipo aperto</span><span class="sxs-lookup"><span data-stu-id="65129-726">Open Type</span></span>                        | <span data-ttu-id="65129-727">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-727">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-728">Apri per la lettura</span><span class="sxs-lookup"><span data-stu-id="65129-728">Open for Read</span></span>                    | <span data-ttu-id="65129-729">0x00</span><span class="sxs-lookup"><span data-stu-id="65129-729">(0x00)</span></span>  |
  |  <span data-ttu-id="65129-730">Apri per scrittura</span><span class="sxs-lookup"><span data-stu-id="65129-730">Open for Write</span></span>                   | <span data-ttu-id="65129-731">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-731">(0x01)</span></span>  |
  |  <span data-ttu-id="65129-732">Apertura rapida per la lettura</span><span class="sxs-lookup"><span data-stu-id="65129-732">Fast Open for Read</span></span>               | <span data-ttu-id="65129-733">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-733">(0x02)</span></span>  |

### <a name="file-read"></a><span data-ttu-id="65129-734">Lettura file</span><span class="sxs-lookup"><span data-stu-id="65129-734">File Read</span></span> 

#### <a name="fx_file_read"></a><span data-ttu-id="65129-735">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="65129-735">fx_file_read</span></span>

<span data-ttu-id="65129-736">**Icona** ![ di Icona lettura file](./media/user-guide/fx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="65129-736">**Icon** ![File read icon](./media/user-guide/fx-events/image43.png)</span></span>

<span data-ttu-id="65129-737">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-737">**Description**</span></span>

<span data-ttu-id="65129-738">Questo evento rappresenta un evento di lettura del file.</span><span class="sxs-lookup"><span data-stu-id="65129-738">This event represents a file read event.</span></span>

<span data-ttu-id="65129-739">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-739">**Information Fields**</span></span>

- <span data-ttu-id="65129-740">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-740">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-741">Informazioni sul campo 2: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-741">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="65129-742">Informazioni sul campo 3: dimensioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="65129-742">Info Field 3: Request size.</span></span>
- <span data-ttu-id="65129-743">Campo dati 4: dimensioni effettive lette.</span><span class="sxs-lookup"><span data-stu-id="65129-743">Info Field 4: Actual size read.</span></span>

### <a name="file-relative-seek"></a><span data-ttu-id="65129-744">Ricerca relativa ai file</span><span class="sxs-lookup"><span data-stu-id="65129-744">File Relative Seek</span></span> 

#### <a name="fx_file_relative_seek"></a><span data-ttu-id="65129-745">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="65129-745">fx_file_relative_seek</span></span>

<span data-ttu-id="65129-746">**Icona** ![ di Icona di ricerca relativa ai file](./media/user-guide/fx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="65129-746">**Icon** ![File relative seek icon](./media/user-guide/fx-events/image44.png)</span></span>

<span data-ttu-id="65129-747">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-747">**Description**</span></span>

<span data-ttu-id="65129-748">Questo evento rappresenta un evento di ricerca relativo al file.</span><span class="sxs-lookup"><span data-stu-id="65129-748">This event represents a file relative seek event.</span></span>

<span data-ttu-id="65129-749">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-749">**Information Fields**</span></span>

- <span data-ttu-id="65129-750">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-750">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-751">Informazioni sul campo 2: offset di byte.</span><span class="sxs-lookup"><span data-stu-id="65129-751">Info Field 2: Byte offset.</span></span>
- <span data-ttu-id="65129-752">Campo informazioni 3: cerca da:</span><span class="sxs-lookup"><span data-stu-id="65129-752">Info Field 3: Seek from:</span></span>

  | <span data-ttu-id="65129-753">Evento</span><span class="sxs-lookup"><span data-stu-id="65129-753">Event</span></span>                             | <span data-ttu-id="65129-754">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-754">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-755">Dall'inizio</span><span class="sxs-lookup"><span data-stu-id="65129-755">From Beginning</span></span>                   | <span data-ttu-id="65129-756">0x00</span><span class="sxs-lookup"><span data-stu-id="65129-756">(0x00)</span></span>  |
  |  <span data-ttu-id="65129-757">Da fine</span><span class="sxs-lookup"><span data-stu-id="65129-757">From End</span></span>                         | <span data-ttu-id="65129-758">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-758">(0x01)</span></span>  | 
  |  <span data-ttu-id="65129-759">Inoltra</span><span class="sxs-lookup"><span data-stu-id="65129-759">Forward</span></span>                          | <span data-ttu-id="65129-760">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-760">(0x02)</span></span>  |
  |  <span data-ttu-id="65129-761">indietro</span><span class="sxs-lookup"><span data-stu-id="65129-761">Backward</span></span>                         | <span data-ttu-id="65129-762">0x03</span><span class="sxs-lookup"><span data-stu-id="65129-762">(0x03)</span></span>  |
- <span data-ttu-id="65129-763">Campo informazioni 4: offset precedente.</span><span class="sxs-lookup"><span data-stu-id="65129-763">Info Field 4: Previous offset.</span></span>

### <a name="file-rename"></a><span data-ttu-id="65129-764">Ridenominazione file</span><span class="sxs-lookup"><span data-stu-id="65129-764">File Rename</span></span> 

#### <a name="fx_file_rename"></a><span data-ttu-id="65129-765">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="65129-765">fx_file_rename</span></span>

<span data-ttu-id="65129-766">**Icona** ![ di Icona Rinomina file](./media/user-guide/fx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="65129-766">**Icon** ![File rename icon](./media/user-guide/fx-events/image45.png)</span></span>

<span data-ttu-id="65129-767">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-767">**Description**</span></span>

<span data-ttu-id="65129-768">Questo evento rappresenta un evento di ridenominazione del file.</span><span class="sxs-lookup"><span data-stu-id="65129-768">This event represents a file rename event.</span></span>

<span data-ttu-id="65129-769">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-769">**Information Fields**</span></span>

- <span data-ttu-id="65129-770">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-770">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-771">Informazioni sul campo 2: puntatore al nome del file precedente.</span><span class="sxs-lookup"><span data-stu-id="65129-771">Info Field 2: Pointer to old file name.</span></span>
- <span data-ttu-id="65129-772">Info Field 3: puntatore al nuovo nome file.</span><span class="sxs-lookup"><span data-stu-id="65129-772">Info Field 3: Pointer to new file name.</span></span>
- <span data-ttu-id="65129-773">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-773">Info Field 4: Not used.</span></span>

### <a name="file-seek"></a><span data-ttu-id="65129-774">Ricerca file</span><span class="sxs-lookup"><span data-stu-id="65129-774">File Seek</span></span> 

#### <a name="fx_file_seek"></a><span data-ttu-id="65129-775">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="65129-775">fx_file_seek</span></span>

<span data-ttu-id="65129-776">**Icona** ![ di Icona di ricerca file](./media/user-guide/fx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="65129-776">**Icon** ![File seek icon](./media/user-guide/fx-events/image46.png)</span></span>

<span data-ttu-id="65129-777">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-777">**Description**</span></span>

<span data-ttu-id="65129-778">Questo evento rappresenta un evento di ricerca di file.</span><span class="sxs-lookup"><span data-stu-id="65129-778">This event represents a file seek event.</span></span>

<span data-ttu-id="65129-779">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-779">**Information Fields**</span></span> 

- <span data-ttu-id="65129-780">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-780">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-781">Informazioni sul campo 2: offset di byte.</span><span class="sxs-lookup"><span data-stu-id="65129-781">Info Field 2: Byte offset.</span></span>
- <span data-ttu-id="65129-782">Informazioni sul campo 3: offset precedente.</span><span class="sxs-lookup"><span data-stu-id="65129-782">Info Field 3: Previous offset.</span></span>
- <span data-ttu-id="65129-783">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-783">Info Field 4: Not used.</span></span>

### <a name="file-truncate"></a><span data-ttu-id="65129-784">Troncamento file</span><span class="sxs-lookup"><span data-stu-id="65129-784">File Truncate</span></span> 

#### <a name="fx_file_truncate"></a><span data-ttu-id="65129-785">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="65129-785">fx_file_truncate</span></span>

<span data-ttu-id="65129-786">**Icona** ![ di Icona troncamento file](./media/user-guide/fx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="65129-786">**Icon** ![File truncate icon](./media/user-guide/fx-events/image47.png)</span></span>

<span data-ttu-id="65129-787">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-787">**Description**</span></span>

<span data-ttu-id="65129-788">Questo evento rappresenta un evento di troncamento del file.</span><span class="sxs-lookup"><span data-stu-id="65129-788">This event represents a file truncate event.</span></span>

<span data-ttu-id="65129-789">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-789">**Information Fields**</span></span>

- <span data-ttu-id="65129-790">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-790">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-791">Campo informazioni 2: dimensione richiesta.</span><span class="sxs-lookup"><span data-stu-id="65129-791">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="65129-792">Informazioni sul campo 3: dimensioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="65129-792">Info Field 3: Previous size.</span></span>
- <span data-ttu-id="65129-793">Campo informazioni 4: nuove dimensioni.</span><span class="sxs-lookup"><span data-stu-id="65129-793">Info Field 4: New size.</span></span>

### <a name="file-truncate-release"></a><span data-ttu-id="65129-794">Versione troncamento file</span><span class="sxs-lookup"><span data-stu-id="65129-794">File Truncate Release</span></span> 

#### <a name="fx_file_truncate_release"></a><span data-ttu-id="65129-795">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="65129-795">fx_file_truncate_release</span></span> 

<span data-ttu-id="65129-796">**Icona** ![ di Icona versione troncamento file](./media/user-guide/fx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="65129-796">**Icon** ![File truncate release icon](./media/user-guide/fx-events/image48.png)</span></span>

<span data-ttu-id="65129-797">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-797">**Description**</span></span>

<span data-ttu-id="65129-798">Questo evento rappresenta un evento di rilascio troncato del file.</span><span class="sxs-lookup"><span data-stu-id="65129-798">This event represents a file truncate release event.</span></span>

<span data-ttu-id="65129-799">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-799">**Information Fields**</span></span>

- <span data-ttu-id="65129-800">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-800">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-801">Campo informazioni 2: dimensione richiesta.</span><span class="sxs-lookup"><span data-stu-id="65129-801">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="65129-802">Informazioni sul campo 3: dimensioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="65129-802">Info Field 3: Previous size.</span></span>
- <span data-ttu-id="65129-803">Campo informazioni 4: nuove dimensioni.</span><span class="sxs-lookup"><span data-stu-id="65129-803">Info Field 4: New size.</span></span>

### <a name="file-write"></a><span data-ttu-id="65129-804">Scrittura file</span><span class="sxs-lookup"><span data-stu-id="65129-804">File Write</span></span> 

#### <a name="fx_file_write"></a><span data-ttu-id="65129-805">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="65129-805">fx_file_write</span></span> 

<span data-ttu-id="65129-806">**Icona** ![ di Icona scrittura file](./media/user-guide/fx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="65129-806">**Icon** ![File write icon](./media/user-guide/fx-events/image49.png)</span></span>

<span data-ttu-id="65129-807">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-807">**Description**</span></span>

<span data-ttu-id="65129-808">Questo evento rappresenta un evento di scrittura di file.</span><span class="sxs-lookup"><span data-stu-id="65129-808">This event represents a file write event.</span></span>

<span data-ttu-id="65129-809">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-809">**Information Fields**</span></span>

- <span data-ttu-id="65129-810">Info Field 1: puntatore al file.</span><span class="sxs-lookup"><span data-stu-id="65129-810">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="65129-811">Informazioni sul campo 2: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-811">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="65129-812">Informazioni sul campo 3: dimensioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="65129-812">Info Field 3: Request size.</span></span>
- <span data-ttu-id="65129-813">Informazioni campo 4: dimensioni effettive scritte.</span><span class="sxs-lookup"><span data-stu-id="65129-813">Info Field 4: Actual size written.</span></span>

### <a name="media-abort"></a><span data-ttu-id="65129-814">Interruzione supporto</span><span class="sxs-lookup"><span data-stu-id="65129-814">Media Abort</span></span> 

#### <a name="fx_media_abort"></a><span data-ttu-id="65129-815">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="65129-815">fx_media_abort</span></span> 

<span data-ttu-id="65129-816">**Icona** ![ di Icona Interrompi supporto](./media/user-guide/fx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="65129-816">**Icon** ![Media abort icon](./media/user-guide/fx-events/image50.png)</span></span>

<span data-ttu-id="65129-817">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-817">**Description**</span></span>

<span data-ttu-id="65129-818">Questo evento rappresenta un evento di interruzione del supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-818">This event represents a media abort event.</span></span>

<span data-ttu-id="65129-819">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-819">**Information Fields**</span></span>

- <span data-ttu-id="65129-820">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-820">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-821">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-821">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-822">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-822">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-823">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-823">Info Field 4: Not used.</span></span>

### <a name="media-cache-invalidate"></a><span data-ttu-id="65129-824">Media cache invalidata</span><span class="sxs-lookup"><span data-stu-id="65129-824">Media Cache Invalidate</span></span>

#### <a name="fx_media_cache_invalidate"></a><span data-ttu-id="65129-825">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="65129-825">fx_media_cache_invalidate</span></span>

<span data-ttu-id="65129-826">**Icona** ![ di Icona di invalidamento della cache multimediale](./media/user-guide/fx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="65129-826">**Icon** ![Media cache invalidate icon](./media/user-guide/fx-events/image51.png)</span></span>

<span data-ttu-id="65129-827">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-827">**Description**</span></span>

<span data-ttu-id="65129-828">Questo evento rappresenta un evento di invalidamento della cache multimediale.</span><span class="sxs-lookup"><span data-stu-id="65129-828">This event represents a media cache invalidate event.</span></span>

<span data-ttu-id="65129-829">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-829">**Information Fields**</span></span>

- <span data-ttu-id="65129-830">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-830">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-831">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-831">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-832">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-832">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-833">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-833">Info Field 4: Not used.</span></span>

### <a name="media-check"></a><span data-ttu-id="65129-834">Controllo dei supporti</span><span class="sxs-lookup"><span data-stu-id="65129-834">Media Check</span></span> 

#### <a name="fx_media_check"></a><span data-ttu-id="65129-835">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="65129-835">fx_media_check</span></span>

<span data-ttu-id="65129-836">**Icona** ![ di Icona del controllo del supporto](./media/user-guide/fx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="65129-836">**Icon** ![Media check icon](./media/user-guide/fx-events/image52.png)</span></span>

<span data-ttu-id="65129-837">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-837">**Description**</span></span>

<span data-ttu-id="65129-838">Questo evento rappresenta un evento di controllo del supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-838">This event represents a media check event.</span></span>

<span data-ttu-id="65129-839">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-839">**Information Fields**</span></span> 

- <span data-ttu-id="65129-840">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-840">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-841">Informazioni sul campo 2: puntatore di memoria Scratch.</span><span class="sxs-lookup"><span data-stu-id="65129-841">Info Field 2: Scratch memory pointer.</span></span>
- <span data-ttu-id="65129-842">Informazioni sul campo 3: dimensioni della memoria Scratch.</span><span class="sxs-lookup"><span data-stu-id="65129-842">Info Field 3: Scratch memory size.</span></span>
- <span data-ttu-id="65129-843">Informazioni sul campo 4: errori mappa di bit:</span><span class="sxs-lookup"><span data-stu-id="65129-843">Info Field 4: Errors bit map:</span></span>

  | <span data-ttu-id="65129-844">Tipo di errore</span><span class="sxs-lookup"><span data-stu-id="65129-844">Error type</span></span>                        | <span data-ttu-id="65129-845">Valore</span><span class="sxs-lookup"><span data-stu-id="65129-845">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="65129-846">Errore catena FAT</span><span class="sxs-lookup"><span data-stu-id="65129-846">FAT Chain Error</span></span>                  | <span data-ttu-id="65129-847">0x01</span><span class="sxs-lookup"><span data-stu-id="65129-847">(0x01)</span></span>  |
  |  <span data-ttu-id="65129-848">Errore directory</span><span class="sxs-lookup"><span data-stu-id="65129-848">Directory Error</span></span>                  | <span data-ttu-id="65129-849">0x02</span><span class="sxs-lookup"><span data-stu-id="65129-849">(0x02)</span></span>  |
  |  <span data-ttu-id="65129-850">Errore del cluster perso</span><span class="sxs-lookup"><span data-stu-id="65129-850">Lost Cluster Error</span></span>               | <span data-ttu-id="65129-851">0x04</span><span class="sxs-lookup"><span data-stu-id="65129-851">(0x04)</span></span>  |
  |  <span data-ttu-id="65129-852">Errore dimensioni file</span><span class="sxs-lookup"><span data-stu-id="65129-852">File Size Error</span></span>                  | <span data-ttu-id="65129-853">0x08</span><span class="sxs-lookup"><span data-stu-id="65129-853">(0x08)</span></span>  |

### <a name="media-close"></a><span data-ttu-id="65129-854">Chiusura supporti</span><span class="sxs-lookup"><span data-stu-id="65129-854">Media Close</span></span> 

#### <a name="fx_media_close"></a><span data-ttu-id="65129-855">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="65129-855">fx_media_close</span></span>

<span data-ttu-id="65129-856">**Icona** ![ di Icona di chiusura supporti](./media/user-guide/fx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="65129-856">**Icon** ![Media Close icon](./media/user-guide/fx-events/image53.png)</span></span>

<span data-ttu-id="65129-857">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-857">**Description**</span></span>

<span data-ttu-id="65129-858">Questo evento rappresenta un evento di chiusura dei supporti.</span><span class="sxs-lookup"><span data-stu-id="65129-858">This event represents a media close event.</span></span>

<span data-ttu-id="65129-859">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-859">**Information Fields**</span></span> 

- <span data-ttu-id="65129-860">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-860">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-861">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-861">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-862">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-862">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-863">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-863">Info Field 4: Not used.</span></span>

### <a name="media-flush"></a><span data-ttu-id="65129-864">Scaricamento supporti</span><span class="sxs-lookup"><span data-stu-id="65129-864">Media Flush</span></span> 

#### <a name="fx_media_flush"></a><span data-ttu-id="65129-865">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="65129-865">fx_media_flush</span></span>

<span data-ttu-id="65129-866">**Icona** ![ di Icona di scaricamento supporti](./media/user-guide/fx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="65129-866">**Icon** ![Media flush icon](./media/user-guide/fx-events/image54.png)</span></span>

<span data-ttu-id="65129-867">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-867">**Description**</span></span>

<span data-ttu-id="65129-868">Questo evento rappresenta un evento di scaricamento dei supporti.</span><span class="sxs-lookup"><span data-stu-id="65129-868">This event represents a media flush event.</span></span>

<span data-ttu-id="65129-869">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-869">**Information Fields**</span></span>

- <span data-ttu-id="65129-870">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-870">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-871">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-871">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-872">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-872">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-873">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-873">Info Field 4: Not used.</span></span>

### <a name="media-format"></a><span data-ttu-id="65129-874">Formato multimediale</span><span class="sxs-lookup"><span data-stu-id="65129-874">Media Format</span></span> 

#### <a name="fx_media_format"></a><span data-ttu-id="65129-875">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="65129-875">fx_media_format</span></span>

<span data-ttu-id="65129-876">**Icona** ![ di Icona formato supporto](./media/user-guide/fx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="65129-876">**Icon** ![Media format icon](./media/user-guide/fx-events/image55.png)</span></span>

<span data-ttu-id="65129-877">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-877">**Description**</span></span>

<span data-ttu-id="65129-878">Questo evento rappresenta un evento di formato multimediale.</span><span class="sxs-lookup"><span data-stu-id="65129-878">This event represents a media format event.</span></span>

<span data-ttu-id="65129-879">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-879">**Information Fields**</span></span>

- <span data-ttu-id="65129-880">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-880">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-881">Campo informazioni 2: numero di voci radice.</span><span class="sxs-lookup"><span data-stu-id="65129-881">Info Field 2: Number of root entries.</span></span>
- <span data-ttu-id="65129-882">Campo info 3: settori.</span><span class="sxs-lookup"><span data-stu-id="65129-882">Info Field 3: Sectors.</span></span>
- <span data-ttu-id="65129-883">Campo dati 4: settori per cluster.</span><span class="sxs-lookup"><span data-stu-id="65129-883">Info Field 4: Sectors per cluster.</span></span>

### <a name="media-open"></a><span data-ttu-id="65129-884">Supporto aperto</span><span class="sxs-lookup"><span data-stu-id="65129-884">Media Open</span></span> 

#### <a name="fx_media_open"></a><span data-ttu-id="65129-885">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="65129-885">fx_media_open</span></span>

<span data-ttu-id="65129-886">**Icona** ![ di Icona del supporto aperto](./media/user-guide/fx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="65129-886">**Icon** ![Media open icon](./media/user-guide/fx-events/image56.png)</span></span>

<span data-ttu-id="65129-887">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-887">**Description**</span></span>

<span data-ttu-id="65129-888">Questo evento rappresenta un evento di apertura del supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-888">This event represents a media open event.</span></span>

<span data-ttu-id="65129-889">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-889">**Information Fields**</span></span>

- <span data-ttu-id="65129-890">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-890">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-891">Informazioni sul campo 2: puntatore alla voce del driver multimediale.</span><span class="sxs-lookup"><span data-stu-id="65129-891">Info Field 2: Pointer to media driver entry.</span></span>
- <span data-ttu-id="65129-892">Campo info 3: puntatore di memoria.</span><span class="sxs-lookup"><span data-stu-id="65129-892">Info Field 3: Memory pointer.</span></span>
- <span data-ttu-id="65129-893">Informazioni sul campo 4: dimensioni della memoria.</span><span class="sxs-lookup"><span data-stu-id="65129-893">Info Field 4: Memory size.</span></span>

### <a name="media-read-media-read"></a><span data-ttu-id="65129-894">Media lettura media lettura</span><span class="sxs-lookup"><span data-stu-id="65129-894">Media Read Media Read</span></span> 

#### <a name="fx_media_read"></a><span data-ttu-id="65129-895">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="65129-895">fx_media_read</span></span>

<span data-ttu-id="65129-896">**Icona** ![ di Icona di lettura del supporto](./media/user-guide/fx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="65129-896">**Icon** ![Media read icon](./media/user-guide/fx-events/image57.png)</span></span>

<span data-ttu-id="65129-897">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-897">**Description**</span></span>

<span data-ttu-id="65129-898">Questo evento rappresenta un evento di lettura del supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-898">This event represents a media read event.</span></span>

<span data-ttu-id="65129-899">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-899">**Information Fields**</span></span>

- <span data-ttu-id="65129-900">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-900">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-901">Campo informazioni 2: settore logico.</span><span class="sxs-lookup"><span data-stu-id="65129-901">Info Field 2: Logical sector.</span></span>
- <span data-ttu-id="65129-902">Campo info 3: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-902">Info Field 3: Buffer pointer.</span></span>
- <span data-ttu-id="65129-903">Campo informazioni 4: byte letti.</span><span class="sxs-lookup"><span data-stu-id="65129-903">Info Field 4: Bytes read.</span></span>

### <a name="media-space-available"></a><span data-ttu-id="65129-904">Spazio multimediale disponibile</span><span class="sxs-lookup"><span data-stu-id="65129-904">Media Space Available</span></span> 

#### <a name="fx_media_space_available"></a><span data-ttu-id="65129-905">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="65129-905">fx_media_space_available</span></span>

<span data-ttu-id="65129-906">**Icona** ![ di Icona spazio multimediale disponibile](./media/user-guide/fx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="65129-906">**Icon** ![Media space available icon](./media/user-guide/fx-events/image58.png)</span></span>

<span data-ttu-id="65129-907">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-907">**Description**</span></span>

<span data-ttu-id="65129-908">Questo evento rappresenta un evento di spazio multimediale disponibile.</span><span class="sxs-lookup"><span data-stu-id="65129-908">This event represents a media space available event.</span></span>

<span data-ttu-id="65129-909">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-909">**Information Fields**</span></span> 

- <span data-ttu-id="65129-910">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-910">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-911">Informazioni sul campo 2: puntatore byte disponibili.</span><span class="sxs-lookup"><span data-stu-id="65129-911">Info Field 2: Available bytes pointer.</span></span>
- <span data-ttu-id="65129-912">Campo info 3: numero di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="65129-912">Info Field 3: Number of free clusters.</span></span>
- <span data-ttu-id="65129-913">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-913">Info Field 4: Not used.</span></span>

### <a name="media-volume-get"></a><span data-ttu-id="65129-914">Volume multimediale Get</span><span class="sxs-lookup"><span data-stu-id="65129-914">Media Volume Get</span></span> 

#### <a name="fx_media_volume_get"></a><span data-ttu-id="65129-915">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="65129-915">fx_media_volume_get</span></span>

<span data-ttu-id="65129-916">**Icona** ![ di Icona Ottieni volume multimediale](./media/user-guide/fx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="65129-916">**Icon** ![Media volume get icon](./media/user-guide/fx-events/image59.png)</span></span>

<span data-ttu-id="65129-917">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-917">**Description**</span></span>

<span data-ttu-id="65129-918">Questo evento rappresenta un evento media volume Get.</span><span class="sxs-lookup"><span data-stu-id="65129-918">This event represents a media volume get event.</span></span>

<span data-ttu-id="65129-919">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-919">**Information Fields**</span></span>

- <span data-ttu-id="65129-920">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-920">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-921">Informazioni sul campo 2: puntatore al nome del volume.</span><span class="sxs-lookup"><span data-stu-id="65129-921">Info Field 2: Pointer to volume name.</span></span>
- <span data-ttu-id="65129-922">Informazioni sul campo 3: origine del volume.</span><span class="sxs-lookup"><span data-stu-id="65129-922">Info Field 3: Volume source.</span></span>
- <span data-ttu-id="65129-923">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-923">Info Field 4: Not used.</span></span>

### <a name="media-volume-set"></a><span data-ttu-id="65129-924">Set di volumi multimediali</span><span class="sxs-lookup"><span data-stu-id="65129-924">Media Volume Set</span></span> 

#### <a name="fx_media_volume_set"></a><span data-ttu-id="65129-925">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="65129-925">fx_media_volume_set</span></span>

<span data-ttu-id="65129-926">**Icona** ![ di Icona del set di volumi multimediali](./media/user-guide/fx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="65129-926">**Icon** ![Media volume set icon](./media/user-guide/fx-events/image60.png)</span></span>

<span data-ttu-id="65129-927">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-927">**Description**</span></span>

<span data-ttu-id="65129-928">Questo evento rappresenta un evento del set di volumi multimediali.</span><span class="sxs-lookup"><span data-stu-id="65129-928">This event represents a media volume set event.</span></span>

<span data-ttu-id="65129-929">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-929">**Information Fields**</span></span> 
- <span data-ttu-id="65129-930">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-930">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-931">Informazioni sul campo 2: puntatore al nome del volume.</span><span class="sxs-lookup"><span data-stu-id="65129-931">Info Field 2: Pointer to volume name.</span></span>
- <span data-ttu-id="65129-932">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-932">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-933">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-933">Info Field 4: Not used.</span></span>

### <a name="media-write"></a><span data-ttu-id="65129-934">Scrittura supporti</span><span class="sxs-lookup"><span data-stu-id="65129-934">Media Write</span></span> 

#### <a name="fx_media_write"></a><span data-ttu-id="65129-935">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="65129-935">fx_media_write</span></span>

<span data-ttu-id="65129-936">**Icona** ![ di Icona scrittura supporti](./media/user-guide/fx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="65129-936">**Icon** ![Media write icon](./media/user-guide/fx-events/image61.png)</span></span>

<span data-ttu-id="65129-937">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-937">**Description**</span></span>

<span data-ttu-id="65129-938">Questo evento rappresenta un evento di scrittura del supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-938">This event represents a media write event.</span></span>

<span data-ttu-id="65129-939">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-939">**Information Fields**</span></span>

- <span data-ttu-id="65129-940">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-940">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-941">Campo informazioni 2: settore logico.</span><span class="sxs-lookup"><span data-stu-id="65129-941">Info Field 2: Logical sector.</span></span>
- <span data-ttu-id="65129-942">Campo info 3: puntatore del buffer.</span><span class="sxs-lookup"><span data-stu-id="65129-942">Info Field 3: Buffer pointer.</span></span>
- <span data-ttu-id="65129-943">Campo informazioni 4: byte scritti.</span><span class="sxs-lookup"><span data-stu-id="65129-943">Info Field 4: Bytes written.</span></span>

### <a name="system-date-get"></a><span data-ttu-id="65129-944">Data di sistema Get</span><span class="sxs-lookup"><span data-stu-id="65129-944">System Date Get</span></span> 

#### <a name="fx_system_date_get"></a><span data-ttu-id="65129-945">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="65129-945">fx_system_date_get</span></span> 

<span data-ttu-id="65129-946">**Icona** ![ di Icona Data di sistema Get](./media/user-guide/fx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="65129-946">**Icon** ![System date get icon](./media/user-guide/fx-events/image62.png)</span></span>

<span data-ttu-id="65129-947">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-947">**Description**</span></span>

<span data-ttu-id="65129-948">Questo evento rappresenta un evento System Date Get.</span><span class="sxs-lookup"><span data-stu-id="65129-948">This event represents a system date get event.</span></span>

<span data-ttu-id="65129-949">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-949">**Information Fields**</span></span>

- <span data-ttu-id="65129-950">Campo informazioni 1: anno.</span><span class="sxs-lookup"><span data-stu-id="65129-950">Info Field 1: Year.</span></span>
- <span data-ttu-id="65129-951">Campo informazioni 2: mese.</span><span class="sxs-lookup"><span data-stu-id="65129-951">Info Field 2: Month.</span></span>
- <span data-ttu-id="65129-952">Campo informazioni 3: giorno.</span><span class="sxs-lookup"><span data-stu-id="65129-952">Info Field 3: Day.</span></span>
- <span data-ttu-id="65129-953">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-953">Info Field 4: Not used.</span></span>

### <a name="system-date-set"></a><span data-ttu-id="65129-954">Set di date di sistema</span><span class="sxs-lookup"><span data-stu-id="65129-954">System Date Set</span></span> 

#### <a name="fx_system_date_set"></a><span data-ttu-id="65129-955">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="65129-955">fx_system_date_set</span></span> 

<span data-ttu-id="65129-956">**Icona** ![ di Icona del set di dati di sistema](./media/user-guide/fx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="65129-956">**Icon** ![System date set icon](./media/user-guide/fx-events/image63.png)</span></span>

<span data-ttu-id="65129-957">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-957">**Description**</span></span>

<span data-ttu-id="65129-958">Questo evento rappresenta un evento di data set di sistema.</span><span class="sxs-lookup"><span data-stu-id="65129-958">This event represents a system date set event.</span></span>

<span data-ttu-id="65129-959">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-959">**Information Fields**</span></span>

- <span data-ttu-id="65129-960">Campo informazioni 1: anno.</span><span class="sxs-lookup"><span data-stu-id="65129-960">Info Field 1: Year.</span></span>
- <span data-ttu-id="65129-961">Campo informazioni 2: mese.</span><span class="sxs-lookup"><span data-stu-id="65129-961">Info Field 2: Month.</span></span>
- <span data-ttu-id="65129-962">Campo informazioni 3: giorno.</span><span class="sxs-lookup"><span data-stu-id="65129-962">Info Field 3: Day.</span></span>
- <span data-ttu-id="65129-963">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-963">Info Field 4: Not used.</span></span>

### <a name="system-initialize"></a><span data-ttu-id="65129-964">Inizializzazione sistema</span><span class="sxs-lookup"><span data-stu-id="65129-964">System Initialize</span></span> 

#### <a name="fx_system_initialize"></a><span data-ttu-id="65129-965">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="65129-965">fx_system_initialize</span></span> 

<span data-ttu-id="65129-966">**Icona** ![ di Icona Inizializzazione sistema](./media/user-guide/fx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="65129-966">**Icon** ![System initialize icon](./media/user-guide/fx-events/image64.png)</span></span>

<span data-ttu-id="65129-967">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-967">**Description**</span></span>

<span data-ttu-id="65129-968">Questo evento rappresenta un evento di inizializzazione del sistema.</span><span class="sxs-lookup"><span data-stu-id="65129-968">This event represents a system initialize event.</span></span>

<span data-ttu-id="65129-969">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-969">**Information Fields**</span></span>

- <span data-ttu-id="65129-970">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-970">Info Field 1: Not used.</span></span>
- <span data-ttu-id="65129-971">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-971">Info Field 2: Not used.</span></span>
- <span data-ttu-id="65129-972">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-972">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-973">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-973">Info Field 4: Not used.</span></span>

### <a name="system-time-get"></a><span data-ttu-id="65129-974">Ora di sistema Get</span><span class="sxs-lookup"><span data-stu-id="65129-974">System Time Get</span></span> 

#### <a name="fx_system_time_get"></a><span data-ttu-id="65129-975">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="65129-975">fx_system_time_get</span></span> 

<span data-ttu-id="65129-976">**Icona** ![ di Icona dell'ora di sistema Get](./media/user-guide/fx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="65129-976">**Icon** ![System time get icon](./media/user-guide/fx-events/image65.png)</span></span>

<span data-ttu-id="65129-977">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-977">**Description**</span></span>

<span data-ttu-id="65129-978">Questo evento rappresenta un evento di ottenimento dell'ora di sistema.</span><span class="sxs-lookup"><span data-stu-id="65129-978">This event represents a system time get event.</span></span>

<span data-ttu-id="65129-979">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-979">**Information Fields**</span></span> 

- <span data-ttu-id="65129-980">Campo informazioni 1: ora.</span><span class="sxs-lookup"><span data-stu-id="65129-980">Info Field 1: Hour.</span></span>
- <span data-ttu-id="65129-981">Campo informazioni 2: minuti.</span><span class="sxs-lookup"><span data-stu-id="65129-981">Info Field 2: Minute.</span></span>
- <span data-ttu-id="65129-982">Campo informazioni 3: secondo.</span><span class="sxs-lookup"><span data-stu-id="65129-982">Info Field 3: Second.</span></span>
- <span data-ttu-id="65129-983">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-983">Info Field 4: Not used.</span></span>

### <a name="system-time-set"></a><span data-ttu-id="65129-984">Impostazione dell'ora di sistema</span><span class="sxs-lookup"><span data-stu-id="65129-984">System Time Set</span></span> 

#### <a name="fx_system_time_set"></a><span data-ttu-id="65129-985">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="65129-985">fx_system_time_set</span></span> 

<span data-ttu-id="65129-986">**Icona** ![ di Icona del set di impostazioni dell'ora di sistema](./media/user-guide/fx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="65129-986">**Icon** ![System time set icon](./media/user-guide/fx-events/image66.png)</span></span>

<span data-ttu-id="65129-987">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-987">**Description**</span></span>

<span data-ttu-id="65129-988">Questo evento rappresenta un evento di impostazione dell'ora di sistema.</span><span class="sxs-lookup"><span data-stu-id="65129-988">This event represents a system time set event.</span></span>

<span data-ttu-id="65129-989">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-989">**Information Fields**</span></span>

- <span data-ttu-id="65129-990">Campo informazioni 1: ora.</span><span class="sxs-lookup"><span data-stu-id="65129-990">Info Field 1: Hour.</span></span>
- <span data-ttu-id="65129-991">Campo informazioni 2: minuti.</span><span class="sxs-lookup"><span data-stu-id="65129-991">Info Field 2: Minute.</span></span>
- <span data-ttu-id="65129-992">Campo informazioni 3: secondo.</span><span class="sxs-lookup"><span data-stu-id="65129-992">Info Field 3: Second.</span></span>
- <span data-ttu-id="65129-993">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-993">Info Field 4: Not used.</span></span>

### <a name="unicode-directory-create"></a><span data-ttu-id="65129-994">Creazione directory Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-994">Unicode Directory Create</span></span> 

#### <a name="fx_unicode_directory_create"></a><span data-ttu-id="65129-995">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="65129-995">fx_unicode_directory_create</span></span> 

<span data-ttu-id="65129-996">**Icona** ![ di Icona di creazione directory Unicode](./media/user-guide/fx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="65129-996">**Icon** ![Unicode directory create icon](./media/user-guide/fx-events/image67.png)</span></span>

<span data-ttu-id="65129-997">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-997">**Description**</span></span>

<span data-ttu-id="65129-998">Questo evento rappresenta un evento di creazione della directory Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-998">This event represents a Unicode directory create event.</span></span>

<span data-ttu-id="65129-999">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-999">**Information Fields**</span></span> 

- <span data-ttu-id="65129-1000">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-1000">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-1001">Informazioni sul campo 2: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1001">Info Field 2: Pointer to Unicode name.</span></span>
- <span data-ttu-id="65129-1002">Info Field 3: dimensioni del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1002">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="65129-1003">Informazioni sul campo 4: puntatore al nome breve.</span><span class="sxs-lookup"><span data-stu-id="65129-1003">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-directory-rename"></a><span data-ttu-id="65129-1004">Ridenominazione della directory Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-1004">Unicode Directory Rename</span></span> 

#### <a name="fx_unicode_directory_rename"></a><span data-ttu-id="65129-1005">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="65129-1005">fx_unicode_directory_rename</span></span>

<span data-ttu-id="65129-1006">**Icona** ![ di Icona Rinomina Directory Unicode](./media/user-guide/fx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="65129-1006">**Icon** ![Unicode directory rename icon](./media/user-guide/fx-events/image68.png)</span></span>

<span data-ttu-id="65129-1007">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-1007">**Description**</span></span>

<span data-ttu-id="65129-1008">Questo evento rappresenta un evento di ridenominazione della directory Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1008">This event represents a Unicode directory rename event.</span></span>

<span data-ttu-id="65129-1009">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-1009">**Information Fields**</span></span> 

- <span data-ttu-id="65129-1010">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-1010">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-1011">Informazioni sul campo 2: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1011">Info Field 2: Pointer to Unicode name.</span></span>
- <span data-ttu-id="65129-1012">Info Field 3: dimensioni del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1012">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="65129-1013">Informazioni sul campo 4: puntatore al nome breve.</span><span class="sxs-lookup"><span data-stu-id="65129-1013">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-file-create"></a><span data-ttu-id="65129-1014">Creazione file Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-1014">Unicode File Create</span></span> 

#### <a name="fx_unicode_file_create"></a><span data-ttu-id="65129-1015">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="65129-1015">fx_unicode_file_create</span></span>

<span data-ttu-id="65129-1016">**Icona** ![ di Icona di creazione file Unicode](./media/user-guide/fx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="65129-1016">**Icon** ![Unicode file create icon](./media/user-guide/fx-events/image69.png)</span></span>

<span data-ttu-id="65129-1017">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-1017">**Description**</span></span>

<span data-ttu-id="65129-1018">Questo evento rappresenta un evento di creazione di file Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1018">This event represents a Unicode file create event.</span></span>

<span data-ttu-id="65129-1019">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-1019">**Information Fields**</span></span>

- <span data-ttu-id="65129-1020">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-1020">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-1021">Info Field 2: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1021">Info Field 2: Pointer to the Unicode name.</span></span>
- <span data-ttu-id="65129-1022">Info Field 3: dimensioni del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1022">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="65129-1023">Informazioni sul campo 4: puntatore al nome breve.</span><span class="sxs-lookup"><span data-stu-id="65129-1023">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-file-rename"></a><span data-ttu-id="65129-1024">Ridenominazione file Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-1024">Unicode File Rename</span></span> 

#### <a name="fx_unicode_file_rename"></a><span data-ttu-id="65129-1025">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="65129-1025">fx_unicode_file_rename</span></span>

<span data-ttu-id="65129-1026">**Icona** ![ di Icona Rinomina file Unicode](./media/user-guide/fx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="65129-1026">**Icon** ![Unicode file rename icon](./media/user-guide/fx-events/image70.png)</span></span>

<span data-ttu-id="65129-1027">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-1027">**Description**</span></span>

<span data-ttu-id="65129-1028">Questo evento rappresenta un evento di ridenominazione di file Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1028">This event represents a Unicode file rename event.</span></span>

<span data-ttu-id="65129-1029">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-1029">**Information Fields**</span></span>

- <span data-ttu-id="65129-1030">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-1030">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-1031">Informazioni sul campo 2: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1031">Info Field 2: Pointer to Unicode name.</span></span>
- <span data-ttu-id="65129-1032">Info Field 3: dimensioni del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1032">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="65129-1033">Informazioni sul campo 4: puntatore al nome breve.</span><span class="sxs-lookup"><span data-stu-id="65129-1033">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-length-get"></a><span data-ttu-id="65129-1034">Get lunghezza Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-1034">Unicode Length Get</span></span> 

#### <a name="fx_unicode_length_get"></a><span data-ttu-id="65129-1035">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="65129-1035">fx_unicode_length_get</span></span>

<span data-ttu-id="65129-1036">**Icona** ![ di Icona Ottieni lunghezza Unicode](./media/user-guide/fx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="65129-1036">**Icon** ![Unicode length get icon](./media/user-guide/fx-events/image71.png)</span></span>

<span data-ttu-id="65129-1037">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-1037">**Description**</span></span>

<span data-ttu-id="65129-1038">Questo evento rappresenta un evento Get di lunghezza Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1038">This event represents a Unicode length get event.</span></span>

<span data-ttu-id="65129-1039">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-1039">**Information Fields**</span></span>

- <span data-ttu-id="65129-1040">Info Field 1: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1040">Info Field 1: Pointer to the Unicode name.</span></span>
- <span data-ttu-id="65129-1041">Campo informazioni 2: lunghezza.</span><span class="sxs-lookup"><span data-stu-id="65129-1041">Info Field 2: Length.</span></span>
- <span data-ttu-id="65129-1042">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-1042">Info Field 3: Not used.</span></span>
- <span data-ttu-id="65129-1043">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="65129-1043">Info Field 4: Not used.</span></span>

### <a name="unicode-name-get"></a><span data-ttu-id="65129-1044">Get nome Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-1044">Unicode Name Get</span></span> 

#### <a name="fx_unicode_name_get"></a><span data-ttu-id="65129-1045">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="65129-1045">fx_unicode_name_get</span></span>

<span data-ttu-id="65129-1046">**Icona** ![ di Icona Ottieni nome Unicode](./media/user-guide/fx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="65129-1046">**Icon** ![Unicode name get icon](./media/user-guide/fx-events/image72.png)</span></span>

<span data-ttu-id="65129-1047">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-1047">**Description**</span></span>

<span data-ttu-id="65129-1048">Questo evento rappresenta un evento Get del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1048">This event represents a Unicode name get event.</span></span>

<span data-ttu-id="65129-1049">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-1049">**Information Fields**</span></span>

- <span data-ttu-id="65129-1050">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-1050">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-1051">Informazioni sul campo 2: nome breve di origine.</span><span class="sxs-lookup"><span data-stu-id="65129-1051">Info Field 2: Source short name.</span></span>
- <span data-ttu-id="65129-1052">Informazioni sul campo 3: puntatore al nome Unicode di destinazione.</span><span class="sxs-lookup"><span data-stu-id="65129-1052">Info Field 3: Destination Unicode name pointer.</span></span>
- <span data-ttu-id="65129-1053">Informazioni campo 4: lunghezza del nome Unicode di destinazione.</span><span class="sxs-lookup"><span data-stu-id="65129-1053">Info Field 4: Destination Unicode name length.</span></span>

### <a name="unicode-short-name-get"></a><span data-ttu-id="65129-1054">Get nome breve Unicode</span><span class="sxs-lookup"><span data-stu-id="65129-1054">Unicode Short Name Get</span></span> 

#### <a name="fx_unicode_short_name_get"></a><span data-ttu-id="65129-1055">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="65129-1055">fx_unicode_short_name_get</span></span>

<span data-ttu-id="65129-1056">**Icona** ![ di Icona di Get con nome breve Unicode](./media/user-guide/fx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="65129-1056">**Icon** ![Unicode short name get icon](./media/user-guide/fx-events/image73.png)</span></span>

<span data-ttu-id="65129-1057">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="65129-1057">**Description**</span></span>

<span data-ttu-id="65129-1058">Questo evento rappresenta un evento di ottenimento nome breve Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1058">This event represents a Unicode short name get event.</span></span>

<span data-ttu-id="65129-1059">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="65129-1059">**Information Fields**</span></span>

- <span data-ttu-id="65129-1060">Info Field 1: puntatore al supporto.</span><span class="sxs-lookup"><span data-stu-id="65129-1060">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="65129-1061">Informazioni sul campo 2: puntatore al nome Unicode di origine.</span><span class="sxs-lookup"><span data-stu-id="65129-1061">Info Field 2: Pointer to source Unicode name.</span></span>
- <span data-ttu-id="65129-1062">Info Field 3: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="65129-1062">Info Field 3: Length of Unicode name.</span></span>
- <span data-ttu-id="65129-1063">Informazioni sul campo 4: puntatore al nome breve.</span><span class="sxs-lookup"><span data-stu-id="65129-1063">Info Field 4: Pointer to short name.</span></span>