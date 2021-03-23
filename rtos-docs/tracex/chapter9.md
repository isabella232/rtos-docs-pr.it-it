---
title: 'Capitolo 9: eventi di traccia di Azure RTO USBX'
description: Questo capitolo contiene una descrizione degli eventi USBX di Azure RTO visualizzati da TraceX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 98561fe1d131e1d1b0893b7d89eb720881a82ac8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824254"
---
# <a name="chapter-9---azure-rtos-usbx-trace-events"></a><span data-ttu-id="5cc78-103">Capitolo 9: eventi di traccia di Azure RTO USBX</span><span class="sxs-lookup"><span data-stu-id="5cc78-103">Chapter 9 - Azure RTOS USBX trace events</span></span>

<span data-ttu-id="5cc78-104">Questo capitolo contiene una descrizione degli eventi USBX di Azure RTO visualizzati da TraceX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-104">This chapter contains a description of the Azure RTOS USBX events displayed by TraceX.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="5cc78-105">Elenco di eventi e icone</span><span class="sxs-lookup"><span data-stu-id="5cc78-105">List of Events and Icons</span></span>

<span data-ttu-id="5cc78-106">Di seguito è riportato un elenco di eventi USBX visualizzati da TraceX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-106">The following is a list of USBX events displayed by TraceX.</span></span>

| <span data-ttu-id="5cc78-107">Icona</span><span class="sxs-lookup"><span data-stu-id="5cc78-107">Icon</span></span>                             | <span data-ttu-id="5cc78-108">Significato</span><span class="sxs-lookup"><span data-stu-id="5cc78-108">Meaning</span></span>                               |
| -------------------------------- | ------------------------------------- |
| ![Icona di attivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image1.png)    | <span data-ttu-id="5cc78-110">**Classe dispositivo CDC Activate** *(ux_device_class_cdc_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-110">**Device Class Cdc Activate** *(ux_device_class_cdc_activate)*</span></span> |
| ![Icona di disattivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image2.png)    | <span data-ttu-id="5cc78-112">**Classe dispositivo CDC Deactivate** *(ux_device_class_cdc_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-112">**Device Class Cdc Deactivate** *(ux_device_class_cdc_deactivate)*</span></span> |
| ![Icona di lettura della classe del dispositivo c D](./media/user-guide/usbx-events/image3.png)    | <span data-ttu-id="5cc78-114">**Classe dispositivo CDC Read** *(ux_device_class_cdc_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-114">**Device Class Cdc Read** *(ux_device_class_cdc_read)*</span></span> |
| ![Icona di scrittura della classe del dispositivo c D C](./media/user-guide/usbx-events/image4.png)    | <span data-ttu-id="5cc78-116">**Classe dispositivo-scrittura CDC** *(ux_device_class_cdc_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-116">**Device Class Cdc Write** *(ux_device_class_cdc_write)*</span></span> |
| ![Icona di attivazione della classe Device DPUMP](./media/user-guide/usbx-events/image5.png)    | <span data-ttu-id="5cc78-118">**Classe dispositivo DPUMP Activate** *(ux_device_class_dpump_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-118">**Device Class Dpump Activate** *(ux_device_class_dpump_activate)*</span></span> |
| ![Icona di disattivazione della classe Device DPUMP](./media/user-guide/usbx-events/image6.png)    | <span data-ttu-id="5cc78-120">**Classe dispositivo DPUMP disattivare** *(ux_device_class_dpump_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-120">**Device Class Dpump Deactivate** *(ux_device_class_dpump_deactivate)*</span></span> |
| ![Icona di lettura della classe del dispositivo DPUMP](./media/user-guide/usbx-events/image7.png)    | <span data-ttu-id="5cc78-122">**Classe dispositivo DPUMP Read** *(ux_device_class_dpump_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-122">**Device Class Dpump Read** *(ux_device_class_dpump_read)*</span></span> |
| ![Icona di scrittura della classe Device DPUMP](./media/user-guide/usbx-events/image8.png)    | <span data-ttu-id="5cc78-124">**Classe dispositivo DPUMP Write** *(ux_device_class_dpump_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-124">**Device Class Dpump Write** *(ux_device_class_dpump_write)*</span></span> |
| ![Icona di attivazione HID della classe dispositivo](./media/user-guide/usbx-events/image9.png)    | <span data-ttu-id="5cc78-126">**Attivazione HID della classe dispositivo** *(ux_device_class_hid_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-126">**Device Class Hid Activate** *(ux_device_class_hid_activate)*</span></span> |
| ![Icona di disattivazione HID della classe dispositivo](./media/user-guide/usbx-events/image10.png)    | <span data-ttu-id="5cc78-128">**Disattivazione HID della classe dispositivo** *(ux_device_class_hid_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-128">**Device Class Hid Deactivate** *(ux_device_class_hid_deactivate)*</span></span> |
| ![Icona di invio del descrittore HID della classe dispositivo](./media/user-guide/usbx-events/image11.png)    | <span data-ttu-id="5cc78-130">**Classe dispositivo-invia descrittore HID** *(ux_device_class_hid_descriptor_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-130">**Device Class Hid Descriptor Send** *(ux_device_class_hid_descriptor_send)*</span></span> |
| ![Icona di Get dell'evento HID della classe dispositivo](./media/user-guide/usbx-events/image12.png)    | <span data-ttu-id="5cc78-132">**Classe dispositivo HID Event Get** *(ux_device_class_hid_event_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-132">**Device Class Hid Event Get** *(ux_device_class_hid_event_get)*</span></span> |
| ![Icona del set di eventi HID della classe dispositivo](./media/user-guide/usbx-events/image13.png)    | <span data-ttu-id="5cc78-134">**Set di eventi HID della classe Device** *(ux_device_class_hid_event_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-134">**Device Class Hid Event Set** *(ux_device_class_hid_event_set)*</span></span> |
| ![Icona di Get del report HID della classe dispositivo](./media/user-guide/usbx-events/image14.png)    | <span data-ttu-id="5cc78-136">**Classe dispositivo HID report Get** *(ux_device_class_hid_report_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-136">**Device Class Hid Report Get** *(ux_device_class_hid_report_get)*</span></span> |
| ![Icona del set di report HID della classe dispositivo](./media/user-guide/usbx-events/image15.png)    | <span data-ttu-id="5cc78-138">**Set di report HID della classe dispositivo** *(ux_device_class_hid_report_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-138">**Device Class Hid Report Set** *(ux_device_class_hid_report_set)*</span></span> |
| ![Icona di attivazione Pima della classe dispositivo](./media/user-guide/usbx-events/image16.png)    | <span data-ttu-id="5cc78-140">**Classe dispositivo di attivazione Pima** *(ux_device_class_pima_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-140">**Device Class Pima Activate** *(ux_device_class_pima_activate)*</span></span> |
| ![Icona di disattivazione della classe di dispositivo Pima](./media/user-guide/usbx-events/image17.png)    | <span data-ttu-id="5cc78-142">**Classe dispositivo Pima Deactivate** *(ux_device_class_pima_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-142">**Device Class Pima Deactivate** *(ux_device_class_pima_deactivate)*</span></span> |
| ![Icona di invio informazioni sul dispositivo Pima della classe dispositivo](./media/user-guide/usbx-events/image18.png)    | <span data-ttu-id="5cc78-144">**Classe dispositivo Pima invio informazioni sul dispositivo** *(ux_device_class_pima_device_info_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-144">**Device Class Pima Device Info Send** *(ux_device_class_pima_device_info_send)*</span></span> |
| ![Icona di Get evento di classe dispositivo Pima](./media/user-guide/usbx-events/image19.png)    | <span data-ttu-id="5cc78-146">**Classe dispositivo Pima evento Get** *(ux_device_class_pima_event_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-146">**Device Class Pima Event Get** *(ux_device_class_pima_event_get)*</span></span> |
| ![Icona del set di eventi Pima della classe Device](./media/user-guide/usbx-events/image20.png)    | <span data-ttu-id="5cc78-148">**Set di eventi Pima della classe Device** *(ux_device_class_pima_event_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-148">**Device Class Pima Event Set** *(ux_device_class_pima_event_set)*</span></span> |
| ![Icona di aggiunta oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image21.png)    | <span data-ttu-id="5cc78-150">**Classe dispositivo-Aggiunta oggetto Pima** *(ux_device_class_pima_object_add)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-150">**Device Class Pima Object Add** *(ux_device_class_pima_object_add)*</span></span> |
| ![Icona di visualizzazione dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image22.png)    | <span data-ttu-id="5cc78-152">**Classe dispositivo dati oggetto Pima Get** *(ux_device_class_pima_object_data_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-152">**Device Class Pima Object Data Get** *(ux_device_class_pima_object_data_get)*</span></span> |
| ![Icona di invio dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image23.png)    | <span data-ttu-id="5cc78-154">**Classe dispositivo-invio dati oggetti Pima** *(ux_device_class_pima_object_data_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-154">**Device Class Pima Object Data Send** *(ux_device_class_pima_object_data_send)*</span></span> |
| ![Icona di eliminazione oggetti Pima classe dispositivo](./media/user-guide/usbx-events/image24.png)    | <span data-ttu-id="5cc78-156">**Classe dispositivo eliminazione oggetti Pima** *(ux_device_class_pima_object_delete)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-156">**Device Class Pima Object Delete** *(ux_device_class_pima_object_delete)*</span></span> |
| ![Icona di invio handle oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image25.png)    | <span data-ttu-id="5cc78-158">**Classe dispositivo gestisce l'invio** *(ux_device_class_pima_object_handles_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-158">**Device Class Pima Object Handles Send** *(ux_device_class_pima_object_handles_send)*</span></span> |
| ![Icona di visualizzazione informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image26.png)    | <span data-ttu-id="5cc78-160">**Classe dispositivo informazioni su oggetti Pima Get** *(ux_device_class_pima_object_info_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-160">**Device Class Pima Object Info Get** *(ux_device_class_pima_object_info_get)*</span></span> |
| ![Icona di invio informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image27.png)    | <span data-ttu-id="5cc78-162">**Classe dispositivo-invio informazioni oggetto Pima** *(ux_device_class_pima_object_info_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-162">**Device Class Pima Object Info Send** *(ux_device_class_pima_object_info_send)*</span></span> |
| ![Icona di invio numero di oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image28.png)    | <span data-ttu-id="5cc78-164">**Classe dispositivo numero oggetti Pima invio** *(ux_device_class_pima_objects_number_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-164">**Device Class Pima Objects Number Send** *(ux_device_class_pima_objects_number_send)*</span></span> |
| ![Icona di visualizzazione dati oggetto parziale classe dispositivo Pima](./media/user-guide/usbx-events/image29.png)    | <span data-ttu-id="5cc78-166">**Classe dispositivo i dati dell'oggetto parziale Pima Get** *(ux_device_class_pima_partial_object_data_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-166">**Device Class Pima Partial Object Data Get** *(ux_device_class_pima_partial_object_data_get)*</span></span> |
| ![Icona di invio risposta Pima della classe dispositivo](./media/user-guide/usbx-events/image30.png)    | <span data-ttu-id="5cc78-168">**Classe dispositivo-invio risposta Pima** *(ux_device_class_pima_response_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-168">**Device Class Pima Response Send** *(ux_device_class_pima_response_send)*</span></span>|
| ![Icona di archiviazione della classe dispositivo Pima archiviazione I D](./media/user-guide/usbx-events/image31.png)    | <span data-ttu-id="5cc78-170">**Classe dispositivo ID archiviazione Pima** *(ux_device_class_pima_storage_id_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-170">**Device Class Pima Storage Id Send** *(ux_device_class_pima_storage_id_send)*</span></span> |
| ![Icona di invio info di archiviazione Pima della classe dispositivo](./media/user-guide/usbx-events/image32.png)    | <span data-ttu-id="5cc78-172">**Classe dispositivo informazioni di archiviazione Pima invio** *(ux_device_class_pima_storage_info_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-172">**Device Class Pima Storage Info Send** *(ux_device_class_pima_storage_info_send)*</span></span> |
| ![Icona di attivazione della classe dispositivo R N D I S](./media/user-guide/usbx-events/image33.png)    | <span data-ttu-id="5cc78-174">**Classe dispositivo RNDIS Activate** *(ux_device_class_rndis_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-174">**Device Class Rndis Activate** *(ux_device_class_rndis_activate)*</span></span> |
| ![Icona di disattivazione della classe dispositivo R N D](./media/user-guide/usbx-events/image34.png)    | <span data-ttu-id="5cc78-176">**Classe dispositivo RNDIS disattivare** *(ux_device_class_rndis_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-176">**Device Class Rndis Deactivate** *(ux_device_class_rndis_deactivate)*</span></span> |
| ![Classe dispositivo R N D I messaggio keep Aliveicon](./media/user-guide/usbx-events/image35.png)    | <span data-ttu-id="5cc78-178">**Classe dispositivo RNDIS messaggio keep-alive** *(ux_device_class_rndis_msg_keep_alive)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-178">**Device Class Rndis Message Keep Alive** *(ux_device_class_rndis_msg_keep_alive)*</span></span> |
| ![Icona della query del messaggio di classe del dispositivo R N D I](./media/user-guide/usbx-events/image36.png)    | <span data-ttu-id="5cc78-180">**Query del messaggio RNDIS della classe dispositivo** *(ux_device_class_rndis_msg_query)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-180">**Device Class Rndis Message Query** *(ux_device_class_rndis_msg_query)*</span></span> |
| ![Icona di reimpostazione del messaggio di classe dispositivo R N D I](./media/user-guide/usbx-events/image37.png)    | <span data-ttu-id="5cc78-182">**Classe dispositivo reimpostazione del messaggio RNDIS** *(ux_device_class_rndis_msg_reset)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-182">**Device Class Rndis Message Reset** *(ux_device_class_rndis_msg_reset)*</span></span> |
| ![Icona del set di messaggi di classe dispositivo R N D I S](./media/user-guide/usbx-events/image38.png)    | <span data-ttu-id="5cc78-184">**Set di messaggi RNDIS della classe dispositivo** *(ux_device_class_rndis_msg_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-184">**Device Class Rndis Message Set** *(ux_device_class_rndis_msg_set)*</span></span> |
| ![Icona di ricezione pacchetti di classe dispositivo R N D I](./media/user-guide/usbx-events/image39.png)    | <span data-ttu-id="5cc78-186">**Classe dispositivo RNDIS ricezione pacchetti** *(ux_device_class_rndis_packet_receive)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-186">**Device Class Rndis Packet Receive** *(ux_device_class_rndis_packet_receive)*</span></span> |
| ![Icona di trasmissione pacchetti della classe dispositivo R N D I](./media/user-guide/usbx-events/image40.png)    | <span data-ttu-id="5cc78-188">**Classe dispositivo RNDIS trasmissione pacchetti** *(ux_device_class_rndis_packet_transmit)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-188">**Device Class Rndis Packet Transmit** *(ux_device_class_rndis_packet_transmit)*</span></span> |
| ![Icona di attivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image41.png)    | <span data-ttu-id="5cc78-190">**Attivazione dell'archiviazione della classe dispositivo** *(ux_device_class_storage_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-190">**Device Class Storage Activate** *(ux_device_class_storage_activate)*</span></span> |
| ![Icona di disattivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image42.png)    | <span data-ttu-id="5cc78-192">**Disattivazione archiviazione classe dispositivo** *(ux_device_class_storage_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-192">**Device Class Storage Deactivate** *(ux_device_class_storage_deactivate)*</span></span> |
| ![Icona del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image43.png)    | <span data-ttu-id="5cc78-194">**Formato di archiviazione della classe dispositivo** *(ux_device_class_storage_format)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-194">**Device Class Storage Format** *(ux_device_class_storage_format)*</span></span> |
| ![Icona di richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image44.png)    | <span data-ttu-id="5cc78-196">**Richiesta di archiviazione della classe dispositivo** *(ux_device_class_storage_inquiry)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-196">**Device Class Storage Inquiry** *(ux_device_class_storage_inquiry)*</span></span> |
| ![Icona di selezione modalità di archiviazione classe dispositivo](./media/user-guide/usbx-events/image45.png)    | <span data-ttu-id="5cc78-198">**Selezione della modalità di archiviazione della classe dispositivo** *(ux_device_class_storage_mode_select)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-198">**Device Class Storage Mode Select** *(ux_device_class_storage_mode_select)*</span></span> |
| ![Icona di rilevamento della modalità di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image46.png)    | <span data-ttu-id="5cc78-200">**Rilevamento della modalità di archiviazione della classe dispositivo** *(ux_device_class_storage_mode_sense)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-200">**Device Class Storage Mode Sense** *(ux_device_class_storage_mode_sense)*</span></span> |
| ![Archiviazione della classe dispositivo Impedisci l'uso dell'icona Consenti rimozione supporti](./media/user-guide/usbx-events/image47.png)    | <span data-ttu-id="5cc78-202">L' **archiviazione delle classi di dispositivi impedisce la rimozione dei supporti** *(ux_device_class_storage_prevent_allow_media_removal)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-202">**Device Class Storage Prevent Allow Media Removal** *(ux_device_class_storage_prevent_allow_media_removal)*</span></span> |
| ![Icona di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image48.png)    | <span data-ttu-id="5cc78-204">**Lettura archiviazione classe dispositivo** *(ux_device_class_storage_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-204">**Device Class Storage Read** *(ux_device_class_storage_read)*</span></span> |
| ![Icona capacità di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image49.png)    | <span data-ttu-id="5cc78-206">**Capacità di lettura di archiviazione della classe dispositivo** *(ux_device_class_storage_read_capacity)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-206">**Device Class Storage Read Capacity** *(ux_device_class_storage_read_capacity)*</span></span> |
| ![Icona della capacità di lettura del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image50.png)    | <span data-ttu-id="5cc78-208">**Capacità di lettura formato di archiviazione della classe dispositivo** *(ux_device_class_storage_read_format_capacity)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-208">**Device Class Storage Read Format Capacity** *(ux_device_class_storage_read_format_capacity)*</span></span> |
| ![Icona di lettura Sommario archiviazione classe dispositivo](./media/user-guide/usbx-events/image51.png)    | <span data-ttu-id="5cc78-210">**Sommario di lettura della classe dispositivo archiviazione** *(ux_device_class_storage_read_toc)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-210">**Device Class Storage Read TOC** *(ux_device_class_storage_read_toc)*</span></span> |
| ![Icona del senso della richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image52.png)    | <span data-ttu-id="5cc78-212">**Rilevamento delle richieste di archiviazione della classe dispositivo** *(ux_device_class_storage_request_sense)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-212">**Device Class Storage Request Sense** *(ux_device_class_storage_request_sense)*</span></span> |
| ![Icona di avvio dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image53.png)    | <span data-ttu-id="5cc78-214">**Inizio arresto archiviazione classe dispositivo** *(ux_device_class_storage_start_stop)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-214">**Device Class Storage Start Stop** *(ux_device_class_storage_start_stop)*</span></span> |
| ![Icona dei test di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image54.png)    | <span data-ttu-id="5cc78-216">**Pronto per il test di archiviazione della classe dispositivo** *(ux_device_class_storage_test_ready)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-216">**Device Class Storage Test Ready** *(ux_device_class_storage_test_ready)*</span></span> |
| ![Icona di verifica archiviazione classe dispositivo](./media/user-guide/usbx-events/image55.png)    | <span data-ttu-id="5cc78-218">**Verifica archiviazione classe dispositivo** *(ux_device_class_storage_verify)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-218">**Device Class Storage Verify** *(ux_device_class_storage_verify)*</span></span> |
| ![Icona di scrittura archiviazione classe dispositivo](./media/user-guide/usbx-events/image56.png)    | <span data-ttu-id="5cc78-220">**Scrittura archiviazione classe dispositivo** *(ux_device_class_storage_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-220">**Device Class Storage Write** *(ux_device_class_storage_write)*</span></span> |
| ![Icona del Get dell'impostazione alternativa dello stack del dispositivo](./media/user-guide/usbx-events/image57.png)    | <span data-ttu-id="5cc78-222">**Impostazione alternativa stack del dispositivo Get** *(ux_device_stack_alternate_setting_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-222">**Device Stack Alternate Setting Get** *(ux_device_stack_alternate_setting_get)*</span></span> |
| ![Icona del set di impostazioni alternativo dello stack del dispositivo](./media/user-guide/usbx-events/image58.png)    | <span data-ttu-id="5cc78-224">**Set di impostazioni alternativo dello stack del dispositivo** *(ux_device_stack_alternate_setting_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-224">**Device Stack Alternate Setting Set** *(ux_device_stack_alternate_setting_set)*</span></span> |
| ![Icona di registro classe stack del dispositivo](./media/user-guide/usbx-events/image59.png)    | <span data-ttu-id="5cc78-226">**Registro classe stack del dispositivo** *(ux_device_stack_class_register)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-226">**Device Stack Class Register** *(ux_device_stack_class_register)*</span></span> |
| ![Icona della funzionalità cancellazione dello stack del dispositivo](./media/user-guide/usbx-events/image60.png)    | <span data-ttu-id="5cc78-228">**Funzionalità di cancellazione dello stack del dispositivo** *(ux_device_stack_clear_feature)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-228">**Device Stack Clear Feature** *(ux_device_stack_clear_feature)*</span></span> |
| ![Icona di Get della configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image61.png)    | <span data-ttu-id="5cc78-230">**Configurazione dello stack del dispositivo Get** *(ux_device_stack_configuration_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-230">**Device Stack Configuration Get** *(ux_device_stack_configuration_get)*</span></span> |
| ![Icona del set di configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image62.png)    | <span data-ttu-id="5cc78-232">**Set di configurazione dello stack del dispositivo** *(ux_device_stack_configuration_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-232">**Device Stack Configuration Set** *(ux_device_stack_configuration_set)*</span></span> |
| ![Icona di connessione dello stack del dispositivo](./media/user-guide/usbx-events/image63.png)    | <span data-ttu-id="5cc78-234">**Connessione stack del dispositivo** *(ux_device_stack_connect)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-234">**Device Stack Connect** *(ux_device_stack_connect)*</span></span> |
| ![Icona di invio del descrittore dello stack del dispositivo](./media/user-guide/usbx-events/image64.png)    | <span data-ttu-id="5cc78-236">**Invio del descrittore dello stack del dispositivo** *(ux_device_stack_descriptor_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-236">**Device Stack Descriptor Send** *(ux_device_stack_descriptor_send)*</span></span> |
| ![Icona di disconnessione dello stack del dispositivo](./media/user-guide/usbx-events/image65.png)    | <span data-ttu-id="5cc78-238">**Disconnessione dello stack del dispositivo** *(ux_device_stack_disconnect)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-238">**Device Stack Disconnect** *(ux_device_stack_disconnect)*</span></span> |
| ![Icona dello stallo dello stack dell'endpoint del dispositivo](./media/user-guide/usbx-events/image66.png)    | <span data-ttu-id="5cc78-240">Blocco **endpoint dello stack del dispositivo** *(ux_device_stack_endpoint_stall)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-240">**Device Stack Endpoint Stall** *(ux_device_stack_endpoint_stall)*</span></span> |
| ![Icona dello stato di Get dello stack del dispositivo](./media/user-guide/usbx-events/image67.png)    | <span data-ttu-id="5cc78-242">**Stato di Get dello stack del dispositivo** *(ux_device_stack_get_status)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-242">**Device Stack Get Status** *(ux_device_stack_get_status)*</span></span> |
| ![Icona di riattivazione host stack del dispositivo](./media/user-guide/usbx-events/image68.png)    | <span data-ttu-id="5cc78-244">Riattivazione **host stack del dispositivo** *(ux_device_stack_host_wakeup)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-244">**Device Stack Host Wakeup** *(ux_device_stack_host_wakeup)*</span></span> |
| ![Icona di inizializzazione dello stack del dispositivo](./media/user-guide/usbx-events/image69.png)    | <span data-ttu-id="5cc78-246">**Inizializzazione dello stack del dispositivo** *(ux_device_stack_initialize)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-246">**Device Stack Initialize** *(ux_device_stack_initialize)*</span></span> |
| ![Icona di eliminazione dell'interfaccia dello stack del dispositivo](./media/user-guide/usbx-events/image70.png)    | <span data-ttu-id="5cc78-248">**Eliminazione interfaccia dello stack di dispositivi** *(ux_device_stack_interface_delete)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-248">**Device Stack Interface Delete** *(ux_device_stack_interface_delete)*</span></span> |
| ![Icona Ottieni interfaccia stack di dispositivi](./media/user-guide/usbx-events/image71.png)    | <span data-ttu-id="5cc78-250">**Interfaccia stack del dispositivo Get** *(ux_device_stack_interface_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-250">**Device Stack Interface Get** *(ux_device_stack_interface_get)*</span></span> |
| ![Icona del set di interfacce dello stack di dispositivi](./media/user-guide/usbx-events/image72.png)    | <span data-ttu-id="5cc78-252">**Set di interfacce dello stack di dispositivi** *(ux_device_stack_interface_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-252">**Device Stack Interface Set** *(ux_device_stack_interface_set)*</span></span> |
| ![Icona della funzionalità set di stack del dispositivo](./media/user-guide/usbx-events/image73.png)    | <span data-ttu-id="5cc78-254">**Funzionalità set di stack del dispositivo** *(ux_device_stack_set_feature)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-254">**Device Stack Set Feature** *(ux_device_stack_set_feature)*</span></span> |
| ![Icona di interruzione del trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image74.png)    | <span data-ttu-id="5cc78-256">**Interruzione trasferimento stack del dispositivo** *(ux_device_stack_transfer_abort)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-256">**Device Stack Transfer Abort** *(ux_device_stack_transfer_abort)*</span></span> |
| ![\* Icona di interruzione della richiesta di trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image75.png)    | <span data-ttu-id="5cc78-258">**Interruzione della richiesta di trasferimento dello stack del dispositivo** *(ux_device_stack_transfer_all_request_abort)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-258">**Device Stack Transfer All Request Abort** *(ux_device_stack_transfer_all_request_abort)*</span></span> |
| ![Icona della richiesta di trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image76.png)    | <span data-ttu-id="5cc78-260">**Richiesta di trasferimento dello stack del dispositivo** *(ux_device_stack_transfer_request)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-260">**Device Stack Transfer Request** *(ux_device_stack_transfer_request)*</span></span> |
| ![Icona di attivazione della classe host ASIX](./media/user-guide/usbx-events/image77.png)    | <span data-ttu-id="5cc78-262">**Classe host ASIX Activate** *(ux_host_class_asix_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-262">**Host Class Asix Activate** *(ux_host_class_asix_activate)*</span></span> |
| ![Icona ASIX della classe host disattiva](./media/user-guide/usbx-events/image78.png)    | <span data-ttu-id="5cc78-264">**Classe host ASIX disattivare** *(ux_host_class_asix_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-264">**Host Class Asix Deactivate** *(ux_host_class_asix_deactivate)*</span></span> |
| ![Icona della notifica di interrupt della classe host ASIX](./media/user-guide/usbx-events/image79.png)    | <span data-ttu-id="5cc78-266">**Notifica di interrupt della classe host ASIX** *(ux_host_class_asix_interrupt_notification)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-266">**Host Class Asix Interrupt Notification** *(ux_host_class_asix_interrupt_notification)*</span></span> |
| ![Icona di lettura della classe host ASIX](./media/user-guide/usbx-events/image80.png)    | <span data-ttu-id="5cc78-268">**Classe host ASIX Read** *(ux_host_class_asix_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-268">**Host Class Asix Read** *(ux_host_class_asix_read)*</span></span> |
| ![Icona di scrittura della classe host ASIX](./media/user-guide/usbx-events/image81.png)    | <span data-ttu-id="5cc78-270">**Classe host ASIX Write** *(ux_host_class_asix_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-270">**Host Class Asix Write** *(ux_host_class_asix_write)*</span></span> |
| ![Icona di attivazione dell'audio della classe host](./media/user-guide/usbx-events/image82.png)    | <span data-ttu-id="5cc78-272">**Attivazione audio classe host** *(ux_host_class_audio_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-272">**Host Class Audio Activate** *(ux_host_class_audio_activate)*</span></span> |
| ![Icona Get del valore del controllo audio della classe host](./media/user-guide/usbx-events/image83.png)    | <span data-ttu-id="5cc78-274">**Valore di controllo audio della classe host Get** *(ux_host_class_audio_control_value_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-274">**Host Class Audio Control Value Get** *(ux_host_class_audio_control_value_get)*</span></span> |
| ![Icona del set di valori del controllo audio della classe host](./media/user-guide/usbx-events/image84.png)    | <span data-ttu-id="5cc78-276">**Impostazione del valore del controllo audio della classe host** *(ux_host_class_audio_control_value_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-276">**Host Class Audio Control Value Set** *(ux_host_class_audio_control_value_set)*</span></span> |
| ![Icona di disattivazione audio della classe host](./media/user-guide/usbx-events/image85.png)    | <span data-ttu-id="5cc78-278">**Disattivazione audio della classe host** *(ux_host_class_audio_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-278">**Host Class Audio Deactivate** *(ux_host_class_audio_deactivate)*</span></span> |
| ![Icona di lettura audio della classe host](./media/user-guide/usbx-events/image86.png)    | <span data-ttu-id="5cc78-280">**Lettura audio classe host** *(ux_host_class_audio_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-280">**Host Class Audio Read** *(ux_host_class_audio_read)*</span></span> |
| ![Icona di Get del campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image87.png)    | <span data-ttu-id="5cc78-282">**Ottenere il campionamento del flusso audio della classe host** *(ux_host_class_audio_streaming_sampling_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-282">**Host Class Audio Streaming Sampling Get** *(ux_host_class_audio_streaming_sampling_get)*</span></span> |
| ![Icona del set di campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image88.png)    | <span data-ttu-id="5cc78-284">**Set di campionamento del flusso audio della classe host** *(ux_host_class_audio_streaming_sampling_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-284">**Host Class Audio Streaming Sampling Set** *(ux_host_class_audio_streaming_sampling_set)*</span></span> |
| ![Icona di scrittura audio della classe host](./media/user-guide/usbx-events/image89.png)    | <span data-ttu-id="5cc78-286">**Scrittura audio della classe host** *(ux_host_class_audio_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-286">**Host Class Audio Write** *(ux_host_class_audio_write)*</span></span> |
| ![Icona di attivazione della classe host C D C A C M](./media/user-guide/usbx-events/image90.png)    | <span data-ttu-id="5cc78-288">**Classe host CDC ACM Activate** *(ux_host_class_cdc_acm_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-288">**Host Class Cdc Acm Activate** *(ux_host_class_cdc_acm_activate)*</span></span> |
| ![Classe host C D C A C M icona di disattivazione](./media/user-guide/usbx-events/image91.png)    | <span data-ttu-id="5cc78-290">**Classe host CDC ACM Deactivate** *(ux_host_class_cdc_acm_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-290">**Host Class Cdc Acm Deactivate** *(ux_host_class_cdc_acm_deactivate)*</span></span> |
| ![Classe host C D C A C M I O C T L nell'icona pipe](./media/user-guide/usbx-events/image92.png)    | <span data-ttu-id="5cc78-292">**Classe host CDC per l'interruzione IOCTL ACM in pipe** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-292">**Host Class Cdc Acm Ioctl Abort In Pipe** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)*</span></span> |
| ![Classe host C D C A C M I O C T L pulsante Interrompi barra verticale](./media/user-guide/usbx-events/image93.png)    | <span data-ttu-id="5cc78-294">**Classe host CDC ACM, Interrompi pipe out pipe** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-294">**Host Class Cdc Acm Ioctl Abort Out Pipe** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)*</span></span> |
| ![Classe host C D C A C M I O C T L icona di stato del dispositivo Get](./media/user-guide/usbx-events/image94.png)    | <span data-ttu-id="5cc78-296">**Classe host CDC ACM IOCTL per ottenere lo stato del dispositivo** *(ux_host_class_cdc_acm_ioctl_get_device_status)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-296">**Host Class Cdc Acm Ioctl Get Device Status** *(ux_host_class_cdc_acm_ioctl_get_device_status)*</span></span> |
| ![Classe host C D C A C M I O C T L ottenere l'icona di codifica della riga](./media/user-guide/usbx-events/image95.png)    | <span data-ttu-id="5cc78-298">**Classe host CDC ACM IOCTL Get line Coding** *(ux_host_class_cdc_acm_ioctl_get_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-298">**Host Class Cdc Acm Ioctl Get Line Coding** *(ux_host_class_cdc_acm_ioctl_get_line_coding)*</span></span> |
| ![Classe host C D C A C M I O C T L icona di callback di notifica](./media/user-guide/usbx-events/image96.png)    | <span data-ttu-id="5cc78-300">**Callback delle notifiche IOCTL di classe host CDC ACM** *(ux_host_class_cdc_acm_ioctl_notification_callback)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-300">**Host Class Cdc Acm Ioctl Notification Callback** *(ux_host_class_cdc_acm_ioctl_notification_callback)*</span></span> |
| ![Classe host C D C A C M I O C T L invio icona di interruzioni](./media/user-guide/usbx-events/image97.png)    | <span data-ttu-id="5cc78-302">**Classe host CDC ACM di invio** *(ux_host_class_cdc_acm_ioctl_send_break)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-302">**Host Class Cdc Acm Ioctl Send Break** *(ux_host_class_cdc_acm_ioctl_send_break)*</span></span> |
| ![Classe host C D C A C M I O C T L impostare l'icona di codifica della riga](./media/user-guide/usbx-events/image98.png)    | <span data-ttu-id="5cc78-304">Codifica a linee del set di righe *(ux_host_class_cdc_acm_ioctl_set_line_coding)* della **classe host CDC ACM** .</span><span class="sxs-lookup"><span data-stu-id="5cc78-304">**Host Class Cdc Acm Ioctl Set Line Coding** *(ux_host_class_cdc_acm_ioctl_set_line_coding)*</span></span> |
| ![Classe host C D C A C M I O C T L impostare lo stato della riga icona](./media/user-guide/usbx-events/image99.png)    | <span data-ttu-id="5cc78-306">**Stato della riga set IOCTL di classe host CDC ACM** *(ux_host_class_cdc_acm_ioctl_set_line_state)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-306">**Host Class Cdc Acm Ioctl Set Line State** *(ux_host_class_cdc_acm_ioctl_set_line_state)*</span></span> |
| ![Icona di lettura c M di classe host c D](./media/user-guide/usbx-events/image100.png)    | <span data-ttu-id="5cc78-308">**Classe host CDC ACM Read** *(ux_host_class_cdc_acm_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-308">**Host Class Cdc Acm Read** *(ux_host_class_cdc_acm_read)*</span></span> |
| ![Icona di avvio della ricezione c M della classe host C D C](./media/user-guide/usbx-events/image101.png)    | <span data-ttu-id="5cc78-310">**Classe host CDC ACM reception Start** *(ux_host_class_cdc_acm_reception_start)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-310">**Host Class Cdc Acm Reception Start** *(ux_host_class_cdc_acm_reception_start)*</span></span> |
| ![Icona di arresto della ricezione c M per la classe host C D C](./media/user-guide/usbx-events/image102.png)    | <span data-ttu-id="5cc78-312">**Arresto della ricezione della classe host CDC ACM** *(ux_host_class_cdc_acm_reception_stop)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-312">**Host Class Cdc Acm Reception Stop** *(ux_host_class_cdc_acm_reception_stop)*</span></span> |
| ![Icona di scrittura della classe host C D C A C M](./media/user-guide/usbx-events/image103.png)    | <span data-ttu-id="5cc78-314">**Classe host CDC ACM Write** *(ux_host_class_cdc_acm_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-314">**Host Class Cdc Acm Write** *(ux_host_class_cdc_acm_write)*</span></span> |
| ![Icona di attivazione della classe host DPUMP](./media/user-guide/usbx-events/image104.png)    | <span data-ttu-id="5cc78-316">**Classe host DPUMP Activate** *(ux_host_class_dpump_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-316">**Host Class Dpump Activate** *(ux_host_class_dpump_activate)*</span></span> |
| ![Icona DPUMP della classe host disattiva](./media/user-guide/usbx-events/image105.png)    | <span data-ttu-id="5cc78-318">**Classe host DPUMP disattivare** *(ux_host_class_dpump_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-318">**Host Class Dpump Deactivate** *(ux_host_class_dpump_deactivate)*</span></span> |
| ![Icona di lettura della classe host DPUMP](./media/user-guide/usbx-events/image106.png)    | <span data-ttu-id="5cc78-320">**Classe host DPUMP Read** *(ux_host_class_dpump_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-320">**Host Class Dpump Read** *(ux_host_class_dpump_read)*</span></span> |
| ![Icona di scrittura della classe host DPUMP](./media/user-guide/usbx-events/image107.png)    | <span data-ttu-id="5cc78-322">**Classe host DPUMP Write** *(ux_host_class_dpump_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-322">**Host Class Dpump Write** *(ux_host_class_dpump_write)*</span></span> |
| ![Icona di attivazione HID della classe host](./media/user-guide/usbx-events/image108.png)    | <span data-ttu-id="5cc78-324">**Attivazione HID della classe host** *(ux_host_class_hid_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-324">**Host Class Hid Activate** *(ux_host_class_hid_activate)*</span></span> |
| ![Icona di registro del client HID della classe host](./media/user-guide/usbx-events/image109.png)    | <span data-ttu-id="5cc78-326">**Registro del client HID della classe host** *(ux_host_class_hid_client_register)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-326">**Host Class Hid Client Register** *(ux_host_class_hid_client_register)*</span></span> |
| ![Icona di disattivazione HID della classe host](./media/user-guide/usbx-events/image110.png)    | <span data-ttu-id="5cc78-328">**Disattivazione HID della classe host** *(ux_host_class_hid_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-328">**Host Class Hid Deactivate** *(ux_host_class_hid_deactivate)*</span></span> |
| ![Icona della classe host HID Idle Get](./media/user-guide/usbx-events/image111.png)    | <span data-ttu-id="5cc78-330">**Classe host HID Idle Get** *(ux_host_class_hid_idle_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-330">**Host Class Hid Idle Get** *(ux_host_class_hid_idle_get)*</span></span> |
| ![Icona del set di inattività HID della classe host](./media/user-guide/usbx-events/image112.png)    | <span data-ttu-id="5cc78-332">**Set di inattività HID della classe host** *(ux_host_class_hid_idle_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-332">**Host Class Hid Idle Set** *(ux_host_class_hid_idle_set)*</span></span> |
| ![Icona di attivazione della tastiera HID della classe host](./media/user-guide/usbx-events/image113.png)    | <span data-ttu-id="5cc78-334">**Attiva tastiera HID della classe host** *(ux_host_class_hid_keyboard_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-334">**Host Class Hid Keyboard Activate** *(ux_host_class_hid_keyboard_activate)*</span></span> |
| ![Icona di disattivazione tastiera HID della classe host](./media/user-guide/usbx-events/image114.png)    | <span data-ttu-id="5cc78-336">**Disattiva la tastiera HID della classe host** *(ux_host_class_hid_keyboard_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-336">**Host Class Hid Keyboard Deactivate** *(ux_host_class_hid_keyboard_deactivate)*</span></span> |
| ![Icona di attivazione della classe host HID mouse](./media/user-guide/usbx-events/image115.png)    | <span data-ttu-id="5cc78-338">**Attivazione mouse HID classe host** *(ux_host_class_hid_mouse_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-338">**Host Class Hid Mouse Activate** *(ux_host_class_hid_mouse_activate)*</span></span> |
| ![Icona di disattivazione della classe host HID mouse](./media/user-guide/usbx-events/image116.png)    | <span data-ttu-id="5cc78-340">Deactivate *(ux_host_class_hid_mouse_deactivate)* della **classe host HID mouse**</span><span class="sxs-lookup"><span data-stu-id="5cc78-340">**Host Class Hid Mouse Deactivate** *(ux_host_class_hid_mouse_deactivate)*</span></span> |
| ![Icona di attivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image117.png)    | <span data-ttu-id="5cc78-342">**Attivazione del controllo remoto HID della classe host** *(ux_host_class_hid_remote_control_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-342">**Host Class Hid Remote Control Activate** *(ux_host_class_hid_remote_control_activate)*</span></span> |
| ![Icona di disattivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image118.png)    | <span data-ttu-id="5cc78-344">**Disattivazione del controllo remoto HID della classe host** *(ux_host_class_hid_remote_control_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-344">**Host Class Hid Remote Control Deactivate** *(ux_host_class_hid_remote_control_deactivate)*</span></span> |
| ![Icona di Get del report HID della classe host](./media/user-guide/usbx-events/image119.png)    | <span data-ttu-id="5cc78-346">**Classe host (report HID) Get** *(ux_host_class_hid_report_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-346">**Host Class Hid Report Get** *(ux_host_class_hid_report_get)*</span></span> |
| ![Icona del set di report HID della classe host](./media/user-guide/usbx-events/image120.png)    | <span data-ttu-id="5cc78-348">**Set di report HID della classe host** *(ux_host_class_hid_report_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-348">**Host Class Hid Report Set** *(ux_host_class_hid_report_set)*</span></span> |
| ![Icona di attivazione dell'hub classe host](./media/user-guide/usbx-events/image121.png)    | <span data-ttu-id="5cc78-350">**Attivazione Hub classe host** *(ux_host_class_hub_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-350">**Host Class Hub Activate** *(ux_host_class_hub_activate)*</span></span> |
| ![Icona rilevamento modifiche Hub classe host](./media/user-guide/usbx-events/image122.png)    | <span data-ttu-id="5cc78-352">**Rilevamento modifiche Hub classe host** *(ux_host_class_hub_change_detect)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-352">**Host Class Hub Change Detect** *(ux_host_class_hub_change_detect)*</span></span> |
| ![\* Icona di disattivazione dell'hub classe host](./media/user-guide/usbx-events/image123.png)    | <span data-ttu-id="5cc78-354">**Disattivazione dell'hub della classe host** *(ux_host_class_hub_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-354">**Host Class Hub Deactivate** *(ux_host_class_hub_deactivate)*</span></span> |
| ![Icona del processo di connessione della porta dell'hub della classe host](./media/user-guide/usbx-events/image124.png)    | <span data-ttu-id="5cc78-356">**Processo di connessione modifica porta hub classe host** *(ux_host_class_hub_port_change_connection_process)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-356">**Host Class Hub Port Change Connection Process** *(ux_host_class_hub_port_change_connection_process)*</span></span> |
| ![Icona di abilitazione del processo modifica porta hub classe host](./media/user-guide/usbx-events/image125.png)    | <span data-ttu-id="5cc78-358">**Processo di abilitazione della porta dell'hub della classe host** *(ux_host_class_hub_port_change_enable_process)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-358">**Host Class Hub Port Change Enable Process** *(ux_host_class_hub_port_change_enable_process)*</span></span> |
| ![Icona modifica porta hub classe host sull'icona del processo corrente](./media/user-guide/usbx-events/image126.png)    | <span data-ttu-id="5cc78-360">**Modifica della porta dell'hub della classe host per il processo corrente** *(ux_host_class_hub_port_change_over_current_process)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-360">**Host Class Hub Port Change Over Current Process** *(ux_host_class_hub_port_change_over_current_process)*</span></span> |
| ![Icona del processo di reimpostazione della porta dell'hub della classe host](./media/user-guide/usbx-events/image127.png)    | <span data-ttu-id="5cc78-362">**Processo di reimpostazione della porta dell'hub della classe host** *(ux_host_class_hub_port_change_reset_process)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-362">**Host Class Hub Port Change Reset Process** *(ux_host_class_hub_port_change_reset_process)*</span></span> |
| ![Icona di sospensione del processo di modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image128.png)    | <span data-ttu-id="5cc78-364">**Processo di sospensione delle modifiche della porta dell'hub della classe host** *(ux_host_class_hub_port_change_suspend_process)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-364">**Host Class Hub Port Change Suspend Process** *(ux_host_class_hub_port_change_suspend_process)*</span></span> |
| ![Icona di attivazione della classe host Pima](./media/user-guide/usbx-events/image129.png)    | <span data-ttu-id="5cc78-366">**Classe host Pima Activate** *(ux_host_class_prima_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-366">**Host Class Pima Activate** *(ux_host_class_prima_activate)*</span></span> |
| ![Icona di disattivazione della classe host Pima](./media/user-guide/usbx-events/image130.png)    | <span data-ttu-id="5cc78-368">**Classe host Pima Deactivate** *(ux_host_class_pima_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-368">**Host Class Pima Deactivate** *(ux_host_class_pima_deactivate)*</span></span> |
| ![Icona di informazioni sul dispositivo Pima della classe host](./media/user-guide/usbx-events/image131.png)    | <span data-ttu-id="5cc78-370">**Classe host informazioni sul dispositivo Pima Get** *(ux_host_class_pima_device_info_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-370">**Host Class Pima Device Info Get** *(ux_host_class_pima_device_info_get)*</span></span> |
| ![Icona di reimpostazione del dispositivo Pima della classe host](./media/user-guide/usbx-events/image132.png)    | <span data-ttu-id="5cc78-372">**Reimpostazione del dispositivo Pima della classe host** *(ux_host_class_pima_device_reset)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-372">**Host Class Pima Device Reset** *(ux_host_class_pima_device_reset)*</span></span> |
| ![Icona di notifica classe host Pima](./media/user-guide/usbx-events/image133.png)    | <span data-ttu-id="5cc78-374">**Notifica classe host Pima** *(ux_host_class_pima_notification)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-374">**Host Class Pima Notification** *(ux_host_class_pima_notification)*</span></span> |
| ![Icona di visualizzazione degli oggetti numero Pima della classe host](./media/user-guide/usbx-events/image134.png)    | <span data-ttu-id="5cc78-376">**Classe host numero Pima oggetti Get** *(ux_host_class_pima_num_objects_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-376">**Host Class Pima Number Objects Get** *(ux_host_class_pima_num_objects_get)*</span></span> |
| ![Icona di chiusura oggetto classe host Pima](./media/user-guide/usbx-events/image135.png)    | <span data-ttu-id="5cc78-378">**Chiusura oggetto Pima classe host** *(ux_host_class_pima_object_close)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-378">**Host Class Pima Object Close** *(ux_host_class_pima_object_close)*</span></span> |
| ![Icona di copia dell'oggetto classe host Pima](./media/user-guide/usbx-events/image136.png)    | <span data-ttu-id="5cc78-380">**Classe host copia oggetto Pima** *(ux_host_class_pima_object_copy)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-380">**Host Class Pima Object Copy** *(ux_host_class_pima_object_copy)*</span></span> |
| ![Icona di eliminazione oggetto classe host Pima](./media/user-guide/usbx-events/image137.png)    | <span data-ttu-id="5cc78-382">**Classe host Elimina oggetto Pima** *(ux_host_class_pima_object_delete)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-382">**Host Class Pima Object Delete** *(ux_host_class_pima_object_delete)*</span></span> |
| ![Icona di Get oggetto della classe host Pima](./media/user-guide/usbx-events/image138.png)    | <span data-ttu-id="5cc78-384">**Classe host (oggetto Pima) Get** *(ux_host_class_pima_object_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-384">**Host Class Pima Object Get** *(ux_host_class_pima_object_get)*</span></span> |
| ![Icona di visualizzazione delle informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image139.png)    | <span data-ttu-id="5cc78-386">**Classe host, informazioni sull'oggetto Pima Get** *(ux_host_class_pima_object_info_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-386">**Host Class Pima Object Info Get** *(ux_host_class_pima_object_info_get)*</span></span> |
| ![Icona di invio info oggetto Pima classe host](./media/user-guide/usbx-events/image140.png)    | <span data-ttu-id="5cc78-388">**Classe host-informazioni sull'oggetto Pima Send** *(ux_host_class_pima_object_info_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-388">**Host Class Pima Object Info Send** *(ux_host_class_pima_object_info_send)*</span></span> |
| ![Icona di spostamento oggetto classe host Pima](./media/user-guide/usbx-events/image141.png)    | <span data-ttu-id="5cc78-390">**Spostamento oggetto classe host Pima** *(ux_host_class_pima_object_move)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-390">**Host Class Pima Object Move** *(ux_host_class_pima_object_move)*</span></span> |
| ![Icona di invio oggetto Pima classe host](./media/user-guide/usbx-events/image142.png)    | <span data-ttu-id="5cc78-392">**Classe host per l'invio di oggetti Pima** *(ux_host_class_pima_object_send)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-392">**Host Class Pima Object Send** *(ux_host_class_pima_object_send)*</span></span> |
| ![Icona di interruzione trasferimento oggetti Pima classe host](./media/user-guide/usbx-events/image143.png)    | <span data-ttu-id="5cc78-394">**Interruzione del trasferimento di oggetti Pima della classe host** *(ux_host_class_object_transfer_abort)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-394">**Host Class Pima Object Transfer Abort** *(ux_host_class_object_transfer_abort)*</span></span> |
| ![Icona di lettura della classe host Pima](./media/user-guide/usbx-events/image144.png)    | <span data-ttu-id="5cc78-396">**Classe host Pima Read** *(ux_host_class_pima_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-396">**Host Class Pima Read** *(ux_host_class_pima_read)*</span></span> |
| ![Icona di annullamento richiesta Pima della classe host](./media/user-guide/usbx-events/image145.png)    | <span data-ttu-id="5cc78-398">**Classe host Pima richiesta Cancel** *(ux_host_class_pima_request_cancel)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-398">**Host Class Pima Request Cancel** *(ux_host_class_pima_request_cancel)*</span></span> |
| ![Icona di chiusura della sessione Pima della classe host](./media/user-guide/usbx-events/image146.png)    | <span data-ttu-id="5cc78-400">**Chiusura della sessione Pima della classe host** *(ux_host_class_pima_session_close)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-400">**Host Class Pima Session Close** *(ux_host_class_pima_session_close)*</span></span> |
| ![Icona di apertura della sessione Pima della classe host](./media/user-guide/usbx-events/image147.png)    | <span data-ttu-id="5cc78-402">La **sessione Pima della classe host è aperta** *(ux_host_class_pima_session_open)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-402">**Host Class Pima Session Open** *(ux_host_class_pima_session_open)*</span></span> |
| ![Icona di Get dell'ID di archiviazione Pima della classe host](./media/user-guide/usbx-events/image148.png)    | <span data-ttu-id="5cc78-404">**Classe host (ID di archiviazione Pima) Get** *(ux_host_class_pima_storage_ids_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-404">**Host Class Pima Storage Ids Get** *(ux_host_class_pima_storage_ids_get)*</span></span> |
| ![Icona di informazioni di archiviazione per la classe host Pima](./media/user-guide/usbx-events/image149.png)    | <span data-ttu-id="5cc78-406">**Classe host Pima info archiviazione Get** *(ux_host_class_pima_storage_info_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-406">**Host Class Pima Storage Info Get** *(ux_host_class_pima_storage_info_get)*</span></span> |
| ![Icona della classe host Pima Thumb Get](./media/user-guide/usbx-events/image150.png)    | <span data-ttu-id="5cc78-408">**Classe host Pima Thumb Get** *(ux_host_class_pima_thumb_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-408">**Host Class Pima Thumb Get** *(ux_host_class_pima_thumb_get)*</span></span> |
| ![Icona di scrittura della classe host Pima](./media/user-guide/usbx-events/image151.png)    | <span data-ttu-id="5cc78-410">**Classe host di scrittura Pima** *(ux_host_class_pima_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-410">**Host Class Pima Write** *(ux_host_class_pima_write)*</span></span> |
| ![Icona di attivazione della stampante della classe host](./media/user-guide/usbx-events/image152.png)    | <span data-ttu-id="5cc78-412">**Attivazione della stampante della classe host** *(ux_host_class_printer_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-412">**Host Class Printer Activate** *(ux_host_class_printer_activate)*</span></span> |
| ![Icona di disattivazione della stampante della classe host](./media/user-guide/usbx-events/image153.png)    | <span data-ttu-id="5cc78-414">**Disattivazione della stampante della classe host** *(ux_host_class_printer_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-414">**Host Class Printer Deactivate** *(ux_host_class_printer_deactivate)*</span></span> |
| ![Icona di visualizzazione del nome della stampante della classe host](./media/user-guide/usbx-events/image154.png)    | <span data-ttu-id="5cc78-416">**Nome della stampante della classe host Get** *(ux_host_class_printer_name_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-416">**Host Class Printer Name Get** *(ux_host_class_printer_name_get)*</span></span> |
| ![Icona di lettura della stampante della classe host](./media/user-guide/usbx-events/image155.png)    |  <span data-ttu-id="5cc78-418">**Lettura stampante classe host** *(ux_host_class_printer_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-418">**Host Class Printer Read** *(ux_host_class_printer_read)*</span></span> |
| ![Icona di ripristino soft della stampante della classe host](./media/user-guide/usbx-events/image156.png)    | <span data-ttu-id="5cc78-420">**Reimpostazione soft della stampante della classe host** *(ux_host_class_printer_soft_reset)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-420">**Host Class Printer Soft Reset** *(ux_host_class_printer_soft_reset)*</span></span> |
| ![Icona di Get dello stato della stampante della classe host](./media/user-guide/usbx-events/image157.png)    | <span data-ttu-id="5cc78-422">**Stato della stampante della classe host Get** *(ux_host_class_printer_status_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-422">**Host Class Printer Status Get** *(ux_host_class_printer_status_get)*</span></span> |
| ![Icona di scrittura della stampante della classe host](./media/user-guide/usbx-events/image158.png)    | <span data-ttu-id="5cc78-424">**Scrittura della stampante della classe host** *(ux_host_class_printer_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-424">**Host Class Printer Write** *(ux_host_class_printer_write)*</span></span> |
| ![Icona di attivazione della classe host Prolific](./media/user-guide/usbx-events/image159.png)    | <span data-ttu-id="5cc78-426">**Attiva la classe host Prolific** *(ux_host_class_prolific_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-426">**Host Class Prolific Activate** *(ux_host_class_prolific_activate)*</span></span> |
| ![Icona di disattivazione della classe host](./media/user-guide/usbx-events/image160.png)    | <span data-ttu-id="5cc78-428">**Classe host Deactivate** *(ux_host_class_prolific_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-428">**Host Class Prolific Deactivate** *(ux_host_class_prolific_deactivate)*</span></span> |
| ![Icona della classe host I/O per le interruzioni in pipe](./media/user-guide/usbx-events/image161.png)    | <span data-ttu-id="5cc78-430">**Classe host-interruzioni IOCTL in pipe** *(ux_host_class_prolific_ioctl_abort_in_pipe)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-430">**Host Class Prolific Ioctl Abort In Pipe** *(ux_host_class_prolific_ioctl_abort_in_pipe)*</span></span> |
| ![Icona della classe host Prolific I O C T interrompe la pipe](./media/user-guide/usbx-events/image162.png)    | <span data-ttu-id="5cc78-432">**Classe host con IOCTL Abort Abort pipe** *(ux_host_class_prolific_ioctl_abort_out_pipe)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-432">**Host Class Prolific Ioctl Abort Out Pipe** *(ux_host_class_prolific_ioctl_abort_out_pipe)*</span></span> |
| ![Icona dello stato del dispositivo per la classe host Prolific I O C T](./media/user-guide/usbx-events/image163.png)    | <span data-ttu-id="5cc78-434">**Classe host prolifico IOCTL ottenere lo stato del dispositivo** *(ux_host_class_prolific_ioctl_get_device_status)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-434">**Host Class Prolific Ioctl Get Device Status** *(ux_host_class_prolific_ioctl_get_device_status)*</span></span> |
| ![Icona della codifica della riga per la classe host Prolific I O C](./media/user-guide/usbx-events/image164.png)    | <span data-ttu-id="5cc78-436">**Classe host prolifico IOCTL Get line Coding** *(ux_host_class_prolific_ioctl_get_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-436">**Host Class Prolific Ioctl Get Line Coding** *(ux_host_class_prolific_ioctl_get_line_coding)*</span></span> |
| ![Icona di ripulitura della classe host Prolific I O C T](./media/user-guide/usbx-events/image165.png)    | <span data-ttu-id="5cc78-438">**Classe host ripulitura IOCTL** *(ux_host_class_prolific_ioctl_purge)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-438">**Host Class Prolific Ioctl Purge** *(ux_host_class_prolific_ioctl_purge)*</span></span> |
| ![Icona di modifica dello stato del dispositivo di report I O C per la classe host](./media/user-guide/usbx-events/image166.png)    | <span data-ttu-id="5cc78-440">**Modifica dello stato del dispositivo del report IOCTL per la classe host** *(ux_host_class_prolific_ioctl_report_device_status_change)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-440">**Host Class Prolific Ioctl Report Device Status Change** *(ux_host_class_prolific_ioctl_report_device_status_change)*</span></span> |
| ![Icona di invio della classe host Prolific I O C T](./media/user-guide/usbx-events/image167.png)    | <span data-ttu-id="5cc78-442">**Classe host prolifico di invio di IOCTL** *(ux_host_class_prolific_ioctl_send_break)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-442">**Host Class Prolific Ioctl Send Break** *(ux_host_class_prolific_ioctl_send_break)*</span></span> |
| ![Icona del codice a linee set di classe host Prolific I O C T L](./media/user-guide/usbx-events/image168.png)    | <span data-ttu-id="5cc78-444">**Codifica della riga del set IOCTL della classe host** *(ux_host_class_prolific_ioctl_set_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-444">**Host Class Prolific Ioctl Set Line Coding** *(ux_host_class_prolific_ioctl_set_line_coding)*</span></span> |
| ![Icona dello stato della linea di impostazione della classe host Prolific I O C T](./media/user-guide/usbx-events/image169.png)    | <span data-ttu-id="5cc78-446">**Stato della riga set IOCTL prolifico della classe host** *(ux_host_class_prolific_ioctl_set_line_state)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-446">**Host Class Prolific Ioctl Set Line State** *(ux_host_class_prolific_ioctl_set_line_state)*</span></span> |
| ![Icona lettura prolifica classe host](./media/user-guide/usbx-events/image170.png)    | <span data-ttu-id="5cc78-448">**Lettura prolifica della classe host** *(ux_host_class_prolific_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-448">**Host Class Prolific Read** *(ux_host_class_prolific_read)*</span></span> |
| ![Icona di inizio della ricezione prolifico della classe host](./media/user-guide/usbx-events/image171.png)    | <span data-ttu-id="5cc78-450">**Avvio della ricezione prolifico della classe host** *(ux_host_class_prolific_reception_start)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-450">**Host Class Prolific Reception Start** *(ux_host_class_prolific_reception_start)*</span></span> |
| ![Icona di arresto della ricezione della classe host Prolific](./media/user-guide/usbx-events/image172.png)    | <span data-ttu-id="5cc78-452">**Arresto della ricezione prolifico della classe host** *(ux_host_class_prolific_reception_stop)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-452">**Host Class Prolific Reception Stop** *(ux_host_class_prolific_reception_stop)*</span></span> |
| ![Icona di scrittura della classe host Prolific](./media/user-guide/usbx-events/image173.png)    | <span data-ttu-id="5cc78-454">**Classe host-scrittura prolifica** *(ux_host_class_prolific_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-454">**Host Class Prolific Write** *(ux_host_class_prolific_write)*</span></span> |
| ![Icona di attivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image174.png)    | <span data-ttu-id="5cc78-456">**Attivazione dell'archiviazione della classe host** *(ux_host_class_storage_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-456">**Host Class Storage Activate** *(ux_host_class_storage_activate)*</span></span> |
| ![Icona di disattivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image175.png)    | <span data-ttu-id="5cc78-458">**Disattivazione dell'archiviazione della classe host** (*ux_host_class_storage_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-458">**Host Class Storage Deactivate** (*ux_host_class_storage_deactivate)*</span></span> |
| ![Icona Ottieni capacità supporto di archiviazione classe host](./media/user-guide/usbx-events/image176.png)    | <span data-ttu-id="5cc78-460">**Capacità del supporto di archiviazione della classe host Get** *(ux_host_class_storage_media_capacity_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-460">**Host Class Storage Media Capacity Get** *(ux_host_class_storage_media_capacity_get)*</span></span> |
| ![Icona per la capacità del formato del supporto di archiviazione della classe host](./media/user-guide/usbx-events/image177.png)    | <span data-ttu-id="5cc78-462">**Classe host archiviazione della capacità formato supporto Get** *(ux_host_class_storage_media_format_capacity_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-462">**Host Class Storage Media Format Capacity Get** *(ux_host_class_storage_media_format_capacity_get)*</span></span> |
| ![Icona di montaggio dei supporti di archiviazione della classe host](./media/user-guide/usbx-events/image178.png)    | <span data-ttu-id="5cc78-464">**Montaggio dei supporti di archiviazione della classe host** (ux_host_class_storage_media_mount) \*</span><span class="sxs-lookup"><span data-stu-id="5cc78-464">**Host Class Storage Media Mount** (ux_host_class_storage_media_mount)\*</span></span> |
| ![Icona Apri supporto di archiviazione classe host](./media/user-guide/usbx-events/image179.png)    | <span data-ttu-id="5cc78-466">**Supporto di archiviazione della classe host aperto** *(ux_host_class_storage_media_open)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-466">**Host Class Storage Media Open** *(ux_host_class_storage_media_open)*</span></span> |
| ![Icona lettura supporti di archiviazione classe host](./media/user-guide/usbx-events/image180.png)    | <span data-ttu-id="5cc78-468">**Lettura supporto di archiviazione classe host** *(ux_host_class_storage_media_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-468">**Host Class Storage Media Read** *(ux_host_class_storage_media_read)*</span></span> |
| ![Icona Scrivi supporto di archiviazione classe host](./media/user-guide/usbx-events/image181.png)    | <span data-ttu-id="5cc78-470">**Scrittura dei supporti di archiviazione della classe host** *(ux_host_class_storage_media_write)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-470">**Host Class Storage Media Write** *(ux_host_class_storage_media_write)*</span></span> |
| ![Icona del rilevamento della richiesta di archiviazione della classe host](./media/user-guide/usbx-events/image182.png)    | <span data-ttu-id="5cc78-472">**Rilevamento delle richieste di archiviazione della classe host** *(ux_host_class_storage_request_sense)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-472">**Host Class Storage Request Sense** *(ux_host_class_storage_request_sense)*</span></span> |
| ![Icona di avvio dell'archiviazione della classe host](./media/user-guide/usbx-events/image183.png)    | <span data-ttu-id="5cc78-474">**Inizio arresto archiviazione classe host** *(ux_host_class_storage_start_stop)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-474">**Host Class Storage Start Stop** *(ux_host_class_storage_start_stop)*</span></span> |
| ![Icona del test pronto per l'unità di archiviazione della classe host](./media/user-guide/usbx-events/image184.png)    | <span data-ttu-id="5cc78-476">**Test pronto per l'unità di archiviazione della classe host** *(ux_host_class_storage_activate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-476">**Host Class Storage Unit Ready Test** *(ux_host_class_storage_activate)*</span></span> |
| ![Icona di creazione dell'istanza della classe Stack host](./media/user-guide/usbx-events/image185.png)    | <span data-ttu-id="5cc78-478">**Creazione istanza Classe stack host** *(ux_host_stack_class_instance_create)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-478">**Host Stack Class Instance Create** *(ux_host_stack_class_instance_create)*</span></span> |
| ![Icona di eliminazione istanza Classe stack host](./media/user-guide/usbx-events/image186.png)    | <span data-ttu-id="5cc78-480">**Eliminazione istanza Classe stack host** *(ux_host_stack_class_instance_destroy)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-480">**Host Stack Class Instance Destroy** *(ux_host_stack_class_instance_destroy)*</span></span> |
| ![Icona di eliminazione della configurazione dello stack host](./media/user-guide/usbx-events/image187.png)    | <span data-ttu-id="5cc78-482">**Eliminazione della configurazione dello stack host** *(ux_host_stack_configuration_delete)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-482">**Host Stack Configuration Delete** *(ux_host_stack_configuration_delete)*</span></span> |
| ![Icona di enumerazione della configurazione dello stack host](./media/user-guide/usbx-events/image188.png)    | <span data-ttu-id="5cc78-484">**Enumerazione della configurazione dello stack host** *(ux_host_stack_configuration_enumerate)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-484">**Host Stack Configuration Enumerate** *(ux_host_stack_configuration_enumerate)*</span></span> |
| ![Icona di creazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image189.png)    | <span data-ttu-id="5cc78-486">**Creazione dell'istanza di configurazione dello stack host** *(ux_host_stack_configuration_instance_create)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-486">**Host Stack Configuration Instance Create** *(ux_host_stack_configuration_instance_create)*</span></span> |
| ![Icona di eliminazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image190.png)    | <span data-ttu-id="5cc78-488">**Eliminazione dell'istanza di configurazione dello stack host** *(ux_host_stack_configuration_instance_delete)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-488">**Host Stack Configuration Instance Delete** *(ux_host_stack_configuration_instance_delete)*</span></span> |
| ![Icona del set di configurazione dello stack host](./media/user-guide/usbx-events/image191.png)    | <span data-ttu-id="5cc78-490">**Set di configurazione dello stack host** *(ux_host_stack_configuration_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-490">**Host Stack Configuration Set** *(ux_host_stack_configuration_set)*</span></span> |
| ![Icona del set di indirizzi del dispositivo dello stack host](./media/user-guide/usbx-events/image192.png)    | <span data-ttu-id="5cc78-492">**Set di indirizzi dispositivo stack host** *(ux_host_stack_device_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-492">**Host Stack Device Address Set** *(ux_host_stack_device_set)*</span></span> |
| ![Icona get configurazione dispositivo stack host](./media/user-guide/usbx-events/image193.png)    | <span data-ttu-id="5cc78-494">**Configurazione del dispositivo dello stack host Get** *(ux_host_stack_device_configuration_get)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-494">**Host Stack Device Configuration Get** *(ux_host_stack_device_configuration_get)*</span></span> |
| ![Icona di selezione configurazione dispositivo stack host](./media/user-guide/usbx-events/image194.png)    | <span data-ttu-id="5cc78-496">**Selezione configurazione dispositivo stack host** *(ux_host_stack_device_configuration_select)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-496">**Host Stack Device Configuration Select** *(ux_host_stack_device_configuration_select)*</span></span> |
| ![Icona di lettura del descrittore del dispositivo dello stack host](./media/user-guide/usbx-events/image195.png)    | <span data-ttu-id="5cc78-498">**Lettura descrittore dispositivo stack host** *(ux_host_stack_device_descriptor_read)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-498">**Host Stack Device Descriptor Read** *(ux_host_stack_device_descriptor_read)*</span></span> |
| ![Icona Ottieni dispositivo stack host](./media/user-guide/usbx-events/image196.png)    | <span data-ttu-id="5cc78-500">Get (ux_host_stack_device_get) del **dispositivo dello stack host**</span><span class="sxs-lookup"><span data-stu-id="5cc78-500">**Host Stack Device Get** (ux_host_stack_device_get)</span></span> |
| ![Icona Rimuovi dispositivo stack host](./media/user-guide/usbx-events/image197.png)    | <span data-ttu-id="5cc78-502">**Rimozione dispositivo stack host** (ux_host_stack_device_get)</span><span class="sxs-lookup"><span data-stu-id="5cc78-502">**Host Stack Device Remove** (ux_host_stack_device_get)</span></span> |
| ![Icona della risorsa del dispositivo dello stack host](./media/user-guide/usbx-events/image198.png)    | <span data-ttu-id="5cc78-504">**Risorsa dispositivo stack host disponibile** (ux_host_stack_device_resource_free)</span><span class="sxs-lookup"><span data-stu-id="5cc78-504">**Host Stack Device Resource Free** (ux_host_stack_device_resource_free)</span></span> |
| ![Icona di creazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image199.png)    | <span data-ttu-id="5cc78-506">**Creazione dell'istanza dell'endpoint dello stack host** (ux_host_stack_endpoint_instance_create)</span><span class="sxs-lookup"><span data-stu-id="5cc78-506">**Host Stack Endpoint Instance Create** (ux_host_stack_endpoint_instance_create)</span></span> |
| ![Icona di eliminazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image200.png)    | <span data-ttu-id="5cc78-508">**Eliminazione istanza endpoint dello stack host** (ux_host_stack_endpoint_instance_delete)</span><span class="sxs-lookup"><span data-stu-id="5cc78-508">**Host Stack Endpoint Instance Delete** (ux_host_stack_endpoint_instance_delete)</span></span> |
| ![Icona di reimpostazione dell'endpoint dello stack host](./media/user-guide/usbx-events/image201.png)    | <span data-ttu-id="5cc78-510">**Reimpostazione dell'endpoint dello stack host** (ux_host_stack_endpoint_reset)</span><span class="sxs-lookup"><span data-stu-id="5cc78-510">**Host Stack Endpoint Reset** (ux_host_stack_endpoint_reset)</span></span> |
| ![Icona di interruzione del trasferimento dell'endpoint dello stack host](./media/user-guide/usbx-events/image202.png)    | <span data-ttu-id="5cc78-512">**Interruzione trasferimento endpoint dello stack host** (ux_host_stack_endpoint_transfer_abort)</span><span class="sxs-lookup"><span data-stu-id="5cc78-512">**Host Stack Endpoint Transfer Abort** (ux_host_stack_endpoint_transfer_abort)</span></span> |
| ![Icona registro del controller host dello stack host](./media/user-guide/usbx-events/image203.png)    | <span data-ttu-id="5cc78-514">**Registro del controller host dello stack** host *(ux_host_stack_hcd_register)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-514">**Host Stack Host Controller Register** *(ux_host_stack_hcd_register)*</span></span> |
| ![Icona di inizializzazione dello stack host](./media/user-guide/usbx-events/image204.png)    | <span data-ttu-id="5cc78-516">**Inizializzazione stack host** *(ux_host_stack_initialize)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-516">**Host Stack Initialize** *(ux_host_stack_initialize)*</span></span> |
| ![Icona Ottieni endpoint interfaccia stack host](./media/user-guide/usbx-events/image205.png)    | <span data-ttu-id="5cc78-518">Get *(ux_host_stack_interface_endpoint_get)* dell' **endpoint dell'interfaccia dello stack host**</span><span class="sxs-lookup"><span data-stu-id="5cc78-518">**Host Stack Interface Endpoint Get** *(ux_host_stack_interface_endpoint_get)*</span></span> |
| ![Icona di creazione dell'istanza dell'interfaccia dello stack host](./media/user-guide/usbx-events/image206.png)    | <span data-ttu-id="5cc78-520">**Creazione istanza interfaccia stack host** *(ux_host_stack_interface_instance_create)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-520">**Host Stack Interface Instance Create** *(ux_host_stack_interface_instance_create)*</span></span> |
| ![Icona di eliminazione istanza interfaccia stack host](./media/user-guide/usbx-events/image207.png)    | <span data-ttu-id="5cc78-522">**Eliminazione istanza interfaccia stack host** *(ux_host_stack_interface_instance_delete)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-522">**Host Stack Interface Instance Delete** *(ux_host_stack_interface_instance_delete)*</span></span> |
| ![Icona del set di interfacce dello stack host](./media/user-guide/usbx-events/image208.png)    | <span data-ttu-id="5cc78-524">**Set di interfacce dello stack host** *(ux_host_stack_interface_set)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-524">**Host Stack Interface Set** *(ux_host_stack_interface_set)*</span></span> |
| ![Icona di selezione dell'impostazione dell'interfaccia dello stack host](./media/user-guide/usbx-events/image209.png)    | <span data-ttu-id="5cc78-526">**Impostazione dell'interfaccia dello stack host Select** *(ux_host_stack_interface_setting_select)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-526">**Host Stack Interface Setting Select** *(ux_host_stack_interface_setting_select)*</span></span> |
| ![Icona di creazione nuova configurazione dello stack host](./media/user-guide/usbx-events/image210.png)    | <span data-ttu-id="5cc78-528">**Creazione dello stack host nuova configurazione** *(ux_host_stack_new_configuration_create)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-528">**Host Stack New Configuration Create** *(ux_host_stack_new_configuration_create)*</span></span> |
| ![Icona di creazione nuovo dispositivo dello stack host](./media/user-guide/usbx-events/image211.png)    | <span data-ttu-id="5cc78-530">**Stack host nuovo dispositivo creato** *(ux_host_stack_new_device_create)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-530">**Host Stack New Device Create** *(ux_host_stack_new_device_create)*</span></span> |
| ![Icona di creazione nuovo endpoint dello stack host](./media/user-guide/usbx-events/image212.png)    | <span data-ttu-id="5cc78-532">**Creazione di un nuovo endpoint dello stack host** *(ux_host_stack_new_endpoint_create)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-532">**Host Stack New Endpoint Create** *(ux_host_stack_new_endpoint_create)*</span></span> |
| ![Icona del processo di modifica dell'hub radice dello stack host](./media/user-guide/usbx-events/image213.png)    | <span data-ttu-id="5cc78-534">**Processo di modifica dell'hub radice dello stack host** *(ux_host_stack_rh_change_process)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-534">**Host Stack Root Hub Change Process** *(ux_host_stack_rh_change_process)*</span></span> |
| ![Icona di estrazione dispositivo hub radice dello stack host](./media/user-guide/usbx-events/image214.png)    | <span data-ttu-id="5cc78-536">**Estrazione dispositivo hub radice stack host** *(ux_host_stack_rh_device_extraction)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-536">**Host Stack Root Hub Device Extraction** *(ux_host_stack_rh_device_extraction)*</span></span> |
| ![Icona di inserimento dispositivo hub radice stack host](./media/user-guide/usbx-events/image215.png)    | <span data-ttu-id="5cc78-538">**Inserimento dispositivo hub radice stack host** *(ux_host_stack_rh_device_insertion)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-538">**Host Stack Root Hub Device Insertion** *(ux_host_stack_rh_device_insertion)*</span></span> |
| ![Icona della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image216.png)    | <span data-ttu-id="5cc78-540">**Richiesta di trasferimento dello stack host** *(ux_host_stack_transfer_request)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-540">**Host Stack Transfer Request** *(ux_host_stack_transfer_request)*</span></span> |
| ![Icona di interruzione della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image217.png)    | <span data-ttu-id="5cc78-542">**Interruzione richiesta trasferimento stack host** *(ux_host_stack_transfer_request_abort)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-542">**Host Stack Transfer Request Abort** *(ux_host_stack_transfer_request_abort)*</span></span> |
| ![Icona di errore U S B X](./media/user-guide/usbx-events/image218.png)    | <span data-ttu-id="5cc78-544">**Errore USBX** *(ux_error)*</span><span class="sxs-lookup"><span data-stu-id="5cc78-544">**USBX Error** *(ux_error)*</span></span> |

## <a name="event-descriptions"></a><span data-ttu-id="5cc78-545">Descrizioni di eventi</span><span class="sxs-lookup"><span data-stu-id="5cc78-545">Event Descriptions</span></span>

<span data-ttu-id="5cc78-546">Nelle pagine seguenti vengono descritti gli eventi di traccia USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-546">The following pages describe the USBX Trace Events.</span></span>

### <a name="device-class-cdc-activate"></a><span data-ttu-id="5cc78-547">Classe del dispositivo CDC Activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-547">Device Class Cdc Activate</span></span> 

#### <a name="ux_device_class_cdc_activate"></a><span data-ttu-id="5cc78-548">ux_device_class_cdc_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-548">ux_device_class_cdc_activate</span></span>

<span data-ttu-id="5cc78-549">**Icona** ![ di Icona di attivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-549">**Icon** ![Device Class C D C Activate icon](./media/user-guide/usbx-events/image1.png)</span></span>

<span data-ttu-id="5cc78-550">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-550">**Description**</span></span>

<span data-ttu-id="5cc78-551">Questo evento rappresenta un evento di attivazione CDC di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-551">This event represents a USBX Device Class Cdc Activate Event.</span></span>

<span data-ttu-id="5cc78-552">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-552">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-553">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-553">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-554">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-554">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-555">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-555">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-556">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-556">Info Field 4: Not used.</span></span>

### <a name="device-class-cdc-deactivate"></a><span data-ttu-id="5cc78-557">Classe dispositivo CDC Deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-557">Device Class Cdc Deactivate</span></span> 

#### <a name="ux_device_class_cdc_deactivate"></a><span data-ttu-id="5cc78-558">ux_device_class_cdc_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-558">ux_device_class_cdc_deactivate</span></span>

<span data-ttu-id="5cc78-559">**Icona** ![ di Icona di disattivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-559">**Icon** ![Device Class C D C Deactivate icon](./media/user-guide/usbx-events/image2.png)</span></span>

<span data-ttu-id="5cc78-560">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-560">**Description**</span></span>

<span data-ttu-id="5cc78-561">Questo evento rappresenta una classe di dispositivo USBX CDC Deactivate.</span><span class="sxs-lookup"><span data-stu-id="5cc78-561">This event represents a USBX Device Class Cdc Deactivate.</span></span>

<span data-ttu-id="5cc78-562">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="5cc78-562">Information Fields</span></span> 

- <span data-ttu-id="5cc78-563">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-563">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-564">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-564">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-565">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-565">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-566">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-566">Info Field 4: Not used.</span></span>

### <a name="device-class-cdc-read"></a><span data-ttu-id="5cc78-567">Classe dispositivo CDC Read</span><span class="sxs-lookup"><span data-stu-id="5cc78-567">Device Class Cdc Read</span></span> 

#### <a name="ux_device_class_cdc_read"></a><span data-ttu-id="5cc78-568">ux_device_class_cdc_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-568">ux_device_class_cdc_read</span></span>

<span data-ttu-id="5cc78-569">**Icona** ![ di Icona di lettura della classe del dispositivo c D](./media/user-guide/usbx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-569">**Icon** ![Device Class C D C Read icon](./media/user-guide/usbx-events/image3.png)</span></span>

<span data-ttu-id="5cc78-570">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-570">**Description**</span></span>

<span data-ttu-id="5cc78-571">Questo evento rappresenta una classe di dispositivo USBX evento CDC Read.</span><span class="sxs-lookup"><span data-stu-id="5cc78-571">This event represents a USBX Device Class Cdc Read Event.</span></span>

<span data-ttu-id="5cc78-572">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-572">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-573">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-573">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-574">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-574">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-575">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-575">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-576">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-576">Info Field 4: Not used.</span></span>

### <a name="device-class-cdc-write"></a><span data-ttu-id="5cc78-577">Classe dispositivo-scrittura CDC</span><span class="sxs-lookup"><span data-stu-id="5cc78-577">Device Class Cdc Write</span></span> 

#### <a name="ux_device_class_cdc_write"></a><span data-ttu-id="5cc78-578">ux_device_class_cdc_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-578">ux_device_class_cdc_write</span></span>

<span data-ttu-id="5cc78-579">**Icona** ![ di Icona di scrittura della classe del dispositivo c D C](./media/user-guide/usbx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-579">**Icon** ![Device Class C D C Write icon](./media/user-guide/usbx-events/image4.png)</span></span>

<span data-ttu-id="5cc78-580">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-580">**Description**</span></span>

<span data-ttu-id="5cc78-581">Questo evento rappresenta un evento di scrittura CDC della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-581">This event represents a USBX Device Class Cdc Write Event.</span></span>

<span data-ttu-id="5cc78-582">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-582">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-583">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-583">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-584">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-584">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-585">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-585">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-586">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-586">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-activate"></a><span data-ttu-id="5cc78-587">Classe dispositivo DPUMP attiva</span><span class="sxs-lookup"><span data-stu-id="5cc78-587">Device Class Dpump Activate</span></span> 

#### <a name="ux_device_class_dpump_activate"></a><span data-ttu-id="5cc78-588">ux_device_class_dpump_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-588">ux_device_class_dpump_activate</span></span>

<span data-ttu-id="5cc78-589">**Icona** ![ di Icona di attivazione della classe Device DPUMP](./media/user-guide/usbx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-589">**Icon** ![Device Class Dpump Activate icon](./media/user-guide/usbx-events/image5.png)</span></span>

<span data-ttu-id="5cc78-590">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-590">**Description**</span></span>

<span data-ttu-id="5cc78-591">Questo evento rappresenta un evento di attivazione DPUMP di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-591">This event represents a USBX Device Class Dpump Activate Event.</span></span>

<span data-ttu-id="5cc78-592">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-592">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-593">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-593">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-594">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-594">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-595">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-595">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-596">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-596">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-deactivate"></a><span data-ttu-id="5cc78-597">DPUMP classe dispositivo disattiva</span><span class="sxs-lookup"><span data-stu-id="5cc78-597">Device Class Dpump Deactivate</span></span> 

#### <a name="ux_device_class_dpump_deactivate"></a><span data-ttu-id="5cc78-598">ux_device_class_dpump_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-598">ux_device_class_dpump_deactivate</span></span>

<span data-ttu-id="5cc78-599">**Icona** ![ di Icona di disattivazione della classe Device DPUMP](./media/user-guide/usbx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-599">**Icon** ![Device Class Dpump Deactivate icon](./media/user-guide/usbx-events/image6.png)</span></span>

<span data-ttu-id="5cc78-600">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-600">**Description**</span></span>

<span data-ttu-id="5cc78-601">Questo evento rappresenta una classe di dispositivo USBX DPUMP disattivare un evento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-601">This event represents a USBX Device Class Dpump Deactivate Event.</span></span>

<span data-ttu-id="5cc78-602">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-602">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-603">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-603">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-604">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-604">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-605">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-605">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-606">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-606">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-read"></a><span data-ttu-id="5cc78-607">Classe dispositivo DPUMP Read</span><span class="sxs-lookup"><span data-stu-id="5cc78-607">Device Class Dpump Read</span></span> 

#### <a name="ux_device_class_dpump_read"></a><span data-ttu-id="5cc78-608">ux_device_class_dpump_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-608">ux_device_class_dpump_read</span></span>

<span data-ttu-id="5cc78-609">**Icona** ![ di Icona di lettura della classe del dispositivo DPUMP](./media/user-guide/usbx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-609">**Icon** ![Device Class Dpump Read icon](./media/user-guide/usbx-events/image7.png)</span></span>

<span data-ttu-id="5cc78-610">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-610">**Description**</span></span>

<span data-ttu-id="5cc78-611">Questo evento rappresenta un evento di lettura DPUMP di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-611">This event represents a USBX Device Class Dpump Read Event.</span></span>

<span data-ttu-id="5cc78-612">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-612">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-613">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-613">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-614">Informazioni sul campo 2: buffer.</span><span class="sxs-lookup"><span data-stu-id="5cc78-614">Info Field 2: Buffer.</span></span>
- <span data-ttu-id="5cc78-615">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-615">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-616">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-616">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-write"></a><span data-ttu-id="5cc78-617">Classe dispositivo scrittura DPUMP</span><span class="sxs-lookup"><span data-stu-id="5cc78-617">Device Class Dpump Write</span></span> 

#### <a name="ux_device_class_dpump_write"></a><span data-ttu-id="5cc78-618">ux_device_class_dpump_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-618">ux_device_class_dpump_write</span></span>

<span data-ttu-id="5cc78-619">**Icona** ![ di Icona di scrittura della classe Device DPUMP](./media/user-guide/usbx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-619">**Icon** ![Device Class Dpump Write icon](./media/user-guide/usbx-events/image8.png)</span></span>

<span data-ttu-id="5cc78-620">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-620">**Description**</span></span>

<span data-ttu-id="5cc78-621">Questo evento rappresenta un evento di scrittura DPUMP della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-621">This event represents a USBX Device Class Dpump Write Event.</span></span>

<span data-ttu-id="5cc78-622">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-622">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-623">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-623">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-624">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-624">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-625">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-625">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-626">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-626">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-activate"></a><span data-ttu-id="5cc78-627">Attivazione HID Classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-627">Device Class Hid Activate</span></span> 

#### <a name="ux_device_class_hid_activate"></a><span data-ttu-id="5cc78-628">ux_device_class_hid_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-628">ux_device_class_hid_activate</span></span>

<span data-ttu-id="5cc78-629">**Icona** ![ di Icona di attivazione HID della classe dispositivo](./media/user-guide/usbx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-629">**Icon** ![Device Class Hid Activate icon](./media/user-guide/usbx-events/image9.png)</span></span>

<span data-ttu-id="5cc78-630">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-630">**Description**</span></span>

<span data-ttu-id="5cc78-631">Questo evento rappresenta un evento di attivazione HID della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-631">This event represents a USBX Device Class Hid Activate Event.</span></span>

<span data-ttu-id="5cc78-632">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-632">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-633">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-633">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-634">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-634">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-635">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-635">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-636">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-636">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-deactivate"></a><span data-ttu-id="5cc78-637">Classe dispositivo HID disattiva</span><span class="sxs-lookup"><span data-stu-id="5cc78-637">Device Class Hid Deactivate</span></span> 

#### <a name="ux_device_class_hid_deactivate"></a><span data-ttu-id="5cc78-638">ux_device_class_hid_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-638">ux_device_class_hid_deactivate</span></span>

<span data-ttu-id="5cc78-639">**Icona** ![ di Icona di disattivazione HID della classe dispositivo](./media/user-guide/usbx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-639">**Icon** ![Device Class Hid Deactivate icon](./media/user-guide/usbx-events/image10.png)</span></span>

<span data-ttu-id="5cc78-640">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-640">**Description**</span></span>

<span data-ttu-id="5cc78-641">Questo evento rappresenta un evento di disattivazione HID della classe di dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-641">This event represents a USBX Device Class Hid Deactivate Event.</span></span>

<span data-ttu-id="5cc78-642">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-642">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-643">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-643">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-644">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-644">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-645">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-645">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-646">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-646">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-descriptor-send"></a><span data-ttu-id="5cc78-647">Trasmissione del descrittore HID della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-647">Device Class Hid Descriptor Send</span></span> 

#### <a name="ux_device_class_hid_descritpor_send"></a><span data-ttu-id="5cc78-648">ux_device_class_hid_descritpor_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-648">ux_device_class_hid_descritpor_send</span></span>

<span data-ttu-id="5cc78-649">**Icona** ![ di Icona di invio del descrittore HID della classe dispositivo](./media/user-guide/usbx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-649">**Icon** ![Device Class Hid Descriptor Send icon](./media/user-guide/usbx-events/image11.png)</span></span>

<span data-ttu-id="5cc78-650">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-650">**Description**</span></span>

<span data-ttu-id="5cc78-651">Questo evento rappresenta un evento di invio del descrittore HID della classe di dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-651">This event represents a USBX Device Class Hid Descriptor Send Event.</span></span>

<span data-ttu-id="5cc78-652">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-652">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-653">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-653">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-654">Informazioni sul campo 2: tipo di descrittore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-654">Info Field 2: Descriptor type.</span></span>
- <span data-ttu-id="5cc78-655">Informazioni sul campo 3: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-655">Info Field 3: Request index.</span></span>
- <span data-ttu-id="5cc78-656">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-656">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-event-get"></a><span data-ttu-id="5cc78-657">Classe dispositivo (Get) evento HID</span><span class="sxs-lookup"><span data-stu-id="5cc78-657">Device Class Hid Event Get</span></span> 

#### <a name="ux_device_class_hid_event_get"></a><span data-ttu-id="5cc78-658">ux_device_class_hid_event_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-658">ux_device_class_hid_event_get</span></span>

<span data-ttu-id="5cc78-659">**Icona** ![ di Icona di Get dell'evento HID della classe dispositivo](./media/user-guide/usbx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-659">**Icon** ![Device Class Hid Event Get icon](./media/user-guide/usbx-events/image12.png)</span></span>

<span data-ttu-id="5cc78-660">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-660">**Description**</span></span>

<span data-ttu-id="5cc78-661">Questo evento rappresenta un evento di Get evento HID della classe di dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-661">This event represents a USBX Device Class Hid Event Get Event.</span></span>

<span data-ttu-id="5cc78-662">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-662">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-663">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-663">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-664">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-664">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-665">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-665">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-666">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-666">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-event-set"></a><span data-ttu-id="5cc78-667">Set di eventi HID della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-667">Device Class Hid Event Set</span></span> 

#### <a name="ux_device_class_hid_event_set"></a><span data-ttu-id="5cc78-668">ux_device_class_hid_event_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-668">ux_device_class_hid_event_set</span></span>

<span data-ttu-id="5cc78-669">**Icona** ![ di Icona del set di eventi HID della classe dispositivo](./media/user-guide/usbx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-669">**Icon** ![Device Class Hid Event Set icon](./media/user-guide/usbx-events/image13.png)</span></span>

<span data-ttu-id="5cc78-670">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-670">**Description**</span></span>

<span data-ttu-id="5cc78-671">Questo evento rappresenta un set di eventi HID della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-671">This event represents a USBX Device Class Hid Event Set.</span></span>

<span data-ttu-id="5cc78-672">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-672">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-673">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-673">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-674">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-674">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-675">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-675">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-676">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-676">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-report-get"></a><span data-ttu-id="5cc78-677">Classe dispositivo-report HID</span><span class="sxs-lookup"><span data-stu-id="5cc78-677">Device Class Hid Report Get</span></span> 

#### <a name="ux_device_class_hid_report_get"></a><span data-ttu-id="5cc78-678">ux_device_class_hid_report_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-678">ux_device_class_hid_report_get</span></span>

<span data-ttu-id="5cc78-679">**Icona** ![ di Icona di Get del report HID della classe dispositivo](./media/user-guide/usbx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-679">**Icon** ![Device Class Hid Report Get icon](./media/user-guide/usbx-events/image14.png)</span></span>

<span data-ttu-id="5cc78-680">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-680">**Description**</span></span>

<span data-ttu-id="5cc78-681">Questo evento rappresenta un evento di Get del report HID della classe di dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-681">This event represents a USBX Device Class Hid Report Get Event.</span></span>

<span data-ttu-id="5cc78-682">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-682">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-683">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-683">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-684">Informazioni sul campo 2: tipo di descrittore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-684">Info Field 2: Descriptor type.</span></span>
- <span data-ttu-id="5cc78-685">Informazioni sul campo 3: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-685">Info Field 3: Request index.</span></span>
- <span data-ttu-id="5cc78-686">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-686">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-report-set"></a><span data-ttu-id="5cc78-687">Set di report HID della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-687">Device Class Hid Report Set</span></span> 

#### <a name="ux_device_class_hid_report_set"></a><span data-ttu-id="5cc78-688">ux_device_class_hid_report_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-688">ux_device_class_hid_report_set</span></span>

<span data-ttu-id="5cc78-689">**Icona** ![ di Icona del set di report HID della classe dispositivo](./media/user-guide/usbx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-689">**Icon** ![Device Class Hid Report Set icon](./media/user-guide/usbx-events/image15.png)</span></span>

<span data-ttu-id="5cc78-690">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-690">**Description**</span></span>

<span data-ttu-id="5cc78-691">Questo evento rappresenta un evento del set di report HID della classe di dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-691">This event represents a USBX Device Class Hid Report Set Event.</span></span>

<span data-ttu-id="5cc78-692">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-692">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-693">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-693">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-694">Informazioni sul campo 2: tipo di descrittore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-694">Info Field 2: Descriptor type.</span></span>
- <span data-ttu-id="5cc78-695">Informazioni sul campo 3: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-695">Info Field 3: Request index.</span></span>
- <span data-ttu-id="5cc78-696">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-696">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-activate"></a><span data-ttu-id="5cc78-697">Classe dispositivo Pima Activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-697">Device Class Pima Activate</span></span>

#### <a name="ux_device_class_pima_activate"></a><span data-ttu-id="5cc78-698">ux_device_class_pima_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-698">ux_device_class_pima_activate</span></span>

<span data-ttu-id="5cc78-699">**Icona** ![ di Icona di attivazione Pima della classe dispositivo](./media/user-guide/usbx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-699">**Icon** ![Device Class Pima Activate icon](./media/user-guide/usbx-events/image16.png)</span></span>

<span data-ttu-id="5cc78-700">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-700">**Description**</span></span>

<span data-ttu-id="5cc78-701">Questo evento rappresenta un evento di attivazione Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-701">This event represents a USBX Device Class Pima Activate Event.</span></span>

<span data-ttu-id="5cc78-702">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-702">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-703">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-703">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-704">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-704">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-705">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-705">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-706">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-706">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-deactivate"></a><span data-ttu-id="5cc78-707">Classe dispositivo Pima disattivare</span><span class="sxs-lookup"><span data-stu-id="5cc78-707">Device Class Pima Deactivate</span></span> 

#### <a name="ux_device_class_pima_deactivate"></a><span data-ttu-id="5cc78-708">ux_device_class_pima_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-708">ux_device_class_pima_deactivate</span></span>

<span data-ttu-id="5cc78-709">**Icona** ![ di Icona di disattivazione della classe di dispositivo Pima](./media/user-guide/usbx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-709">**Icon** ![Device Class Pima Deactivate icon](./media/user-guide/usbx-events/image17.png)</span></span>

<span data-ttu-id="5cc78-710">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-710">**Description**</span></span>

<span data-ttu-id="5cc78-711">Questo evento rappresenta un evento di disattivazione Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-711">This event represents a USBX Device Class Pima Deactivate Event.</span></span>

<span data-ttu-id="5cc78-712">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-712">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-713">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-713">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-714">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-714">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-715">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-715">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-716">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-716">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-device-info-send"></a><span data-ttu-id="5cc78-717">Classe dispositivo-invio informazioni sul dispositivo Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-717">Device Class Pima Device Info Send</span></span> 

#### <a name="ux_device_class_pima_device_info_send"></a><span data-ttu-id="5cc78-718">ux_device_class_pima_device_info_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-718">ux_device_class_pima_device_info_send</span></span>

<span data-ttu-id="5cc78-719">**Icona** ![ di Icona di invio informazioni sul dispositivo Pima della classe dispositivo](./media/user-guide/usbx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-719">**Icon** ![Device Class Pima Device Info Send icon](./media/user-guide/usbx-events/image18.png)</span></span>

<span data-ttu-id="5cc78-720">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-720">**Description**</span></span>

<span data-ttu-id="5cc78-721">Questo evento rappresenta un evento di invio informazioni sul dispositivo USBX di classe dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-721">This event represents a USBX Device Class Pima Device Info Send Event.</span></span>

<span data-ttu-id="5cc78-722">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-722">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-723">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-723">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-724">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-724">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-725">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-725">Info Field 3: Not used.</span></span>

### <a name="device-class-pima-event-get"></a><span data-ttu-id="5cc78-726">Classe dispositivo Pima evento Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-726">Device Class Pima Event Get</span></span> 

#### <a name="ux_device_class_pima_event_get"></a><span data-ttu-id="5cc78-727">ux_device_class_pima_event_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-727">ux_device_class_pima_event_get</span></span>

<span data-ttu-id="5cc78-728">**Icona** ![ di Icona di Get evento di classe dispositivo Pima](./media/user-guide/usbx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-728">**Icon** ![Device Class Pima Event Get icon](./media/user-guide/usbx-events/image19.png)</span></span>

<span data-ttu-id="5cc78-729">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-729">**Description**</span></span>

<span data-ttu-id="5cc78-730">Questo evento rappresenta un evento di Get evento Pima di classe Device USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-730">This event represents a USBX Device Class Pima Event Get Event.</span></span>

<span data-ttu-id="5cc78-731">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-731">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-732">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-732">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-733">Campo Info 2: evento Pima.</span><span class="sxs-lookup"><span data-stu-id="5cc78-733">Info Field 2: Pima event.</span></span>
- <span data-ttu-id="5cc78-734">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-734">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-735">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-735">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-event-set"></a><span data-ttu-id="5cc78-736">Set di eventi Pima della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-736">Device Class Pima Event Set</span></span> 

#### <a name="ux_device_class_pima_event_set"></a><span data-ttu-id="5cc78-737">ux_device_class_pima_event_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-737">ux_device_class_pima_event_set</span></span>

<span data-ttu-id="5cc78-738">**Icona** ![ di Icona del set di eventi Pima della classe Device](./media/user-guide/usbx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-738">**Icon** ![Device Class Pima Event Set icon](./media/user-guide/usbx-events/image20.png)</span></span>

<span data-ttu-id="5cc78-739">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-739">**Description**</span></span>

<span data-ttu-id="5cc78-740">Questo evento rappresenta un evento del set di eventi Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-740">This event represents a USBX Device Class Pima Event Set Event.</span></span>

<span data-ttu-id="5cc78-741">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-741">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-742">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-742">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-743">Campo Info 2: evento Pima.</span><span class="sxs-lookup"><span data-stu-id="5cc78-743">Info Field 2: Pima event.</span></span>
- <span data-ttu-id="5cc78-744">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-744">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-745">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-745">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-add"></a><span data-ttu-id="5cc78-746">Classe dispositivo-aggiunta di oggetti Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-746">Device Class Pima Object Add</span></span> 

#### <a name="ux_device_class_pima_object_add"></a><span data-ttu-id="5cc78-747">ux_device_class_pima_object_add</span><span class="sxs-lookup"><span data-stu-id="5cc78-747">ux_device_class_pima_object_add</span></span>

<span data-ttu-id="5cc78-748">**Icona** ![ di Icona di aggiunta oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-748">**Icon** ![Device Class Pima Object Add icon](./media/user-guide/usbx-events/image21.png)</span></span>

<span data-ttu-id="5cc78-749">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-749">**Description**</span></span>

<span data-ttu-id="5cc78-750">Questo evento rappresenta un evento di aggiunta di un oggetto Pima di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-750">This event represents a USBX Device Class Pima Object Add Event.</span></span>

<span data-ttu-id="5cc78-751">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-751">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-752">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-752">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-753">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-753">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-754">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-754">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-755">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-755">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-data-get"></a><span data-ttu-id="5cc78-756">Classe dispositivo Pima dati oggetto Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-756">Device Class Pima Object Data Get</span></span> 

#### <a name="ux_device_class_pima_object_data_get"></a><span data-ttu-id="5cc78-757">ux_device_class_pima_object_data_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-757">ux_device_class_pima_object_data_get</span></span>

<span data-ttu-id="5cc78-758">**Icona** ![ di Icona di visualizzazione dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-758">**Icon** ![Device Class Pima Object Data Get icon](./media/user-guide/usbx-events/image22.png)</span></span>

<span data-ttu-id="5cc78-759">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-759">**Description**</span></span>

<span data-ttu-id="5cc78-760">Questo evento rappresenta un evento di Get di dati dell'oggetto Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-760">This event represents a USBX Device Class Pima Object Data Get Event.</span></span>

<span data-ttu-id="5cc78-761">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-761">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-762">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-762">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-763">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-763">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-764">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-764">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-765">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-765">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-data-send"></a><span data-ttu-id="5cc78-766">Trasmissione dati oggetto Pima classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-766">Device Class Pima Object Data Send</span></span> 

#### <a name="ux_device_class_pima_object_data_send"></a><span data-ttu-id="5cc78-767">ux_device_class_pima_object_data_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-767">ux_device_class_pima_object_data_send</span></span>

<span data-ttu-id="5cc78-768">**Icona** ![ di Icona di invio dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-768">**Icon** ![Device Class Pima Object Data Send icon](./media/user-guide/usbx-events/image23.png)</span></span>

<span data-ttu-id="5cc78-769">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-769">**Description**</span></span>

<span data-ttu-id="5cc78-770">Questo evento rappresenta un evento di trasmissione dati oggetto Pima classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-770">This event represents a USBX Device Class Pima Object Data Send Event.</span></span>

<span data-ttu-id="5cc78-771">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-771">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-772">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-772">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-773">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-773">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-774">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-774">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-775">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-775">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-delete"></a><span data-ttu-id="5cc78-776">Classe dispositivo-Elimina oggetto Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-776">Device Class Pima Object Delete</span></span> 

#### <a name="ux_device_class_pima_object_delete"></a><span data-ttu-id="5cc78-777">ux_device_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-777">ux_device_class_pima_object_delete</span></span>

<span data-ttu-id="5cc78-778">**Icona** ![ di Icona di eliminazione oggetti Pima classe dispositivo](./media/user-guide/usbx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-778">**Icon** ![Device Class Pima Object Delete icon](./media/user-guide/usbx-events/image24.png)</span></span>

<span data-ttu-id="5cc78-779">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-779">**Description**</span></span>

<span data-ttu-id="5cc78-780">Questo evento rappresenta un evento di eliminazione di oggetti Pima di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-780">This event represents a USBX Device Class Pima Object Delete Event.</span></span>

<span data-ttu-id="5cc78-781">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-781">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-782">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-782">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-783">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-783">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-784">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-784">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-785">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-785">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-handles-send"></a><span data-ttu-id="5cc78-786">Classe dispositivo gestisce l'invio di oggetti Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-786">Device Class Pima Object Handles Send</span></span> 

#### <a name="ux_device_class_pima_object_handles_send"></a><span data-ttu-id="5cc78-787">ux_device_class_pima_object_handles_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-787">ux_device_class_pima_object_handles_send</span></span>

<span data-ttu-id="5cc78-788">**Icona** ![ di Icona di invio handle oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-788">**Icon** ![Device Class Pima Object Handles Send icon](./media/user-guide/usbx-events/image25.png)</span></span>

<span data-ttu-id="5cc78-789">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-789">**Description**</span></span>

<span data-ttu-id="5cc78-790">Questo evento rappresenta una classe di dispositivi USBX che gestisce l'evento di invio.</span><span class="sxs-lookup"><span data-stu-id="5cc78-790">This event represents a USBX Device Class Pima Object Handles Send Event.</span></span>

<span data-ttu-id="5cc78-791">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-791">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-792">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-792">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-793">Informazioni sul campo 2: ID archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-793">Info Field 2: Storage ID.</span></span>
- <span data-ttu-id="5cc78-794">Informazioni sul campo 3: codice del formato dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-794">Info Field 3: Object format code.</span></span>
- <span data-ttu-id="5cc78-795">Campo informazioni 4: associazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="5cc78-795">Info Field 4: Object association.</span></span>

### <a name="device-class-pima-object-info-get"></a><span data-ttu-id="5cc78-796">Classe dispositivo. informazioni sull'oggetto Pima Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-796">Device Class Pima Object Info Get</span></span> 

#### <a name="ux_device_class_pima_object_info_send"></a><span data-ttu-id="5cc78-797">ux_device_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-797">ux_device_class_pima_object_info_send</span></span>

<span data-ttu-id="5cc78-798">**Icona** ![ di Icona di visualizzazione informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-798">**Icon** ![Device Class Pima Object Info Get icon](./media/user-guide/usbx-events/image26.png)</span></span>

<span data-ttu-id="5cc78-799">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-799">**Description**</span></span>

<span data-ttu-id="5cc78-800">Questo evento rappresenta un evento di informazioni di oggetto Pima per la classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-800">This event represents a USBX Device Class Pima Object Info Get Event.</span></span>

<span data-ttu-id="5cc78-801">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-801">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-802">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-802">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-803">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-803">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-804">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-804">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-805">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-805">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-info-send"></a><span data-ttu-id="5cc78-806">Classe dispositivo-invio informazioni oggetto Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-806">Device Class Pima Object Info Send</span></span> 

#### <a name="ux_device_class_pima_object_info_send"></a><span data-ttu-id="5cc78-807">ux_device_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-807">ux_device_class_pima_object_info_send</span></span>

<span data-ttu-id="5cc78-808">**Icona** ![ di Icona di invio informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-808">**Icon** ![Device Class Pima Object Info Send icon](./media/user-guide/usbx-events/image27.png)</span></span>

<span data-ttu-id="5cc78-809">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-809">**Description**</span></span>

<span data-ttu-id="5cc78-810">Questo evento rappresenta un evento di invio delle informazioni sull'oggetto Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-810">This event represents a USBX Device Class Pima Object Info Send Event.</span></span>

<span data-ttu-id="5cc78-811">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-811">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-812">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-812">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-813">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-813">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-814">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-814">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-815">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-815">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-objects-number-send"></a><span data-ttu-id="5cc78-816">Classe dispositivo numero oggetti Pima invio</span><span class="sxs-lookup"><span data-stu-id="5cc78-816">Device Class Pima Objects Number Send</span></span> 

#### <a name="ux_device_class_pima_object_number_send"></a><span data-ttu-id="5cc78-817">ux_device_class_pima_object_number_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-817">ux_device_class_pima_object_number_send</span></span>

<span data-ttu-id="5cc78-818">**Icona** ![ di Icona di invio numero di oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-818">**Icon** ![Device Class Pima Objects Number Send icon](./media/user-guide/usbx-events/image28.png)</span></span>

<span data-ttu-id="5cc78-819">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-819">**Description**</span></span>

<span data-ttu-id="5cc78-820">Questo evento rappresenta un evento di invio di un numero di oggetto Pima di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-820">This event represents a USBX Device Class Pima Object Number Send event.</span></span>

<span data-ttu-id="5cc78-821">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-821">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-822">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-822">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-823">Informazioni sul campo 2: ID archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-823">Info Field 2: Storage ID.</span></span>
- <span data-ttu-id="5cc78-824">Informazioni sul campo 3: codice del formato dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-824">Info Field 3: Object format code.</span></span>
- <span data-ttu-id="5cc78-825">Campo dati 4: oggetto associato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-825">Info Field 4: Object associate.</span></span>

### <a name="device-class-pima-partial-object-data-get"></a><span data-ttu-id="5cc78-826">Classe dispositivo i dati dell'oggetto parziale Pima Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-826">Device Class Pima Partial Object Data Get</span></span>

#### <a name="ux_device_class_pima_partial_object_data_get"></a><span data-ttu-id="5cc78-827">ux_device_class_pima_partial_object_data_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-827">ux_device_class_pima_partial_object_data_get</span></span>

<span data-ttu-id="5cc78-828">**Icona** ![ di Icona di visualizzazione dati oggetto parziale classe dispositivo Pima](./media/user-guide/usbx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-828">**Icon** ![Device Class Pima Partial Object Data Get icon](./media/user-guide/usbx-events/image29.png)</span></span>

<span data-ttu-id="5cc78-829">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-829">**Description**</span></span>

<span data-ttu-id="5cc78-830">Questo evento rappresenta un evento di Get parziale dei dati degli oggetti Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-830">This event represents a USBX Device Class Pima Partial Object Data Get Event.</span></span>

<span data-ttu-id="5cc78-831">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-831">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-832">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-832">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-833">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-833">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-834">Informazioni campo 3: offset richiesto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-834">Info Field 3: Offset requested.</span></span>
- <span data-ttu-id="5cc78-835">Informazioni campo 4: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-835">Info Field 4: Length requested.</span></span>

### <a name="device-class-pima-response-send"></a><span data-ttu-id="5cc78-836">Classe dispositivo-invio risposta Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-836">Device Class Pima Response Send</span></span> 

#### <a name="ux_device_class_pima_response_send"></a><span data-ttu-id="5cc78-837">ux_device_class_pima_response_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-837">ux_device_class_pima_response_send</span></span>

<span data-ttu-id="5cc78-838">**Icona** ![ di Icona di invio risposta Pima della classe dispositivo](./media/user-guide/usbx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-838">**Icon** ![Device Class Pima Response Send icon](./media/user-guide/usbx-events/image30.png)</span></span>

<span data-ttu-id="5cc78-839">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-839">**Description**</span></span>

<span data-ttu-id="5cc78-840">Questo evento rappresenta un evento di trasmissione della risposta Pima della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-840">This event represents a USBX Device Class Pima Response Send Event.</span></span>

<span data-ttu-id="5cc78-841">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-841">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-842">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-842">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-843">Informazioni sul campo 2: codice di risposta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-843">Info Field 2: Response code.</span></span>
- <span data-ttu-id="5cc78-844">Campo info 3: parametro number.</span><span class="sxs-lookup"><span data-stu-id="5cc78-844">Info Field 3: Number parameter.</span></span>
- <span data-ttu-id="5cc78-845">Informazioni sul campo 4: Pima parametro 1.</span><span class="sxs-lookup"><span data-stu-id="5cc78-845">Info Field 4: Pima parameter 1.</span></span>

### <a name="device-class-pima-storage-id-send"></a><span data-ttu-id="5cc78-846">Classe dispositivo-invio ID archiviazione Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-846">Device Class Pima Storage Id Send</span></span> 

#### <a name="ux_device_class_pima_storage_id_send"></a><span data-ttu-id="5cc78-847">ux_device_class_pima_storage_id_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-847">ux_device_class_pima_storage_id_send</span></span>

<span data-ttu-id="5cc78-848">**Icona** ![ di Icona di invio ID archiviazione Pima della classe dispositivo](./media/user-guide/usbx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-848">**Icon** ![Device Class Pima Storage Id Send icon](./media/user-guide/usbx-events/image31.png)</span></span>

<span data-ttu-id="5cc78-849">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-849">**Description**</span></span>

<span data-ttu-id="5cc78-850">Questo evento rappresenta un evento di invio dell'ID di archiviazione Pima di classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-850">This event represents a USBX Device Class Pima Storage Id Send Event.</span></span>

<span data-ttu-id="5cc78-851">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-851">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-852">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-852">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-853">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-853">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-854">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-854">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-855">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-855">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-storage-info-send"></a><span data-ttu-id="5cc78-856">Classe dispositivo-informazioni archiviazione Pima invio</span><span class="sxs-lookup"><span data-stu-id="5cc78-856">Device Class Pima Storage Info Send</span></span> 

#### <a name="ux_device_class_pima_storage_info_send"></a><span data-ttu-id="5cc78-857">ux_device_class_pima_storage_info_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-857">ux_device_class_pima_storage_info_send</span></span>

<span data-ttu-id="5cc78-858">**Icona** ![ di Icona di invio info di archiviazione Pima della classe dispositivo](./media/user-guide/usbx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-858">**Icon** ![Device Class Pima Storage Info Send icon](./media/user-guide/usbx-events/image32.png)</span></span>

<span data-ttu-id="5cc78-859">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-859">**Description**</span></span>

<span data-ttu-id="5cc78-860">Questo evento rappresenta un evento di invio di informazioni di archiviazione Pima di classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-860">This event represents a USBX Device Class Pima Storage Info Send Event.</span></span>

<span data-ttu-id="5cc78-861">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-861">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-862">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-862">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-863">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-863">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-864">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-864">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-865">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-865">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-activate"></a><span data-ttu-id="5cc78-866">Classe dispositivo RNDIS attiva</span><span class="sxs-lookup"><span data-stu-id="5cc78-866">Device Class Rndis Activate</span></span> 

#### <a name="ux_device_class_rndis_activate"></a><span data-ttu-id="5cc78-867">ux_device_class_rndis_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-867">ux_device_class_rndis_activate</span></span>

<span data-ttu-id="5cc78-868">**Icona** ![ di Icona di attivazione della classe Device RNDIS](./media/user-guide/usbx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-868">**Icon** ![Device Class Rndis Activate icon](./media/user-guide/usbx-events/image33.png)</span></span>

<span data-ttu-id="5cc78-869">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-869">**Description**</span></span>

<span data-ttu-id="5cc78-870">Questo evento rappresenta un evento di attivazione RNDIS di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-870">This event represents a USBX Device Class Rndis Activate Event.</span></span>

<span data-ttu-id="5cc78-871">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-871">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-872">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-872">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-873">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-873">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-874">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-874">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-875">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-875">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-deactivate"></a><span data-ttu-id="5cc78-876">RNDIS classe dispositivo disattiva</span><span class="sxs-lookup"><span data-stu-id="5cc78-876">Device Class Rndis Deactivate</span></span> 

#### <a name="ux_device_class_rndis_deactivate"></a><span data-ttu-id="5cc78-877">ux_device_class_rndis_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-877">ux_device_class_rndis_deactivate</span></span>

<span data-ttu-id="5cc78-878">**Icona** ![ di Icona di disattivazione della classe Device RNDIS](./media/user-guide/usbx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-878">**Icon** ![Device Class Rndis Deactivate icon](./media/user-guide/usbx-events/image34.png)</span></span>

<span data-ttu-id="5cc78-879">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-879">**Description**</span></span>

<span data-ttu-id="5cc78-880">Questo evento rappresenta una classe di dispositivo USBX RNDIS disattivare un evento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-880">This event represents a USBX Device Class Rndis Deactivate Event.</span></span>

<span data-ttu-id="5cc78-881">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-881">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-882">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-882">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-883">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-883">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-884">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-884">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-885">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-885">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-message-keep-alive"></a><span data-ttu-id="5cc78-886">Classe dispositivo RNDIS messaggio keep-alive</span><span class="sxs-lookup"><span data-stu-id="5cc78-886">Device Class Rndis Message Keep Alive</span></span> 

#### <a name="ux_device_class_rndis_msg_keep_alive"></a><span data-ttu-id="5cc78-887">ux_device_class_rndis_msg_keep_alive</span><span class="sxs-lookup"><span data-stu-id="5cc78-887">ux_device_class_rndis_msg_keep_alive</span></span>

<span data-ttu-id="5cc78-888">**Icona** ![ di Icona del messaggio keep alive di classe Device RNDIS](./media/user-guide/usbx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-888">**Icon** ![Device Class Rndis Message Keep Alive icon](./media/user-guide/usbx-events/image35.png)</span></span>

<span data-ttu-id="5cc78-889">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-889">**Description**</span></span>

<span data-ttu-id="5cc78-890">Questo evento rappresenta una classe di dispositivo USBX RNDIS messaggio keep alive.</span><span class="sxs-lookup"><span data-stu-id="5cc78-890">This event represents a USBX Device Class Rndis Message Keep Alive Event.</span></span>

<span data-ttu-id="5cc78-891">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-891">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-892">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-892">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-893">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-893">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-894">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-894">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-895">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-895">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-message-query"></a><span data-ttu-id="5cc78-896">Query del messaggio RNDIS della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-896">Device Class Rndis Message Query</span></span> 

#### <a name="ux_device_class_rndis_msg_keep_query"></a><span data-ttu-id="5cc78-897">ux_device_class_rndis_msg_keep_query</span><span class="sxs-lookup"><span data-stu-id="5cc78-897">ux_device_class_rndis_msg_keep_query</span></span>

<span data-ttu-id="5cc78-898">**Icona** ![ di Icona della query del messaggio RNDIS della classe dispositivo](./media/user-guide/usbx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-898">**Icon** ![Device Class Rndis Message Query icon](./media/user-guide/usbx-events/image36.png)</span></span>

<span data-ttu-id="5cc78-899">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-899">**Description**</span></span>

<span data-ttu-id="5cc78-900">Questo evento rappresenta un evento di query del messaggio RNDIS del messaggio USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-900">This event represents a USBX Device Class Rndis Message Query Event.</span></span>

<span data-ttu-id="5cc78-901">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-901">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-902">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-902">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-903">Informazioni sul campo 2: RNDIS OID.</span><span class="sxs-lookup"><span data-stu-id="5cc78-903">Info Field 2: Rndis OID.</span></span>
- <span data-ttu-id="5cc78-904">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-904">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-905">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-905">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-message-reset"></a><span data-ttu-id="5cc78-906">Classe dispositivo reimpostazione del messaggio RNDIS</span><span class="sxs-lookup"><span data-stu-id="5cc78-906">Device Class Rndis Message Reset</span></span> 

#### <a name="ux_device_class_rndis_msg_reset"></a><span data-ttu-id="5cc78-907">ux_device_class_rndis_msg_reset</span><span class="sxs-lookup"><span data-stu-id="5cc78-907">ux_device_class_rndis_msg_reset</span></span>

<span data-ttu-id="5cc78-908">**Icona** ![ di Icona di reimpostazione del messaggio RNDIS della classe dispositivo](./media/user-guide/usbx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-908">**Icon** ![Device Class Rndis Message Reset icon](./media/user-guide/usbx-events/image37.png)</span></span>

<span data-ttu-id="5cc78-909">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-909">**Description**</span></span>

<span data-ttu-id="5cc78-910">Questo evento rappresenta un evento di reimpostazione del messaggio RNDIS per la classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-910">This event represents a USBX Device Class Rndis Message Reset Event.</span></span>

<span data-ttu-id="5cc78-911">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-911">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-912">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-912">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-913">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-913">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-914">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-914">Info Field 3: Not used.</span></span>

### <a name="device-class-rndis-message-set"></a><span data-ttu-id="5cc78-915">Set di messaggi RNDIS della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-915">Device Class Rndis Message Set</span></span> 

#### <a name="ux_device_class_rndis_msg_set"></a><span data-ttu-id="5cc78-916">ux_device_class_rndis_msg_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-916">ux_device_class_rndis_msg_set</span></span>

<span data-ttu-id="5cc78-917">**Icona** ![ di Icona del set di messaggi RNDIS della classe dispositivo](./media/user-guide/usbx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-917">**Icon** ![Device Class Rndis Message Set icon](./media/user-guide/usbx-events/image38.png)</span></span>

<span data-ttu-id="5cc78-918">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-918">**Description**</span></span>

<span data-ttu-id="5cc78-919">Questo evento rappresenta un evento del set di messaggi RNDIS della classe di dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-919">This event represents a USBX Device Class Rndis Message Set Event.</span></span>

<span data-ttu-id="5cc78-920">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-920">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-921">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-921">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-922">Informazioni sul campo 2: RNDIS OID.</span><span class="sxs-lookup"><span data-stu-id="5cc78-922">Info Field 2: Rndis OID.</span></span>
- <span data-ttu-id="5cc78-923">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-923">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-924">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-924">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-packet-receive"></a><span data-ttu-id="5cc78-925">Classe dispositivo RNDIS ricezione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5cc78-925">Device Class Rndis Packet Receive</span></span> 

#### <a name="ux_device_class_rndis_packet_receive"></a><span data-ttu-id="5cc78-926">ux_device_class_rndis_packet_receive</span><span class="sxs-lookup"><span data-stu-id="5cc78-926">ux_device_class_rndis_packet_receive</span></span>

<span data-ttu-id="5cc78-927">**Icona** ![ di Icona di ricezione del pacchetto della classe Device RNDIS](./media/user-guide/usbx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-927">**Icon** ![Device Class Rndis Packet Receive icon](./media/user-guide/usbx-events/image39.png)</span></span>

<span data-ttu-id="5cc78-928">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-928">**Description**</span></span>

<span data-ttu-id="5cc78-929">Questo evento rappresenta un evento di ricezione del pacchetto RNDIS di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-929">This event represents a USBX Device Class Rndis Packet Receive Event.</span></span>

<span data-ttu-id="5cc78-930">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-930">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-931">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-931">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-932">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-932">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-933">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-933">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-934">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-934">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-packet-transmit"></a><span data-ttu-id="5cc78-935">Classe dispositivo trasmissione pacchetti RNDIS</span><span class="sxs-lookup"><span data-stu-id="5cc78-935">Device Class Rndis Packet Transmit</span></span> 

#### <a name="ux_device_class_rndis_packet_transmit"></a><span data-ttu-id="5cc78-936">ux_device_class_rndis_packet_transmit</span><span class="sxs-lookup"><span data-stu-id="5cc78-936">ux_device_class_rndis_packet_transmit</span></span>

<span data-ttu-id="5cc78-937">**Icona** ![ di Icona di trasmissione dei pacchetti della classe Device RNDIS](./media/user-guide/usbx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-937">**Icon** ![Device Class Rndis Packet Transmit icon](./media/user-guide/usbx-events/image40.png)</span></span>

<span data-ttu-id="5cc78-938">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-938">**Description**</span></span>

<span data-ttu-id="5cc78-939">Questo evento rappresenta un evento di trasmissione pacchetti RNDIS di classe dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-939">This event represents a USBX Device Class Rndis Packet Transmit Event.</span></span>

<span data-ttu-id="5cc78-940">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-940">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-941">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-941">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-942">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-942">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-943">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-943">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-944">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-944">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-activate"></a><span data-ttu-id="5cc78-945">Attivazione dell'archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-945">Device Class Storage Activate</span></span> 

#### <a name="ux_device_class_storage_activate"></a><span data-ttu-id="5cc78-946">ux_device_class_storage_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-946">ux_device_class_storage_activate</span></span>

<span data-ttu-id="5cc78-947">**Icona** ![ di Icona di attivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-947">**Icon** ![Device Class Storage Activate icon](./media/user-guide/usbx-events/image41.png)</span></span>

<span data-ttu-id="5cc78-948">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-948">**Description**</span></span>

<span data-ttu-id="5cc78-949">Questo evento rappresenta un evento di attivazione dell'archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-949">This event represents a USBX Device Class Storage Activate Event.</span></span>

<span data-ttu-id="5cc78-950">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-950">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-951">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-951">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-952">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-952">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-953">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-953">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-954">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-954">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-deactivate"></a><span data-ttu-id="5cc78-955">Disattivazione dell'archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-955">Device Class Storage Deactivate</span></span> 

#### <a name="ux_device_class_storage_deactivate"></a><span data-ttu-id="5cc78-956">ux_device_class_storage_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-956">ux_device_class_storage_deactivate</span></span>

<span data-ttu-id="5cc78-957">**Icona** ![ di Icona di disattivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-957">**Icon** ![Device Class Storage Deactivate icon](./media/user-guide/usbx-events/image42.png)</span></span>

<span data-ttu-id="5cc78-958">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-958">**Description**</span></span>

<span data-ttu-id="5cc78-959">Questo evento rappresenta un evento di disattivazione dell'archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-959">This event represents a USBX Device Class Storage Deactivate Event.</span></span>

<span data-ttu-id="5cc78-960">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-960">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-961">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-961">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-962">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-962">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-963">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-963">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-964">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-964">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-format"></a><span data-ttu-id="5cc78-965">Formato di archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-965">Device Class Storage Format</span></span> 

#### <a name="ux_device_class_storage_format"></a><span data-ttu-id="5cc78-966">ux_device_class_storage_format</span><span class="sxs-lookup"><span data-stu-id="5cc78-966">ux_device_class_storage_format</span></span>

<span data-ttu-id="5cc78-967">**Icona** ![ di Icona del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-967">**Icon** ![Device Class Storage Format icon](./media/user-guide/usbx-events/image43.png)</span></span>

<span data-ttu-id="5cc78-968">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-968">**Description**</span></span>

<span data-ttu-id="5cc78-969">Questo evento rappresenta un evento del formato di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-969">This event represents a USBX Device Class Storage Format Event.</span></span>

<span data-ttu-id="5cc78-970">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-970">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-971">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-971">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-972">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-972">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-973">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-973">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-974">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-974">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-inquiry"></a><span data-ttu-id="5cc78-975">Richiesta di archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-975">Device Class Storage Inquiry</span></span> 

#### <a name="ux_device_class_storage_inquiry"></a><span data-ttu-id="5cc78-976">ux_device_class_storage_inquiry</span><span class="sxs-lookup"><span data-stu-id="5cc78-976">ux_device_class_storage_inquiry</span></span>

<span data-ttu-id="5cc78-977">**Icona** ![ di Icona di richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-977">**Icon** ![Device Class Storage Inquiry icon](./media/user-guide/usbx-events/image44.png)</span></span>

<span data-ttu-id="5cc78-978">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-978">**Description**</span></span>

<span data-ttu-id="5cc78-979">Questo evento rappresenta un evento di richiesta di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-979">This event represents a USBX Device Class Storage Inquiry Event.</span></span>

<span data-ttu-id="5cc78-980">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-980">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-981">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-981">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-982">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-982">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-983">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-983">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-984">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-984">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-mode-select"></a><span data-ttu-id="5cc78-985">Selezione della modalità di archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-985">Device Class Storage Mode Select</span></span>

#### <a name="ux_device_class_storage_mode_select"></a><span data-ttu-id="5cc78-986">ux_device_class_storage_mode_select</span><span class="sxs-lookup"><span data-stu-id="5cc78-986">ux_device_class_storage_mode_select</span></span>

<span data-ttu-id="5cc78-987">**Icona** ![ di Icona di selezione modalità di archiviazione classe dispositivo](./media/user-guide/usbx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-987">**Icon** ![Device Class Storage Mode Select icon](./media/user-guide/usbx-events/image45.png)</span></span>

<span data-ttu-id="5cc78-988">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-988">**Description**</span></span>

<span data-ttu-id="5cc78-989">Questo evento rappresenta un evento di selezione della modalità di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-989">This event represents a USBX Device Class Storage Mode Select Event.</span></span>

<span data-ttu-id="5cc78-990">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-990">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-991">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-991">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-992">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-992">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-993">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-993">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-994">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-994">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-mode-sense"></a><span data-ttu-id="5cc78-995">Rilevamento della modalità di archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-995">Device Class Storage Mode Sense</span></span> 

#### <a name="ux_device_class_storage_mode_sense"></a><span data-ttu-id="5cc78-996">ux_device_class_storage_mode_sense</span><span class="sxs-lookup"><span data-stu-id="5cc78-996">ux_device_class_storage_mode_sense</span></span>

<span data-ttu-id="5cc78-997">**Icona** ![ di Icona di rilevamento della modalità di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-997">**Icon** ![Device Class Storage Mode Sense icon](./media/user-guide/usbx-events/image46.png)</span></span>

<span data-ttu-id="5cc78-998">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-998">**Description**</span></span>

<span data-ttu-id="5cc78-999">Questo evento rappresenta un evento del senso della modalità di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-999">This event represents a USBX Device Class Storage Mode Sense Event.</span></span>

<span data-ttu-id="5cc78-1000">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="5cc78-1000">Information Fields</span></span> 

- <span data-ttu-id="5cc78-1001">Campo NFO 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1001">nfo Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1002">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1002">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1003">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1003">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1004">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1004">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-prevent-allow-media-removal"></a><span data-ttu-id="5cc78-1005">L'archiviazione delle classi di dispositivi impedisce la rimozione di supporti</span><span class="sxs-lookup"><span data-stu-id="5cc78-1005">Device Class Storage Prevent Allow Media Removal</span></span> 

#### <a name="ux_device_class_storage_prevent_allow_media_removal"></a><span data-ttu-id="5cc78-1006">ux_device_class_storage_prevent_allow_media_removal</span><span class="sxs-lookup"><span data-stu-id="5cc78-1006">ux_device_class_storage_prevent_allow_media_removal</span></span>

<span data-ttu-id="5cc78-1007">**Icona** ![ di Archiviazione della classe dispositivo Impedisci l'uso dell'icona Consenti rimozione supporti](./media/user-guide/usbx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1007">**Icon** ![Device Class Storage Prevent Allow Media Removal icon](./media/user-guide/usbx-events/image47.png)</span></span>

<span data-ttu-id="5cc78-1008">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1008">**Description**</span></span>

<span data-ttu-id="5cc78-1009">Questo evento rappresenta un'archiviazione della classe del dispositivo USBX Impedisci l'evento di rimozione dei supporti.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1009">This event represents a USBX Device Class Storage Prevent Allow Media Removal Event.</span></span>

<span data-ttu-id="5cc78-1010">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1010">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1011">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1011">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1012">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1012">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1013">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1013">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1014">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1014">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-read"></a><span data-ttu-id="5cc78-1015">Lettura archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1015">Device Class Storage Read</span></span> 

#### <a name="ux_device_class_storage_read"></a><span data-ttu-id="5cc78-1016">ux_device_class_storage_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1016">ux_device_class_storage_read</span></span>

<span data-ttu-id="5cc78-1017">**Icona** ![ di Icona di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1017">**Icon** ![Device Class Storage Read icon](./media/user-guide/usbx-events/image48.png)</span></span>

<span data-ttu-id="5cc78-1018">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1018">**Description**</span></span>

<span data-ttu-id="5cc78-1019">Questo evento rappresenta un evento di lettura di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1019">This event represents a USBX Device Class Storage Read Event.</span></span>

<span data-ttu-id="5cc78-1020">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1020">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1021">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1021">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1022">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1022">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1023">Campo informazioni 3: settore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1023">Info Field 3: Sector.</span></span>
- <span data-ttu-id="5cc78-1024">Campo dati 4: settori numerici.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1024">Info Field 4: Number sectors.</span></span>

### <a name="device-class-storage-read-capacity"></a><span data-ttu-id="5cc78-1025">Capacità lettura archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1025">Device Class Storage Read Capacity</span></span> 

#### <a name="ux_device_class_storage_read_capacity"></a><span data-ttu-id="5cc78-1026">ux_device_class_storage_read_capacity</span><span class="sxs-lookup"><span data-stu-id="5cc78-1026">ux_device_class_storage_read_capacity</span></span>

<span data-ttu-id="5cc78-1027">**Icona** ![ di Icona capacità di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1027">**Icon** ![Device Class Storage Read Capacity icon](./media/user-guide/usbx-events/image49.png)</span></span>

<span data-ttu-id="5cc78-1028">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1028">**Description**</span></span>

<span data-ttu-id="5cc78-1029">Questo evento rappresenta un evento di capacità di lettura di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1029">This event represents a USBX Device Class Storage Read Capacity Event.</span></span>

<span data-ttu-id="5cc78-1030">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1030">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1031">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1031">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1032">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1032">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1033">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1033">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1034">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1034">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-read-format-capacity"></a><span data-ttu-id="5cc78-1035">Capacità di lettura del formato di archiviazione della classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1035">Device Class Storage Read Format Capacity</span></span> 

#### <a name="ux_device_class_storage_read_format_capacity"></a><span data-ttu-id="5cc78-1036">ux_device_class_storage_read_format_capacity</span><span class="sxs-lookup"><span data-stu-id="5cc78-1036">ux_device_class_storage_read_format_capacity</span></span>

<span data-ttu-id="5cc78-1037">**Icona** ![ di Icona della capacità di lettura del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1037">**Icon** ![Device Class Storage Read Format Capacity icon](./media/user-guide/usbx-events/image50.png)</span></span>

<span data-ttu-id="5cc78-1038">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1038">**Description**</span></span>

<span data-ttu-id="5cc78-1039">Questo evento rappresenta un evento di capacità di lettura del formato di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1039">This event represents a USBX Device Class Storage Read Format Capacity Event.</span></span>

<span data-ttu-id="5cc78-1040">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1040">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1041">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1041">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1042">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1042">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1043">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1043">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1044">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1044">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-read-toc"></a><span data-ttu-id="5cc78-1045">Sommario di lettura per archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1045">Device Class Storage Read TOC</span></span> 

#### <a name="ux_device_class_storage_read_toc"></a><span data-ttu-id="5cc78-1046">ux_device_class_storage_read_toc</span><span class="sxs-lookup"><span data-stu-id="5cc78-1046">ux_device_class_storage_read_toc</span></span>

<span data-ttu-id="5cc78-1047">**Icona** ![ di Icona di lettura Sommario archiviazione classe dispositivo](./media/user-guide/usbx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1047">**Icon** ![Device Class Storage Read TOC icon](./media/user-guide/usbx-events/image51.png)</span></span>

<span data-ttu-id="5cc78-1048">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1048">**Description**</span></span>

<span data-ttu-id="5cc78-1049">Questo evento rappresenta un evento di lettura del sommario di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1049">This event represents a USBX Device Class Storage Read TOC Event.</span></span>

<span data-ttu-id="5cc78-1050">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1050">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1051">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1051">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1052">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1052">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1053">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1053">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1054">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1054">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-request-sense"></a><span data-ttu-id="5cc78-1055">Senso richiesta archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1055">Device Class Storage Request Sense</span></span> 

#### <a name="ux_device_class_storage_request_sense"></a><span data-ttu-id="5cc78-1056">ux_device_class_storage_request_sense</span><span class="sxs-lookup"><span data-stu-id="5cc78-1056">ux_device_class_storage_request_sense</span></span>

<span data-ttu-id="5cc78-1057">**Icona** ![ di Icona del senso della richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1057">**Icon** ![Device Class Storage Request Sense icon](./media/user-guide/usbx-events/image52.png)</span></span>

<span data-ttu-id="5cc78-1058">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1058">**Description**</span></span>

<span data-ttu-id="5cc78-1059">Questo evento rappresenta un evento del senso della richiesta di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1059">This event represents a USBX Device Class Storage Request Sense Event.</span></span>

<span data-ttu-id="5cc78-1060">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1060">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1061">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1061">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1062">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1062">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1063">Informazioni sul campo 3: chiave Sense.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1063">Info Field 3: Sense key.</span></span>
- <span data-ttu-id="5cc78-1064">Campo informazioni 4: codice.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1064">Info Field 4: Code.</span></span>

### <a name="device-class-storage-start-stop"></a><span data-ttu-id="5cc78-1065">Inizio arresto archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1065">Device Class Storage Start Stop</span></span> 

#### <a name="ux_device_class_storage_start_stop"></a><span data-ttu-id="5cc78-1066">ux_device_class_storage_start_stop</span><span class="sxs-lookup"><span data-stu-id="5cc78-1066">ux_device_class_storage_start_stop</span></span>

<span data-ttu-id="5cc78-1067">**Icona** ![ di Icona di avvio dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1067">**Icon** ![Device Class Storage Start Stop icon](./media/user-guide/usbx-events/image53.png)</span></span>

<span data-ttu-id="5cc78-1068">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1068">**Description**</span></span>

<span data-ttu-id="5cc78-1069">Questo evento rappresenta un evento di avvio di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1069">This event represents a USBX Device Class Storage Start Stop Event.</span></span>

<span data-ttu-id="5cc78-1070">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1070">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1071">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1071">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1072">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1072">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1073">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1073">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1074">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1074">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-test-ready"></a><span data-ttu-id="5cc78-1075">Il test di archiviazione della classe dispositivo è pronto</span><span class="sxs-lookup"><span data-stu-id="5cc78-1075">Device Class Storage Test Ready</span></span> 

#### <a name="ux_device_class_storage_test_ready"></a><span data-ttu-id="5cc78-1076">ux_device_class_storage_test_ready</span><span class="sxs-lookup"><span data-stu-id="5cc78-1076">ux_device_class_storage_test_ready</span></span>

<span data-ttu-id="5cc78-1077">**Icona** ![ di Icona dei test di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1077">**Icon** ![Device Class Storage Test Ready icon](./media/user-guide/usbx-events/image54.png)</span></span>

<span data-ttu-id="5cc78-1078">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1078">**Description**</span></span>

<span data-ttu-id="5cc78-1079">Questo evento rappresenta un evento pronto per il test di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1079">This event represents a USBX Device Class Storage Test Ready Event.</span></span>

<span data-ttu-id="5cc78-1080">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1080">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1081">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1081">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1082">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1082">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1083">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1083">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1084">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1084">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-verify"></a><span data-ttu-id="5cc78-1085">Verifica archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1085">Device Class Storage Verify</span></span> 

#### <a name="ux_device_class_storage_verify"></a><span data-ttu-id="5cc78-1086">ux_device_class_storage_verify</span><span class="sxs-lookup"><span data-stu-id="5cc78-1086">ux_device_class_storage_verify</span></span>

<span data-ttu-id="5cc78-1087">**Icona** ![ di Icona di verifica archiviazione classe dispositivo](./media/user-guide/usbx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1087">**Icon** ![Device Class Storage Verify icon](./media/user-guide/usbx-events/image55.png)</span></span>

<span data-ttu-id="5cc78-1088">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1088">**Description**</span></span>

<span data-ttu-id="5cc78-1089">Questo evento rappresenta un evento di verifica dell'archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1089">This event represents a USBX Device Class Storage Verify Event.</span></span>

<span data-ttu-id="5cc78-1090">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1090">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1091">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1091">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1092">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1092">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1093">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1093">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1094">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1094">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-write"></a><span data-ttu-id="5cc78-1095">Scrittura archiviazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1095">Device Class Storage Write</span></span> 

#### <a name="ux_device_class_storage_write"></a><span data-ttu-id="5cc78-1096">ux_device_class_storage_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1096">ux_device_class_storage_write</span></span>

<span data-ttu-id="5cc78-1097">**Icona** ![ di Icona di scrittura archiviazione classe dispositivo](./media/user-guide/usbx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1097">**Icon** ![Device Class Storage Write icon](./media/user-guide/usbx-events/image56.png)</span></span>

<span data-ttu-id="5cc78-1098">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1098">**Description**</span></span>

<span data-ttu-id="5cc78-1099">Questo evento rappresenta un evento di scrittura di archiviazione della classe del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1099">This event represents a USBX Device Class Storage Write Event.</span></span>

<span data-ttu-id="5cc78-1100">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1100">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1101">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1101">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1102">Informazioni sul campo 2: lun.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1102">Info Field 2: Lun.</span></span>
- <span data-ttu-id="5cc78-1103">Campo informazioni 3: settore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1103">Info Field 3: Sector.</span></span>
- <span data-ttu-id="5cc78-1104">Campo dati 4: settori numerici.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1104">Info Field 4: Number sectors.</span></span>

### <a name="device-stack-alternate-setting-get"></a><span data-ttu-id="5cc78-1105">Impostazione alternativa stack del dispositivo Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1105">Device Stack Alternate Setting Get</span></span> 

#### <a name="ux_device_class_alternate_setting_get"></a><span data-ttu-id="5cc78-1106">ux_device_class_alternate_setting_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1106">ux_device_class_alternate_setting_get</span></span>

<span data-ttu-id="5cc78-1107">**Icona** ![ di Icona del Get dell'impostazione alternativa dello stack del dispositivo](./media/user-guide/usbx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1107">**Icon** ![Device Stack Alternate Setting Get icon](./media/user-guide/usbx-events/image57.png)</span></span>

<span data-ttu-id="5cc78-1108">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1108">**Description**</span></span>

<span data-ttu-id="5cc78-1109">Questo evento rappresenta un'impostazione alternativa di Get Event stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1109">This event represents a USBX Device Stack Alternate Setting Get Event.</span></span>

<span data-ttu-id="5cc78-1110">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1110">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1111">Info Field 1: valore di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1111">Info Field 1: Interface value.</span></span>
- <span data-ttu-id="5cc78-1112">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1112">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1113">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1113">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1114">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1114">Info Field 4: Not used.</span></span>

### <a name="device-stack-alternate-setting-set"></a><span data-ttu-id="5cc78-1115">Set di impostazioni alternativo dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1115">Device Stack Alternate Setting Set</span></span> 

#### <a name="ux_device_class_alternate_setting_set"></a><span data-ttu-id="5cc78-1116">ux_device_class_alternate_setting_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1116">ux_device_class_alternate_setting_set</span></span>

<span data-ttu-id="5cc78-1117">**Icona** ![ di Icona del set di impostazioni alternativo dello stack del dispositivo](./media/user-guide/usbx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1117">**Icon** ![Device Stack Alternate Setting Set icon](./media/user-guide/usbx-events/image58.png)</span></span>

<span data-ttu-id="5cc78-1118">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1118">**Description**</span></span>

<span data-ttu-id="5cc78-1119">Questo evento rappresenta un evento del set di impostazioni alternativo dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1119">This event represents a USBX Device Stack Alternate Setting Set Event.</span></span>

<span data-ttu-id="5cc78-1120">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1120">**Information Fields**</span></span>
- <span data-ttu-id="5cc78-1121">Info Field 1: valore di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1121">Info Field 1: Interface value.</span></span>
- <span data-ttu-id="5cc78-1122">Informazioni sul campo 2: valore dell'impostazione alternativa.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1122">Info Field 2: Alternate setting value.</span></span>
- <span data-ttu-id="5cc78-1123">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1123">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1124">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1124">Info Field 4: Not used.</span></span>

### <a name="device-stack-class-register"></a><span data-ttu-id="5cc78-1125">Registro classe stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1125">Device Stack Class Register</span></span> 

#### <a name="ux_device_stack_class_register"></a><span data-ttu-id="5cc78-1126">ux_device_stack_class_register</span><span class="sxs-lookup"><span data-stu-id="5cc78-1126">ux_device_stack_class_register</span></span>

<span data-ttu-id="5cc78-1127">**Icona** ![ di Icona di registro classe stack del dispositivo](./media/user-guide/usbx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1127">**Icon** ![Device Stack Class Register icon](./media/user-guide/usbx-events/image59.png)</span></span>

<span data-ttu-id="5cc78-1128">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1128">**Description**</span></span>

<span data-ttu-id="5cc78-1129">Questo evento rappresenta un evento di registrazione della classe stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1129">This event represents a USBX Device Stack Class Register Event.</span></span>

<span data-ttu-id="5cc78-1130">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1130">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1131">Info Field 1: nome della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1131">Info Field 1: Class name.</span></span>
- <span data-ttu-id="5cc78-1132">Informazioni sul campo 2: numero di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1132">Info Field 2: Interface number.</span></span>
- <span data-ttu-id="5cc78-1133">Campo info 3: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1133">Info Field 3: Parameter.</span></span>
- <span data-ttu-id="5cc78-1134">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1134">Info Field 4: Not used.</span></span>

### <a name="device-stack-clear-feature"></a><span data-ttu-id="5cc78-1135">Funzionalità di cancellazione dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1135">Device Stack Clear Feature</span></span> 

#### <a name="ux_device_stack_clear_feature"></a><span data-ttu-id="5cc78-1136">ux_device_stack_clear_feature</span><span class="sxs-lookup"><span data-stu-id="5cc78-1136">ux_device_stack_clear_feature</span></span>

<span data-ttu-id="5cc78-1137">**Icona** ![ di Icona della funzionalità cancellazione dello stack del dispositivo](./media/user-guide/usbx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1137">**Icon** ![Device Stack Clear Feature icon](./media/user-guide/usbx-events/image60.png)</span></span>

<span data-ttu-id="5cc78-1138">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1138">**Description**</span></span>

<span data-ttu-id="5cc78-1139">Questo evento rappresenta un evento di funzionalità di cancellazione dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1139">This event represents a USBX Device Stack Clear Feature Event.</span></span>

<span data-ttu-id="5cc78-1140">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1140">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1141">Campo informazioni 1: tipo di richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1141">Info Field 1: Request type.</span></span>
- <span data-ttu-id="5cc78-1142">Informazioni sul campo 2: valore della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1142">Info Field 2: Request value.</span></span> <span data-ttu-id="5cc78-1143">Informazioni sul campo 3: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1143">Info Field 3: Request index.</span></span>
- <span data-ttu-id="5cc78-1144">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1144">Info Field 4: Not used.</span></span>

### <a name="device-stack-configuration-get"></a><span data-ttu-id="5cc78-1145">Configurazione dello stack del dispositivo Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1145">Device Stack Configuration Get</span></span> 

#### <a name="ux_device_stack_configuration_get-t"></a><span data-ttu-id="5cc78-1146">ux_device_stack_configuration_get t</span><span class="sxs-lookup"><span data-stu-id="5cc78-1146">ux_device_stack_configuration_get t</span></span>

<span data-ttu-id="5cc78-1147">**Icona** ![ di Icona di Get della configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1147">**Icon** ![Device Stack Configuration Get icon](./media/user-guide/usbx-events/image61.png)</span></span>

<span data-ttu-id="5cc78-1148">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1148">**Description**</span></span>

<span data-ttu-id="5cc78-1149">Questo evento rappresenta un evento Get della configurazione dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1149">This event represents a USBX Device Stack Configuration Get Event.</span></span>

<span data-ttu-id="5cc78-1150">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1150">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1151">Campo informazioni 1: valore di configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1151">Info Field 1: Configuration value.</span></span>
- <span data-ttu-id="5cc78-1152">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1152">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1153">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1153">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1154">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1154">Info Field 4: Not used.</span></span>

### <a name="device-stack-configuration-set"></a><span data-ttu-id="5cc78-1155">Set di configurazione dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1155">Device Stack Configuration Set</span></span> 

#### <a name="ux_device_stack_configuration_set"></a><span data-ttu-id="5cc78-1156">ux_device_stack_configuration_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1156">ux_device_stack_configuration_set</span></span>

<span data-ttu-id="5cc78-1157">**Icona** ![ di Icona del set di configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1157">**Icon** ![Device Stack Configuration Set icon](./media/user-guide/usbx-events/image62.png)</span></span>

<span data-ttu-id="5cc78-1158">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1158">**Description**</span></span>

<span data-ttu-id="5cc78-1159">Questo evento rappresenta un evento del set di configurazione dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1159">This event represents a USBX Device Stack Configuration Set Event.</span></span>

<span data-ttu-id="5cc78-1160">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1160">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1161">Campo informazioni 1: valore di configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1161">Info Field 1: Configuration value.</span></span>
- <span data-ttu-id="5cc78-1162">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1162">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1163">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1163">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1164">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1164">Info Field 4: Not used.</span></span>

### <a name="device-stack-connect"></a><span data-ttu-id="5cc78-1165">Connessione stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1165">Device Stack Connect</span></span> 

#### <a name="ux_device_stack_connect"></a><span data-ttu-id="5cc78-1166">ux_device_stack_connect</span><span class="sxs-lookup"><span data-stu-id="5cc78-1166">ux_device_stack_connect</span></span>

<span data-ttu-id="5cc78-1167">**Icona** ![ di Icona di connessione dello stack del dispositivo](./media/user-guide/usbx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1167">**Icon** ![Device Stack Connect icon](./media/user-guide/usbx-events/image63.png)</span></span>

<span data-ttu-id="5cc78-1168">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1168">**Description**</span></span>

<span data-ttu-id="5cc78-1169">Questo evento rappresenta un evento di invio del descrittore dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1169">This event represents a USBX Device Stack Descriptor Send Event.</span></span>

<span data-ttu-id="5cc78-1170">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1170">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1171">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1171">Info Field 1: Not used.</span></span>
- <span data-ttu-id="5cc78-1172">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1172">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1173">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1173">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1174">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1174">Info Field 4: Not used.</span></span>

### <a name="device-stack-descriptor-send"></a><span data-ttu-id="5cc78-1175">Invio del descrittore dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1175">Device Stack Descriptor Send</span></span> 

#### <a name="ux_device_stack_descriptor_send"></a><span data-ttu-id="5cc78-1176">ux_device_stack_descriptor_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-1176">ux_device_stack_descriptor_send</span></span>

<span data-ttu-id="5cc78-1177">**Icona** ![ di Icona di invio del descrittore dello stack del dispositivo](./media/user-guide/usbx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1177">**Icon** ![Device Stack Descriptor Send icon](./media/user-guide/usbx-events/image64.png)</span></span>

<span data-ttu-id="5cc78-1178">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1178">**Description**</span></span>

<span data-ttu-id="5cc78-1179">Questo evento rappresenta un evento di invio del descrittore dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1179">This event represents a USBX Device Stack Descriptor Send Event.</span></span>

<span data-ttu-id="5cc78-1180">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1180">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1181">Info Field 1: tipo di descrittore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1181">Info Field 1: Descriptor type.</span></span>
- <span data-ttu-id="5cc78-1182">Informazioni sul campo 2: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1182">Info Field 2: Request index.</span></span>
- <span data-ttu-id="5cc78-1183">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1183">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1184">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1184">Info Field 4: Not used.</span></span>

### <a name="device-stack-disconnect"></a><span data-ttu-id="5cc78-1185">Disconnessione dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1185">Device Stack Disconnect</span></span> 

#### <a name="ux_device_stack_disconnect"></a><span data-ttu-id="5cc78-1186">ux_device_stack_disconnect</span><span class="sxs-lookup"><span data-stu-id="5cc78-1186">ux_device_stack_disconnect</span></span>

<span data-ttu-id="5cc78-1187">**Icona** ![ di Icona di disconnessione dello stack del dispositivo](./media/user-guide/usbx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1187">**Icon** ![Device Stack Disconnect icon](./media/user-guide/usbx-events/image65.png)</span></span>

<span data-ttu-id="5cc78-1188">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1188">**Description**</span></span>

<span data-ttu-id="5cc78-1189">Questo evento rappresenta un evento di disconnessione dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1189">This event represents a USBX Device Stack Disconnect Event.</span></span>

<span data-ttu-id="5cc78-1190">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1190">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1191">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1191">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-1192">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1192">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1193">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1193">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1194">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1194">Info Field 4: Not used.</span></span>

### <a name="device-stack-endpoint-stall"></a><span data-ttu-id="5cc78-1195">Stallo dello stack dell'endpoint del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1195">Device Stack Endpoint Stall</span></span> 

#### <a name="ux_device_stack_endpoint_stall"></a><span data-ttu-id="5cc78-1196">ux_device_stack_endpoint_stall</span><span class="sxs-lookup"><span data-stu-id="5cc78-1196">ux_device_stack_endpoint_stall</span></span>

<span data-ttu-id="5cc78-1197">**Icona** ![ di Icona dello stallo dello stack dell'endpoint del dispositivo](./media/user-guide/usbx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1197">**Icon** ![Device Stack Endpoint Stall icon](./media/user-guide/usbx-events/image66.png)</span></span>

<span data-ttu-id="5cc78-1198">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1198">**Description**</span></span>

<span data-ttu-id="5cc78-1199">Questo evento rappresenta un evento di blocco dell'endpoint dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1199">This event represents a USBX Device Stack Endpoint Stall Event.</span></span>

<span data-ttu-id="5cc78-1200">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1200">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1201">Campo informazioni 1: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1201">Info Field 1: Endpoint.</span></span>
- <span data-ttu-id="5cc78-1202">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1202">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1203">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1203">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1204">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1204">Info Field 4: Not used.</span></span>

### <a name="device-stack-get-status"></a><span data-ttu-id="5cc78-1205">Stato di Get dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1205">Device Stack Get Status</span></span> 

#### <a name="ux_device_stack_get_status"></a><span data-ttu-id="5cc78-1206">ux_device_stack_get_status</span><span class="sxs-lookup"><span data-stu-id="5cc78-1206">ux_device_stack_get_status</span></span>

<span data-ttu-id="5cc78-1207">**Icona** ![ di Icona dello stato di Get dello stack del dispositivo](./media/user-guide/usbx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1207">**Icon** ![Device Stack Get Status icon](./media/user-guide/usbx-events/image67.png)</span></span>

<span data-ttu-id="5cc78-1208">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1208">**Description**</span></span>

<span data-ttu-id="5cc78-1209">Questo evento rappresenta un evento di stato di Get dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1209">This event represents a USBX Device Stack Get Status Event.</span></span>

<span data-ttu-id="5cc78-1210">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1210">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1211">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1211">Info Field 1: Not used.</span></span>
- <span data-ttu-id="5cc78-1212">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1212">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1213">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1213">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1214">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1214">Info Field 4: Not used.</span></span>

### <a name="device-stack-host-wakeup"></a><span data-ttu-id="5cc78-1215">Riattivazione host stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1215">Device Stack Host Wakeup</span></span> 

#### <a name="ux_device_stack_host_wakeup"></a><span data-ttu-id="5cc78-1216">ux_device_stack_host_wakeup</span><span class="sxs-lookup"><span data-stu-id="5cc78-1216">ux_device_stack_host_wakeup</span></span>

<span data-ttu-id="5cc78-1217">**Icona** ![ di Icona di riattivazione host stack del dispositivo](./media/user-guide/usbx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1217">**Icon** ![Device Stack Host Wakeup icon](./media/user-guide/usbx-events/image68.png)</span></span>

<span data-ttu-id="5cc78-1218">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1218">**Description**</span></span>

<span data-ttu-id="5cc78-1219">Questo evento rappresenta un evento di riattivazione host dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1219">This event represents a USBX Device Stack Host Wakeup Event.</span></span>

<span data-ttu-id="5cc78-1220">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1220">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1221">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1221">Info Field 1: Not used.</span></span>
- <span data-ttu-id="5cc78-1222">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1222">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1223">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1223">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1224">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1224">Info Field 4: Not used.</span></span>

### <a name="device-stack-initialize"></a><span data-ttu-id="5cc78-1225">Inizializzazione dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1225">Device Stack Initialize</span></span> 

#### <a name="ux_device_stack_initialize"></a><span data-ttu-id="5cc78-1226">ux_device_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="5cc78-1226">ux_device_stack_initialize</span></span>

<span data-ttu-id="5cc78-1227">**Icona** ![ di Icona di inizializzazione dello stack del dispositivo](./media/user-guide/usbx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1227">**Icon** ![Device Stack Initialize icon](./media/user-guide/usbx-events/image69.png)</span></span>

<span data-ttu-id="5cc78-1228">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1228">**Description**</span></span>

<span data-ttu-id="5cc78-1229">Questo evento rappresenta un evento di inizializzazione dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1229">This event represents a USBX Device Stack Initialize Event.</span></span>

<span data-ttu-id="5cc78-1230">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1230">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1231">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1231">Info Field 1: Not used.</span></span>
- <span data-ttu-id="5cc78-1232">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1232">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1233">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1233">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1234">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1234">Info Field 4: Not used.</span></span>

### <a name="device-stack-interface-delete"></a><span data-ttu-id="5cc78-1235">Eliminazione dell'interfaccia dello stack di dispositivi</span><span class="sxs-lookup"><span data-stu-id="5cc78-1235">Device Stack Interface Delete</span></span> 

#### <a name="ux_device_stack_interface_delete"></a><span data-ttu-id="5cc78-1236">ux_device_stack_interface_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-1236">ux_device_stack_interface_delete</span></span>

<span data-ttu-id="5cc78-1237">**Icona** ![ di Icona di eliminazione dell'interfaccia dello stack del dispositivo](./media/user-guide/usbx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1237">**Icon** ![Device Stack Interface Delete icon](./media/user-guide/usbx-events/image70.png)</span></span>

<span data-ttu-id="5cc78-1238">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1238">**Description**</span></span>

<span data-ttu-id="5cc78-1239">Questo evento rappresenta un evento di eliminazione dell'interfaccia dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1239">This event represents a USBX Device Stack Interface Delete Event.</span></span>

<span data-ttu-id="5cc78-1240">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1240">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1241">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1241">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-1242">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1242">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1243">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1243">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1244">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1244">Info Field 4: Not used.</span></span>

### <a name="device-stack-interface-get"></a><span data-ttu-id="5cc78-1245">Interfaccia stack del dispositivo Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1245">Device Stack Interface Get</span></span> 

#### <a name="ux_device_stack_interface_get"></a><span data-ttu-id="5cc78-1246">ux_device_stack_interface_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1246">ux_device_stack_interface_get</span></span>

<span data-ttu-id="5cc78-1247">**Icona** ![ di Icona Ottieni interfaccia stack di dispositivi](./media/user-guide/usbx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1247">**Icon** ![Device Stack Interface Get icon](./media/user-guide/usbx-events/image71.png)</span></span>

<span data-ttu-id="5cc78-1248">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1248">**Description**</span></span>

<span data-ttu-id="5cc78-1249">Questo evento rappresenta un evento Get dell'interfaccia dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1249">This event represents a USBX Device Stack Interface Get Event.</span></span>

<span data-ttu-id="5cc78-1250">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1250">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1251">Info Field 1: valore di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1251">Info Field 1: Interface value.</span></span>
- <span data-ttu-id="5cc78-1252">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1252">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1253">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1253">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1254">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1254">Info Field 4: Not used.</span></span>

### <a name="device-stack-interface-set"></a><span data-ttu-id="5cc78-1255">Set di interfacce dello stack di dispositivi</span><span class="sxs-lookup"><span data-stu-id="5cc78-1255">Device Stack Interface Set</span></span> 

#### <a name="ux_device_stack_interface_set"></a><span data-ttu-id="5cc78-1256">ux_device_stack_interface_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1256">ux_device_stack_interface_set</span></span>

<span data-ttu-id="5cc78-1257">**Icona** ![ di Icona del set di interfacce dello stack di dispositivi](./media/user-guide/usbx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1257">**Icon** ![Device Stack Interface Set icon](./media/user-guide/usbx-events/image72.png)</span></span>

<span data-ttu-id="5cc78-1258">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1258">**Description**</span></span>

<span data-ttu-id="5cc78-1259">Questo evento rappresenta un evento del set di interfacce dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1259">This event represents a USBX Device Stack Interface Set Event.</span></span>

<span data-ttu-id="5cc78-1260">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1260">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1261">Campo informazioni 1: valore della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1261">Info Field 1: Request value.</span></span> <span data-ttu-id="5cc78-1262">Informazioni sul campo 2: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1262">Info Field 2: Request index.</span></span>
- <span data-ttu-id="5cc78-1263">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1263">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1264">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1264">Info Field 4: Not used.</span></span>

### <a name="device-stack-set-feature"></a><span data-ttu-id="5cc78-1265">Funzionalità set di stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1265">Device Stack Set Feature</span></span> 

#### <a name="ux_device_stack_set_feature"></a><span data-ttu-id="5cc78-1266">ux_device_stack_set_feature</span><span class="sxs-lookup"><span data-stu-id="5cc78-1266">ux_device_stack_set_feature</span></span>

<span data-ttu-id="5cc78-1267">**Icona** ![ di Icona della funzionalità set di stack del dispositivo](./media/user-guide/usbx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1267">**Icon** ![Device Stack Set Feature icon](./media/user-guide/usbx-events/image73.png)</span></span>

<span data-ttu-id="5cc78-1268">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1268">**Description**</span></span>

<span data-ttu-id="5cc78-1269">Questo evento rappresenta un evento di funzionalità del set di stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1269">This event represents a USBX Device Stack Set Feature Event.</span></span>

<span data-ttu-id="5cc78-1270">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1270">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1271">Campo informazioni 1: valore della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1271">Info Field 1: Request value.</span></span> <span data-ttu-id="5cc78-1272">Informazioni sul campo 2: indice della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1272">Info Field 2: Request index.</span></span>
- <span data-ttu-id="5cc78-1273">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1273">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1274">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1274">Info Field 4: Not used.</span></span>

### <a name="device-stack-transfer-abort"></a><span data-ttu-id="5cc78-1275">Interruzione trasferimento stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1275">Device Stack Transfer Abort</span></span> 

#### <a name="ux_device_stack_transfer_abort"></a><span data-ttu-id="5cc78-1276">ux_device_stack_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="5cc78-1276">ux_device_stack_transfer_abort</span></span>

<span data-ttu-id="5cc78-1277">**Icona** ![ di Icona di interruzione del trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image74.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1277">**Icon** ![Device Stack Transfer Abort icon](./media/user-guide/usbx-events/image74.png)</span></span>

<span data-ttu-id="5cc78-1278">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1278">**Description**</span></span>

<span data-ttu-id="5cc78-1279">Questo evento rappresenta un evento di interruzione del trasferimento dello stack del dispositivo USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1279">This event represents a USBX Device Stack Transfer Abort Event.</span></span>

<span data-ttu-id="5cc78-1280">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1280">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1281">Campo informazioni 1: richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1281">Info Field 1: Transfer request.</span></span>
- <span data-ttu-id="5cc78-1282">Informazioni sul campo 2: codice di completamento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1282">Info Field 2: Completion code.</span></span>
- <span data-ttu-id="5cc78-1283">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1283">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1284">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1284">Info Field 4: Not used.</span></span>

### <a name="device-stack-transfer-all-request-abort"></a><span data-ttu-id="5cc78-1285">Interruzione richiesta tutti i trasferimenti stack di dispositivi</span><span class="sxs-lookup"><span data-stu-id="5cc78-1285">Device Stack Transfer All Request Abort</span></span> 

#### <a name="ux_device_stack_transfer_all_request_abort"></a><span data-ttu-id="5cc78-1286">ux_device_stack_transfer_all_request_abort</span><span class="sxs-lookup"><span data-stu-id="5cc78-1286">ux_device_stack_transfer_all_request_abort</span></span>

<span data-ttu-id="5cc78-1287">**Icona** ![ di Icona di interruzione della richiesta di trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image75.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1287">**Icon** ![Device Stack Transfer All Request Abort icon](./media/user-guide/usbx-events/image75.png)</span></span>

<span data-ttu-id="5cc78-1288">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1288">**Description**</span></span>

<span data-ttu-id="5cc78-1289">Questo evento rappresenta un evento di interruzione della richiesta di trasferimento dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1289">This event represents a USBX Device Stack Transfer All Request Abort Event.</span></span>

<span data-ttu-id="5cc78-1290">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1290">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1291">Campo informazioni 1: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1291">Info Field 1: Endpoint.</span></span>
- <span data-ttu-id="5cc78-1292">Informazioni sul campo 2: codice di completamento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1292">Info Field 2: Completion code.</span></span>
- <span data-ttu-id="5cc78-1293">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1293">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1294">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1294">Info Field 4: Not used.</span></span>

### <a name="device-stack-transfer-request"></a><span data-ttu-id="5cc78-1295">Richiesta di trasferimento dello stack del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1295">Device Stack Transfer Request</span></span> 

#### <a name="ux_device_stack_transfer_request"></a><span data-ttu-id="5cc78-1296">ux_device_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="5cc78-1296">ux_device_stack_transfer_request</span></span>

<span data-ttu-id="5cc78-1297">**Icona** ![ di Icona della richiesta di trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image76.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1297">**Icon** ![Device Stack Transfer Request icon](./media/user-guide/usbx-events/image76.png)</span></span>

<span data-ttu-id="5cc78-1298">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1298">**Description**</span></span>

<span data-ttu-id="5cc78-1299">Questo evento rappresenta un evento di richiesta di trasferimento dello stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1299">This event represents a USBX Device Stack Transfer Request Event.</span></span>

<span data-ttu-id="5cc78-1300">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1300">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1301">Campo informazioni 1: richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1301">Info Field 1: Transfer request.</span></span>
- <span data-ttu-id="5cc78-1302">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1302">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1303">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1303">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1304">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1304">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-activate"></a><span data-ttu-id="5cc78-1305">Classe host ASIX Activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1305">Host Class Asix Activate</span></span> 

#### <a name="ux_host_class_asix_activate"></a><span data-ttu-id="5cc78-1306">ux_host_class_asix_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1306">ux_host_class_asix_activate</span></span>

<span data-ttu-id="5cc78-1307">**Icona** ![ di Icona di attivazione della classe host ASIX](./media/user-guide/usbx-events/image77.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1307">**Icon** ![Host Class Asix Activate icon](./media/user-guide/usbx-events/image77.png)</span></span>

<span data-ttu-id="5cc78-1308">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1308">**Description**</span></span>

<span data-ttu-id="5cc78-1309">Questo evento rappresenta una classe host USBX ASIX Activate.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1309">This event represents a USBX Host Class Asix Activate.</span></span>

<span data-ttu-id="5cc78-1310">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1310">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1311">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1311">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1312">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1312">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1313">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1313">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1314">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1314">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-deactivate"></a><span data-ttu-id="5cc78-1315">Classe host ASIX disattivare</span><span class="sxs-lookup"><span data-stu-id="5cc78-1315">Host Class Asix Deactivate</span></span> 

#### <a name="ux_host_class_asix_deactivate"></a><span data-ttu-id="5cc78-1316">ux_host_class_asix_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1316">ux_host_class_asix_deactivate</span></span>

<span data-ttu-id="5cc78-1317">**Icona** ![ di Icona ASIX della classe host disattiva](./media/user-guide/usbx-events/image78.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1317">**Icon** ![Host Class Asix Deactivate icon](./media/user-guide/usbx-events/image78.png)</span></span>

<span data-ttu-id="5cc78-1318">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1318">**Description**</span></span>

<span data-ttu-id="5cc78-1319">Questo evento rappresenta una classe host USBX ASIX disattivare un evento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1319">This event represents a USBX Host Class Asix Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1320">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1320">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1321">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1321">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1322">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1322">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1323">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1323">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1324">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1324">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-interrupt-notification"></a><span data-ttu-id="5cc78-1325">Notifica di interrupt della classe host ASIX</span><span class="sxs-lookup"><span data-stu-id="5cc78-1325">Host Class Asix Interrupt Notification</span></span> 

#### <a name="ux_host_class_asix_interrupt_notification"></a><span data-ttu-id="5cc78-1326">ux_host_class_asix_interrupt_notification</span><span class="sxs-lookup"><span data-stu-id="5cc78-1326">ux_host_class_asix_interrupt_notification</span></span>

<span data-ttu-id="5cc78-1327">**Icona** ![ di Icona della notifica di interrupt della classe host ASIX](./media/user-guide/usbx-events/image79.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1327">**Icon** ![Host Class Asix Interrupt Notification icon](./media/user-guide/usbx-events/image79.png)</span></span>

<span data-ttu-id="5cc78-1328">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1328">**Description**</span></span>

<span data-ttu-id="5cc78-1329">Questo evento rappresenta un evento di notifica di interrupt ASIX di classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1329">This event represents a USBX Host Class Asix Interrupt Notification Event.</span></span>

<span data-ttu-id="5cc78-1330">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1330">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1331">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1331">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-1332">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1332">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1333">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1333">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1334">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1334">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-read"></a><span data-ttu-id="5cc78-1335">Classe host ASIX Read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1335">Host Class Asix Read</span></span> 

#### <a name="ux_host_class_asix_read"></a><span data-ttu-id="5cc78-1336">ux_host_class_asix_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1336">ux_host_class_asix_read</span></span>

<span data-ttu-id="5cc78-1337">**Icona** ![ di Icona di lettura della classe host ASIX](./media/user-guide/usbx-events/image80.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1337">**Icon** ![Host Class Asix Read icon](./media/user-guide/usbx-events/image80.png)</span></span>

<span data-ttu-id="5cc78-1338">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1338">**Description**</span></span>

<span data-ttu-id="5cc78-1339">Questo evento rappresenta un evento di lettura ASIX della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1339">This event represents a USBX Host Class Asix Read Event.</span></span>

<span data-ttu-id="5cc78-1340">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1340">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1341">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1341">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1342">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1342">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1343">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1343">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-1344">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1344">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-write"></a><span data-ttu-id="5cc78-1345">Classe host ASIX Write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1345">Host Class Asix Write</span></span> 

#### <a name="ux_host_class_asix_write"></a><span data-ttu-id="5cc78-1346">ux_host_class_asix_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1346">ux_host_class_asix_write</span></span>

<span data-ttu-id="5cc78-1347">**Icona** ![ di Icona di scrittura della classe host ASIX](./media/user-guide/usbx-events/image81.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1347">**Icon** ![Host Class Asix Write icon](./media/user-guide/usbx-events/image81.png)</span></span>

<span data-ttu-id="5cc78-1348">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1348">**Description**</span></span>

<span data-ttu-id="5cc78-1349">Questo evento rappresenta un evento di scrittura ASIX della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1349">This event represents a USBX Host Class Asix Write Event.</span></span>

<span data-ttu-id="5cc78-1350">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1350">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1351">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1351">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1352">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1352">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1353">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1353">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-1354">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1354">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-activate"></a><span data-ttu-id="5cc78-1355">Attivazione audio classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1355">Host Class Audio Activate</span></span> 

#### <a name="ux_host_class_audio_activate"></a><span data-ttu-id="5cc78-1356">ux_host_class_audio_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1356">ux_host_class_audio_activate</span></span>

<span data-ttu-id="5cc78-1357">**Icona** ![ di Icona di attivazione dell'audio della classe host](./media/user-guide/usbx-events/image82.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1357">**Icon** ![Host Class Audio Activate icon](./media/user-guide/usbx-events/image82.png)</span></span>

<span data-ttu-id="5cc78-1358">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1358">**Description**</span></span>

<span data-ttu-id="5cc78-1359">Questo evento rappresenta un evento di attivazione audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1359">This event represents a USBX Host Class Audio Activate Event.</span></span>

<span data-ttu-id="5cc78-1360">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1360">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1361">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1361">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1362">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1362">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1363">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1363">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1364">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1364">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-control-value-get"></a><span data-ttu-id="5cc78-1365">Valore di controllo audio della classe host Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1365">Host Class Audio Control Value Get</span></span> 

#### <a name="ux_host_class_audio_control_value_get"></a><span data-ttu-id="5cc78-1366">ux_host_class_audio_control_value_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1366">ux_host_class_audio_control_value_get</span></span>

<span data-ttu-id="5cc78-1367">**Icona** ![ di Icona Get del valore del controllo audio della classe host](./media/user-guide/usbx-events/image83.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1367">**Icon** ![Host Class Audio Control Value Get icon](./media/user-guide/usbx-events/image83.png)</span></span>

<span data-ttu-id="5cc78-1368">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1368">**Description**</span></span>

<span data-ttu-id="5cc78-1369">Questo evento rappresenta un evento Get del valore di controllo audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1369">This event represents a USBX Host Class Audio Control Value Get Event.</span></span>

<span data-ttu-id="5cc78-1370">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1370">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1371">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1371">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1372">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1372">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1373">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1373">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1374">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1374">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-control-value-set"></a><span data-ttu-id="5cc78-1375">Valore del controllo audio della classe host impostato</span><span class="sxs-lookup"><span data-stu-id="5cc78-1375">Host Class Audio Control Value Set</span></span> 

#### <a name="ux_host_class_audio_control_value_set"></a><span data-ttu-id="5cc78-1376">ux_host_class_audio_control_value_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1376">ux_host_class_audio_control_value_set</span></span>

<span data-ttu-id="5cc78-1377">**Icona** ![ di Icona del set di valori del controllo audio della classe host](./media/user-guide/usbx-events/image84.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1377">**Icon** ![Host Class Audio Control Value Set icon](./media/user-guide/usbx-events/image84.png)</span></span>

<span data-ttu-id="5cc78-1378">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1378">**Description**</span></span>

<span data-ttu-id="5cc78-1379">Questo evento rappresenta un evento di elaborazione posticipato del driver di I/O NetX interno.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1379">This event represents an internal NetX I/O driver deferred processing event.</span></span>

<span data-ttu-id="5cc78-1380">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1380">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1381">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1381">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1382">Informazioni sul campo 2: controllo audio.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1382">Info Field 2: Audio control.</span></span>
- <span data-ttu-id="5cc78-1383">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1383">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1384">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1384">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-deactivate"></a><span data-ttu-id="5cc78-1385">Disattivazione audio della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1385">Host Class Audio Deactivate</span></span> 

#### <a name="ux_host_class_audio_deactivate"></a><span data-ttu-id="5cc78-1386">ux_host_class_audio_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1386">ux_host_class_audio_deactivate</span></span>

<span data-ttu-id="5cc78-1387">**Icona** ![ di Icona di disattivazione audio della classe host](./media/user-guide/usbx-events/image85.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1387">**Icon** ![Host Class Audio Deactivate icon](./media/user-guide/usbx-events/image85.png)</span></span>

<span data-ttu-id="5cc78-1388">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1388">**Description**</span></span>

<span data-ttu-id="5cc78-1389">Questo evento rappresenta un evento di disattivazione audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1389">This event represents a USBX Host Class Audio Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1390">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1390">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1391">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1391">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1392">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1392">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1393">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1393">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1394">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1394">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-read"></a><span data-ttu-id="5cc78-1395">Lettura audio classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1395">Host Class Audio Read</span></span> 

#### <a name="ux_host_class_audio_read"></a><span data-ttu-id="5cc78-1396">ux_host_class_audio_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1396">ux_host_class_audio_read</span></span>

<span data-ttu-id="5cc78-1397">**Icona** ![ di Icona di lettura audio della classe host](./media/user-guide/usbx-events/image86.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1397">**Icon** ![Host Class Audio Read icon](./media/user-guide/usbx-events/image86.png)</span></span>

<span data-ttu-id="5cc78-1398">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1398">**Description**</span></span>

<span data-ttu-id="5cc78-1399">Questo evento rappresenta un evento di lettura audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1399">This event represents a USBX Host Class Audio Read Event.</span></span>

- <span data-ttu-id="5cc78-1400">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="5cc78-1400">Information Fields</span></span> 
- <span data-ttu-id="5cc78-1401">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1401">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1402">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1402">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1403">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1403">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-1404">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1404">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-streaming-sampling-get"></a><span data-ttu-id="5cc78-1405">Raccolta di campionamento flusso audio della classe host Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1405">Host Class Audio Streaming Sampling Get</span></span> 

#### <a name="ux_host_class_audio_streaming_sampling_get"></a><span data-ttu-id="5cc78-1406">ux_host_class_audio_streaming_sampling_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1406">ux_host_class_audio_streaming_sampling_get</span></span>

<span data-ttu-id="5cc78-1407">**Icona** ![ di Icona di Get del campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image87.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1407">**Icon** ![Host Class Audio Streaming Sampling Get icon](./media/user-guide/usbx-events/image87.png)</span></span>

<span data-ttu-id="5cc78-1408">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1408">**Description**</span></span>

<span data-ttu-id="5cc78-1409">Questo evento rappresenta un evento di ottenimento del campionamento del flusso audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1409">This event represents a USBX Host Class Audio Streaming Sampling Get Event.</span></span>

<span data-ttu-id="5cc78-1410">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1410">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1411">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1411">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1412">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1412">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1413">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1413">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1414">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1414">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-streaming-sampling-set"></a><span data-ttu-id="5cc78-1415">Set di campionamento del flusso audio della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1415">Host Class Audio Streaming Sampling Set</span></span> 

#### <a name="ux_host_class_audio_streaming_sampling_set"></a><span data-ttu-id="5cc78-1416">ux_host_class_audio_streaming_sampling_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1416">ux_host_class_audio_streaming_sampling_set</span></span>

<span data-ttu-id="5cc78-1417">**Icona** ![ di Icona del set di campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image88.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1417">**Icon** ![Host Class Audio Streaming Sampling Set icon](./media/user-guide/usbx-events/image88.png)</span></span>

<span data-ttu-id="5cc78-1418">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1418">**Description**</span></span>

<span data-ttu-id="5cc78-1419">Questo evento rappresenta un evento del set di campionamento di flusso audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1419">This event represents a USBX Host Class Audio Streaming Sampling Set Event.</span></span>

<span data-ttu-id="5cc78-1420">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1420">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1421">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1421">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1422">Informazioni sul campo 2: campionamento audio.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1422">Info Field 2: Audio Sampling.</span></span>
- <span data-ttu-id="5cc78-1423">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1423">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1424">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1424">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-write"></a><span data-ttu-id="5cc78-1425">Scrittura audio della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1425">Host Class Audio Write</span></span> 

#### <a name="ux_host_class_audio_write"></a><span data-ttu-id="5cc78-1426">ux_host_class_audio_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1426">ux_host_class_audio_write</span></span>

<span data-ttu-id="5cc78-1427">**Icona** ![ di Icona di scrittura audio della classe host](./media/user-guide/usbx-events/image89.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1427">**Icon** ![Host Class Audio Write icon](./media/user-guide/usbx-events/image89.png)</span></span>

<span data-ttu-id="5cc78-1428">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1428">**Description**</span></span>

<span data-ttu-id="5cc78-1429">Questo evento rappresenta un evento di scrittura audio della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1429">This event represents a USBX Host Class Audio Write Event.</span></span>

<span data-ttu-id="5cc78-1430">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1430">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1431">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1431">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1432">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1432">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1433">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1433">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-1434">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1434">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-activate"></a><span data-ttu-id="5cc78-1435">Classe host CDC ACM Activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1435">Host Class Cdc Acm Activate</span></span> 

#### <a name="ux_host_class_cdc_acm_activate"></a><span data-ttu-id="5cc78-1436">ux_host_class_cdc_acm_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1436">ux_host_class_cdc_acm_activate</span></span>

<span data-ttu-id="5cc78-1437">**Icona** ![ di Icona di attivazione della classe host C D C A C M](./media/user-guide/usbx-events/image90.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1437">**Icon** ![Host Class C D C A C M Activate icon](./media/user-guide/usbx-events/image90.png)</span></span>

<span data-ttu-id="5cc78-1438">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1438">**Description**</span></span>

<span data-ttu-id="5cc78-1439">Questo evento rappresenta una classe host USBX CDC ACM Activate Event.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1439">This event represents a USBX Host Class Cdc Acm Activate Event.</span></span>

<span data-ttu-id="5cc78-1440">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1440">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1441">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1441">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1442">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1442">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1443">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1443">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1444">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1444">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-deactivate"></a><span data-ttu-id="5cc78-1445">Classe host CDC ACM Deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1445">Host Class Cdc Acm Deactivate</span></span> 

#### <a name="ux_host_class_cdc_acm_deactivate"></a><span data-ttu-id="5cc78-1446">ux_host_class_cdc_acm_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1446">ux_host_class_cdc_acm_deactivate</span></span>

<span data-ttu-id="5cc78-1447">**Icona** ![ di Classe host C D C A C M icona di disattivazione](./media/user-guide/usbx-events/image91.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1447">**Icon** ![Host Class C D C A C M Deactivate icon](./media/user-guide/usbx-events/image91.png)</span></span>

<span data-ttu-id="5cc78-1448">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1448">**Description**</span></span>

<span data-ttu-id="5cc78-1449">Questo evento rappresenta una classe host USBX CDC ACM Deactivate event.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1449">This event represents a USBX Host Class Cdc Acm Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1450">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1450">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1451">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1451">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1452">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1452">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1453">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1453">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1454">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1454">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-abort-in-pipe"></a><span data-ttu-id="5cc78-1455">Classe host CDC per l'interruzione IOCTL ACM nella pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-1455">Host Class Cdc Acm Ioctl Abort In Pipe</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_abort_in_pipe"></a><span data-ttu-id="5cc78-1456">ux_host_class_cdc_acm_ioctl_abort_in_pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-1456">ux_host_class_cdc_acm_ioctl_abort_in_pipe</span></span>

<span data-ttu-id="5cc78-1457">**Icona** ![ di Classe host C D C A C M I O C T L interruzione nell'icona pipe](./media/user-guide/usbx-events/image92.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1457">**Icon** ![Host Class C D C A C M I O C T L Abort In Pipe icon](./media/user-guide/usbx-events/image92.png)</span></span>

<span data-ttu-id="5cc78-1458">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1458">**Description**</span></span>

<span data-ttu-id="5cc78-1459">Questo evento rappresenta una classe host USBX CDC ACM IOCTL Abort nell'evento pipe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1459">This event represents a USBX Host Class Cdc Acm Ioctl Abort In Pipe Event.</span></span>

<span data-ttu-id="5cc78-1460">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="5cc78-1460">Information Fields</span></span> 

- <span data-ttu-id="5cc78-1461">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1461">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1462">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1462">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-1463">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1463">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1464">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1464">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-abort-out-pipe"></a><span data-ttu-id="5cc78-1465">Classe host CDC ACM ACM Interrompi pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-1465">Host Class Cdc Acm Ioctl Abort Out Pipe</span></span> 

#### <a name="ux_host_class_cdc_acm_ioct_abort_out_pipe"></a><span data-ttu-id="5cc78-1466">ux_host_class_cdc_acm_ioct_abort_out_pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-1466">ux_host_class_cdc_acm_ioct_abort_out_pipe</span></span>

<span data-ttu-id="5cc78-1467">**Icona** ! [[Classe host c D c A c M I O c T L pulsante Interrompi barra verticale](./media/user-guide/usbx-events/image93.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1467">**Icon** ![[Host Class C D C A C M I O C T L Abort Out Pipe icon](./media/user-guide/usbx-events/image93.png)</span></span>

<span data-ttu-id="5cc78-1468">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1468">**Description**</span></span>

<span data-ttu-id="5cc78-1469">Questo evento rappresenta una classe host USBX CDC ACM IOCTL Interrompi pipe evento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1469">This event represents a USBX Host Class Cdc Acm Ioctl Abort Out Pipe Event.</span></span>

<span data-ttu-id="5cc78-1470">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1470">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1471">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1471">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1472">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1472">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-1473">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1473">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1474">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1474">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-get-device-status"></a><span data-ttu-id="5cc78-1475">Classe host CDC ACM per l'ottenimento dello stato del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1475">Host Class Cdc Acm Ioctl Get Device Status</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_get_device_status"></a><span data-ttu-id="5cc78-1476">ux_host_class_cdc_acm_ioctl_get_device_status</span><span class="sxs-lookup"><span data-stu-id="5cc78-1476">ux_host_class_cdc_acm_ioctl_get_device_status</span></span>

<span data-ttu-id="5cc78-1477">**Icona** ![ di Classe host C D C A C M I O C T L icona di stato del dispositivo Get](./media/user-guide/usbx-events/image94.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1477">**Icon** ![Host Class C D C A C M I O C T L Get Device Status icon](./media/user-guide/usbx-events/image94.png)</span></span>

<span data-ttu-id="5cc78-1478">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1478">**Description**</span></span>

<span data-ttu-id="5cc78-1479">Questo evento rappresenta una classe host USBX CDC ACM IOCTL Get Device Status Event.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1479">This event represents a USBX Host Class Cdc Acm Ioctl Get Device Status Event.</span></span>

<span data-ttu-id="5cc78-1480">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1480">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1481">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1481">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1482">Informazioni sul campo 2: stato del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1482">Info Field 2: Device status.</span></span>
- <span data-ttu-id="5cc78-1483">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1483">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1484">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1484">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-get-line-coding"></a><span data-ttu-id="5cc78-1485">Classe host CDC ACM per ottenere la codifica della riga</span><span class="sxs-lookup"><span data-stu-id="5cc78-1485">Host Class Cdc Acm Ioctl Get Line Coding</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_get_line_coding"></a><span data-ttu-id="5cc78-1486">ux_host_class_cdc_acm_ioctl_get_line_coding</span><span class="sxs-lookup"><span data-stu-id="5cc78-1486">ux_host_class_cdc_acm_ioctl_get_line_coding</span></span>

<span data-ttu-id="5cc78-1487">**Icona** ![ di Classe host C D C A C M I O C T L ottenere l'icona di codifica della riga](./media/user-guide/usbx-events/image95.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1487">**Icon** ![Host Class C D C A C M I O C T L Get Line Coding icon](./media/user-guide/usbx-events/image95.png)</span></span>

<span data-ttu-id="5cc78-1488">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1488">**Description**</span></span>

<span data-ttu-id="5cc78-1489">Questo evento rappresenta una classe host USBX CDC ACM per l'evento di codifica della riga.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1489">This event represents a USBX Host Class Cdc Acm Ioctl Get Line Coding Event.</span></span>

<span data-ttu-id="5cc78-1490">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1490">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1491">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1491">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1492">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1492">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-1493">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1493">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1494">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1494">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-notification-callback"></a><span data-ttu-id="5cc78-1495">Callback delle notifiche IOCTL di classe host CDC ACM</span><span class="sxs-lookup"><span data-stu-id="5cc78-1495">Host Class Cdc Acm Ioctl Notification Callback</span></span>

#### <a name="ux_host_class_cdc_acm_ioctl_notification_callback"></a><span data-ttu-id="5cc78-1496">ux_host_class_cdc_acm_ioctl_notification_callback</span><span class="sxs-lookup"><span data-stu-id="5cc78-1496">ux_host_class_cdc_acm_ioctl_notification_callback</span></span>

<span data-ttu-id="5cc78-1497">**Icona** ![ di Classe host C D C A C M I O C T L icona di callback di notifica](./media/user-guide/usbx-events/image96.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1497">**Icon** ![Host Class C D C A C M I O C T L Notification Callback icon](./media/user-guide/usbx-events/image96.png)</span></span>

<span data-ttu-id="5cc78-1498">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1498">**Description**</span></span>

<span data-ttu-id="5cc78-1499">Questo evento rappresenta una classe host USBX CDC ACM, evento di callback di notifica IOCTL.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1499">This event represents a USBX Host Class Cdc Acm Ioctl Notification Callback Event.</span></span>

<span data-ttu-id="5cc78-1500">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1500">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1501">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1501">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1502">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1502">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-1503">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1503">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1504">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1504">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-send-break"></a><span data-ttu-id="5cc78-1505">Classe host CDC ACM di invio-Interrompi</span><span class="sxs-lookup"><span data-stu-id="5cc78-1505">Host Class Cdc Acm Ioctl Send Break</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_send_break"></a><span data-ttu-id="5cc78-1506">ux_host_class_cdc_acm_ioctl_send_break</span><span class="sxs-lookup"><span data-stu-id="5cc78-1506">ux_host_class_cdc_acm_ioctl_send_break</span></span>

<span data-ttu-id="5cc78-1507">**Icona** ![ di Classe host C D C A C M I O C T L invio icona di interruzioni](./media/user-guide/usbx-events/image97.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1507">**Icon** ![Host Class C D C A C M I O C T L Send Break icon](./media/user-guide/usbx-events/image97.png)</span></span>

<span data-ttu-id="5cc78-1508">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1508">**Description**</span></span>

<span data-ttu-id="5cc78-1509">Questo evento rappresenta una classe host USBX CDC ACM di invio di un evento di rottura.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1509">This event represents a USBX Host Class Cdc Acm Ioctl Send Break Event.</span></span>

<span data-ttu-id="5cc78-1510">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1510">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1511">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1511">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1512">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1512">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-1513">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1513">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1514">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1514">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-set-line-coding"></a><span data-ttu-id="5cc78-1515">Codifica della riga set IOCTL di classe host CDC ACM</span><span class="sxs-lookup"><span data-stu-id="5cc78-1515">Host Class Cdc Acm Ioctl Set Line Coding</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_coding"></a><span data-ttu-id="5cc78-1516">ux_host_class_cdc_acm_ioctl_set_line_coding</span><span class="sxs-lookup"><span data-stu-id="5cc78-1516">ux_host_class_cdc_acm_ioctl_set_line_coding</span></span>

<span data-ttu-id="5cc78-1517">**Icona** ![ di La classe host C D C A C M I O C T L impostare l'icona dell'icona di codifica della riga ](./media/user-guide/usbx-events/image97.png) ] (./media/user-guide/usbx-events/image98.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1517">**Icon** ![The Host Class C D C A C M I O C T L Set Line Coding icon](./media/user-guide/usbx-events/image97.png) icon](./media/user-guide/usbx-events/image98.png)</span></span>

<span data-ttu-id="5cc78-1518">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1518">**Description**</span></span>

<span data-ttu-id="5cc78-1519">Questo evento rappresenta una classe host USBX CDC ACM per set di codifica della riga.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1519">This event represents a USBX Host Class Cdc Acm Ioctl Set Line Coding Event.</span></span>

<span data-ttu-id="5cc78-1520">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1520">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1521">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1521">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1522">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1522">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-1523">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1523">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1524">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1524">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-set-line-state"></a><span data-ttu-id="5cc78-1525">Stato della riga set IOCTL di classe host CDC ACM</span><span class="sxs-lookup"><span data-stu-id="5cc78-1525">Host Class Cdc Acm Ioctl Set Line State</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_state"></a><span data-ttu-id="5cc78-1526">ux_host_class_cdc_acm_ioctl_set_line_state</span><span class="sxs-lookup"><span data-stu-id="5cc78-1526">ux_host_class_cdc_acm_ioctl_set_line_state</span></span>

<span data-ttu-id="5cc78-1527">**Icona** ![ di Classe host C D C A C M I O C T L impostare lo stato della riga icona](./media/user-guide/usbx-events/image99.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1527">**Icon** ![Host Class C D C A C M I O C T L Set Line State icon](./media/user-guide/usbx-events/image99.png)</span></span>

<span data-ttu-id="5cc78-1528">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1528">**Description**</span></span>

<span data-ttu-id="5cc78-1529">Questo evento rappresenta un evento di stato della riga set di linee di USBX di classe host CDC ACM.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1529">This event represents a USBX Host Class Cdc Acm Ioctl Set Line State Event.</span></span>

<span data-ttu-id="5cc78-1530">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1530">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1531">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1531">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1532">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1532">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-1533">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1533">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1534">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1534">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-read"></a><span data-ttu-id="5cc78-1535">Classe host CDC ACM Read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1535">Host Class Cdc Acm Read</span></span> 

#### <a name="ux_host_class_cdc_acm_read"></a><span data-ttu-id="5cc78-1536">ux_host_class_cdc_acm_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1536">ux_host_class_cdc_acm_read</span></span>

<span data-ttu-id="5cc78-1537">**Icona** ![ di Icona di lettura c M di classe host c D](./media/user-guide/usbx-events/image100.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1537">**Icon** ![Host Class C D C A C M Read icon](./media/user-guide/usbx-events/image100.png)</span></span>

<span data-ttu-id="5cc78-1538">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1538">**Description**</span></span>

<span data-ttu-id="5cc78-1539">Questo evento rappresenta una classe host USBX, un evento di lettura di CDC ACM.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1539">This event represents a USBX Host Class Cdc Acm Read Event.</span></span>

<span data-ttu-id="5cc78-1540">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1540">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1541">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1541">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1542">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1542">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1543">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1543">Info Field 3: Requested Length.</span></span>
- <span data-ttu-id="5cc78-1544">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1544">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-reception-start"></a><span data-ttu-id="5cc78-1545">Classe host CDC ACM reception Start</span><span class="sxs-lookup"><span data-stu-id="5cc78-1545">Host Class Cdc Acm Reception Start</span></span> 

#### <a name="ux_host_class_cdc_acm_reception_start"></a><span data-ttu-id="5cc78-1546">ux_host_class_cdc_acm_reception_start</span><span class="sxs-lookup"><span data-stu-id="5cc78-1546">ux_host_class_cdc_acm_reception_start</span></span>

<span data-ttu-id="5cc78-1547">**Icona** ![ di Icona di avvio della ricezione c M della classe host C D C](./media/user-guide/usbx-events/image101.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1547">**Icon** ![Host Class C D C A C M Reception Start icon](./media/user-guide/usbx-events/image101.png)</span></span>

<span data-ttu-id="5cc78-1548">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1548">**Description**</span></span>

<span data-ttu-id="5cc78-1549">Questo evento rappresenta un evento di avvio della ricezione USBX di CDC ACM di classe host.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1549">This event represents a USBX Host Class Cdc Acm Reception Start Event.</span></span>

<span data-ttu-id="5cc78-1550">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1550">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1551">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1551">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1552">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1552">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1553">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1553">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1554">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1554">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-reception-stop"></a><span data-ttu-id="5cc78-1555">Arresto della ricezione della classe host CDC ACM</span><span class="sxs-lookup"><span data-stu-id="5cc78-1555">Host Class Cdc Acm Reception Stop</span></span> 

#### <a name="ux_host_class_cdc_acm_reception_stop"></a><span data-ttu-id="5cc78-1556">ux_host_class_cdc_acm_reception_stop</span><span class="sxs-lookup"><span data-stu-id="5cc78-1556">ux_host_class_cdc_acm_reception_stop</span></span>

<span data-ttu-id="5cc78-1557">**Icona** ![ di Icona di arresto della ricezione c M per la classe host C D C](./media/user-guide/usbx-events/image102.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1557">**Icon** ![Host Class C D C A C M Reception Stop icon](./media/user-guide/usbx-events/image102.png)</span></span>

<span data-ttu-id="5cc78-1558">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1558">**Description**</span></span>

<span data-ttu-id="5cc78-1559">Questo evento rappresenta una classe host USBX CDC ACM reception Event stop.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1559">This event represents a USBX Host Class Cdc Acm Reception Stop Event.</span></span>

<span data-ttu-id="5cc78-1560">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1560">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1561">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1561">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1562">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1562">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1563">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1563">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-write"></a><span data-ttu-id="5cc78-1564">Classe host CDC ACM Write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1564">Host Class Cdc Acm Write</span></span> 

#### <a name="ux_host_class_acm_write"></a><span data-ttu-id="5cc78-1565">ux_host_class_acm_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1565">ux_host_class_acm_write</span></span>

<span data-ttu-id="5cc78-1566">**Icona** ![ di Icona di scrittura della classe host C D C A C M](./media/user-guide/usbx-events/image103.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1566">**Icon** ![Host Class C D C A C M Write icon](./media/user-guide/usbx-events/image103.png)</span></span>

<span data-ttu-id="5cc78-1567">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1567">**Description**</span></span>

<span data-ttu-id="5cc78-1568">Questo evento rappresenta una classe host USBX CDC ACM Write Event.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1568">This event represents a USBX Host Class Cdc Acm Write Event.</span></span>

<span data-ttu-id="5cc78-1569">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1569">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1570">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1570">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1571">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1571">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1572">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1572">Info Field 3: Requested Length.</span></span>
- <span data-ttu-id="5cc78-1573">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1573">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-activate"></a><span data-ttu-id="5cc78-1574">Classe host DPUMP Activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1574">Host Class Dpump Activate</span></span> 

#### <a name="ux_host_class_dpump_activate"></a><span data-ttu-id="5cc78-1575">ux_host_class_dpump_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1575">ux_host_class_dpump_activate</span></span>

<span data-ttu-id="5cc78-1576">**Icona** ![ di Icona di attivazione della classe host DPUMP](./media/user-guide/usbx-events/image104.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1576">**Icon** ![Host Class Dpump Activate icon](./media/user-guide/usbx-events/image104.png)</span></span>

<span data-ttu-id="5cc78-1577">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1577">**Description**</span></span>

<span data-ttu-id="5cc78-1578">Questo evento rappresenta un evento DPUMP Activate della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1578">This event represents a USBX Host Class Dpump Activate Event.</span></span>

<span data-ttu-id="5cc78-1579">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1579">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1580">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1580">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1581">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1581">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1582">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1582">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1583">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1583">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-deactivate"></a><span data-ttu-id="5cc78-1584">Classe host DPUMP disattivare</span><span class="sxs-lookup"><span data-stu-id="5cc78-1584">Host Class Dpump Deactivate</span></span> 

#### <a name="ux_host_class_dpump_deactivate"></a><span data-ttu-id="5cc78-1585">ux_host_class_dpump_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1585">ux_host_class_dpump_deactivate</span></span>

<span data-ttu-id="5cc78-1586">**Icona** ![ di Icona DPUMP della classe host disattiva](./media/user-guide/usbx-events/image105.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1586">**Icon** ![Host Class Dpump Deactivate icon](./media/user-guide/usbx-events/image105.png)</span></span>

<span data-ttu-id="5cc78-1587">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1587">**Description**</span></span>

<span data-ttu-id="5cc78-1588">Questo evento rappresenta una classe host USBX DPUMP disattivare un evento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1588">This event represents a USBX Host Class Dpump Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1589">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1589">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1590">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1590">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1591">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1591">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1592">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1592">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1593">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1593">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-read"></a><span data-ttu-id="5cc78-1594">Classe host DPUMP Read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1594">Host Class Dpump Read</span></span> 

#### <a name="ux_host_class_dpump_read"></a><span data-ttu-id="5cc78-1595">ux_host_class_dpump_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1595">ux_host_class_dpump_read</span></span>

<span data-ttu-id="5cc78-1596">**Icona** ![ di Icona di lettura della classe host DPUMP](./media/user-guide/usbx-events/image106.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1596">**Icon** ![Host Class Dpump Read icon](./media/user-guide/usbx-events/image106.png)</span></span>

<span data-ttu-id="5cc78-1597">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1597">**Description**</span></span>

<span data-ttu-id="5cc78-1598">Questo evento rappresenta un evento di lettura DPUMP della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1598">This event represents a USBX Host Class Dpump Read Event.</span></span>

<span data-ttu-id="5cc78-1599">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1599">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1600">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1600">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1601">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1601">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1602">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1602">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-1603">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1603">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-write"></a><span data-ttu-id="5cc78-1604">Classe host DPUMP Write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1604">Host Class Dpump Write</span></span> 

#### <a name="ux_host_class_dpump_write"></a><span data-ttu-id="5cc78-1605">ux_host_class_dpump_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-1605">ux_host_class_dpump_write</span></span>

<span data-ttu-id="5cc78-1606">**Icona** ![ di Icona di scrittura della classe host DPUMP](./media/user-guide/usbx-events/image107.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1606">**Icon** ![Host Class Dpump Write icon](./media/user-guide/usbx-events/image107.png)</span></span>

<span data-ttu-id="5cc78-1607">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1607">**Description**</span></span>

<span data-ttu-id="5cc78-1608">Questo evento rappresenta un evento di scrittura DPUMP della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1608">This event represents a USBX Host Class Dpump Write Event.</span></span>

<span data-ttu-id="5cc78-1609">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1609">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1610">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1610">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1611">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1611">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1612">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1612">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-1613">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1613">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-activate"></a><span data-ttu-id="5cc78-1614">Attivazione HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1614">Host Class Hid Activate</span></span> 

#### <a name="ux_host_class_hid_activate"></a><span data-ttu-id="5cc78-1615">ux_host_class_hid_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1615">ux_host_class_hid_activate</span></span>

<span data-ttu-id="5cc78-1616">**Icona** ![ di Icona di attivazione HID della classe host](./media/user-guide/usbx-events/image108.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1616">**Icon** ![Host Class Hid Activate icon](./media/user-guide/usbx-events/image108.png)</span></span>

<span data-ttu-id="5cc78-1617">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1617">**Description**</span></span>

<span data-ttu-id="5cc78-1618">Questo evento rappresenta un evento di attivazione HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1618">This event represents a USBX Host Class Hid Activate Event.</span></span>

<span data-ttu-id="5cc78-1619">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1619">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1620">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1620">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1621">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1621">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1622">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1622">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1623">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1623">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-client-register"></a><span data-ttu-id="5cc78-1624">Registro del client HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1624">Host Class Hid Client Register</span></span> 

#### <a name="ux_host_class_hid_client_register"></a><span data-ttu-id="5cc78-1625">ux_host_class_hid_client_register</span><span class="sxs-lookup"><span data-stu-id="5cc78-1625">ux_host_class_hid_client_register</span></span>

<span data-ttu-id="5cc78-1626">**Icona** ![ di Icona di registro del client HID della classe host](./media/user-guide/usbx-events/image109.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1626">**Icon** ![Host Class Hid Client Register icon](./media/user-guide/usbx-events/image109.png)</span></span>

<span data-ttu-id="5cc78-1627">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1627">**Description**</span></span>

<span data-ttu-id="5cc78-1628">Questo evento rappresenta un evento di registrazione del client HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1628">This event represents a USBX Host Class Hid Client Register Event.</span></span>

<span data-ttu-id="5cc78-1629">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1629">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1630">Campo informazioni 1: nome client nascosto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1630">Info Field 1: Hid client name.</span></span>
- <span data-ttu-id="5cc78-1631">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1631">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1632">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1632">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1633">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1633">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-deactivate"></a><span data-ttu-id="5cc78-1634">Disattivazione HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1634">Host Class Hid Deactivate</span></span> 

#### <a name="ux_host_class_hid_deactivate"></a><span data-ttu-id="5cc78-1635">ux_host_class_hid_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1635">ux_host_class_hid_deactivate</span></span>

<span data-ttu-id="5cc78-1636">**Icona** ![ di Icona di disattivazione HID della classe host](./media/user-guide/usbx-events/image110.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1636">**Icon** ![Host Class Hid Deactivate icon](./media/user-guide/usbx-events/image110.png)</span></span>

<span data-ttu-id="5cc78-1637">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1637">**Description**</span></span>

<span data-ttu-id="5cc78-1638">Questo evento rappresenta un evento di disattivazione HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1638">This event represents a USBX Host Class Hid Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1639">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1639">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1640">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1640">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1641">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1641">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1642">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1642">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1643">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1643">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-idle-get"></a><span data-ttu-id="5cc78-1644">Classe host HID Idle Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1644">Host Class Hid Idle Get</span></span> 

#### <a name="ux_host_class_hid_idle_get"></a><span data-ttu-id="5cc78-1645">ux_host_class_hid_idle_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1645">ux_host_class_hid_idle_get</span></span>

<span data-ttu-id="5cc78-1646">**Icona** ![ di Icona della classe host HID Idle Get](./media/user-guide/usbx-events/image111.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1646">**Icon** ![Host Class Hid Idle Get icon](./media/user-guide/usbx-events/image111.png)</span></span>

<span data-ttu-id="5cc78-1647">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1647">**Description**</span></span>

<span data-ttu-id="5cc78-1648">Questo evento rappresenta una classe host USBX. evento di Get inattivo HID.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1648">This event represents a USBX Host Class Hid Idle Get Event.</span></span>

<span data-ttu-id="5cc78-1649">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1649">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1650">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1650">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1651">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1651">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1652">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1652">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1653">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1653">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-idle-set"></a><span data-ttu-id="5cc78-1654">Set inattivo HID classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1654">Host Class Hid Idle Set</span></span> 

#### <a name="ux_host_class_hid_idle_set"></a><span data-ttu-id="5cc78-1655">ux_host_class_hid_idle_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1655">ux_host_class_hid_idle_set</span></span>

<span data-ttu-id="5cc78-1656">**Icona** ![ di Icona del set di inattività HID della classe host](./media/user-guide/usbx-events/image112.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1656">**Icon** ![Host Class Hid Idle Set icon](./media/user-guide/usbx-events/image112.png)</span></span>

<span data-ttu-id="5cc78-1657">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1657">**Description**</span></span>

<span data-ttu-id="5cc78-1658">Questo evento rappresenta un evento set inattivo HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1658">This event represents a USBX Host Class Hid Idle Set Event.</span></span>

<span data-ttu-id="5cc78-1659">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1659">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1660">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1660">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1661">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1661">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1662">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1662">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1663">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1663">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-keyboard-activate"></a><span data-ttu-id="5cc78-1664">Attivazione della tastiera HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1664">Host Class Hid Keyboard Activate</span></span> 

#### <a name="ux_host_class_hid_keyboard_activate"></a><span data-ttu-id="5cc78-1665">ux_host_class_hid_keyboard_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1665">ux_host_class_hid_keyboard_activate</span></span>

<span data-ttu-id="5cc78-1666">**Icona** ![ di Icona di attivazione della tastiera HID della classe host](./media/user-guide/usbx-events/image113.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1666">**Icon** ![Host Class Hid Keyboard Activate icon](./media/user-guide/usbx-events/image113.png)</span></span>

<span data-ttu-id="5cc78-1667">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1667">**Description**</span></span>

<span data-ttu-id="5cc78-1668">Questo evento rappresenta un evento di attivazione della tastiera HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1668">This event represents a USBX Host Class Hid Keyboard Activate Event.</span></span>

<span data-ttu-id="5cc78-1669">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1669">**Information Fields**</span></span>
<p><span data-ttu-id="5cc78-1670">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1670">Info Field 1: Class instance.</span></span>
<p><span data-ttu-id="5cc78-1671">Campo informazioni 2: istanza client nascosta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1671">Info Field 2: Hid client instance.</span></span>
<p><span data-ttu-id="5cc78-1672">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1672">Info Field 3: Not used.</span></span>
<p><span data-ttu-id="5cc78-1673">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1673">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-keyboard-deactivate"></a><span data-ttu-id="5cc78-1674">Disattiva la tastiera HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1674">Host Class Hid Keyboard Deactivate</span></span> 

#### <a name="ux_host_class_hid_keyboard_deactivate"></a><span data-ttu-id="5cc78-1675">ux_host_class_hid_keyboard_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1675">ux_host_class_hid_keyboard_deactivate</span></span>

<span data-ttu-id="5cc78-1676">**Icona** ![ di Icona di disattivazione tastiera HID della classe host](./media/user-guide/usbx-events/image114.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1676">**Icon** ![Host Class Hid Keyboard Deactivate icon](./media/user-guide/usbx-events/image114.png)</span></span>

<span data-ttu-id="5cc78-1677">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1677">**Description**</span></span>

<span data-ttu-id="5cc78-1678">Questo evento rappresenta un evento di disattivazione della tastiera HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1678">This event represents a USBX Host Class Hid Keyboard Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1679">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1679">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1680">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1680">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1681">Campo informazioni 2: istanza client nascosta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1681">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="5cc78-1682">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1682">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1683">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1683">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-mouse-activate"></a><span data-ttu-id="5cc78-1684">Attivazione mouse HID classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1684">Host Class Hid Mouse Activate</span></span> 

#### <a name="ux_host_class_hid_mouse_activate"></a><span data-ttu-id="5cc78-1685">ux_host_class_hid_mouse_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1685">ux_host_class_hid_mouse_activate</span></span>

<span data-ttu-id="5cc78-1686">**Icona** ![ di Icona di attivazione della classe host HID mouse](./media/user-guide/usbx-events/image115.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1686">**Icon** ![Host Class Hid Mouse Activate icon](./media/user-guide/usbx-events/image115.png)</span></span>

<span data-ttu-id="5cc78-1687">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1687">**Description**</span></span>

<span data-ttu-id="5cc78-1688">Questo evento rappresenta un evento di attivazione del mouse HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1688">This event represents a USBX Host Class Hid Mouse Activate Event.</span></span>

<span data-ttu-id="5cc78-1689">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1689">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1690">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1690">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1691">Campo informazioni 2: istanza client nascosta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1691">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="5cc78-1692">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1692">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1693">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1693">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-mouse-deactivate"></a><span data-ttu-id="5cc78-1694">Disattivazione del mouse della classe host HID</span><span class="sxs-lookup"><span data-stu-id="5cc78-1694">Host Class Hid Mouse Deactivate</span></span> 

#### <a name="ux_host_class_hid_mouse_deactivate"></a><span data-ttu-id="5cc78-1695">ux_host_class_hid_mouse_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1695">ux_host_class_hid_mouse_deactivate</span></span>

<span data-ttu-id="5cc78-1696">**Icona** ![ di Icona di disattivazione della classe host HID mouse](./media/user-guide/usbx-events/image116.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1696">**Icon** ![Host Class Hid Mouse Deactivate icon](./media/user-guide/usbx-events/image116.png)</span></span>

<span data-ttu-id="5cc78-1697">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1697">**Description**</span></span>

- <span data-ttu-id="5cc78-1698">Questo evento rappresenta un evento di deattivazione del mouse HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1698">This event represents a USBX Host Class Hid Mouse Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1699">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1699">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1700">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1700">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1701">Campo informazioni 2: istanza client nascosta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1701">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="5cc78-1702">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1702">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1703">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1703">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-remote-control-activate"></a><span data-ttu-id="5cc78-1704">Attivazione del controllo remoto HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1704">Host Class Hid Remote Control Activate</span></span> 

#### <a name="ux_host_class_hid_remote_control_activate"></a><span data-ttu-id="5cc78-1705">ux_host_class_hid_remote_control_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1705">ux_host_class_hid_remote_control_activate</span></span>

<span data-ttu-id="5cc78-1706">**Icona** ![ di Icona di attivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image117.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1706">**Icon** ![Host Class Hid Remote Control Activate icon](./media/user-guide/usbx-events/image117.png)</span></span>

<span data-ttu-id="5cc78-1707">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1707">**Description**</span></span>

<span data-ttu-id="5cc78-1708">Questo evento rappresenta un evento di attivazione del controllo remoto HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1708">This event represents a USBX Host Class Hid Remote Control Activate Event.</span></span>

<span data-ttu-id="5cc78-1709">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1709">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1710">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1710">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1711">Campo informazioni 2: istanza client nascosta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1711">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="5cc78-1712">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1712">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1713">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1713">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-remote-control-deactivate"></a><span data-ttu-id="5cc78-1714">Disattivazione del controllo remoto HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1714">Host Class Hid Remote Control Deactivate</span></span> 

#### <a name="ux_host_class_hid_remote_control_deactivate"></a><span data-ttu-id="5cc78-1715">ux_host_class_hid_remote_control_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1715">ux_host_class_hid_remote_control_deactivate</span></span>

<span data-ttu-id="5cc78-1716">**Icona** ![ di Icona di disattivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image118.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1716">**Icon** ![Host Class Hid Remote Control Deactivate icon](./media/user-guide/usbx-events/image118.png)</span></span>

<span data-ttu-id="5cc78-1717">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1717">**Description**</span></span>

<span data-ttu-id="5cc78-1718">Questo evento rappresenta un evento di disattivazione del controllo remoto HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1718">This event represents a USBX Host Class Hid Remote Control Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1719">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1719">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1720">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1720">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1721">Campo informazioni 2: istanza client nascosta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1721">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="5cc78-1722">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1722">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1723">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1723">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-report-get"></a><span data-ttu-id="5cc78-1724">Classe host-report HID</span><span class="sxs-lookup"><span data-stu-id="5cc78-1724">Host Class Hid Report Get</span></span> 

#### <a name="ux_host_class_hid_report_get"></a><span data-ttu-id="5cc78-1725">ux_host_class_hid_report_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1725">ux_host_class_hid_report_get</span></span>

<span data-ttu-id="5cc78-1726">**Icona** ![ di Icona di Get del report HID della classe host](./media/user-guide/usbx-events/image119.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1726">**Icon** ![Host Class Hid Report Get icon](./media/user-guide/usbx-events/image119.png)</span></span>

<span data-ttu-id="5cc78-1727">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1727">**Description**</span></span>

<span data-ttu-id="5cc78-1728">Questo evento rappresenta una classe host USBX di report HID.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1728">This event represents a USBX Host Class Hid Report Get.</span></span>

<span data-ttu-id="5cc78-1729">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1729">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1730">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1730">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1731">Campo informazioni 2: report client.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1731">Info Field 2: Client report.</span></span>
- <span data-ttu-id="5cc78-1732">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1732">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1733">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1733">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-report-set"></a><span data-ttu-id="5cc78-1734">Set di report HID della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1734">Host Class Hid Report Set</span></span> 

#### <a name="ux_host_class_hid_report_set"></a><span data-ttu-id="5cc78-1735">ux_host_class_hid_report_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-1735">ux_host_class_hid_report_set</span></span>

<span data-ttu-id="5cc78-1736">**Icona** ![ di Icona del set di report HID della classe host](./media/user-guide/usbx-events/image120.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1736">**Icon** ![Host Class Hid Report Set icon](./media/user-guide/usbx-events/image120.png)</span></span>

<span data-ttu-id="5cc78-1737">**Descrizione** di Questo evento rappresenta un set di report HID della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1737">**Description** This event represents a USBX Host Class Hid Report Set.</span></span>

<span data-ttu-id="5cc78-1738">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1738">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1739">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1739">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1740">Campo informazioni 2: report client.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1740">Info Field 2: Client report.</span></span>
- <span data-ttu-id="5cc78-1741">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1741">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1742">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1742">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-activate"></a><span data-ttu-id="5cc78-1743">Attivazione dell'hub classi host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1743">Host Class Hub Activate</span></span> 

#### <a name="ux_host_class_hub_activate"></a><span data-ttu-id="5cc78-1744">ux_host_class_hub_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1744">ux_host_class_hub_activate</span></span>

<span data-ttu-id="5cc78-1745">**Icona** ![ di Icona di attivazione dell'hub classe host](./media/user-guide/usbx-events/image121.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1745">**Icon** ![Host Class Hub Activate icon](./media/user-guide/usbx-events/image121.png)</span></span>

<span data-ttu-id="5cc78-1746">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1746">**Description**</span></span>

<span data-ttu-id="5cc78-1747">Questo evento rappresenta un evento di attivazione dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1747">This event represents a USBX Host Class Hub Activate Event.</span></span>

<span data-ttu-id="5cc78-1748">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1748">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-1749">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1749">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1750">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1750">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1751">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1751">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1752">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1752">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-change-detect"></a><span data-ttu-id="5cc78-1753">Rilevamento modifiche Hub classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1753">Host Class Hub Change Detect</span></span> 

#### <a name="ux_host_class_hub_change_detect"></a><span data-ttu-id="5cc78-1754">ux_host_class_hub_change_detect</span><span class="sxs-lookup"><span data-stu-id="5cc78-1754">ux_host_class_hub_change_detect</span></span>

<span data-ttu-id="5cc78-1755">**Icona** ![ di Icona rilevamento modifiche Hub classe host](./media/user-guide/usbx-events/image122.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1755">**Icon** ![Host Class Hub Change Detect icon](./media/user-guide/usbx-events/image122.png)</span></span>

<span data-ttu-id="5cc78-1756">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1756">**Description**</span></span>

<span data-ttu-id="5cc78-1757">Questo evento rappresenta un evento di rilevamento delle modifiche dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1757">This event represents a USBX Host Class Hub Change Detect Event.</span></span>

<span data-ttu-id="5cc78-1758">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1758">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1759">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1759">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1760">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1760">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1761">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1761">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1762">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1762">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-deactivate"></a><span data-ttu-id="5cc78-1763">Disattivazione dell'hub della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1763">Host Class Hub Deactivate</span></span> 

#### <a name="ux_host_class_hub_deactivate"></a><span data-ttu-id="5cc78-1764">ux_host_class_hub_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1764">ux_host_class_hub_deactivate</span></span>

<span data-ttu-id="5cc78-1765">**Icona** ![ di Icona di disattivazione dell'hub classe host](./media/user-guide/usbx-events/image123.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1765">**Icon** ![Host Class Hub Deactivate icon](./media/user-guide/usbx-events/image123.png)</span></span>

<span data-ttu-id="5cc78-1766">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1766">**Description**</span></span>

<span data-ttu-id="5cc78-1767">Questo evento rappresenta un evento di disattivazione dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1767">This event represents a USBX Host Class Hub Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1768">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1768">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1769">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1769">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1770">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1770">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1771">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1771">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1772">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1772">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-connection-process"></a><span data-ttu-id="5cc78-1773">Processo di connessione per la modifica della porta dell'hub classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1773">Host Class Hub Port Change Connection Process</span></span> 

#### <a name="ux_host_class_hub_change_connection_process"></a><span data-ttu-id="5cc78-1774">ux_host_class_hub_change_connection_process</span><span class="sxs-lookup"><span data-stu-id="5cc78-1774">ux_host_class_hub_change_connection_process</span></span>

<span data-ttu-id="5cc78-1775">**Icona** ![ di Icona del processo di connessione della porta dell'hub della classe host](./media/user-guide/usbx-events/image124.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1775">**Icon** ![Host Class Hub Port Change Connection Process icon](./media/user-guide/usbx-events/image124.png)</span></span>

<span data-ttu-id="5cc78-1776">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1776">**Description**</span></span>

<span data-ttu-id="5cc78-1777">Questo evento rappresenta un evento del processo di connessione di modifica della porta dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1777">This event represents a USBX Host Class Hub Port Change Connection Process Event.</span></span>

<span data-ttu-id="5cc78-1778">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1778">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1779">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1779">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1780">Informazioni sul campo 2: porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1780">Info Field 2: Port.</span></span>
- <span data-ttu-id="5cc78-1781">Informazioni sul campo 3: stato della porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1781">Info Field 3: Port status.</span></span>
- <span data-ttu-id="5cc78-1782">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1782">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-enable-process"></a><span data-ttu-id="5cc78-1783">Modifica della porta dell'hub della classe host Abilita processo</span><span class="sxs-lookup"><span data-stu-id="5cc78-1783">Host Class Hub Port Change Enable Process</span></span> 

#### <a name="ux_host_class_hub_port_change_enable_process"></a><span data-ttu-id="5cc78-1784">ux_host_class_hub_port_change_enable_process</span><span class="sxs-lookup"><span data-stu-id="5cc78-1784">ux_host_class_hub_port_change_enable_process</span></span>

<span data-ttu-id="5cc78-1785">**Icona** ![ di Icona di abilitazione del processo modifica porta hub classe host](./media/user-guide/usbx-events/image125.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1785">**Icon** ![Host Class Hub Port Change Enable Process icon](./media/user-guide/usbx-events/image125.png)</span></span>

<span data-ttu-id="5cc78-1786">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1786">**Description**</span></span>

<span data-ttu-id="5cc78-1787">Questo evento rappresenta un evento del processo di attivazione della porta dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1787">This event represents a USBX Host Class Hub Port Change Enable Process Event.</span></span>

<span data-ttu-id="5cc78-1788">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1788">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1789">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1789">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1790">Informazioni sul campo 2: porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1790">Info Field 2: Port.</span></span>
- <span data-ttu-id="5cc78-1791">Informazioni sul campo 3: stato della porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1791">Info Field 3: Port status.</span></span>
- <span data-ttu-id="5cc78-1792">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1792">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-over-current-process"></a><span data-ttu-id="5cc78-1793">Modifica della porta dell'hub della classe host per il processo corrente</span><span class="sxs-lookup"><span data-stu-id="5cc78-1793">Host Class Hub Port Change Over Current Process</span></span> 

#### <a name="ux_host_class_hub_port_change_over_current_process"></a><span data-ttu-id="5cc78-1794">ux_host_class_hub_port_change_over_current_process</span><span class="sxs-lookup"><span data-stu-id="5cc78-1794">ux_host_class_hub_port_change_over_current_process</span></span>

<span data-ttu-id="5cc78-1795">**Icona** ![ di Icona modifica porta hub classe host sull'icona del processo corrente](./media/user-guide/usbx-events/image126.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1795">**Icon** ![Host Class Hub Port Change Over Current Process icon](./media/user-guide/usbx-events/image126.png)</span></span>

<span data-ttu-id="5cc78-1796">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1796">**Description**</span></span>

<span data-ttu-id="5cc78-1797">Questo evento rappresenta l'allocazione di un pacchetto tramite nx_packet_allocate.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1797">This event represents allocating a packet via nx_packet_allocate.</span></span>

<span data-ttu-id="5cc78-1798">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1798">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1799">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1799">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1800">Informazioni sul campo 2: porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1800">Info Field 2: Port.</span></span>
- <span data-ttu-id="5cc78-1801">Informazioni sul campo 3: stato della porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1801">Info Field 3: Port status.</span></span>
- <span data-ttu-id="5cc78-1802">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1802">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-reset-process"></a><span data-ttu-id="5cc78-1803">Processo di reimpostazione della porta dell'hub della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1803">Host Class Hub Port Change Reset Process</span></span> 

#### <a name="ux_host_class_hub_port_change_reset_process"></a><span data-ttu-id="5cc78-1804">ux_host_class_hub_port_change_reset_process</span><span class="sxs-lookup"><span data-stu-id="5cc78-1804">ux_host_class_hub_port_change_reset_process</span></span>

<span data-ttu-id="5cc78-1805">**Icona** ![ di Icona del processo di reimpostazione della porta dell'hub della classe host](./media/user-guide/usbx-events/image127.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1805">**Icon** ![Host Class Hub Port Change Reset Process icon](./media/user-guide/usbx-events/image127.png)</span></span>

<span data-ttu-id="5cc78-1806">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1806">**Description**</span></span>

<span data-ttu-id="5cc78-1807">Questo evento rappresenta un evento del processo di reimpostazione della porta dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1807">This event represents a USBX Host Class Hub Port Change Reset Process Event.</span></span>

<span data-ttu-id="5cc78-1808">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1808">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1809">Campo informazioni 1: Hub.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1809">Info Field 1: Hub.</span></span> <span data-ttu-id="5cc78-1810">Informazioni sul campo 2: porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1810">Info Field 2: Port.</span></span>
- <span data-ttu-id="5cc78-1811">Informazioni sul campo 3: stato della porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1811">Info Field 3: Port status.</span></span>
- <span data-ttu-id="5cc78-1812">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1812">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-suspend-process"></a><span data-ttu-id="5cc78-1813">Processo di sospensione delle modifiche della porta dell'hub della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1813">Host Class Hub Port Change Suspend Process</span></span> 

#### <a name="ux_host_class_hub_port_change_suspend_process"></a><span data-ttu-id="5cc78-1814">ux_host_class_hub_port_change_suspend_process</span><span class="sxs-lookup"><span data-stu-id="5cc78-1814">ux_host_class_hub_port_change_suspend_process</span></span>

<span data-ttu-id="5cc78-1815">**Icona** ![ di Icona di sospensione del processo di modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image128.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1815">**Icon** ![Host Class Hub Port Change Suspend Process icon](./media/user-guide/usbx-events/image128.png)</span></span>

<span data-ttu-id="5cc78-1816">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1816">**Description**</span></span>

<span data-ttu-id="5cc78-1817">Questo evento rappresenta un evento di sospensione del processo di modifica della porta dell'hub della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1817">This event represents a USBX Host Class Hub Port Change Suspend Process Event.</span></span>

<span data-ttu-id="5cc78-1818">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1818">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1819">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1819">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1820">Informazioni sul campo 2: porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1820">Info Field 2: Port.</span></span>
- <span data-ttu-id="5cc78-1821">Informazioni sul campo 3: stato della porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1821">Info Field 3: Port status.</span></span>
- <span data-ttu-id="5cc78-1822">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1822">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-activate"></a><span data-ttu-id="5cc78-1823">Classe host Pima Activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1823">Host Class Pima Activate</span></span> 

#### <a name="ux_host_class_pima_activate"></a><span data-ttu-id="5cc78-1824">ux_host_class_pima_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1824">ux_host_class_pima_activate</span></span>

<span data-ttu-id="5cc78-1825">**Icona** ![ di Icona di attivazione della classe host Pima](./media/user-guide/usbx-events/image129.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1825">**Icon** ![Host Class Pima Activate icon](./media/user-guide/usbx-events/image129.png)</span></span>

<span data-ttu-id="5cc78-1826">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1826">**Description**</span></span>

<span data-ttu-id="5cc78-1827">Questo evento rappresenta un evento di attivazione Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1827">This event represents a USBX Host Class Pima Activate Event.</span></span>

<span data-ttu-id="5cc78-1828">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1828">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1829">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1829">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1830">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1830">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1831">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1831">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1832">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1832">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-deactivate"></a><span data-ttu-id="5cc78-1833">Classe host Pima Deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1833">Host Class Pima Deactivate</span></span> 

#### <a name="ux_host_class_pima_deactivate"></a><span data-ttu-id="5cc78-1834">ux_host_class_pima_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-1834">ux_host_class_pima_deactivate</span></span>

<span data-ttu-id="5cc78-1835">**Icona** ![ di Icona di disattivazione della classe host Pima](./media/user-guide/usbx-events/image130.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1835">**Icon** ![Host Class Pima Deactivate icon](./media/user-guide/usbx-events/image130.png)</span></span>

<span data-ttu-id="5cc78-1836">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1836">**Description**</span></span>

<span data-ttu-id="5cc78-1837">Questo evento rappresenta un evento di disattivazione Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1837">This event represents a USBX Host Class Pima Deactivate Event.</span></span>

<span data-ttu-id="5cc78-1838">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1838">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1839">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1839">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1840">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1840">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1841">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1841">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1842">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1842">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-device-info-get"></a><span data-ttu-id="5cc78-1843">Classe host informazioni sul dispositivo Pima Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1843">Host Class Pima Device Info Get</span></span> 

#### <a name="ux_host_class_pima_device_info_get"></a><span data-ttu-id="5cc78-1844">ux_host_class_pima_device_info_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1844">ux_host_class_pima_device_info_get</span></span>

<span data-ttu-id="5cc78-1845">**Icona** ![ di Icona di informazioni sul dispositivo Pima della classe host](./media/user-guide/usbx-events/image131.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1845">**Icon** ![Host Class Pima Device Info Get icon](./media/user-guide/usbx-events/image131.png)</span></span>

<span data-ttu-id="5cc78-1846">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1846">**Description**</span></span>

<span data-ttu-id="5cc78-1847">Questo evento rappresenta un evento di informazioni sul dispositivo Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1847">This event represents a USBX Host Class Pima Device Info Get Event.</span></span>

<span data-ttu-id="5cc78-1848">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1848">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1849">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1849">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1850">Campo informazioni 2: dispositivo Pima.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1850">Info Field 2: Pima device.</span></span>
- <span data-ttu-id="5cc78-1851">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1851">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1852">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1852">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-device-reset"></a><span data-ttu-id="5cc78-1853">Classe host reimpostazione del dispositivo Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1853">Host Class Pima Device Reset</span></span> 

#### <a name="ux_host_class_pima_device_reset"></a><span data-ttu-id="5cc78-1854">ux_host_class_pima_device_reset</span><span class="sxs-lookup"><span data-stu-id="5cc78-1854">ux_host_class_pima_device_reset</span></span>

<span data-ttu-id="5cc78-1855">**Icona** ![ di Icona di reimpostazione del dispositivo Pima della classe host](./media/user-guide/usbx-events/image132.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1855">**Icon** ![Host Class Pima Device Reset icon](./media/user-guide/usbx-events/image132.png)</span></span>

<span data-ttu-id="5cc78-1856">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1856">**Description**</span></span>

<span data-ttu-id="5cc78-1857">Questo evento rappresenta un evento di reimpostazione del dispositivo Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1857">This event represents a USBX Host Class Pima Device Reset Event.</span></span>

<span data-ttu-id="5cc78-1858">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1858">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1859">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1859">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1860">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1860">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1861">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1861">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1862">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1862">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-notification"></a><span data-ttu-id="5cc78-1863">Notifica classe host Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1863">Host Class Pima Notification</span></span> 

#### <a name="ux_host_class_pima_notification"></a><span data-ttu-id="5cc78-1864">ux_host_class_pima_notification</span><span class="sxs-lookup"><span data-stu-id="5cc78-1864">ux_host_class_pima_notification</span></span>

<span data-ttu-id="5cc78-1865">**Icona** ![ di Icona di notifica classe host Pima](./media/user-guide/usbx-events/image133.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1865">**Icon** ![Host Class Pima Notification icon](./media/user-guide/usbx-events/image133.png)</span></span>

<span data-ttu-id="5cc78-1866">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1866">**Description**</span></span>

<span data-ttu-id="5cc78-1867">Questo evento rappresenta un evento di notifica Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1867">This event represents a USBX Host Class Pima Notification Event.</span></span>

<span data-ttu-id="5cc78-1868">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1868">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1869">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1869">Info Field 1: Class instance.</span></span> <span data-ttu-id="5cc78-1870">Informazioni sul campo 2: codice evento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1870">Info Field 2: Event code.</span></span>
- <span data-ttu-id="5cc78-1871">Informazioni sul campo 3: ID transazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1871">Info Field 3: Transaction ID.</span></span>
- <span data-ttu-id="5cc78-1872">Informazioni sul campo 4: parametro1.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1872">Info Field 4: Parameter1.</span></span>

### <a name="host-class-pima-number-objects-get"></a><span data-ttu-id="5cc78-1873">Classe host numero Pima oggetti Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1873">Host Class Pima Number Objects Get</span></span> 

#### <a name="ux_host_class_pima_number_objects_get"></a><span data-ttu-id="5cc78-1874">ux_host_class_pima_number_objects_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1874">ux_host_class_pima_number_objects_get</span></span>

<span data-ttu-id="5cc78-1875">**Icona** ![ di Icona di visualizzazione degli oggetti numero Pima della classe host](./media/user-guide/usbx-events/image134.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1875">**Icon** ![Host Class Pima Number Objects Get icon](./media/user-guide/usbx-events/image134.png)</span></span>

<span data-ttu-id="5cc78-1876">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1876">**Description**</span></span>

<span data-ttu-id="5cc78-1877">Questo evento rappresenta un evento USBX della classe host di un numero Pima di oggetti.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1877">This event represents a USBX Host Class Pima Number Objects Get Event.</span></span>

<span data-ttu-id="5cc78-1878">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1878">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1879">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1879">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1880">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1880">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1881">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1881">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1882">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1882">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-close"></a><span data-ttu-id="5cc78-1883">Chiusura dell'oggetto Pima della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1883">Host Class Pima Object Close</span></span> 

#### <a name="ux_host_class_pima_object_close"></a><span data-ttu-id="5cc78-1884">ux_host_class_pima_object_close</span><span class="sxs-lookup"><span data-stu-id="5cc78-1884">ux_host_class_pima_object_close</span></span>

<span data-ttu-id="5cc78-1885">**Icona** ![ di Icona di chiusura oggetto classe host Pima](./media/user-guide/usbx-events/image135.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1885">**Icon** ![Host Class Pima Object Close icon](./media/user-guide/usbx-events/image135.png)</span></span>

<span data-ttu-id="5cc78-1886">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1886">**Description**</span></span>

<span data-ttu-id="5cc78-1887">Questo evento rappresenta un evento di chiusura dell'oggetto Pima per la classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1887">This event represents a USBX Host Class Pima Object Close Event.</span></span>

<span data-ttu-id="5cc78-1888">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1888">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1889">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1889">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1890">Campo informazioni 2: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1890">Info Field 2: Object.</span></span>
- <span data-ttu-id="5cc78-1891">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1891">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1892">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1892">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-copy"></a><span data-ttu-id="5cc78-1893">Classe host copia di oggetti Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1893">Host Class Pima Object Copy</span></span> 

#### <a name="ux_host_class_pima_object_copy"></a><span data-ttu-id="5cc78-1894">ux_host_class_pima_object_copy</span><span class="sxs-lookup"><span data-stu-id="5cc78-1894">ux_host_class_pima_object_copy</span></span>

<span data-ttu-id="5cc78-1895">**Icona** ![ di Icona di copia dell'oggetto classe host Pima](./media/user-guide/usbx-events/image136.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1895">**Icon** ![Host Class Pima Object Copy icon](./media/user-guide/usbx-events/image136.png)</span></span>

<span data-ttu-id="5cc78-1896">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1896">**Description**</span></span>

<span data-ttu-id="5cc78-1897">Questo evento rappresenta un evento di copia dell'oggetto Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1897">This event represents a USBX Host Class Pima Object Copy Event.</span></span>

<span data-ttu-id="5cc78-1898">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1898">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1899">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1899">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1900">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1900">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-1901">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1901">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1902">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1902">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-delete"></a><span data-ttu-id="5cc78-1903">Classe host Elimina oggetto Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1903">Host Class Pima Object Delete</span></span> 

#### <a name="ux_host_class_pima_object_delete"></a><span data-ttu-id="5cc78-1904">ux_host_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-1904">ux_host_class_pima_object_delete</span></span>

<span data-ttu-id="5cc78-1905">**Icona** ![ di Icona di eliminazione oggetto classe host Pima](./media/user-guide/usbx-events/image137.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1905">**Icon** ![Host Class Pima Object Delete icon](./media/user-guide/usbx-events/image137.png)</span></span>

<span data-ttu-id="5cc78-1906">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1906">**Description**</span></span>

<span data-ttu-id="5cc78-1907">Questo evento rappresenta un evento di eliminazione di oggetti Pima di classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1907">This event represents a USBX Host Class Pima Object Delete Event.</span></span>

<span data-ttu-id="5cc78-1908">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1908">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1909">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1909">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1910">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1910">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-1911">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1911">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1912">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1912">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-get"></a><span data-ttu-id="5cc78-1913">Classe host (oggetto Pima) Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1913">Host Class Pima Object Get</span></span> 

#### <a name="ux_host_class_pima_object_get"></a><span data-ttu-id="5cc78-1914">ux_host_class_pima_object_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1914">ux_host_class_pima_object_get</span></span>

<span data-ttu-id="5cc78-1915">**Icona** ![ di Icona di Get oggetto della classe host Pima](./media/user-guide/usbx-events/image138.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1915">**Icon** ![Host Class Pima Object Get icon](./media/user-guide/usbx-events/image138.png)</span></span>

<span data-ttu-id="5cc78-1916">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1916">**Description**</span></span>

<span data-ttu-id="5cc78-1917">Questo evento rappresenta l'acquisizione di informazioni RARP tramite nx_rarp_info_get.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1917">This event represents getting RARP information via nx_rarp_info_get.</span></span>

<span data-ttu-id="5cc78-1918">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1918">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1919">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1919">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1920">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1920">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-1921">Campo info 3: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1921">Info Field 3: Object.</span></span>
- <span data-ttu-id="5cc78-1922">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1922">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-info-get"></a><span data-ttu-id="5cc78-1923">Classe host. informazioni sull'oggetto Pima Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1923">Host Class Pima Object Info Get</span></span> 

#### <a name="ux_host_class_pima_object_info_get"></a><span data-ttu-id="5cc78-1924">ux_host_class_pima_object_info_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-1924">ux_host_class_pima_object_info_get</span></span>

<span data-ttu-id="5cc78-1925">**Icona** ![ di Icona di visualizzazione delle informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image139.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1925">**Icon** ![Host Class Pima Object Info Get icon](./media/user-guide/usbx-events/image139.png)</span></span>

<span data-ttu-id="5cc78-1926">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1926">**Description**</span></span>

<span data-ttu-id="5cc78-1927">Questo evento rappresenta una classe host USBX per le informazioni di Get dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1927">This event represents a USBX Host Class Pima Object Info Get Event.</span></span>

<span data-ttu-id="5cc78-1928">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1928">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1929">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1929">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1930">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1930">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-1931">Campo info 3: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1931">Info Field 3: Object.</span></span>
- <span data-ttu-id="5cc78-1932">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1932">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-info-send"></a><span data-ttu-id="5cc78-1933">Invio di informazioni sull'oggetto classe host Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1933">Host Class Pima Object Info Send</span></span> 

#### <a name="ux_host_class_pima_object_info_send"></a><span data-ttu-id="5cc78-1934">ux_host_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="5cc78-1934">ux_host_class_pima_object_info_send</span></span>

<span data-ttu-id="5cc78-1935">**Icona** ![ di Icona di invio info oggetto Pima classe host](./media/user-guide/usbx-events/image140.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1935">**Icon** ![Host Class Pima Object Info Send icon](./media/user-guide/usbx-events/image140.png)</span></span>

<span data-ttu-id="5cc78-1936">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1936">**Description**</span></span>

<span data-ttu-id="5cc78-1937">Questo evento rappresenta un evento di invio di informazioni sull'oggetto Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1937">This event represents a USBX Host Class Pima Object Info Send Event.</span></span>

<span data-ttu-id="5cc78-1938">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1938">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1939">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1939">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1940">Campo informazioni 2: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1940">Info Field 2: Object.</span></span>
- <span data-ttu-id="5cc78-1941">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1941">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1942">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1942">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-move"></a><span data-ttu-id="5cc78-1943">Spostamento oggetto classe host Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1943">Host Class Pima Object Move</span></span> 

#### <a name="ux_host_class_pima_object_move"></a><span data-ttu-id="5cc78-1944">ux_host_class_pima_object_move</span><span class="sxs-lookup"><span data-stu-id="5cc78-1944">ux_host_class_pima_object_move</span></span>

<span data-ttu-id="5cc78-1945">**Icona** ![ di Icona di spostamento oggetto classe host Pima](./media/user-guide/usbx-events/image141.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1945">**Icon** ![Host Class Pima Object Move icon](./media/user-guide/usbx-events/image141.png)</span></span>

<span data-ttu-id="5cc78-1946">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1946">**Description**</span></span>

<span data-ttu-id="5cc78-1947">Questo evento reprThis di evento rappresenta un evento di spostamento dell'oggetto Pima di una classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1947">This event reprThis event represents a USBX Host Class Pima Object Move Event.</span></span>

<span data-ttu-id="5cc78-1948">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1948">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1949">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1949">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1950">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1950">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-1951">Campo info 3: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1951">Info Field 3: Object.</span></span>
- <span data-ttu-id="5cc78-1952">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1952">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-send"></a><span data-ttu-id="5cc78-1953">Classe host-invio oggetto Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1953">Host Class Pima Object Send</span></span> 

#### <a name="ux_host_class_pima_object_move"></a><span data-ttu-id="5cc78-1954">ux_host_class_pima_object_move</span><span class="sxs-lookup"><span data-stu-id="5cc78-1954">ux_host_class_pima_object_move</span></span>

<span data-ttu-id="5cc78-1955">**Icona** ![ di Icona di invio oggetto Pima classe host](./media/user-guide/usbx-events/image142.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1955">**Icon** ![Host Class Pima Object Send icon](./media/user-guide/usbx-events/image142.png)</span></span>

<span data-ttu-id="5cc78-1956">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1956">**Description**</span></span>

<span data-ttu-id="5cc78-1957">Questo evento rappresenta un evento di invio di oggetti Pima di classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1957">This event represents a USBX Host Class Pima Object Send Event.</span></span>

<span data-ttu-id="5cc78-1958">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1958">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1959">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1959">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1960">Campo informazioni 2: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1960">Info Field 2: Object.</span></span>
- <span data-ttu-id="5cc78-1961">Campo info 3: buffer oggetti.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1961">Info Field 3: Object buffer.</span></span>
- <span data-ttu-id="5cc78-1962">Campo dati 4: lunghezza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1962">Info Field 4: Object length.</span></span>

### <a name="host-class-pima-object-transfer-abort"></a><span data-ttu-id="5cc78-1963">Interruzione del trasferimento di oggetti Pima della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1963">Host Class Pima Object Transfer Abort</span></span> 

#### <a name="ux_host_class_pima_object_transfer_abort"></a><span data-ttu-id="5cc78-1964">ux_host_class_pima_object_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="5cc78-1964">ux_host_class_pima_object_transfer_abort</span></span>

<span data-ttu-id="5cc78-1965">**Icona** ![ di Icona di interruzione trasferimento oggetti Pima classe host](./media/user-guide/usbx-events/image143.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1965">**Icon** ![Host Class Pima Object Transfer Abort icon](./media/user-guide/usbx-events/image143.png)</span></span>

<span data-ttu-id="5cc78-1966">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1966">**Description**</span></span>

<span data-ttu-id="5cc78-1967">Questo evento rappresenta un evento di interruzione del trasferimento di oggetti Pima per la classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1967">This event represents a USBX Host Class Pima Object Transfer Abort Event.</span></span>

<span data-ttu-id="5cc78-1968">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1968">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1969">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1969">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1970">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1970">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-1971">Campo info 3: oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1971">Info Field 3: Object.</span></span>
- <span data-ttu-id="5cc78-1972">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1972">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-read"></a><span data-ttu-id="5cc78-1973">Lettura classe host Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-1973">Host Class Pima Read</span></span> 

#### <a name="ux_host_class_pima_read"></a><span data-ttu-id="5cc78-1974">ux_host_class_pima_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-1974">ux_host_class_pima_read</span></span>

<span data-ttu-id="5cc78-1975">**Icona** ![ di Icona di lettura della classe host Pima](./media/user-guide/usbx-events/image144.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1975">**Icon** ![Host Class Pima Read icon](./media/user-guide/usbx-events/image144.png)</span></span>

<span data-ttu-id="5cc78-1976">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1976">**Description**</span></span>

<span data-ttu-id="5cc78-1977">Questo evento rappresenta un evento di lettura Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1977">This event represents a USBX Host Class Pima Read Event.</span></span>

<span data-ttu-id="5cc78-1978">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1978">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1979">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1979">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1980">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1980">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-1981">Informazioni sul campo 3: lunghezza dei dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1981">Info Field 3: Data length.</span></span>
- <span data-ttu-id="5cc78-1982">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1982">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-request-cancel"></a><span data-ttu-id="5cc78-1983">Annullamento della richiesta Pima della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1983">Host Class Pima Request Cancel</span></span> 

#### <a name="ux_host_class_pima_request_cancel"></a><span data-ttu-id="5cc78-1984">ux_host_class_pima_request_cancel</span><span class="sxs-lookup"><span data-stu-id="5cc78-1984">ux_host_class_pima_request_cancel</span></span>

<span data-ttu-id="5cc78-1985">**Icona** ![ di Icona di annullamento richiesta Pima della classe host](./media/user-guide/usbx-events/image145.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1985">**Icon** ![Host Class Pima Request Cancel icon](./media/user-guide/usbx-events/image145.png)</span></span>

<span data-ttu-id="5cc78-1986">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1986">**Description**</span></span>

<span data-ttu-id="5cc78-1987">Questo evento rappresenta un evento di annullamento della richiesta Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1987">This event represents a USBX Host Class Pima Request Cancel Event.</span></span>

<span data-ttu-id="5cc78-1988">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1988">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1989">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1989">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-1990">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1990">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-1991">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1991">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-1992">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1992">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-session-close"></a><span data-ttu-id="5cc78-1993">Chiusura della sessione Pima della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-1993">Host Class Pima Session Close</span></span> 

#### <a name="ux_host_class_pima_session_close"></a><span data-ttu-id="5cc78-1994">ux_host_class_pima_session_close</span><span class="sxs-lookup"><span data-stu-id="5cc78-1994">ux_host_class_pima_session_close</span></span>

<span data-ttu-id="5cc78-1995">**Icona** ![ di Icona di chiusura della sessione Pima della classe host](./media/user-guide/usbx-events/image146.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-1995">**Icon** ![Host Class Pima Session Close icon](./media/user-guide/usbx-events/image146.png)</span></span>

<span data-ttu-id="5cc78-1996">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1996">**Description**</span></span>

<span data-ttu-id="5cc78-1997">Questo evento rappresenta un evento di chiusura della sessione Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1997">This event represents a USBX Host Class Pima Session Close Event.</span></span>

<span data-ttu-id="5cc78-1998">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-1998">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-1999">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-1999">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2000">Informazioni sul campo 2: sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2000">Info Field 2: Pima session.</span></span>
- <span data-ttu-id="5cc78-2001">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2001">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2002">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2002">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-session-open"></a><span data-ttu-id="5cc78-2003">Sessione Pima della classe host aperta</span><span class="sxs-lookup"><span data-stu-id="5cc78-2003">Host Class Pima Session Open</span></span> 

#### <a name="ux_host_class_pima_session_open"></a><span data-ttu-id="5cc78-2004">ux_host_class_pima_session_open</span><span class="sxs-lookup"><span data-stu-id="5cc78-2004">ux_host_class_pima_session_open</span></span>

<span data-ttu-id="5cc78-2005">**Icona** ![ di Icona di apertura della sessione Pima della classe host](./media/user-guide/usbx-events/image147.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2005">**Icon** ![Host Class Pima Session Open icon](./media/user-guide/usbx-events/image147.png)</span></span>

<span data-ttu-id="5cc78-2006">**Descrizione** di Questo evento rappresenta un evento di apertura della sessione Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2006">**Description** This event represents a USBX Host Class Pima Session Open Event.</span></span>

<span data-ttu-id="5cc78-2007">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2007">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2008">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2008">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2009">Informazioni sul campo 2: sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2009">Info Field 2: Pima session.</span></span>
- <span data-ttu-id="5cc78-2010">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2010">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2011">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2011">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-storage-ids-get"></a><span data-ttu-id="5cc78-2012">Classe host Pima ID archiviazione Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2012">Host Class Pima Storage Ids Get</span></span> 

#### <a name="ux_host_class_pima_session_ids_get"></a><span data-ttu-id="5cc78-2013">ux_host_class_pima_session_ids_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2013">ux_host_class_pima_session_ids_get</span></span>

<span data-ttu-id="5cc78-2014">**Icona** ![ di Icona di Get dell'ID di archiviazione Pima della classe host](./media/user-guide/usbx-events/image148.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2014">**Icon** ![Host Class Pima Storage Ids Get icon](./media/user-guide/usbx-events/image148.png)</span></span>

<span data-ttu-id="5cc78-2015">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2015">**Description**</span></span>

<span data-ttu-id="5cc78-2016">Questo evento rappresenta un evento di Get dell'ID di archiviazione Pima della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2016">This event represents a USBX Host Class Pima Storage Ids Get Event.</span></span>

<span data-ttu-id="5cc78-2017">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2017">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2018">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2018">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2019">Campo NFO 2: Array ID archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2019">nfo Field 2: Storage ID array.</span></span>
- <span data-ttu-id="5cc78-2020">Informazioni campo 3: lunghezza ID archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2020">Info Field 3: Storage ID length.</span></span>
<span data-ttu-id="5cc78-2021">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2021">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-storage-info-get"></a><span data-ttu-id="5cc78-2022">Classe host-informazioni di archiviazione Pima Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2022">Host Class Pima Storage Info Get</span></span> 

#### <a name="ux_host_class_pima_storage_info_get"></a><span data-ttu-id="5cc78-2023">ux_host_class_pima_storage_info_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2023">ux_host_class_pima_storage_info_get</span></span>

<span data-ttu-id="5cc78-2024">**Icona** ![ di Icona di informazioni di archiviazione per la classe host Pima](./media/user-guide/usbx-events/image149.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2024">**Icon** ![Host Class Pima Storage Info Get icon](./media/user-guide/usbx-events/image149.png)</span></span>

<span data-ttu-id="5cc78-2025">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2025">**Description**</span></span>

<span data-ttu-id="5cc78-2026">Questo evento rappresenta un evento USBX di archiviazione di informazioni di archiviazione Pima della classe host.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2026">This event represents a USBX Host Class Pima Storage Info Get Event.</span></span>

<span data-ttu-id="5cc78-2027">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2027">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2028">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2028">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2029">Informazioni sul campo 2: ID archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2029">Info Field 2: Storage ID.</span></span>
- <span data-ttu-id="5cc78-2030">Campo informazioni 3: archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2030">Info Field 3: Storage.</span></span>
- <span data-ttu-id="5cc78-2031">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2031">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-thumb-get"></a><span data-ttu-id="5cc78-2032">Classe host Pima Thumb Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2032">Host Class Pima Thumb Get</span></span> 

#### <a name="ux_host_class_pima_thumb_get"></a><span data-ttu-id="5cc78-2033">ux_host_class_pima_thumb_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2033">ux_host_class_pima_thumb_get</span></span>

<span data-ttu-id="5cc78-2034">**Icona** ![ di Icona della classe host Pima Thumb Get](./media/user-guide/usbx-events/image150.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2034">**Icon** ![Host Class Pima Thumb Get icon](./media/user-guide/usbx-events/image150.png)</span></span>

<span data-ttu-id="5cc78-2035">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2035">**Description**</span></span>

<span data-ttu-id="5cc78-2036">Questo evento rappresenta l'inaccettazione di una connessione al server TCP tramite nx_tcp_server_socket_unaccept.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2036">This event represents unaccepting a TCP server connection via nx_tcp_server_socket_unaccept.</span></span>

<span data-ttu-id="5cc78-2037">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2037">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-2038">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2038">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2039">Informazioni sul campo 2: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2039">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="5cc78-2040">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2040">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2041">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2041">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-write"></a><span data-ttu-id="5cc78-2042">Classe host scrittura Pima</span><span class="sxs-lookup"><span data-stu-id="5cc78-2042">Host Class Pima Write</span></span> 

#### <a name="ux_host_class_pima_thumb_get"></a><span data-ttu-id="5cc78-2043">ux_host_class_pima_thumb_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2043">ux_host_class_pima_thumb_get</span></span>

<span data-ttu-id="5cc78-2044">**Icona** ![ di Icona di scrittura della classe host Pima](./media/user-guide/usbx-events/image151.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2044">**Icon** ![Host Class Pima Write icon](./media/user-guide/usbx-events/image151.png)</span></span>

<span data-ttu-id="5cc78-2045">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2045">**Description**</span></span>

<span data-ttu-id="5cc78-2046">Questo evento rappresenta una classe host USBX Pima Write.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2046">This event represents a USBX Host Class Pima Write.</span></span>

<span data-ttu-id="5cc78-2047">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2047">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2048">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2048">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="5cc78-2049">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2049">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-2050">Informazioni sul campo 3: lunghezza dei dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2050">Info Field 3: Data length.</span></span>
- <span data-ttu-id="5cc78-2051">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2051">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-activate"></a><span data-ttu-id="5cc78-2052">Attivazione della stampante della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2052">Host Class Printer Activate</span></span> 

#### <a name="ux_host_class_printer_activate"></a><span data-ttu-id="5cc78-2053">ux_host_class_printer_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2053">ux_host_class_printer_activate</span></span>

<span data-ttu-id="5cc78-2054">**Icona** ![ di Icona di attivazione della stampante della classe host](./media/user-guide/usbx-events/image152.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2054">**Icon** ![Host Class Printer Activate icon](./media/user-guide/usbx-events/image152.png)</span></span>

<span data-ttu-id="5cc78-2055">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2055">**Description**</span></span>

<span data-ttu-id="5cc78-2056">Questo evento rappresenta un evento di attivazione della stampante della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2056">This event represents a USBX Host Class Printer Activate Event.</span></span>

<span data-ttu-id="5cc78-2057">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2057">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2058">Info Field 1: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2058">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="5cc78-2059">Informazioni sul campo 2: puntatore al socket.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2059">Info Field 2: Pointer to socket.</span></span>
- <span data-ttu-id="5cc78-2060">Informazioni sul campo 3: tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2060">Info Field 3: Type of service.</span></span>
- <span data-ttu-id="5cc78-2061">Informazioni sul campo 4: dimensioni della finestra di ricezione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2061">Info Field 4: Receive window size.</span></span>

### <a name="host-class-printer-deactivate"></a><span data-ttu-id="5cc78-2062">Disattivazione della stampante della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2062">Host Class Printer Deactivate</span></span> 

#### <a name="ux_host_class_printer_deactivate"></a><span data-ttu-id="5cc78-2063">ux_host_class_printer_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2063">ux_host_class_printer_deactivate</span></span>

<span data-ttu-id="5cc78-2064">**Icona** ![ di Icona di disattivazione della stampante della classe host](./media/user-guide/usbx-events/image153.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2064">**Icon** ![Host Class Printer Deactivate icon](./media/user-guide/usbx-events/image153.png)</span></span>

<span data-ttu-id="5cc78-2065">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2065">**Description**</span></span>

<span data-ttu-id="5cc78-2066">Questo evento rappresenta un evento di disattivazione della stampante della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2066">This event represents a USBX Host Class Printer Deactivate Event.</span></span>

<span data-ttu-id="5cc78-2067">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2067">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2068">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2068">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2069">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2069">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2070">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2070">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2071">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2071">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-name-get"></a><span data-ttu-id="5cc78-2072">Nome della stampante della classe host Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2072">Host Class Printer Name Get</span></span> 

#### <a name="ux_host_class_printer_name_get"></a><span data-ttu-id="5cc78-2073">ux_host_class_printer_name_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2073">ux_host_class_printer_name_get</span></span>

<span data-ttu-id="5cc78-2074">**Icona** ![ di Icona di visualizzazione del nome della stampante della classe host](./media/user-guide/usbx-events/image154.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2074">**Icon** ![Host Class Printer Name Get icon](./media/user-guide/usbx-events/image154.png)</span></span>

<span data-ttu-id="5cc78-2075">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2075">**Description**</span></span>

<span data-ttu-id="5cc78-2076">Questo evento rappresenta un evento Get della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2076">This event represents a USBX Host Class Printer Name Get Event.</span></span>

<span data-ttu-id="5cc78-2077">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2077">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-2078">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2078">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2079">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2079">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2080">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2080">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2081">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2081">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-read"></a><span data-ttu-id="5cc78-2082">Lettura stampante classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2082">Host Class Printer Read</span></span> 

#### <a name="ux_host_class_printer_read"></a><span data-ttu-id="5cc78-2083">ux_host_class_printer_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-2083">ux_host_class_printer_read</span></span>

<span data-ttu-id="5cc78-2084">**Icona** ![ di Icona di lettura della stampante della classe host](./media/user-guide/usbx-events/image155.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2084">**Icon** ![Host Class Printer Read icon](./media/user-guide/usbx-events/image155.png)</span></span>

<span data-ttu-id="5cc78-2085">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2085">**Description**</span></span>

<span data-ttu-id="5cc78-2086">Questo evento rappresenta un evento di lettura della stampante della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2086">This event represents a USBX Host Class Printer Read Event.</span></span>

<span data-ttu-id="5cc78-2087">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2087">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2088">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2088">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2089">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2089">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-2090">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2090">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-2091">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2091">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-soft-reset"></a><span data-ttu-id="5cc78-2092">Ripristino soft della stampante della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2092">Host Class Printer Soft Reset</span></span> 

#### <a name="ux_host_class_printer_soft_reset"></a><span data-ttu-id="5cc78-2093">ux_host_class_printer_soft_reset</span><span class="sxs-lookup"><span data-stu-id="5cc78-2093">ux_host_class_printer_soft_reset</span></span>

<span data-ttu-id="5cc78-2094">**Icona** ![ di Icona di ripristino soft della stampante della classe host](./media/user-guide/usbx-events/image156.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2094">**Icon** ![Host Class Printer Soft Reset icon](./media/user-guide/usbx-events/image156.png)</span></span>

<span data-ttu-id="5cc78-2095">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2095">**Description**</span></span>

<span data-ttu-id="5cc78-2096">Questo evento rappresenta un evento di reimpostazione del software della stampante della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2096">This event represents a USBX Host Class Printer Soft Reset Event.</span></span>

<span data-ttu-id="5cc78-2097">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2097">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2098">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2098">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2099">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2099">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2100">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2100">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2101">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2101">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-status-get"></a><span data-ttu-id="5cc78-2102">Stato della stampante della classe host Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2102">Host Class Printer Status Get</span></span> 

#### <a name="ux_host_class_printer_status_get"></a><span data-ttu-id="5cc78-2103">ux_host_class_printer_status_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2103">ux_host_class_printer_status_get</span></span>

<span data-ttu-id="5cc78-2104">**Icona** ![ di Icona di Get dello stato della stampante della classe host](./media/user-guide/usbx-events/image157.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2104">**Icon** ![Host Class Printer Status Get icon](./media/user-guide/usbx-events/image157.png)</span></span>

<span data-ttu-id="5cc78-2105">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2105">**Description**</span></span>

<span data-ttu-id="5cc78-2106">Questo evento rappresenta un evento Get dello stato della stampante della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2106">This event represents a USBX Host Class Printer Status Get Event.</span></span>

<span data-ttu-id="5cc78-2107">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2107">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2108">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2108">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2109">Informazioni sul campo 2: stato della stampante.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2109">Info Field 2: Printer status.</span></span>
- <span data-ttu-id="5cc78-2110">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2110">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2111">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2111">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-write"></a><span data-ttu-id="5cc78-2112">Scrittura della stampante della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2112">Host Class Printer Write</span></span> 

#### <a name="ux_host_class_printer_write"></a><span data-ttu-id="5cc78-2113">ux_host_class_printer_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-2113">ux_host_class_printer_write</span></span>

<span data-ttu-id="5cc78-2114">**Icona** ![ di Icona di scrittura della stampante della classe host](./media/user-guide/usbx-events/image158.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2114">**Icon** ![Host Class Printer Write icon](./media/user-guide/usbx-events/image158.png)</span></span>

<span data-ttu-id="5cc78-2115">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2115">**Description**</span></span>

<span data-ttu-id="5cc78-2116">Questo evento rappresenta una scrittura della stampante della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2116">This event represents a USBX Host Class Printer Write.</span></span>

<span data-ttu-id="5cc78-2117">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2117">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-2118">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2118">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2119">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2119">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-2120">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2120">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-2121">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2121">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-activate"></a><span data-ttu-id="5cc78-2122">Attivazione prolifica della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2122">Host Class Prolific Activate</span></span> 

#### <a name="ux_host_class_prolific_activate"></a><span data-ttu-id="5cc78-2123">ux_host_class_prolific_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2123">ux_host_class_prolific_activate</span></span> 

<span data-ttu-id="5cc78-2124">**Icona** ![ di Icona di attivazione della classe host Prolific](./media/user-guide/usbx-events/image159.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2124">**Icon** ![Host Class Prolific Activate icon](./media/user-guide/usbx-events/image159.png)</span></span>

<span data-ttu-id="5cc78-2125">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2125">**Description**</span></span>

<span data-ttu-id="5cc78-2126">Questo evento rappresenta un evento di attivazione prolifico della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2126">This event represents a USBX Host Class Prolific Activate Event.</span></span>

<span data-ttu-id="5cc78-2127">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2127">**Information Fields**</span></span> 

- <span data-ttu-id="5cc78-2128">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2128">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2129">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2129">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2130">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2130">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2131">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2131">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-deactivate"></a><span data-ttu-id="5cc78-2132">Disattivazione della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2132">Host Class Prolific Deactivate</span></span> 

#### <a name="ux_host_class_prolific_deactivate"></a><span data-ttu-id="5cc78-2133">ux_host_class_prolific_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2133">ux_host_class_prolific_deactivate</span></span> 

<span data-ttu-id="5cc78-2134">**Icona** ![ di Icona di disattivazione della classe host](./media/user-guide/usbx-events/image160.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2134">**Icon** ![Host Class Prolific Deactivate icon](./media/user-guide/usbx-events/image160.png)</span></span>

<span data-ttu-id="5cc78-2135">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2135">**Description**</span></span>

<span data-ttu-id="5cc78-2136">Questo evento rappresenta un evento di disattivazione prolifico della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2136">This event represents a USBX Host Class Prolific Deactivate Event.</span></span>

<span data-ttu-id="5cc78-2137">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2137">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2138">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2138">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2139">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2139">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2140">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2140">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2141">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2141">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-abort-in-pipe"></a><span data-ttu-id="5cc78-2142">Classe host-interruzioni IOCTL in pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-2142">Host Class Prolific Ioctl Abort In Pipe</span></span> 

#### <a name="ux_host_class_prolific_ioctl_abort_in_pipe"></a><span data-ttu-id="5cc78-2143">ux_host_class_prolific_ioctl_abort_in_pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-2143">ux_host_class_prolific_ioctl_abort_in_pipe</span></span>

<span data-ttu-id="5cc78-2144">**Icona** ![ di Icona della classe host I/O per le interruzioni in pipe](./media/user-guide/usbx-events/image161.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2144">**Icon** ![Host Class Prolific I O C T L Abort In Pipe icon](./media/user-guide/usbx-events/image161.png)</span></span>

<span data-ttu-id="5cc78-2145">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2145">**Description**</span></span>

<span data-ttu-id="5cc78-2146">Questo evento rappresenta una classe host USBX prolifica IOCTL Abort nell'evento pipe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2146">This event represents a USBX Host Class Prolific Ioctl Abort In Pipe Event.</span></span>

<span data-ttu-id="5cc78-2147">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2147">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2148">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2148">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2149">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2149">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2150">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2150">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2151">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2151">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-abort-out-pipe"></a><span data-ttu-id="5cc78-2152">Classe host-Interrompi IOCTL interruzione pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-2152">Host Class Prolific Ioctl Abort Out Pipe</span></span> 

#### <a name="ux_host_class_prolific_ioctl_abort_out_pipe"></a><span data-ttu-id="5cc78-2153">ux_host_class_prolific_ioctl_abort_out_pipe</span><span class="sxs-lookup"><span data-stu-id="5cc78-2153">ux_host_class_prolific_ioctl_abort_out_pipe</span></span>

<span data-ttu-id="5cc78-2154">**Icona** ![ di Icona della classe host Prolific I O C T interrompe la pipe](./media/user-guide/usbx-events/image162.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2154">**Icon** ![Host Class Prolific I O C T L Abort Out Pipe icon](./media/user-guide/usbx-events/image162.png)</span></span>

<span data-ttu-id="5cc78-2155">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2155">**Description**</span></span>

<span data-ttu-id="5cc78-2156">Questo evento rappresenta una classe host USBX per l'evento di pipe Abort Abort.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2156">This event represents a USBX Host Class Prolific Ioctl Abort Out Pipe Event.</span></span>

<span data-ttu-id="5cc78-2157">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2157">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2158">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2158">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2159">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2159">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2160">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2160">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2161">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2161">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-get-device-status"></a><span data-ttu-id="5cc78-2162">Classe host prolifico IOCTL ottenere lo stato del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-2162">Host Class Prolific Ioctl Get Device Status</span></span> 

#### <a name="ux_host_class_prolific_ioctl_get_device_status"></a><span data-ttu-id="5cc78-2163">ux_host_class_prolific_ioctl_get_device_status</span><span class="sxs-lookup"><span data-stu-id="5cc78-2163">ux_host_class_prolific_ioctl_get_device_status</span></span>

<span data-ttu-id="5cc78-2164">**Icona** ![ di Icona dello stato del dispositivo per la classe host Prolific I O C T](./media/user-guide/usbx-events/image163.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2164">**Icon** ![Host Class Prolific I O C T L Get Device Status icon](./media/user-guide/usbx-events/image163.png)</span></span>

<span data-ttu-id="5cc78-2165">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2165">**Description**</span></span>

<span data-ttu-id="5cc78-2166">Questo evento rappresenta una classe host USBX che prolifico IOCTL ottiene un evento di stato del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2166">This event represents a USBX Host Class Prolific Ioctl Get Device Status Event.</span></span>

<span data-ttu-id="5cc78-2167">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2167">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2168">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2168">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2169">Informazioni sul campo 2: stato del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2169">Info Field 2: Device status.</span></span>
- <span data-ttu-id="5cc78-2170">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2170">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2171">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2171">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-get-line-coding"></a><span data-ttu-id="5cc78-2172">Classe host prolifico IOCTL Get line codifica</span><span class="sxs-lookup"><span data-stu-id="5cc78-2172">Host Class Prolific Ioctl Get Line Coding</span></span> 

#### <a name="ux_host_class_prolific_ioctl_get_line_coding"></a><span data-ttu-id="5cc78-2173">ux_host_class_prolific_ioctl_get_line_coding</span><span class="sxs-lookup"><span data-stu-id="5cc78-2173">ux_host_class_prolific_ioctl_get_line_coding</span></span>

<span data-ttu-id="5cc78-2174">**Icona** ![ di Icona della codifica della riga per la classe host Prolific I O C](./media/user-guide/usbx-events/image164.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2174">**Icon** ![Host Class Prolific I O C T L Get Line Coding icon](./media/user-guide/usbx-events/image164.png)</span></span>

<span data-ttu-id="5cc78-2175">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2175">**Description**</span></span>

<span data-ttu-id="5cc78-2176">Questo evento rappresenta una classe host USBX prolifico IOCTL ottenere un evento di codifica della riga.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2176">This event represents a USBX Host Class Prolific Ioctl Get Line Coding Event.</span></span>

<span data-ttu-id="5cc78-2177">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2177">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2178">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2178">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2179">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2179">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-2180">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2180">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2181">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2181">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-purge"></a><span data-ttu-id="5cc78-2182">Classe host-ripulitura IOCTL</span><span class="sxs-lookup"><span data-stu-id="5cc78-2182">Host Class Prolific Ioctl Purge</span></span> 

#### <a name="ux_host_class_prolific_ioctl_purge"></a><span data-ttu-id="5cc78-2183">ux_host_class_prolific_ioctl_purge</span><span class="sxs-lookup"><span data-stu-id="5cc78-2183">ux_host_class_prolific_ioctl_purge</span></span>

<span data-ttu-id="5cc78-2184">**Icona** ![ di Icona per la ripulitura IOCTL della classe host](./media/user-guide/usbx-events/image165.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2184">**Icon** ![Host Class Prolific Ioctl Purge icon](./media/user-guide/usbx-events/image165.png)</span></span>

<span data-ttu-id="5cc78-2185">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2185">**Description**</span></span>

<span data-ttu-id="5cc78-2186">Questo evento rappresenta una classe host USBX prolifico evento IOCTL Purge.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2186">This event represents a USBX Host Class Prolific Ioctl Purge Event.</span></span>

<span data-ttu-id="5cc78-2187">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2187">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2188">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2188">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2189">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2189">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-2190">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2190">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2191">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2191">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-report-device"></a><span data-ttu-id="5cc78-2192">Classe host-dispositivo di report IOCTL prolifico</span><span class="sxs-lookup"><span data-stu-id="5cc78-2192">Host Class Prolific Ioctl Report Device</span></span> 

#### <a name="ux_host_class_prolific_ioctl_report_device"></a><span data-ttu-id="5cc78-2193">ux_host_class_prolific_ioctl_report_device</span><span class="sxs-lookup"><span data-stu-id="5cc78-2193">ux_host_class_prolific_ioctl_report_device</span></span>

<span data-ttu-id="5cc78-2194">**Icona** ![ di Icona del dispositivo di report I O C di classe host Prolific](./media/user-guide/usbx-events/image166.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2194">**Icon** ![Host Class Prolific I O C T L Report Device icon](./media/user-guide/usbx-events/image166.png)</span></span>

<span data-ttu-id="5cc78-2195">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2195">**Description**</span></span>

<span data-ttu-id="5cc78-2196">Questo evento rappresenta un evento di modifica dello stato del dispositivo di report IOCTL per la classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2196">This event represents a USBX Host Class Prolific Ioctl Report Device Status Change Event.</span></span>

<span data-ttu-id="5cc78-2197">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2197">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2198">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2198">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2199">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2199">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-2200">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2200">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2201">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2201">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-send-break"></a><span data-ttu-id="5cc78-2202">Classe host prolifico invio di IOCTL</span><span class="sxs-lookup"><span data-stu-id="5cc78-2202">Host Class Prolific Ioctl Send Break</span></span> 

#### <a name="ux_host_class_prolific_ioctl_send_break"></a><span data-ttu-id="5cc78-2203">ux_host_class_prolific_ioctl_send_break</span><span class="sxs-lookup"><span data-stu-id="5cc78-2203">ux_host_class_prolific_ioctl_send_break</span></span>

<span data-ttu-id="5cc78-2204">**Icona** ![ di Icona di invio della classe host Prolific I O C T](./media/user-guide/usbx-events/image167.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2204">**Icon** ![Host Class Prolific I O C T L Send Break icon](./media/user-guide/usbx-events/image167.png)</span></span>

<span data-ttu-id="5cc78-2205">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2205">**Description**</span></span>

<span data-ttu-id="5cc78-2206">Questo evento rappresenta una classe host USBX prolifico evento di invio di interruzioni IOCTL.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2206">This event represents a USBX Host Class Prolific Ioctl Send Break Event.</span></span>

<span data-ttu-id="5cc78-2207">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2207">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2208">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2208">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2209">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2209">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2210">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2210">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2211">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2211">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-set-line-coding"></a><span data-ttu-id="5cc78-2212">Codifica della riga del set IOCTL della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2212">Host Class Prolific Ioctl Set Line Coding</span></span> 

#### <a name="ux_host_class_prolific_ioctl_set_line_coding"></a><span data-ttu-id="5cc78-2213">ux_host_class_prolific_ioctl_set_line_coding</span><span class="sxs-lookup"><span data-stu-id="5cc78-2213">ux_host_class_prolific_ioctl_set_line_coding</span></span>

<span data-ttu-id="5cc78-2214">**Icona** ![ di Icona del codice a linee set di classe host Prolific I O C T L](./media/user-guide/usbx-events/image168.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2214">**Icon** ![Host Class Prolific I O C T L Set Line Coding icon](./media/user-guide/usbx-events/image168.png)</span></span>

<span data-ttu-id="5cc78-2215">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2215">**Description**</span></span>

<span data-ttu-id="5cc78-2216">Questo evento rappresenta una classe host USBX, un evento di codifica della riga set IOCTL.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2216">This event represents a USBX Host Class Prolific Ioctl Set Line Coding Event.</span></span>

<span data-ttu-id="5cc78-2217">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2217">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2218">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2218">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2219">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2219">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-2220">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2220">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2221">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2221">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-set-line-state"></a><span data-ttu-id="5cc78-2222">Stato della riga set IOCTL della classe host Prolific</span><span class="sxs-lookup"><span data-stu-id="5cc78-2222">Host Class Prolific Ioctl Set Line State</span></span> 

#### <a name="ux_host_class_prolific_ioctl_set_line_state"></a><span data-ttu-id="5cc78-2223">ux_host_class_prolific_ioctl_set_line_state</span><span class="sxs-lookup"><span data-stu-id="5cc78-2223">ux_host_class_prolific_ioctl_set_line_state</span></span>

<span data-ttu-id="5cc78-2224">**Icona** ![ di Icona dello stato della linea di impostazione della classe host Prolific I O C T](./media/user-guide/usbx-events/image169.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2224">**Icon** ![Host Class Prolific I O C T L Set Line State icon](./media/user-guide/usbx-events/image169.png)</span></span>

<span data-ttu-id="5cc78-2225">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2225">**Description**</span></span>

<span data-ttu-id="5cc78-2226">Questo evento rappresenta un evento di stato riga set IOCTL per la classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2226">This event represents a USBX Host Class Prolific Ioctl Set Line State Event.</span></span>

<span data-ttu-id="5cc78-2227">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2227">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2228">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2228">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2229">Informazioni sul campo 2: parametro.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2229">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="5cc78-2230">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2230">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2231">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2231">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-read"></a><span data-ttu-id="5cc78-2232">Lettura prolifica classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2232">Host Class Prolific Read</span></span> 

#### <a name="ux_host_class_prolific_read"></a><span data-ttu-id="5cc78-2233">ux_host_class_prolific_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-2233">ux_host_class_prolific_read</span></span>

<span data-ttu-id="5cc78-2234">**Icona** ![ di Icona lettura prolifica classe host](./media/user-guide/usbx-events/image170.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2234">**Icon** ![Host Class Prolific Read icon](./media/user-guide/usbx-events/image170.png)</span></span>

<span data-ttu-id="5cc78-2235">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2235">**Description**</span></span>

<span data-ttu-id="5cc78-2236">Questo evento rappresenta un evento di lettura prolifico della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2236">This event represents a USBX Host Class Prolific Read Event.</span></span>

<span data-ttu-id="5cc78-2237">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2237">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2238">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2238">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2239">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2239">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-2240">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2240">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-2241">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2241">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-reception-start"></a><span data-ttu-id="5cc78-2242">Inizio della ricezione prolifico della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2242">Host Class Prolific Reception Start</span></span> 

#### <a name="ux_host_class_prolific_reception_start"></a><span data-ttu-id="5cc78-2243">ux_host_class_prolific_reception_start</span><span class="sxs-lookup"><span data-stu-id="5cc78-2243">ux_host_class_prolific_reception_start</span></span>

<span data-ttu-id="5cc78-2244">**Icona** ![ di Icona di inizio della ricezione prolifico della classe host](./media/user-guide/usbx-events/image171.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2244">**Icon** ![Host Class Prolific Reception Start icon](./media/user-guide/usbx-events/image171.png)</span></span>

<span data-ttu-id="5cc78-2245">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2245">**Description**</span></span>

<span data-ttu-id="5cc78-2246">Questo evento rappresenta un evento di avvio della ricezione prolifico della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2246">This event represents a USBX Host Class Prolific Reception Start Event.</span></span>

<span data-ttu-id="5cc78-2247">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2247">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2248">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2248">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2249">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2249">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2250">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2250">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2251">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2251">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-reception-stop"></a><span data-ttu-id="5cc78-2252">Arresto della ricezione della classe host Prolific</span><span class="sxs-lookup"><span data-stu-id="5cc78-2252">Host Class Prolific Reception Stop</span></span> 

#### <a name="ux_host_class_prolific_reception_stop"></a><span data-ttu-id="5cc78-2253">ux_host_class_prolific_reception_stop</span><span class="sxs-lookup"><span data-stu-id="5cc78-2253">ux_host_class_prolific_reception_stop</span></span>

<span data-ttu-id="5cc78-2254">**Icona** ![ di Icona di arresto della ricezione della classe host Prolific](./media/user-guide/usbx-events/image172.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2254">**Icon** ![Host Class Prolific Reception Stop icon](./media/user-guide/usbx-events/image172.png)</span></span>

<span data-ttu-id="5cc78-2255">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2255">**Description**</span></span>

<span data-ttu-id="5cc78-2256">Questo evento rappresenta un evento di arresto della ricezione prolifico della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2256">This event represents a USBX Host Class Prolific Reception Stop Event.</span></span>

<span data-ttu-id="5cc78-2257">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2257">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2258">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2258">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2259">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2259">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2260">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2260">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2261">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2261">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-write"></a><span data-ttu-id="5cc78-2262">Scrittura prolifica della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2262">Host Class Prolific Write</span></span> 

#### <a name="ux_host_class_prolific_write"></a><span data-ttu-id="5cc78-2263">ux_host_class_prolific_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-2263">ux_host_class_prolific_write</span></span>

<span data-ttu-id="5cc78-2264">**Icona** ![ di Icona di scrittura della classe host Prolific](./media/user-guide/usbx-events/image173.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2264">**Icon** ![Host Class Prolific Write icon](./media/user-guide/usbx-events/image173.png)</span></span>

<span data-ttu-id="5cc78-2265">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2265">**Description**</span></span>

<span data-ttu-id="5cc78-2266">Questo evento rappresenta un evento di scrittura prolifico della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2266">This event represents a USBX Host Class Prolific Write Event.</span></span>

<span data-ttu-id="5cc78-2267">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2267">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2268">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2268">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2269">Campo informazioni 2: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2269">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="5cc78-2270">Informazioni campo 3: lunghezza richiesta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2270">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="5cc78-2271">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2271">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-activate"></a><span data-ttu-id="5cc78-2272">Attivazione dell'archiviazione della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2272">Host Class Storage Activate</span></span> 

#### <a name="ux_host_class_storage_activate"></a><span data-ttu-id="5cc78-2273">ux_host_class_storage_activate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2273">ux_host_class_storage_activate</span></span>

<span data-ttu-id="5cc78-2274">**Icona** ![ di Icona di attivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image174.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2274">**Icon** ![Host Class Storage Activate icon](./media/user-guide/usbx-events/image174.png)</span></span>

<span data-ttu-id="5cc78-2275">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2275">**Description**</span></span>

<span data-ttu-id="5cc78-2276">Questo evento rappresenta un evento di attivazione dell'archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2276">This event represents a USBX Host Class Storage Activate Event.</span></span>

<span data-ttu-id="5cc78-2277">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2277">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2278">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2278">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2279">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2279">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2280">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2280">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2281">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2281">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-deactivate"></a><span data-ttu-id="5cc78-2282">Disattivazione dell'archiviazione della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2282">Host Class Storage Deactivate</span></span> 

#### <a name="ux_host_class_storage_deactivate"></a><span data-ttu-id="5cc78-2283">ux_host_class_storage_deactivate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2283">ux_host_class_storage_deactivate</span></span>

<span data-ttu-id="5cc78-2284">**Icona** ![ di Icona di disattivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image175.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2284">**Icon** ![Host Class Storage Deactivate icon](./media/user-guide/usbx-events/image175.png)</span></span>

<span data-ttu-id="5cc78-2285">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2285">**Description**</span></span>

<span data-ttu-id="5cc78-2286">Questo evento rappresenta un evento di disattivazione dell'archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2286">This event represents a USBX Host Class Storage Deactivate Event.</span></span>

<span data-ttu-id="5cc78-2287">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2287">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2288">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2288">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2289">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2289">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2290">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2290">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2291">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2291">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-capacity-get"></a><span data-ttu-id="5cc78-2292">Capacità del supporto di archiviazione della classe host Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2292">Host Class Storage Media Capacity Get</span></span> 

#### <a name="ux_host_class_storage_media_capacity_get"></a><span data-ttu-id="5cc78-2293">ux_host_class_storage_media_capacity_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2293">ux_host_class_storage_media_capacity_get</span></span>

<span data-ttu-id="5cc78-2294">**Icona** ![ di Icona Ottieni capacità supporto di archiviazione classe host](./media/user-guide/usbx-events/image176.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2294">**Icon** ![Host Class Storage Media Capacity Get icon](./media/user-guide/usbx-events/image176.png)</span></span>

<span data-ttu-id="5cc78-2295">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2295">**Description**</span></span>

<span data-ttu-id="5cc78-2296">Questo evento rappresenta un evento di ottenimento della capacità del supporto di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2296">This event represents a USBX Host Class Storage Media Capacity Get Event.</span></span>

<span data-ttu-id="5cc78-2297">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2297">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2298">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2298">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2299">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2299">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2300">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2300">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2301">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2301">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-format-capacity-get"></a><span data-ttu-id="5cc78-2302">Classe host capacità formato supporti di archiviazione Get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2302">Host Class Storage Media Format Capacity Get</span></span>

#### <a name="ux_host_class_storage_media_format_capacity_get"></a><span data-ttu-id="5cc78-2303">ux_host_class_storage_media_format_capacity_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2303">ux_host_class_storage_media_format_capacity_get</span></span>

<span data-ttu-id="5cc78-2304">**Icona** ![ di Icona per la capacità del formato del supporto di archiviazione della classe host](./media/user-guide/usbx-events/image177.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2304">**Icon** ![Host Class Storage Media Format Capacity Get icon](./media/user-guide/usbx-events/image177.png)</span></span>

<span data-ttu-id="5cc78-2305">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2305">**Description**</span></span>

<span data-ttu-id="5cc78-2306">Questo evento rappresenta un evento di ottenimento della capacità del formato multimediale di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2306">This event represents a USBX Host Class Storage Media Format Capacity Get Event.</span></span>

<span data-ttu-id="5cc78-2307">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2307">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2308">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2308">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2309">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2309">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2310">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2310">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2311">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2311">Info Field 4: Not used.</span></span>

#### <a name="host-class-storage-media-mount"></a><span data-ttu-id="5cc78-2312">Montaggio dei supporti di archiviazione della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2312">Host Class Storage Media Mount</span></span> 

#### <a name="ux_host_class_storage_media_mount"></a><span data-ttu-id="5cc78-2313">ux_host_class_storage_media_mount</span><span class="sxs-lookup"><span data-stu-id="5cc78-2313">ux_host_class_storage_media_mount</span></span>

<span data-ttu-id="5cc78-2314">**Icona** ![ di Icona di montaggio dei supporti di archiviazione della classe host](./media/user-guide/usbx-events/image178.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2314">**Icon** ![Host Class Storage Media Mount icon](./media/user-guide/usbx-events/image178.png)</span></span>

<span data-ttu-id="5cc78-2315">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2315">**Description**</span></span>

<span data-ttu-id="5cc78-2316">Questo evento rappresenta un evento di montaggio dei supporti di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2316">This event represents a USBX Host Class Storage Media Mount Event.</span></span>

<span data-ttu-id="5cc78-2317">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2317">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2318">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2318">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2319">Informazioni sul campo 2: settore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2319">Info Field 2: Sector.</span></span>
- <span data-ttu-id="5cc78-2320">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2320">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2321">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2321">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-open"></a><span data-ttu-id="5cc78-2322">Supporto di archiviazione della classe host aperto</span><span class="sxs-lookup"><span data-stu-id="5cc78-2322">Host Class Storage Media Open</span></span> 

#### <a name="ux_host_class_storage_media_open"></a><span data-ttu-id="5cc78-2323">ux_host_class_storage_media_open</span><span class="sxs-lookup"><span data-stu-id="5cc78-2323">ux_host_class_storage_media_open</span></span>

<span data-ttu-id="5cc78-2324">**Icona** ![ di Icona Apri supporto di archiviazione classe host](./media/user-guide/usbx-events/image179.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2324">**Icon** ![Host Class Storage Media Open icon](./media/user-guide/usbx-events/image179.png)</span></span>

<span data-ttu-id="5cc78-2325">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2325">**Description**</span></span>

<span data-ttu-id="5cc78-2326">Questo evento rappresenta un evento di apertura del supporto di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2326">This event represents a USBX Host Class Storage Media Open Event.</span></span>

<span data-ttu-id="5cc78-2327">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2327">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2328">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2328">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2329">Informazioni sul campo 2: supporto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2329">Info Field 2: Media.</span></span>
- <span data-ttu-id="5cc78-2330">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2330">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2331">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2331">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-read"></a><span data-ttu-id="5cc78-2332">Lettura supporti di archiviazione classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2332">Host Class Storage Media Read</span></span> 

#### <a name="ux_host_class_storage_media_read"></a><span data-ttu-id="5cc78-2333">ux_host_class_storage_media_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-2333">ux_host_class_storage_media_read</span></span>

<span data-ttu-id="5cc78-2334">**Icona** ![ di Icona lettura supporti di archiviazione classe host](./media/user-guide/usbx-events/image180.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2334">**Icon** ![Host Class Storage Media Read icon](./media/user-guide/usbx-events/image180.png)</span></span>

<span data-ttu-id="5cc78-2335">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2335">**Description**</span></span>

<span data-ttu-id="5cc78-2336">Questo evento rappresenta un evento di lettura del supporto di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2336">This event represents a USBX Host Class Storage Media Read Event.</span></span>

<span data-ttu-id="5cc78-2337">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2337">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2338">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2338">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2339">Campo informazioni 2: inizio settore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2339">Info Field 2: Sector start.</span></span>
- <span data-ttu-id="5cc78-2340">Informazioni sul campo 3: conteggio settori.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2340">Info Field 3: Sector count.</span></span>
- <span data-ttu-id="5cc78-2341">Informazioni sul campo 4: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2341">Info Field 4: Data pointer.</span></span>

### <a name="host-class-storage-media-write"></a><span data-ttu-id="5cc78-2342">Scrittura dei supporti di archiviazione della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2342">Host Class Storage Media Write</span></span> 

#### <a name="ux_host_class_storage_media_write"></a><span data-ttu-id="5cc78-2343">ux_host_class_storage_media_write</span><span class="sxs-lookup"><span data-stu-id="5cc78-2343">ux_host_class_storage_media_write</span></span>

<span data-ttu-id="5cc78-2344">**Icona** ![ di Icona Scrivi supporto di archiviazione classe host](./media/user-guide/usbx-events/image181.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2344">**Icon** ![Host Class Storage Media Write icon](./media/user-guide/usbx-events/image181.png)</span></span>

<span data-ttu-id="5cc78-2345">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2345">**Description**</span></span>

<span data-ttu-id="5cc78-2346">Questo evento rappresenta un evento di scrittura del supporto di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2346">This event represents a USBX Host Class Storage Media Write Event.</span></span>

<span data-ttu-id="5cc78-2347">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2347">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2348">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2348">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2349">Campo informazioni 2: inizio settore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2349">Info Field 2: Sector start.</span></span>
- <span data-ttu-id="5cc78-2350">Informazioni sul campo 3: conteggio settori.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2350">Info Field 3: Sector count.</span></span>
- <span data-ttu-id="5cc78-2351">Informazioni sul campo 4: puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2351">Info Field 4: Data pointer.</span></span>

### <a name="host-class-storage-request-sense"></a><span data-ttu-id="5cc78-2352">Rilevamento delle richieste di archiviazione della classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2352">Host Class Storage Request Sense</span></span> 

#### <a name="ux_host_class_storage_request_sense"></a><span data-ttu-id="5cc78-2353">ux_host_class_storage_request_sense</span><span class="sxs-lookup"><span data-stu-id="5cc78-2353">ux_host_class_storage_request_sense</span></span>

<span data-ttu-id="5cc78-2354">**Icona** ![ di Icona del rilevamento della richiesta di archiviazione della classe host](./media/user-guide/usbx-events/image182.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2354">**Icon** ![Host Class Storage Request Sense icon](./media/user-guide/usbx-events/image182.png)</span></span>

<span data-ttu-id="5cc78-2355">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2355">**Description**</span></span>

<span data-ttu-id="5cc78-2356">Questo evento rappresenta un evento del senso della richiesta di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2356">This event represents a USBX Host Class Storage Request Sense Event.</span></span>

<span data-ttu-id="5cc78-2357">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2357">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2358">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2358">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2359">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2359">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2360">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2360">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2361">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2361">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-start-stop"></a><span data-ttu-id="5cc78-2362">Avvio arresto archiviazione classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2362">Host Class Storage Start Stop</span></span> 

#### <a name="ux_host_class_storage_start_stop"></a><span data-ttu-id="5cc78-2363">ux_host_class_storage_start_stop</span><span class="sxs-lookup"><span data-stu-id="5cc78-2363">ux_host_class_storage_start_stop</span></span>

<span data-ttu-id="5cc78-2364">**Icona** ![ di Icona di avvio dell'archiviazione della classe host](./media/user-guide/usbx-events/image183.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2364">**Icon** ![Host Class Storage Start Stop icon](./media/user-guide/usbx-events/image183.png)</span></span>

<span data-ttu-id="5cc78-2365">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2365">**Description**</span></span>

<span data-ttu-id="5cc78-2366">Questo evento rappresenta un evento di inizio arresto dell'archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2366">This event represents a USBX Host Class Storage Start Stop Event.</span></span>

<span data-ttu-id="5cc78-2367">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2367">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2368">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2368">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2369">Informazioni sul campo 2: avviare il segnale di arresto.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2369">Info Field 2: Start stop signal.</span></span>
- <span data-ttu-id="5cc78-2370">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2370">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2371">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2371">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-unit-ready-test"></a><span data-ttu-id="5cc78-2372">Test pronto unità di archiviazione classe host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2372">Host Class Storage Unit Ready Test</span></span> 

#### <a name="ux_host_class_storage_unit_ready_test"></a><span data-ttu-id="5cc78-2373">ux_host_class_storage_unit_ready_test</span><span class="sxs-lookup"><span data-stu-id="5cc78-2373">ux_host_class_storage_unit_ready_test</span></span>

<span data-ttu-id="5cc78-2374">**Icona** ![ di Icona del test pronto per l'unità di archiviazione della classe host](./media/user-guide/usbx-events/image184.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2374">**Icon** ![Host Class Storage Unit Ready Test icon](./media/user-guide/usbx-events/image184.png)</span></span>

<span data-ttu-id="5cc78-2375">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2375">**Description**</span></span>

<span data-ttu-id="5cc78-2376">Questo evento rappresenta un evento di test dell'unità di archiviazione della classe host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2376">This event represents a USBX Host Class Storage Unit Ready Test Event.</span></span>

<span data-ttu-id="5cc78-2377">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2377">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2378">Campo informazioni 1: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2378">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="5cc78-2379">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2379">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2380">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2380">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2381">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2381">Info Field 4: Not used.</span></span>

### <a name="host-stack-class-instance-create"></a><span data-ttu-id="5cc78-2382">Creazione istanza Classe stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2382">Host Stack Class Instance Create</span></span> 

#### <a name="ux_host_class_instance_create"></a><span data-ttu-id="5cc78-2383">ux_host_class_instance_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2383">ux_host_class_instance_create</span></span>

<span data-ttu-id="5cc78-2384">**Icona** ![ di Icona di creazione dell'istanza della classe Stack host](./media/user-guide/usbx-events/image185.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2384">**Icon** ![Host Stack Class Instance Create icon](./media/user-guide/usbx-events/image185.png)</span></span>

<span data-ttu-id="5cc78-2385">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2385">**Description**</span></span>

<span data-ttu-id="5cc78-2386">Questo evento rappresenta un evento di creazione dell'istanza della classe dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2386">This event represents a USBX Host Stack Class Instance Create Event.</span></span>

<span data-ttu-id="5cc78-2387">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2387">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2388">Informazioni campo 1: classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2388">Info Field 1: Class.</span></span>
- <span data-ttu-id="5cc78-2389">Campo informazioni 2: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2389">Info Field 2: Class Instance.</span></span>
- <span data-ttu-id="5cc78-2390">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2390">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2391">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2391">Info Field 4: Not used.</span></span>

### <a name="host-stack-class-instance-destroy"></a><span data-ttu-id="5cc78-2392">Eliminazione istanza Classe stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2392">Host Stack Class Instance Destroy</span></span> 

#### <a name="ux_host_class_instance_create"></a><span data-ttu-id="5cc78-2393">ux_host_class_instance_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2393">ux_host_class_instance_create</span></span>

<span data-ttu-id="5cc78-2394">**Icona** ![ di Icona di eliminazione istanza Classe stack host](./media/user-guide/usbx-events/image186.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2394">**Icon** ![Host Stack Class Instance Destroy icon](./media/user-guide/usbx-events/image186.png)</span></span>

<span data-ttu-id="5cc78-2395">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2395">**Description**</span></span>

<span data-ttu-id="5cc78-2396">Questo evento rappresenta un evento di eliminazione dell'istanza della classe dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2396">This event represents a USBX Host Stack Class Instance Destroy Event.</span></span>

<span data-ttu-id="5cc78-2397">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2397">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2398">Informazioni campo 1: classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2398">Info Field 1: Class.</span></span>
- <span data-ttu-id="5cc78-2399">Campo informazioni 2: istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2399">Info Field 2: Class Instance.</span></span>
- <span data-ttu-id="5cc78-2400">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2400">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2401">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2401">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-delete"></a><span data-ttu-id="5cc78-2402">Eliminazione della configurazione dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2402">Host Stack Configuration Delete</span></span> 

#### <a name="ux_host_class_configuration_delete"></a><span data-ttu-id="5cc78-2403">ux_host_class_configuration_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-2403">ux_host_class_configuration_delete</span></span>

<span data-ttu-id="5cc78-2404">**Icona** ![ di Icona di eliminazione della configurazione dello stack host](./media/user-guide/usbx-events/image187.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2404">**Icon** ![Host Stack Configuration Delete icon](./media/user-guide/usbx-events/image187.png)</span></span>

<span data-ttu-id="5cc78-2405">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2405">**Description**</span></span>

<span data-ttu-id="5cc78-2406">Questo evento rappresenta un evento di eliminazione della configurazione dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2406">This event represents a USBX Host Stack Configuration Delete Event.</span></span>

<span data-ttu-id="5cc78-2407">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2407">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2408">Campo informazioni 1: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2408">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="5cc78-2409">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2409">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2410">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2410">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2411">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2411">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-enumerate"></a><span data-ttu-id="5cc78-2412">Enumerazione della configurazione dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2412">Host Stack Configuration Enumerate</span></span> 

#### <a name="ux_host_stack_configuration_enumerate"></a><span data-ttu-id="5cc78-2413">ux_host_stack_configuration_enumerate</span><span class="sxs-lookup"><span data-stu-id="5cc78-2413">ux_host_stack_configuration_enumerate</span></span>

<span data-ttu-id="5cc78-2414">**Icona** ![ di Icona di enumerazione della configurazione dello stack host](./media/user-guide/usbx-events/image188.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2414">**Icon** ![Host Stack Configuration Enumerate icon](./media/user-guide/usbx-events/image188.png)</span></span>

<span data-ttu-id="5cc78-2415">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2415">**Description**</span></span>

<span data-ttu-id="5cc78-2416">Questo evento rappresenta un evento di enumerazione della configurazione dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2416">This event represents a USBX Host Stack Configuration Enumerate Event.</span></span>

<span data-ttu-id="5cc78-2417">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2417">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2418">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2418">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2419">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2419">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2420">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2420">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2421">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2421">Info Field 4: Not used.</span></span>

### <a name="stack-configuration-instance-create"></a><span data-ttu-id="5cc78-2422">Creazione dell'istanza di configurazione dello stack</span><span class="sxs-lookup"><span data-stu-id="5cc78-2422">Stack Configuration Instance Create</span></span> 

#### <a name="ux_host_stack_configuration_instance_create"></a><span data-ttu-id="5cc78-2423">ux_host_stack_configuration_instance_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2423">ux_host_stack_configuration_instance_create</span></span>

<span data-ttu-id="5cc78-2424">**Icona** ![ di Icona di creazione dell'istanza di configurazione dello stack](./media/user-guide/usbx-events/image189.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2424">**Icon** ![Stack Configuration Instance Create icon](./media/user-guide/usbx-events/image189.png)</span></span>

<span data-ttu-id="5cc78-2425">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2425">**Description**</span></span>

<span data-ttu-id="5cc78-2426">Questo evento rappresenta un evento di creazione dell'istanza di configurazione dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2426">This event represents a USBX Host Stack Configuration Instance Create Event.</span></span>

<span data-ttu-id="5cc78-2427">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2427">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2428">Campo informazioni 1: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2428">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="5cc78-2429">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2429">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2430">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2430">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2431">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2431">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-instance-delete"></a><span data-ttu-id="5cc78-2432">Eliminazione dell'istanza di configurazione dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2432">Host Stack Configuration Instance Delete</span></span> 

#### <a name="ux_host_stack_configuration_instance_delete"></a><span data-ttu-id="5cc78-2433">ux_host_stack_configuration_instance_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-2433">ux_host_stack_configuration_instance_delete</span></span>

<span data-ttu-id="5cc78-2434">**Icona** ![ di Icona di eliminazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image190.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2434">**Icon** ![Host Stack Configuration Instance Delete icon](./media/user-guide/usbx-events/image190.png)</span></span>

<span data-ttu-id="5cc78-2435">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2435">**Description**</span></span>

<span data-ttu-id="5cc78-2436">Questo evento rappresenta un evento di eliminazione dell'istanza di configurazione dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2436">This event represents a USBX Host Stack Configuration Instance Delete Event.</span></span>

<span data-ttu-id="5cc78-2437">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2437">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2438">Campo informazioni 1: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2438">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="5cc78-2439">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2439">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2440">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2440">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2441">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2441">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-set"></a><span data-ttu-id="5cc78-2442">Set di configurazione dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2442">Host Stack Configuration Set</span></span> 

#### <a name="ux_host_stack_configuration_set"></a><span data-ttu-id="5cc78-2443">ux_host_stack_configuration_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-2443">ux_host_stack_configuration_set</span></span>

<span data-ttu-id="5cc78-2444">**Icona** ![ di Icona del set di configurazione dello stack host](./media/user-guide/usbx-events/image191.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2444">**Icon** ![Host Stack Configuration Set icon](./media/user-guide/usbx-events/image191.png)</span></span>

<span data-ttu-id="5cc78-2445">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2445">**Description**</span></span>

<span data-ttu-id="5cc78-2446">Questo evento rappresenta un evento del set di configurazione dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2446">This event represents a USBX Host Stack Configuration Set Event.</span></span>

<span data-ttu-id="5cc78-2447">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2447">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2448">Campo informazioni 1: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2448">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="5cc78-2449">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2449">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2450">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2450">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2451">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2451">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-address-set"></a><span data-ttu-id="5cc78-2452">Set di indirizzi dispositivo stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2452">Host Stack Device Address Set</span></span> 

#### <a name="ux_host_stack_device_address_set"></a><span data-ttu-id="5cc78-2453">ux_host_stack_device_address_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-2453">ux_host_stack_device_address_set</span></span>

<span data-ttu-id="5cc78-2454">**Icona** ![ di Icona del set di indirizzi del dispositivo dello stack host](./media/user-guide/usbx-events/image192.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2454">**Icon** ![Host Stack Device Address Set icon](./media/user-guide/usbx-events/image192.png)</span></span>

<span data-ttu-id="5cc78-2455">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2455">**Description**</span></span>

<span data-ttu-id="5cc78-2456">Questo evento rappresenta un evento del set di indirizzi del dispositivo dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2456">This event represents a USBX Host Stack Device Address Set Event.</span></span>

<span data-ttu-id="5cc78-2457">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2457">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2458">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2458">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2459">Informazioni sul campo 2: indirizzo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2459">Info Field 2: Device Address.</span></span>
- <span data-ttu-id="5cc78-2460">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2460">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2461">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2461">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-configuration-get"></a><span data-ttu-id="5cc78-2462">Get configurazione dispositivo stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2462">Host Stack Device Configuration Get</span></span> 

#### <a name="ux_host_stack_device_configuration_get"></a><span data-ttu-id="5cc78-2463">ux_host_stack_device_configuration_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2463">ux_host_stack_device_configuration_get</span></span>

<span data-ttu-id="5cc78-2464">**Icona** ![ di Icona get configurazione dispositivo stack host](./media/user-guide/usbx-events/image193.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2464">**Icon** ![Host Stack Device Configuration Get icon](./media/user-guide/usbx-events/image193.png)</span></span>

<span data-ttu-id="5cc78-2465">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2465">**Description**</span></span>

<span data-ttu-id="5cc78-2466">Questo evento rappresenta un evento di ottenimento della configurazione del dispositivo dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2466">This event represents a USBX Host Stack Device Configuration Get Event.</span></span>

<span data-ttu-id="5cc78-2467">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2467">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2468">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2468">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2469">Campo NFO 2: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2469">nfo Field 2: Configuration.</span></span>
- <span data-ttu-id="5cc78-2470">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2470">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2471">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2471">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-configuration-select"></a><span data-ttu-id="5cc78-2472">Selezione configurazione dispositivo stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2472">Host Stack Device Configuration Select</span></span> 

#### <a name="ux_host_stack_device_configuration_select"></a><span data-ttu-id="5cc78-2473">ux_host_stack_device_configuration_select</span><span class="sxs-lookup"><span data-stu-id="5cc78-2473">ux_host_stack_device_configuration_select</span></span>

<span data-ttu-id="5cc78-2474">**Icona** ![ di Icona di selezione configurazione dispositivo stack host](./media/user-guide/usbx-events/image194.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2474">**Icon** ![Host Stack Device Configuration Select icon](./media/user-guide/usbx-events/image194.png)</span></span>

<span data-ttu-id="5cc78-2475">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2475">**Description**</span></span>

<span data-ttu-id="5cc78-2476">Questo evento rappresenta un evento di selezione della configurazione del dispositivo dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2476">This event represents a USBX Host Stack Device Configuration Select Event.</span></span>

<span data-ttu-id="5cc78-2477">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2477">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2478">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2478">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2479">Campo informazioni 2: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2479">Info Field 2: Configuration.</span></span>
- <span data-ttu-id="5cc78-2480">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2480">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2481">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2481">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-descriptor-read"></a><span data-ttu-id="5cc78-2482">Lettura descrittore dispositivo stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2482">Host Stack Device Descriptor Read</span></span> 

#### <a name="ux_host_stack_device_descriptor_read"></a><span data-ttu-id="5cc78-2483">ux_host_stack_device_descriptor_read</span><span class="sxs-lookup"><span data-stu-id="5cc78-2483">ux_host_stack_device_descriptor_read</span></span>

<span data-ttu-id="5cc78-2484">**Icona** ![ di Icona di lettura del descrittore del dispositivo dello stack host](./media/user-guide/usbx-events/image195.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2484">**Icon** ![Host Stack Device Descriptor Read icon](./media/user-guide/usbx-events/image195.png)</span></span>

<span data-ttu-id="5cc78-2485">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2485">**Description**</span></span>

<span data-ttu-id="5cc78-2486">Questo evento rappresenta un evento di lettura del descrittore di dispositivo dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2486">This event represents a USBX Host Stack Device Descriptor Read Event.</span></span>

<span data-ttu-id="5cc78-2487">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2487">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2488">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2488">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2489">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2489">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2490">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2490">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2491">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2491">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-get"></a><span data-ttu-id="5cc78-2492">Get del dispositivo dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2492">Host Stack Device Get</span></span> 

#### <a name="ux_host_stack_device_get"></a><span data-ttu-id="5cc78-2493">ux_host_stack_device_get</span><span class="sxs-lookup"><span data-stu-id="5cc78-2493">ux_host_stack_device_get</span></span>

<span data-ttu-id="5cc78-2494">**Icona** ![ di Icona Ottieni dispositivo stack host](./media/user-guide/usbx-events/image196.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2494">**Icon** ![Host Stack Device Get icon](./media/user-guide/usbx-events/image196.png)</span></span>

<span data-ttu-id="5cc78-2495">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2495">**Description**</span></span>

<span data-ttu-id="5cc78-2496">Questo evento rappresenta un evento di Get del dispositivo dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2496">This event represents a USBX Host Stack Device Get Event.</span></span>

<span data-ttu-id="5cc78-2497">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2497">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2498">Informazioni sul campo 1: Indice del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2498">Info Field 1: Device index.</span></span>
- <span data-ttu-id="5cc78-2499">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2499">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2500">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2500">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2501">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2501">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-remove"></a><span data-ttu-id="5cc78-2502">Rimozione dispositivo stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2502">Host Stack Device Remove</span></span> 

#### <a name="ux_host_stack_device_remove"></a><span data-ttu-id="5cc78-2503">ux_host_stack_device_remove</span><span class="sxs-lookup"><span data-stu-id="5cc78-2503">ux_host_stack_device_remove</span></span>

<span data-ttu-id="5cc78-2504">**Icona** ![ di Icona Rimuovi dispositivo stack host](./media/user-guide/usbx-events/image197.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2504">**Icon** ![Host Stack Device Remove icon](./media/user-guide/usbx-events/image197.png)</span></span>

<span data-ttu-id="5cc78-2505">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2505">**Description**</span></span>

<span data-ttu-id="5cc78-2506">Questo evento rappresenta un evento di rimozione del dispositivo dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2506">This event represents a USBX Host Stack Device Remove Event.</span></span>

<span data-ttu-id="5cc78-2507">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2507">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2508">Campo informazioni 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2508">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="5cc78-2509">Campo informazioni 2: padre.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2509">Info Field 2: Parent.</span></span>
- <span data-ttu-id="5cc78-2510">Campo informazioni 3: Indice porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2510">Info Field 3: Port Index.</span></span>
- <span data-ttu-id="5cc78-2511">Informazioni sul campo 4: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2511">Info Field 4: Device.</span></span>

### <a name="host-stack-device-resource-free"></a><span data-ttu-id="5cc78-2512">Risorsa dispositivo stack host disponibile</span><span class="sxs-lookup"><span data-stu-id="5cc78-2512">Host Stack Device Resource Free</span></span> 

#### <a name="ux_host_stack_device_resource_free"></a><span data-ttu-id="5cc78-2513">ux_host_stack_device_resource_free</span><span class="sxs-lookup"><span data-stu-id="5cc78-2513">ux_host_stack_device_resource_free</span></span>

<span data-ttu-id="5cc78-2514">**Icona** ![ di Icona della risorsa del dispositivo dello stack host](./media/user-guide/usbx-events/image198.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2514">**Icon** ![Host Stack Device Resource Free icon](./media/user-guide/usbx-events/image198.png)</span></span>

<span data-ttu-id="5cc78-2515">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2515">**Description**</span></span>

<span data-ttu-id="5cc78-2516">Questo evento rappresenta un evento di risorsa del dispositivo stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2516">This event represents a USBX Host Stack Device Resource Free Event.</span></span>

<span data-ttu-id="5cc78-2517">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2517">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2518">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2518">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2519">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2519">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2520">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2520">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2521">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2521">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-instance-create"></a><span data-ttu-id="5cc78-2522">Creazione dell'istanza dell'endpoint dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2522">Host Stack Endpoint Instance Create</span></span> 

#### <a name="ux_host_stack_endpoint_instance_create"></a><span data-ttu-id="5cc78-2523">ux_host_stack_endpoint_instance_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2523">ux_host_stack_endpoint_instance_create</span></span>

<span data-ttu-id="5cc78-2524">**Icona** ![ di Icona di creazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image199.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2524">**Icon** ![Host Stack Endpoint Instance Create icon](./media/user-guide/usbx-events/image199.png)</span></span>

<span data-ttu-id="5cc78-2525">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2525">**Description**</span></span>

<span data-ttu-id="5cc78-2526">Questo evento rappresenta un evento di creazione dell'istanza dell'endpoint dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2526">This event represents a USBX Host Stack Endpoint Instance Create Event.</span></span>

<span data-ttu-id="5cc78-2527">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2527">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2528">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2528">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2529">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2529">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2530">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2530">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2531">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2531">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-instance-delete"></a><span data-ttu-id="5cc78-2532">Eliminazione dell'istanza dell'endpoint dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2532">Host Stack Endpoint Instance Delete</span></span> 

#### <a name="ux_host_stack_endpoint_instance_delete"></a><span data-ttu-id="5cc78-2533">ux_host_stack_endpoint_instance_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-2533">ux_host_stack_endpoint_instance_delete</span></span>

<span data-ttu-id="5cc78-2534">**Icona** ![ di Icona di eliminazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image200.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2534">**Icon** ![Host Stack Endpoint Instance Delete icon](./media/user-guide/usbx-events/image200.png)</span></span>

<span data-ttu-id="5cc78-2535">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2535">**Description**</span></span>

<span data-ttu-id="5cc78-2536">Questo evento rappresenta un evento di eliminazione dell'istanza dell'endpoint dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2536">This event represents a USBX Host Stack Endpoint Instance Delete Event.</span></span>

<span data-ttu-id="5cc78-2537">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2537">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2538">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2538">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2539">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2539">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2540">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2540">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-reset"></a><span data-ttu-id="5cc78-2541">Reimpostazione dell'endpoint dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2541">Host Stack Endpoint Reset</span></span> 

#### <a name="ux_host_stack_endpoint_reset"></a><span data-ttu-id="5cc78-2542">ux_host_stack_endpoint_reset</span><span class="sxs-lookup"><span data-stu-id="5cc78-2542">ux_host_stack_endpoint_reset</span></span>

<span data-ttu-id="5cc78-2543">**Icona** ![ di Icona di reimpostazione dell'endpoint dello stack host](./media/user-guide/usbx-events/image201.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2543">**Icon** ![Host Stack Endpoint Reset icon](./media/user-guide/usbx-events/image201.png)</span></span>

<span data-ttu-id="5cc78-2544">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2544">**Description**</span></span>

<span data-ttu-id="5cc78-2545">Questo evento rappresenta un evento di reimpostazione dell'endpoint dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2545">This event represents a USBX Host Stack Endpoint Reset Event.</span></span>

<span data-ttu-id="5cc78-2546">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2546">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2547">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2547">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2548">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2548">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2549">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2549">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2550">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2550">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-transfer-abort"></a><span data-ttu-id="5cc78-2551">Interruzione trasferimento endpoint stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2551">Host Stack Endpoint Transfer Abort</span></span> 

#### <a name="ux_host_stack_endpoint_transfer_abort"></a><span data-ttu-id="5cc78-2552">ux_host_stack_endpoint_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="5cc78-2552">ux_host_stack_endpoint_transfer_abort</span></span>

<span data-ttu-id="5cc78-2553">**Icona** ![ di Icona di interruzione del trasferimento dell'endpoint dello stack host](./media/user-guide/usbx-events/image202.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2553">**Icon** ![Host Stack Endpoint Transfer Abort icon](./media/user-guide/usbx-events/image202.png)</span></span>

<span data-ttu-id="5cc78-2554">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2554">**Description**</span></span>

<span data-ttu-id="5cc78-2555">Questo evento rappresenta un evento di interruzione del trasferimento dell'endpoint dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2555">This event represents a USBX Host Stack Endpoint Transfer Abort Event.</span></span>

<span data-ttu-id="5cc78-2556">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2556">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2557">Campo informazioni 1: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2557">Info Field 1: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2558">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2558">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2559">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2559">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2560">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2560">Info Field 4: Not used.</span></span>

### <a name="host-stack-host-controller-register"></a><span data-ttu-id="5cc78-2561">Registro del controller host dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2561">Host Stack Host Controller Register</span></span> 

#### <a name="ux_host_stack_hcd_register"></a><span data-ttu-id="5cc78-2562">ux_host_stack_hcd_register</span><span class="sxs-lookup"><span data-stu-id="5cc78-2562">ux_host_stack_hcd_register</span></span>

<span data-ttu-id="5cc78-2563">**Icona** ![ di Icona registro del controller host dello stack host](./media/user-guide/usbx-events/image203.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2563">**Icon** ![Host Stack Host Controller Register icon](./media/user-guide/usbx-events/image203.png)</span></span>

<span data-ttu-id="5cc78-2564">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2564">**Description**</span></span>

<span data-ttu-id="5cc78-2565">Questo evento rappresenta un registro del controller host dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2565">This event represents a USBX Host Stack Host Controller Register.</span></span>

<span data-ttu-id="5cc78-2566">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2566">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2567">Campo informazioni 1: nome HCD.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2567">Info Field 1: Hcd Name.</span></span>
- <span data-ttu-id="5cc78-2568">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2568">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2569">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2569">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2570">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2570">Info Field 4: Not used.</span></span>

### <a name="host-stack-initialize"></a><span data-ttu-id="5cc78-2571">Inizializzazione stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2571">Host Stack Initialize</span></span> 

#### <a name="ux_host_stack_initialize"></a><span data-ttu-id="5cc78-2572">ux_host_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="5cc78-2572">ux_host_stack_initialize</span></span>

<span data-ttu-id="5cc78-2573">**Icona** ![ di Icona di inizializzazione dello stack host](./media/user-guide/usbx-events/image204.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2573">**Icon** ![Host Stack Initialize icon](./media/user-guide/usbx-events/image204.png)</span></span>

<span data-ttu-id="5cc78-2574">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2574">**Description**</span></span>

<span data-ttu-id="5cc78-2575">Questo evento rappresenta un evento di inizializzazione dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2575">This event represents a USBX Host Stack Initialize Event.</span></span>

<span data-ttu-id="5cc78-2576">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2576">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2577">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2577">Info Field 1: Not used.</span></span>
- <span data-ttu-id="5cc78-2578">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2578">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2579">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2579">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2580">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2580">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-endpoint-get"></a><span data-ttu-id="5cc78-2581">Ottenere l'endpoint dell'interfaccia dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2581">Host Stack Interface Endpoint Get</span></span> 

#### <a name="interface_-tcp-retry-entry"></a><span data-ttu-id="5cc78-2582">Interface_ immissione tentativi TCP</span><span class="sxs-lookup"><span data-stu-id="5cc78-2582">Interface_ TCP retry entry</span></span>

<span data-ttu-id="5cc78-2583">**Icona** ![ di Icona Ottieni endpoint interfaccia stack host](./media/user-guide/usbx-events/image205.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2583">**Icon** ![Host Stack Interface Endpoint Get icon](./media/user-guide/usbx-events/image205.png)</span></span>

<span data-ttu-id="5cc78-2584">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2584">**Description**</span></span>

<span data-ttu-id="5cc78-2585">Questo evento rappresenta un evento di ripetizione NetX TCP interno.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2585">This event represents an internal NetX TCP retry event.</span></span>

<span data-ttu-id="5cc78-2586">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2586">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2587">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2587">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-2588">Campo informazioni 2: Indice endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2588">Info Field 2: Endpoint index.</span></span>
- <span data-ttu-id="5cc78-2589">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2589">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2590">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2590">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-instance-create"></a><span data-ttu-id="5cc78-2591">Creazione istanza interfaccia stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2591">Host Stack Interface Instance Create</span></span> 

#### <a name="ux_host_stack_interface_instance_create"></a><span data-ttu-id="5cc78-2592">ux_host_stack_interface_instance_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2592">ux_host_stack_interface_instance_create</span></span>

<span data-ttu-id="5cc78-2593">**Icona** ![ di Icona di creazione dell'istanza dell'interfaccia dello stack host](./media/user-guide/usbx-events/image206.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2593">**Icon** ![Host Stack Interface Instance Create icon](./media/user-guide/usbx-events/image206.png)</span></span>

<span data-ttu-id="5cc78-2594">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2594">**Description**</span></span>

<span data-ttu-id="5cc78-2595">Questo evento rappresenta un evento di creazione dell'istanza dell'interfaccia dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2595">This event represents a USBX Host Stack Interface Instance Create Event.</span></span>

<span data-ttu-id="5cc78-2596">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2596">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2597">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2597">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-2598">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2598">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2599">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2599">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2600">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2600">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-instance-delete"></a><span data-ttu-id="5cc78-2601">Eliminazione istanza interfaccia stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2601">Host Stack Interface Instance Delete</span></span> 

#### <a name="ux_host_stack_interface_instance_delete"></a><span data-ttu-id="5cc78-2602">ux_host_stack_interface_instance_delete</span><span class="sxs-lookup"><span data-stu-id="5cc78-2602">ux_host_stack_interface_instance_delete</span></span>

<span data-ttu-id="5cc78-2603">**Icona** ![ di Icona di eliminazione istanza interfaccia stack host](./media/user-guide/usbx-events/image207.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2603">**Icon** ![Host Stack Interface Instance Delete icon](./media/user-guide/usbx-events/image207.png)</span></span>

<span data-ttu-id="5cc78-2604">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2604">**Description**</span></span>

<span data-ttu-id="5cc78-2605">Questo evento rappresenta un evento di eliminazione dell'istanza dell'interfaccia dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2605">This event represents a USBX Host Stack Interface Instance Delete Event.</span></span>

<span data-ttu-id="5cc78-2606">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2606">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2607">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2607">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-2608">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2608">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2609">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2609">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2610">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2610">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-set"></a><span data-ttu-id="5cc78-2611">Set di interfacce dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2611">Host Stack Interface Set</span></span> 

#### <a name="ux_host_stack_interface_set"></a><span data-ttu-id="5cc78-2612">ux_host_stack_interface_set</span><span class="sxs-lookup"><span data-stu-id="5cc78-2612">ux_host_stack_interface_set</span></span>

<span data-ttu-id="5cc78-2613">**Icona** ![ di Icona del set di interfacce dello stack host](./media/user-guide/usbx-events/image208.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2613">**Icon** ![Host Stack Interface Set icon](./media/user-guide/usbx-events/image208.png)</span></span>

<span data-ttu-id="5cc78-2614">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2614">**Description**</span></span>

<span data-ttu-id="5cc78-2615">Questo evento rappresenta un evento set dell'interfaccia dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2615">This event represents a USBX Host Stack Interface Set Event.</span></span>

<span data-ttu-id="5cc78-2616">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2616">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2617">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2617">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-2618">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2618">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2619">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2619">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2620">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2620">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-setting-select"></a><span data-ttu-id="5cc78-2621">Impostazione dell'interfaccia dello stack host Select</span><span class="sxs-lookup"><span data-stu-id="5cc78-2621">Host Stack Interface Setting Select</span></span> 

#### <a name="ux_host_stack_interface_setting_select"></a><span data-ttu-id="5cc78-2622">ux_host_stack_interface_setting_select</span><span class="sxs-lookup"><span data-stu-id="5cc78-2622">ux_host_stack_interface_setting_select</span></span>

<span data-ttu-id="5cc78-2623">**Icona** ![ di Icona di selezione dell'impostazione dell'interfaccia dello stack host](./media/user-guide/usbx-events/image209.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2623">**Icon** ![Host Stack Interface Setting Select icon](./media/user-guide/usbx-events/image209.png)</span></span>

<span data-ttu-id="5cc78-2624">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2624">**Description**</span></span>

<span data-ttu-id="5cc78-2625">Questo evento rappresenta un'impostazione dell'evento Select dell'interfaccia dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2625">This event represents a USBX Host Stack Interface Setting Select Event.</span></span>

<span data-ttu-id="5cc78-2626">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2626">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2627">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2627">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-2628">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2628">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2629">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2629">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2630">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2630">Info Field 4: Not used.</span></span>

### <a name="host-stack-new-configuration-create"></a><span data-ttu-id="5cc78-2631">Creazione della nuova configurazione dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2631">Host Stack New Configuration Create</span></span> 

#### <a name="ux_host_stack_new_configuration_create"></a><span data-ttu-id="5cc78-2632">ux_host_stack_new_configuration_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2632">ux_host_stack_new_configuration_create</span></span>

<span data-ttu-id="5cc78-2633">**Icona** ![ di Icona di creazione nuova configurazione dello stack host](./media/user-guide/usbx-events/image210.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2633">**Icon** ![Host Stack New Configuration Create icon](./media/user-guide/usbx-events/image210.png)</span></span>

<span data-ttu-id="5cc78-2634">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2634">**Description**</span></span>
 
<span data-ttu-id="5cc78-2635">Questo evento rappresenta uno stack host USBX nuovo evento di creazione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2635">This event represents a USBX Host Stack New Configuration Create Event.</span></span>

<span data-ttu-id="5cc78-2636">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2636">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2637">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2637">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2638">Campo informazioni 2: configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2638">Info Field 2: Configuration.</span></span>
- <span data-ttu-id="5cc78-2639">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2639">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2640">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2640">Info Field 4: Not used.</span></span>

### <a name="host-stack-new-device-create"></a><span data-ttu-id="5cc78-2641">Stack host creazione nuovo dispositivo</span><span class="sxs-lookup"><span data-stu-id="5cc78-2641">Host Stack New Device Create</span></span> 

#### <a name="ux_host_stack_new_device_create"></a><span data-ttu-id="5cc78-2642">ux_host_stack_new_device_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2642">ux_host_stack_new_device_create</span></span>

<span data-ttu-id="5cc78-2643">**Icona** ![ di Icona di creazione nuovo dispositivo dello stack host](./media/user-guide/usbx-events/image211.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2643">**Icon** ![Host Stack New Device Create icon](./media/user-guide/usbx-events/image211.png)</span></span>

<span data-ttu-id="5cc78-2644">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2644">**Description**</span></span>
 
 <span data-ttu-id="5cc78-2645">Questo evento rappresenta un nuovo evento di creazione del dispositivo di stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2645">This event represents a USBX Host Stack New Device Create Event.</span></span>

<span data-ttu-id="5cc78-2646">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2646">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2647">Campo informazioni 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2647">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="5cc78-2648">Informazioni sul campo 2: proprietario del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2648">Info Field 2: Device owner.</span></span>
- <span data-ttu-id="5cc78-2649">Campo informazioni 3: Indice porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2649">Info Field 3: Port index.</span></span>
- <span data-ttu-id="5cc78-2650">Informazioni sul campo 4: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2650">Info Field 4: Device.</span></span>

### <a name="host-stack-new-endpoint-create"></a><span data-ttu-id="5cc78-2651">Creazione di un nuovo endpoint dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2651">Host Stack New Endpoint Create</span></span> 

#### <a name="ux_host_stack_new_endpoint_create"></a><span data-ttu-id="5cc78-2652">ux_host_stack_new_endpoint_create</span><span class="sxs-lookup"><span data-stu-id="5cc78-2652">ux_host_stack_new_endpoint_create</span></span>

<span data-ttu-id="5cc78-2653">**Icona** ![ di Icona di creazione nuovo endpoint dello stack host](./media/user-guide/usbx-events/image212.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2653">**Icon** ![Host Stack New Endpoint Create icon](./media/user-guide/usbx-events/image212.png)</span></span>

<span data-ttu-id="5cc78-2654">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2654">**Description**</span></span>
 
<span data-ttu-id="5cc78-2655">Questo evento rappresenta uno stack host USBX nuovo evento di creazione endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2655">This event represents a USBX Host Stack New Endpoint Create Event.</span></span>

<span data-ttu-id="5cc78-2656">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2656">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2657">Informazioni sul campo 1: interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2657">Info Field 1: Interface.</span></span>
- <span data-ttu-id="5cc78-2658">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2658">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2659">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2659">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2660">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2660">Info Field 4: Not used.</span></span>

### <a name="host-stack-root-hub-change-process"></a><span data-ttu-id="5cc78-2661">Processo di modifica dell'hub radice dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2661">Host Stack Root Hub Change Process</span></span> 

#### <a name="ux_host_stack_rh_change_process"></a><span data-ttu-id="5cc78-2662">ux_host_stack_rh_change_process</span><span class="sxs-lookup"><span data-stu-id="5cc78-2662">ux_host_stack_rh_change_process</span></span>

<span data-ttu-id="5cc78-2663">**Icona** ![ di Icona del processo di modifica dell'hub radice dello stack host](./media/user-guide/usbx-events/image213.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2663">**Icon** ![Host Stack Root Hub Change Process icon](./media/user-guide/usbx-events/image213.png)</span></span>

<span data-ttu-id="5cc78-2664">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2664">**Description**</span></span>
 
<span data-ttu-id="5cc78-2665">Questo evento rappresenta un processo di modifica dell'hub radice dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2665">This event represents a USBX Host Stack Root Hub Change Process.</span></span>

<span data-ttu-id="5cc78-2666">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2666">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2667">Info Field 1: Port index.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2667">Info Field 1: Port index.</span></span>
- <span data-ttu-id="5cc78-2668">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2668">Info Field 2: Not used.</span></span>
- <span data-ttu-id="5cc78-2669">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2669">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2670">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2670">Info Field 4: Not used.</span></span>

### <a name="host-stack-root-hub-device-extraction"></a><span data-ttu-id="5cc78-2671">Estrazione dispositivo hub radice stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2671">Host Stack Root Hub Device Extraction</span></span> 

#### <a name="ux_host_stack_rh_device_extraction"></a><span data-ttu-id="5cc78-2672">ux_host_stack_rh_device_extraction</span><span class="sxs-lookup"><span data-stu-id="5cc78-2672">ux_host_stack_rh_device_extraction</span></span>

<span data-ttu-id="5cc78-2673">**Icona** ![ di Icona di estrazione dispositivo hub radice dello stack host](./media/user-guide/usbx-events/image214.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2673">**Icon** ![Host Stack Root Hub Device Extraction icon](./media/user-guide/usbx-events/image214.png)</span></span>

<span data-ttu-id="5cc78-2674">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2674">**Description**</span></span>

<span data-ttu-id="5cc78-2675">Questo evento rappresenta un evento di estrazione del dispositivo dell'hub radice dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2675">This event represents a USBX Host Stack Root Hub Device Extraction Event.</span></span>

<span data-ttu-id="5cc78-2676">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2676">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2677">Campo informazioni 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2677">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="5cc78-2678">Informazioni sul campo 2: Indice porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2678">Info Field 2: Port index.</span></span>
- <span data-ttu-id="5cc78-2679">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2679">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2680">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2680">Info Field 4: Not used.</span></span>

### <a name="host-stack-root-hub-device-insertion"></a><span data-ttu-id="5cc78-2681">Inserimento dispositivo hub radice stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2681">Host Stack Root Hub Device Insertion</span></span> 

#### <a name="ux_host_stack_rh_device_insertion"></a><span data-ttu-id="5cc78-2682">ux_host_stack_rh_device_insertion</span><span class="sxs-lookup"><span data-stu-id="5cc78-2682">ux_host_stack_rh_device_insertion</span></span>

<span data-ttu-id="5cc78-2683">**Icona** ![ di Icona di inserimento dispositivo hub radice stack host](./media/user-guide/usbx-events/image215.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2683">**Icon** ![Host Stack Root Hub Device Insertion icon](./media/user-guide/usbx-events/image215.png)</span></span>

<span data-ttu-id="5cc78-2684">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2684">**Description**</span></span>

<span data-ttu-id="5cc78-2685">Questo evento rappresenta l'inserimento di un dispositivo hub radice dello stack host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2685">This event represents a USBX Host Stack Root Hub Device Insertion.</span></span>

<span data-ttu-id="5cc78-2686">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2686">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2687">Campo informazioni 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2687">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="5cc78-2688">Informazioni sul campo 2: Indice porta.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2688">Info Field 2: Port index.</span></span>
- <span data-ttu-id="5cc78-2689">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2689">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2690">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2690">Info Field 4: Not used.</span></span>

### <a name="host-stack-transfer-request"></a><span data-ttu-id="5cc78-2691">Richiesta di trasferimento dello stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2691">Host Stack Transfer Request</span></span> 

#### <a name="ux_host_stack_transfer_request"></a><span data-ttu-id="5cc78-2692">ux_host_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="5cc78-2692">ux_host_stack_transfer_request</span></span>

<span data-ttu-id="5cc78-2693">**Icona** ![ di Icona della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image216.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2693">**Icon** ![Host Stack Transfer Request icon](./media/user-guide/usbx-events/image216.png)</span></span>

<span data-ttu-id="5cc78-2694">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2694">**Description**</span></span>

<span data-ttu-id="5cc78-2695">Questo evento rappresenta una richiesta di trasferimento dello stack dell'host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2695">This event represents a USBX Host Stack Transfer Request.</span></span>

<span data-ttu-id="5cc78-2696">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2696">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2697">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2697">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2698">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2698">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2699">Campo informazioni 3: richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2699">Info Field 3: Transfer request.</span></span>
- <span data-ttu-id="5cc78-2700">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2700">Info Field 4: Not used.</span></span>

### <a name="host-stack-transfer-request-abort"></a><span data-ttu-id="5cc78-2701">Interruzione richiesta trasferimento stack host</span><span class="sxs-lookup"><span data-stu-id="5cc78-2701">Host Stack Transfer Request Abort</span></span> 

#### <a name="internal-io-driver-get-status"></a><span data-ttu-id="5cc78-2702">Stato Get driver I/O interno</span><span class="sxs-lookup"><span data-stu-id="5cc78-2702">Internal I/O driver get status</span></span>

<span data-ttu-id="5cc78-2703">**Icona** ![ di Icona di interruzione della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image217.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2703">**Icon** ![Host Stack Transfer Request Abort icon](./media/user-guide/usbx-events/image217.png)</span></span>

<span data-ttu-id="5cc78-2704">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2704">**Description**</span></span>

<span data-ttu-id="5cc78-2705">Questo evento rappresenta un'interruzione della richiesta di trasferimento dello stack dell'host USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2705">This event represents a USBX Host Stack Transfer Request Abort.</span></span>

<span data-ttu-id="5cc78-2706">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2706">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2707">Informazioni sul campo 1: dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2707">Info Field 1: Device.</span></span>
- <span data-ttu-id="5cc78-2708">Campo informazioni 2: endpoint.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2708">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="5cc78-2709">Campo informazioni 3: richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2709">Info Field 3: Transfer request.</span></span>
- <span data-ttu-id="5cc78-2710">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2710">Info Field 4: Not used.</span></span>

### <a name="usbx-error"></a><span data-ttu-id="5cc78-2711">Errore USBX</span><span class="sxs-lookup"><span data-stu-id="5cc78-2711">USBX Error</span></span> 

#### <a name="ux_error"></a><span data-ttu-id="5cc78-2712">ux_error</span><span class="sxs-lookup"><span data-stu-id="5cc78-2712">ux_error</span></span>

<span data-ttu-id="5cc78-2713">**Icona** ![ di Icona di errore U S B X](./media/user-guide/usbx-events/image218.png)</span><span class="sxs-lookup"><span data-stu-id="5cc78-2713">**Icon** ![U S B X Error icon](./media/user-guide/usbx-events/image218.png)</span></span>

<span data-ttu-id="5cc78-2714">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2714">**Description**</span></span>

<span data-ttu-id="5cc78-2715">Questo evento rappresenta un evento di errore USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2715">This event represents a USBX Error Event.</span></span>

<span data-ttu-id="5cc78-2716">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="5cc78-2716">**Information Fields**</span></span>

- <span data-ttu-id="5cc78-2717">Campo informazioni 1: errore USBX.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2717">Info Field 1: USBX error.</span></span>
- <span data-ttu-id="5cc78-2718">Informazioni sul campo 2: nome dell'errore.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2718">Info Field 2: Error Name.</span></span>
- <span data-ttu-id="5cc78-2719">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2719">Info Field 3: Not used.</span></span>
- <span data-ttu-id="5cc78-2720">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5cc78-2720">Info Field 4: Not used.</span></span>