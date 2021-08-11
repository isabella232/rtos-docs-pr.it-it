---
title: Capitolo 9 - Azure RTOS eventi di traccia USBX
description: Questo capitolo contiene una descrizione dei Azure RTOS USBX visualizzati da TraceX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 015e5feedd1d5e90c6491e156c2d0d57a9abaa47518868d375a34e618770d4aa
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116793967"
---
# <a name="chapter-9---azure-rtos-usbx-trace-events"></a>Capitolo 9 - Azure RTOS eventi di traccia USBX

Questo capitolo contiene una descrizione dei Azure RTOS USBX visualizzati da TraceX. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

Di seguito è riportato un elenco di eventi USBX visualizzati da TraceX.

| Icona                             | Significato                               |
| -------------------------------- | ------------------------------------- |
| ![Icona Device Class C D C Activate](./media/user-guide/usbx-events/image1.png)    | **Classe di dispositivo Cdc Activate** *(ux_device_class_cdc_activate)* |
| ![Icona Disattiva classe dispositivo C D C](./media/user-guide/usbx-events/image2.png)    | **Classe device Cdc Deactivate** *(ux_device_class_cdc_deactivate)* |
| ![Icona Di lettura classe dispositivo C D C](./media/user-guide/usbx-events/image3.png)    | **Classe device Cdc Read** *(ux_device_class_cdc_read)* |
| ![Icona di scrittura della classe dispositivo C D C](./media/user-guide/usbx-events/image4.png)    | **Classe device Cdc Write** *(ux_device_class_cdc_write)* |
| ![Icona Device Class Dpump Activate](./media/user-guide/usbx-events/image5.png)    | **Device Class Dpump Activate** *(ux_device_class_dpump_activate)* |
| ![Icona Device Class Dpump Deactivate](./media/user-guide/usbx-events/image6.png)    | **Device Class Dpump Deactivate** *(ux_device_class_dpump_deactivate)* |
| ![Icona di lettura Dpump classe dispositivo](./media/user-guide/usbx-events/image7.png)    | **Classe Device Dpump Read** *(ux_device_class_dpump_read)* |
| ![Icona di scrittura Dpump classe dispositivo](./media/user-guide/usbx-events/image8.png)    | **Classe Device Dpump Write** *(ux_device_class_dpump_write)* |
| ![Icona Hid Activate della classe device](./media/user-guide/usbx-events/image9.png)    | **Classe Device Hid Activate** *(ux_device_class_hid_activate)* |
| ![Icona Hid Deactivate della classe device](./media/user-guide/usbx-events/image10.png)    | **Classe Device Hid Deactivate** *(ux_device_class_hid_deactivate)* |
| ![Icona Device Class Hid Descriptor Send](./media/user-guide/usbx-events/image11.png)    | **Device Class Hid Descriptor Send** *(ux_device_class_hid_descriptor_send)* |
| ![Icona Device Class Hid Event Get](./media/user-guide/usbx-events/image12.png)    | **Device Class Hid Event Get** *(ux_device_class_hid_event_get)* |
| ![Icona Del set di eventi Hid della classe di dispositivi](./media/user-guide/usbx-events/image13.png)    | **Set di eventi Hid** della classe device *(ux_device_class_hid_event_set)* |
| ![Icona Scarica report hid classe dispositivo](./media/user-guide/usbx-events/image14.png)    | **Device Class Hid Report Get** *(ux_device_class_hid_report_get)* |
| ![Icona Device Class Hid Report Set](./media/user-guide/usbx-events/image15.png)    | **Set di report hid** *classe dispositivo (ux_device_class_hid_report_set)* |
| ![Icona Device Class Pima Activate](./media/user-guide/usbx-events/image16.png)    | **Device Class Pima Activate** *(ux_device_class_pima_activate)* |
| ![Icona Device Class Pima Deactivate](./media/user-guide/usbx-events/image17.png)    | **Device Class Pima Deactivate** *(ux_device_class_pima_deactivate)* |
| ![Icona Device Class Pima Device Info Send](./media/user-guide/usbx-events/image18.png)    | **Device Class Pima Device Info Send** *(ux_device_class_pima_device_info_send)* |
| ![Icona Device Class Pima Event Get](./media/user-guide/usbx-events/image19.png)    | **Device Class Pima Event Get** *(ux_device_class_pima_event_get)* |
| ![Icona Device Class Pima Event Set](./media/user-guide/usbx-events/image20.png)    | **Device Class Pima Event Set** *(ux_device_class_pima_event_set)* |
| ![Icona Aggiungi oggetto Pima della classe device](./media/user-guide/usbx-events/image21.png)    | **Classe Device Pima Object Add** *(ux_device_class_pima_object_add)* |
| ![Icona Device Class Pima Object Data Get](./media/user-guide/usbx-events/image22.png)    | **Device Class Pima Object Data Get** *(ux_device_class_pima_object_data_get)* |
| ![Icona Device Class Pima Object Data Send](./media/user-guide/usbx-events/image23.png)    | **Classe Device Pima Object Data Send** *(ux_device_class_pima_object_data_send)* |
| ![Icona Device Class Pima Object Delete](./media/user-guide/usbx-events/image24.png)    | **Classe Device Pima Object Delete** *(ux_device_class_pima_object_delete)* |
| ![Icona Device Class Pima Object Handles Send](./media/user-guide/usbx-events/image25.png)    | **La classe Device Pima gestisce l'invio** *(ux_device_class_pima_object_handles_send)* |
| ![Icona Device Class Pima Object Info Get](./media/user-guide/usbx-events/image26.png)    | **Device Class Pima Object Info Get** *(ux_device_class_pima_object_info_get)* |
| ![Icona Device Class Pima Object Info Send](./media/user-guide/usbx-events/image27.png)    | **Classe device Pima Object Info Send** *(ux_device_class_pima_object_info_send)* |
| ![Icona Device Class Pima Objects Number Send](./media/user-guide/usbx-events/image28.png)    | **Classe device Pima Objects Number Send** *(ux_device_class_pima_objects_number_send)* |
| ![Icona Device Class Pima Partial Object Data Get](./media/user-guide/usbx-events/image29.png)    | **Device Class Pima Partial Object Data Get** *(ux_device_class_pima_partial_object_data_get)* |
| ![Icona Device Class Pima Response Send](./media/user-guide/usbx-events/image30.png)    | **Classe dispositivo Pima Response Send** *(ux_device_class_pima_response_send)*|
| ![Icona Device Class Pima Archiviazione I D Send](./media/user-guide/usbx-events/image31.png)    | **Device Class Pima Archiviazione ID Send** *(ux_device_class_pima_storage_id_send)* |
| ![Icona Device Class Pima Archiviazione Info Send](./media/user-guide/usbx-events/image32.png)    | **Classe device Pima Archiviazione Info Send** *(ux_device_class_pima_storage_info_send)* |
| ![Icona Device Class R N D I S Activate (Classe dispositivo R N D I S Activate)](./media/user-guide/usbx-events/image33.png)    | **Device Class Rndis Activate** *(ux_device_class_rndis_activate)* |
| ![Icona Disattiva classe dispositivo R N D I S](./media/user-guide/usbx-events/image34.png)    | **Device Class Rndis Deactivate** *(ux_device_class_rndis_deactivate)* |
| ![Classe di dispositivo R N D I S Message Keep Aliveicon](./media/user-guide/usbx-events/image35.png)    | **Classe dispositivo Rndis Message Keep Alive** *(ux_device_class_rndis_msg_keep_alive)* |
| ![Icona query messaggi classe dispositivo R N D I S](./media/user-guide/usbx-events/image36.png)    | **Query dei messaggi Rndis della** classe del *dispositivo (ux_device_class_rndis_msg_query)* |
| ![Icona Reimpostazione messaggio classe dispositivo R N D I S](./media/user-guide/usbx-events/image37.png)    | **Reimpostazione dei messaggi Rndis della** *classe del dispositivo (ux_device_class_rndis_msg_reset)* |
| ![Icona Device Class R N D I S Message Set](./media/user-guide/usbx-events/image38.png)    | **Classe dispositivo Rndis Message Set** *(ux_device_class_rndis_msg_set)* |
| ![Classe di dispositivo R N D I S Packet Receive icona](./media/user-guide/usbx-events/image39.png)    | **Classe dispositivo Rndis Packet Receive** *(ux_device_class_rndis_packet_receive)* |
| ![Classe di dispositivo R N D I S Packet Transmit icona](./media/user-guide/usbx-events/image40.png)    | **Trasmissione pacchetti Rndis** della classe dispositivo *(ux_device_class_rndis_packet_transmit)* |
| ![Icona Attiva Archiviazione Classe dispositivo](./media/user-guide/usbx-events/image41.png)    | **Classe Device Archiviazione Activate** *(ux_device_class_storage_activate)* |
| ![Icona Disattiva Archiviazione Classe dispositivo](./media/user-guide/usbx-events/image42.png)    | **Classe Device Archiviazione Deactivate** *(ux_device_class_storage_deactivate)* |
| ![Icona Formato Archiviazione classe dispositivo](./media/user-guide/usbx-events/image43.png)    | **Formato Archiviazione dispositivo** *(ux_device_class_storage_format)* |
| ![Icona Richiesta Archiviazione classe dispositivo](./media/user-guide/usbx-events/image44.png)    | **Richiesta di informazioni Archiviazione classe** dispositivo *(ux_device_class_storage_inquiry)* |
| ![Icona Di selezione Archiviazione classe dispositivo](./media/user-guide/usbx-events/image45.png)    | **Classe Device Archiviazione Mode Select** *(ux_device_class_storage_mode_select)* |
| ![Icona Device Class Archiviazione Mode Sense](./media/user-guide/usbx-events/image46.png)    | **Device Class Archiviazione Mode Sense** *(ux_device_class_storage_mode_sense)* |
| ![Icona Impedisci rimozione supporti Archiviazione classe dispositivo](./media/user-guide/usbx-events/image47.png)    | **Classe device Archiviazione Impedisci rimozione supporti** *(ux_device_class_storage_prevent_allow_media_removal)* |
| ![Icona Lettura della Archiviazione dispositivo](./media/user-guide/usbx-events/image48.png)    | **Classe Device Archiviazione Read** *(ux_device_class_storage_read)* |
| ![Icona Della capacità Archiviazione di lettura della classe di dispositivi](./media/user-guide/usbx-events/image49.png)    | **Capacità di lettura Archiviazione dispositivi** *(ux_device_class_storage_read_capacity)* |
| ![Icona Della capacità Archiviazione classe di dispositivi per la lettura del formato](./media/user-guide/usbx-events/image50.png)    | **Capacità del formato Archiviazione dispositivo** *(ux_device_class_storage_read_format_capacity)* |
| ![Icona Del sommario Archiviazione classe dispositivo](./media/user-guide/usbx-events/image51.png)    | **Classe device Archiviazione Lettura sommario** *(ux_device_class_storage_read_toc)* |
| ![Icona Di classe Archiviazione richiesta di senso](./media/user-guide/usbx-events/image52.png)    | **Device Class Archiviazione Request Sense** *(ux_device_class_storage_request_sense)* |
| ![Classe dispositivo Archiviazione'icona Avvia arresto](./media/user-guide/usbx-events/image53.png)    | **Classe device Archiviazione Start Stop** *(ux_device_class_storage_start_stop)* |
| ![Icona Di classe Archiviazione test pronto](./media/user-guide/usbx-events/image54.png)    | **Classe device Archiviazione test ready** *(ux_device_class_storage_test_ready)* |
| ![Icona Verifica Archiviazione dispositivo](./media/user-guide/usbx-events/image55.png)    | **Verifica della Archiviazione dispositivo** *(ux_device_class_storage_verify)* |
| ![Icona Di scrittura Archiviazione dispositivo](./media/user-guide/usbx-events/image56.png)    | **Classe Device Archiviazione Write** *(ux_device_class_storage_write)* |
| ![Icona Get dell'impostazione alternativa dello stack di dispositivi](./media/user-guide/usbx-events/image57.png)    | **Get dell'impostazione alternativa dello stack** di *dispositivi (ux_device_stack_alternate_setting_get)* |
| ![Icona del set di impostazioni alternativo dello stack di dispositivi](./media/user-guide/usbx-events/image58.png)    | **Set di impostazioni alternative dello stack** di dispositivi *(ux_device_stack_alternate_setting_set)* |
| ![Icona Device Stack Class Register](./media/user-guide/usbx-events/image59.png)    | **Registro classi dello stack di** dispositivi *(ux_device_stack_class_register)* |
| ![Icona della funzionalità di cancellazione dello stack di dispositivi](./media/user-guide/usbx-events/image60.png)    | **Funzionalità di cancellazione dello stack** *di dispositivi (ux_device_stack_clear_feature)* |
| ![Icona Get della configurazione dello stack di dispositivi](./media/user-guide/usbx-events/image61.png)    | **Device Stack Configuration Get** *(ux_device_stack_configuration_get)* |
| ![Icona del set di configurazione dello stack di dispositivi](./media/user-guide/usbx-events/image62.png)    | **Set di configurazione dello stack di** dispositivi *(ux_device_stack_configuration_set)* |
| ![Icona di stack Connessione dispositivo](./media/user-guide/usbx-events/image63.png)    | **Device Stack Connessione** *(ux_device_stack_connect)* |
| ![Icona Device Stack Descriptor Send (Invio descrittore stack dispositivi)](./media/user-guide/usbx-events/image64.png)    | **Device Stack Descriptor Send** *(ux_device_stack_descriptor_send)* |
| ![Icona di disconnessione dello stack di dispositivi](./media/user-guide/usbx-events/image65.png)    | **Disconnessione dello stack di** *dispositivi (ux_device_stack_disconnect)* |
| ![Icona di blocco dell'endpoint dello stack di dispositivi](./media/user-guide/usbx-events/image66.png)    | **Blocco dell'endpoint dello stack** *di dispositivi (ux_device_stack_endpoint_stall)* |
| ![Icona Get Status (Ottieni stato) dello stack di dispositivi](./media/user-guide/usbx-events/image67.png)    | **Device Stack Get Status** *(Ux_device_stack_get_status)* |
| ![Icona di riattivazione dell'host dello stack di dispositivi](./media/user-guide/usbx-events/image68.png)    | **Riattivazione host** dello stack di *dispositivi (ux_device_stack_host_wakeup)* |
| ![Icona Device Stack Initialize (Inizializza stack di dispositivi)](./media/user-guide/usbx-events/image69.png)    | **Inizializzazione dello stack** *di dispositivi (ux_device_stack_initialize)* |
| ![Icona di eliminazione dell'interfaccia dello stack di dispositivi](./media/user-guide/usbx-events/image70.png)    | **Eliminazione dell'interfaccia** dello stack *di dispositivi (ux_device_stack_interface_delete)* |
| ![Icona Get dell'interfaccia dello stack di dispositivi](./media/user-guide/usbx-events/image71.png)    | **Device Stack Interface Get** *(ux_device_stack_interface_get)* |
| ![Icona del set di interfacce dello stack di dispositivi](./media/user-guide/usbx-events/image72.png)    | **Device Stack Interface Set** *(ux_device_stack_interface_set)* |
| ![Icona della funzionalità Set di stack di dispositivi](./media/user-guide/usbx-events/image73.png)    | **Funzionalità set di stack di** dispositivi *(ux_device_stack_set_feature)* |
| ![Icona di interruzione del trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image74.png)    | **Interruzione del trasferimento dello stack** di dispositivi *(ux_device_stack_transfer_abort)* |
| ![*Icona Device Stack Transfer All Request Abort](./media/user-guide/usbx-events/image75.png)    | **Device Stack Transfer All Request Abort (Interrompi tutte** le richieste di trasferimento dello stack *di dispositivi) (ux_device_stack_transfer_all_request_abort)* |
| ![Icona della richiesta di trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image76.png)    | **Richiesta di trasferimento dello stack di** dispositivi *(ux_device_stack_transfer_request)* |
| ![Icona Asix Activate della classe host](./media/user-guide/usbx-events/image77.png)    | **Classe host Asix Activate** *(ux_host_class_asix_activate)* |
| ![Icona Asix Deactivate della classe host](./media/user-guide/usbx-events/image78.png)    | **Classe host Asix Deactivate** *(ux_host_class_asix_deactivate)* |
| ![Icona asix Interrupt Notification della classe host](./media/user-guide/usbx-events/image79.png)    | **Notifica di interrupt Asix** *della classe host (ux_host_class_asix_interrupt_notification)* |
| ![Icona Asix Read della classe host](./media/user-guide/usbx-events/image80.png)    | **Classe host Asix Read** *(ux_host_class_asix_read)* |
| ![Icona asix write della classe host](./media/user-guide/usbx-events/image81.png)    | **Classe host Asix Write** *(ux_host_class_asix_write)* |
| ![Icona di attivazione audio della classe host](./media/user-guide/usbx-events/image82.png)    | **Host Class Audio Activate** *(ux_host_class_audio_activate)* |
| ![Icona Get del valore del controllo audio della classe host](./media/user-guide/usbx-events/image83.png)    | **Host Class Audio Control Value Get** *(ux_host_class_audio_control_value_get)* |
| ![Icona del set di valori del controllo audio della classe host](./media/user-guide/usbx-events/image84.png)    | **Set di valori di controllo audio della** classe host *(ux_host_class_audio_control_value_set)* |
| ![Icona Disattiva audio classe host](./media/user-guide/usbx-events/image85.png)    | **Host Class Audio Deactivate** *(ux_host_class_audio_deactivate)* |
| ![Icona di lettura audio della classe host](./media/user-guide/usbx-events/image86.png)    | **Lettura audio classe host** *(ux_host_class_audio_read)* |
| ![Icona Get del campionamento di streaming audio della classe host](./media/user-guide/usbx-events/image87.png)    | **Get di campionamento del flusso audio** *della classe host (ux_host_class_audio_streaming_sampling_get)* |
| ![Icona del set di campionamento di streaming audio della classe host](./media/user-guide/usbx-events/image88.png)    | **Set di campionamento di streaming audio** *della classe host (ux_host_class_audio_streaming_sampling_set)* |
| ![Icona di scrittura audio della classe host](./media/user-guide/usbx-events/image89.png)    | **Scrittura audio classe** *host (ux_host_class_audio_write)* |
| ![Icona di attivazione della classe host C D C A C M](./media/user-guide/usbx-events/image90.png)    | **Classe host Cdc Acm Activate** *(ux_host_class_cdc_acm_activate)* |
| ![Host Class C D C A C M Deactivate icon (Classe host C D C A C M Disattiva)](./media/user-guide/usbx-events/image91.png)    | **Host Class Cdc Acm Deactivate** *(ux_host_class_cdc_acm_deactivate)* |
| ![Classe host C D C A C M I O C T L Nella pipe icona](./media/user-guide/usbx-events/image92.png)    | **Classe host Cdc Acm Ioctl Abort nella pipe** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)* |
| ![Classe host C D C A C M I O C T L Icona interrompi pipe](./media/user-guide/usbx-events/image93.png)    | **Classe host Cdc Acm Ioctl Abort Out Pipe** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)* |
| ![Classe host C D C A C M I O C T L Icona Ottieni stato dispositivo](./media/user-guide/usbx-events/image94.png)    | **Classe host Cdc Acm Ioctl Get Device Status** *(ux_host_class_cdc_acm_ioctl_get_device_status)* |
| ![Classe host C D C A C M I O C T L Icona Get Line Coding](./media/user-guide/usbx-events/image95.png)    | **Classe host Cdc Acm Ioctl Get Line Coding** *(ux_host_class_cdc_acm_ioctl_get_line_coding)* |
| ![Classe host C D C A C M I O C T L Icona callback di notifica](./media/user-guide/usbx-events/image96.png)    | **Classe host Cdc Acm Ioctl Notification Callback** *(ux_host_class_cdc_acm_ioctl_notification_callback)* |
| ![Classe host C D C A C M I O C T L Send Break](./media/user-guide/usbx-events/image97.png)    | **Classe host Cdc Acm Ioctl Send Break** *(ux_host_class_cdc_acm_ioctl_send_break)* |
| ![Classe host C D C A C M I O C T L Imposta line coding](./media/user-guide/usbx-events/image98.png)    | **Classe host Cdc Acm Ioctl Set Line Coding** *(ux_host_class_cdc_acm_ioctl_set_line_coding)* |
| ![Classe host C D C A C M I O C T L Imposta stato riga](./media/user-guide/usbx-events/image99.png)    | **Classe host Cdc Acm Ioctl Set Line State** *(ux_host_class_cdc_acm_ioctl_set_line_state)* |
| ![Icona di lettura della classe host C D C A C M](./media/user-guide/usbx-events/image100.png)    | **Classe host Cdc Acm Read** *(ux_host_class_cdc_acm_read)* |
| ![Icona di avvio della ricezione della classe host C D C A C M](./media/user-guide/usbx-events/image101.png)    | **Inizio ricezione classe host Cdc Acm** *(ux_host_class_cdc_acm_reception_start)* |
| ![Icona arresto ricezione classe host C D C A C M](./media/user-guide/usbx-events/image102.png)    | **Host Class Cdc Acm Reception Stop** *(ux_host_class_cdc_acm_reception_stop)* |
| ![Icona di scrittura della classe host C D C A C M](./media/user-guide/usbx-events/image103.png)    | **Classe host Cdc Acm Write** *(ux_host_class_cdc_acm_write)* |
| ![Icona Dpump Activate della classe host](./media/user-guide/usbx-events/image104.png)    | **Classe host Dpump Activate** *(ux_host_class_dpump_activate)* |
| ![Icona Disattiva Dpump della classe host](./media/user-guide/usbx-events/image105.png)    | **Classe host Dpump Deactivate** *(ux_host_class_dpump_deactivate)* |
| ![Icona di lettura Dpump della classe host](./media/user-guide/usbx-events/image106.png)    | **Lettura Dpump della classe** host *(ux_host_class_dpump_read)* |
| ![Icona di scrittura Dpump della classe host](./media/user-guide/usbx-events/image107.png)    | **Classe host Dpump Write** *(ux_host_class_dpump_write)* |
| ![Icona Hid Activate della classe host](./media/user-guide/usbx-events/image108.png)    | **Classe host Hid Activate** *(ux_host_class_hid_activate)* |
| ![Icona Registro client Hid della classe host](./media/user-guide/usbx-events/image109.png)    | **Registro client hid** della classe host *(ux_host_class_hid_client_register)* |
| ![Icona Hid Deactivate della classe host](./media/user-guide/usbx-events/image110.png)    | **Classe host Hid Deactivate** *(ux_host_class_hid_deactivate)* |
| ![Icona Hid Idle Get della classe host](./media/user-guide/usbx-events/image111.png)    | **Classe host Hid Idle Get** *(ux_host_class_hid_idle_get)* |
| ![Icona Hid Idle Set della classe host](./media/user-guide/usbx-events/image112.png)    | **Host Class Hid Idle Set** *(ux_host_class_hid_idle_set)* |
| ![Icona di attivazione della tastiera hid della classe host](./media/user-guide/usbx-events/image113.png)    | **Classe host Hid Keyboard Activate** *(ux_host_class_hid_keyboard_activate)* |
| ![Icona Disattiva tastiera hid della classe host](./media/user-guide/usbx-events/image114.png)    | **Host Class Hid Keyboard Deactivate** *(ux_host_class_hid_keyboard_deactivate)* |
| ![Icona Hid Mouse Activate della classe host](./media/user-guide/usbx-events/image115.png)    | **Classe host Hid Mouse Activate** *(ux_host_class_hid_mouse_activate)* |
| ![Icona di disattivazione del mouse hid della classe host](./media/user-guide/usbx-events/image116.png)    | **Host Class Hid Mouse Deactivate** *(ux_host_class_hid_mouse_deactivate)* |
| ![Icona di attivazione del controllo remoto hid della classe host](./media/user-guide/usbx-events/image117.png)    | **Classe host Hid Remote Control Activate** *(ux_host_class_hid_remote_control_activate)* |
| ![Icona Disattiva controllo remoto hid della classe host](./media/user-guide/usbx-events/image118.png)    | **Host Class Hid Remote Control Deactivate** *(ux_host_class_hid_remote_control_deactivate)* |
| ![Icona Del report Hid Get della classe host](./media/user-guide/usbx-events/image119.png)    | **Classe host Hid Report Get** *(ux_host_class_hid_report_get)* |
| ![Icona Del set di report hid della classe host](./media/user-guide/usbx-events/image120.png)    | **Set di report hid** della classe host *(ux_host_class_hid_report_set)* |
| ![Icona attiva dell'hub della classe host](./media/user-guide/usbx-events/image121.png)    | **Attivazione dell'hub** *di classe host (ux_host_class_hub_activate)* |
| ![Icona Rilevamento modifiche hub classe host](./media/user-guide/usbx-events/image122.png)    | **Rilevamento modifiche hub classe host** *(ux_host_class_hub_change_detect)* |
| ![*Icona Disattiva hub classe host](./media/user-guide/usbx-events/image123.png)    | **Host Class Hub Deactivate** *(ux_host_class_hub_deactivate)* |
| ![Icona Del processo di connessione per la modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image124.png)    | **Processo di modifica della porta dell'hub** della classe host *(ux_host_class_hub_port_change_connection_process)* |
| ![Icona Abilita processo di abilitazione della modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image125.png)    | **Processo di abilitazione della modifica della porta dell'hub** della classe host *(ux_host_class_hub_port_change_enable_process)* |
| ![Icona Modifica della porta dell'hub della classe host rispetto al processo corrente](./media/user-guide/usbx-events/image126.png)    | **Modifica della porta dell'hub della** classe host rispetto al processo corrente *(ux_host_class_hub_port_change_over_current_process)* |
| ![Icona Processo di reimpostazione della modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image127.png)    | **Processo di reimpostazione della modifica della porta dell'hub** *di classe host (ux_host_class_hub_port_change_reset_process)* |
| ![Icona Del processo di sospensione della modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image128.png)    | **Processo di sospensione della modifica della porta dell'hub** *della classe host (ux_host_class_hub_port_change_suspend_process)* |
| ![Icona di Attivazione pima della classe host](./media/user-guide/usbx-events/image129.png)    | **Classe host Pima Activate** *(ux_host_class_prima_activate)* |
| ![Icona Della classe host Pima Deactivate](./media/user-guide/usbx-events/image130.png)    | **Classe host Pima Deactivate** *(ux_host_class_pima_deactivate)* |
| ![Icona Ottieni informazioni sul dispositivo Pima della classe host](./media/user-guide/usbx-events/image131.png)    | **Classe host Pima Device Info Get** *(ux_host_class_pima_device_info_get)* |
| ![Icona Reimpostazione dispositivo Pima della classe host](./media/user-guide/usbx-events/image132.png)    | **Reimpostazione del dispositivo Pima della** classe host *(ux_host_class_pima_device_reset)* |
| ![Icona di notifica pima della classe host](./media/user-guide/usbx-events/image133.png)    | **Notifica pima della classe host** *(ux_host_class_pima_notification)* |
| ![Icona Get degli oggetti numero della classe host Pima](./media/user-guide/usbx-events/image134.png)    | **Classe host Pima Number Objects Get** *(ux_host_class_pima_num_objects_get)* |
| ![Icona Di chiusura dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image135.png)    | **Classe host Pima Object Close** *(ux_host_class_pima_object_close)* |
| ![Icona Copia oggetto Pima della classe host](./media/user-guide/usbx-events/image136.png)    | **Copia dell'oggetto Pima** della classe host *(ux_host_class_pima_object_copy)* |
| ![Icona di eliminazione di oggetti Pima della classe host](./media/user-guide/usbx-events/image137.png)    | **Classe host Pima Object Delete** *(ux_host_class_pima_object_delete)* |
| ![Icona Get dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image138.png)    | **Classe host Pima Object Get** *(ux_host_class_pima_object_get)* |
| ![Icona Ottieni informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image139.png)    | **Get di informazioni sull'oggetto Pima** *della classe host (ux_host_class_pima_object_info_get)* |
| ![Icona di invio delle informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image140.png)    | **Classe host Pima Object Info Send** *(ux_host_class_pima_object_info_send)* |
| ![Icona di spostamento di oggetti Pima della classe host](./media/user-guide/usbx-events/image141.png)    | **Spostamento di oggetti Pima** *(ux_host_class_pima_object_move)* della classe host |
| ![Icona di invio dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image142.png)    | **Classe host Pima Object Send** *(ux_host_class_pima_object_send)* |
| ![Icona interruzione trasferimento oggetti pima della classe host](./media/user-guide/usbx-events/image143.png)    | **Interruzione del trasferimento di oggetti pima** della classe host *(ux_host_class_object_transfer_abort)* |
| ![Icona Di lettura pima della classe host](./media/user-guide/usbx-events/image144.png)    | **Classe host Pima Read** *(ux_host_class_pima_read)* |
| ![Icona Di annullamento della richiesta pima della classe host](./media/user-guide/usbx-events/image145.png)    | **Classe host Pima Request Cancel** *(ux_host_class_pima_request_cancel)* |
| ![Icona di chiusura della sessione pima della classe host](./media/user-guide/usbx-events/image146.png)    | **Chiusura della sessione pima** della classe host *(ux_host_class_pima_session_close)* |
| ![Icona di apertura della sessione Pima della classe host](./media/user-guide/usbx-events/image147.png)    | **Host Class Pima Session Open** *(ux_host_class_pima_session_open)* |
| ![Icona Get degli ID Archiviazione Pima della classe host](./media/user-guide/usbx-events/image148.png)    | **Host Class Pima Archiviazione Ids Get** *(ux_host_class_pima_storage_ids_get)* |
| ![Icona Ottieni informazioni sulla Archiviazione Pima della classe host](./media/user-guide/usbx-events/image149.png)    | **Classe host Pima Archiviazione Info Get** *(ux_host_class_pima_storage_info_get)* |
| ![Icona Get di Pima Thumb per la classe host](./media/user-guide/usbx-events/image150.png)    | **Classe host Pima Thumb Get** *(ux_host_class_pima_thumb_get)* |
| ![Icona di scrittura pima della classe host](./media/user-guide/usbx-events/image151.png)    | **Classe host Pima Write** *(ux_host_class_pima_write)* |
| ![Icona di attivazione della stampante della classe host](./media/user-guide/usbx-events/image152.png)    | **Host Class Printer Activate** *(ux_host_class_printer_activate)* |
| ![Icona Disattiva stampante classe host](./media/user-guide/usbx-events/image153.png)    | **Host Class Printer Deactivate** *(ux_host_class_printer_deactivate)* |
| ![Icona Get nome stampante classe host](./media/user-guide/usbx-events/image154.png)    | **Classe host Printer Name Get** *(ux_host_class_printer_name_get)* |
| ![Icona lettura stampante classe host](./media/user-guide/usbx-events/image155.png)    |  **Lettura stampante classe host** *(ux_host_class_printer_read)* |
| ![Icona reimpostazione soft della stampante della classe host](./media/user-guide/usbx-events/image156.png)    | **Reimpostazione della stampante della classe** host *(ux_host_class_printer_soft_reset)* |
| ![Icona Get relativa allo stato della stampante della classe host](./media/user-guide/usbx-events/image157.png)    | **Ottiene lo stato della stampante della** classe host *(ux_host_class_printer_status_get)* |
| ![Icona di scrittura della stampante della classe host](./media/user-guide/usbx-events/image158.png)    | **Scrittura stampante classe host** *(ux_host_class_printer_write)* |
| ![Icona Di attivazione classe host](./media/user-guide/usbx-events/image159.png)    | **Host Class Activate** *(ux_host_class_prolific_activate)* |
| ![Icona Disattiva classe host](./media/user-guide/usbx-events/image160.png)    | **Host Class Deactivate** *(ux_host_class_prolific_deactivate)* |
| ![Icona dell'interruzione nella pipe della classe host Classi host I O C T L](./media/user-guide/usbx-events/image161.png)    | **Interruzione ioctl nella pipe** della classe host *(ux_host_class_prolific_ioctl_abort_in_pipe)* |
| ![Icona della pipe di interruzione dell'interruzione della classe host- I/O C](./media/user-guide/usbx-events/image162.png)    | **Classe host Ioctl Abort Out Pipe** *(ux_host_class_prolific_ioctl_abort_out_pipe)* |
| ![Icona Get Device Status (Ottieni stato dispositivo) della classe host Per ottenere lo stato del dispositivo](./media/user-guide/usbx-events/image163.png)    | **Classe host Ioctl Get Device Status** *(ux_host_class_prolific_ioctl_get_device_status)* |
| ![Icona Get Line Coding (Ottieni codice riga) della classe host Per ottenere il codice](./media/user-guide/usbx-events/image164.png)    | **Classe host Ioctl Get Line Coding** *(ux_host_class_prolific_ioctl_get_line_coding)* |
| ![Icona Di ripulitura classe host I/O C](./media/user-guide/usbx-events/image165.png)    | **Host Class Ioctl Purge** *(ux_host_class_prolific_ioctl_purge)* |
| ![Icona di modifica dello stato del dispositivo report classe host I/O C](./media/user-guide/usbx-events/image166.png)    | **Modifica stato dispositivo report Ioctl** classe host *(ux_host_class_prolific_ioctl_report_device_status_change)* |
| ![Icona Di interruzione invio classe host I O C T L](./media/user-guide/usbx-events/image167.png)    | **Interruzione invio ioctl classe host** *(ux_host_class_prolific_ioctl_send_break)* |
| ![Icona di codifica della riga impostata per la classe host Classi Host I O C T L](./media/user-guide/usbx-events/image168.png)    | **Classe host Ioctl Set Line Coding** *(ux_host_class_prolific_ioctl_set_line_coding)* |
| ![Icona Imposta stato linea classe host I/O C](./media/user-guide/usbx-events/image169.png)    | **Classe host Ioctl Set Line State** *(ux_host_class_prolific_ioctl_set_line_state)* |
| ![Icona lettura classi host](./media/user-guide/usbx-events/image170.png)    | **Lettura classi host** *(ux_host_class_prolific_read)* |
| ![Icona di avvio della ricezione della classe host](./media/user-guide/usbx-events/image171.png)    | **Inizio ricezione classe host** *(ux_host_class_prolific_reception_start)* |
| ![Icona di arresto della ricezione della classe host](./media/user-guide/usbx-events/image172.png)    | **Arresto della ricezione della classe host** *(ux_host_class_prolific_reception_stop)* |
| ![Icona scrittura classi host](./media/user-guide/usbx-events/image173.png)    | **Scrittura classi host** *(ux_host_class_prolific_write)* |
| ![Icona Attiva Archiviazione classe host](./media/user-guide/usbx-events/image174.png)    | **Classe host Archiviazione Activate** *(ux_host_class_storage_activate)* |
| ![Icona Disattiva Archiviazione classe host](./media/user-guide/usbx-events/image175.png)    | **Host Class Archiviazione Deactivate** (*ux_host_class_storage_deactivate)* |
| ![Icona Ottieni capacità Archiviazione classe host](./media/user-guide/usbx-events/image176.png)    | **Classe host Archiviazione Media Capacity Get** *(ux_host_class_storage_media_capacity_get)* |
| ![Classe host Archiviazione'icona Get della capacità del formato multimediale](./media/user-guide/usbx-events/image177.png)    | **Classe host Archiviazione Media Format Capacity Get** *(ux_host_class_storage_media_format_capacity_get)* |
| ![Icona Montaggio Archiviazione classe host](./media/user-guide/usbx-events/image178.png)    | **Classe host Archiviazione supporto di montaggio** (ux_host_class_storage_media_mount)* |
| ![Icona Apri supporto Archiviazione classe host](./media/user-guide/usbx-events/image179.png)    | **Host Class Archiviazione Media Open** *(ux_host_class_storage_media_open)* |
| ![Icona di lettura Archiviazione classe host](./media/user-guide/usbx-events/image180.png)    | **Classe host Archiviazione media read** *(ux_host_class_storage_media_read)* |
| ![Icona di scrittura Archiviazione classe host](./media/user-guide/usbx-events/image181.png)    | **Classe host Archiviazione Media Write** *(ux_host_class_storage_media_write)* |
| ![Icona di richiesta Archiviazione classe host](./media/user-guide/usbx-events/image182.png)    | **Classe host Archiviazione Request Sense** *(ux_host_class_storage_request_sense)* |
| ![Icona Avvia arresto Archiviazione classe host](./media/user-guide/usbx-events/image183.png)    | **Avvio arresto Archiviazione classe host** *(ux_host_class_storage_start_stop)* |
| ![Icona per lo unit test Archiviazione classe host](./media/user-guide/usbx-events/image184.png)    | **Classe host Archiviazione unit test** *(ux_host_class_storage_activate)* |
| ![Icona di creazione dell'istanza della classe stack host](./media/user-guide/usbx-events/image185.png)    | **Creazione dell'istanza della classe stack** host *(ux_host_stack_class_instance_create)* |
| ![Icona Host Stack Class Instance Destroy (Elimina istanza classe stack host)](./media/user-guide/usbx-events/image186.png)    | **Host Stack Class Instance Destroy (ux_host_stack_class_instance_destroy)**  |
| ![Icona Host Stack Configuration Delete (Elimina configurazione stack host)](./media/user-guide/usbx-events/image187.png)    | **Host Stack Configuration Delete** *(ux_host_stack_configuration_delete)* |
| ![Icona enumera configurazione stack host](./media/user-guide/usbx-events/image188.png)    | **Enumerazione configurazione stack host** *(ux_host_stack_configuration_enumerate)* |
| ![Icona di creazione dell'istanza di configurazione dello stack di host](./media/user-guide/usbx-events/image189.png)    | **Creazione dell'istanza di configurazione** *dello stack host (ux_host_stack_configuration_instance_create)* |
| ![Icona di eliminazione dell'istanza di configurazione dello stack di host](./media/user-guide/usbx-events/image190.png)    | **Eliminazione dell'istanza di configurazione** dello stack host *(ux_host_stack_configuration_instance_delete)* |
| ![Icona del set di configurazione dello stack di host](./media/user-guide/usbx-events/image191.png)    | **Set di configurazione dello stack host** *(ux_host_stack_configuration_set)* |
| ![Icona del set di indirizzi del dispositivo stack host](./media/user-guide/usbx-events/image192.png)    | **Host Stack Device Address Set (ux_host_stack_device_set)**  |
| ![Icona Get della configurazione del dispositivo stack host](./media/user-guide/usbx-events/image193.png)    | **Get della configurazione del dispositivo stack host** *(ux_host_stack_device_configuration_get)* |
| ![Icona Di selezione della configurazione del dispositivo stack host](./media/user-guide/usbx-events/image194.png)    | **Selezione configurazione dispositivo stack host** *(ux_host_stack_device_configuration_select)* |
| ![Icona lettura descrittore dispositivo stack host](./media/user-guide/usbx-events/image195.png)    | **Lettura descrittore dispositivo** stack host *(ux_host_stack_device_descriptor_read)* |
| ![Icona Get del dispositivo stack host](./media/user-guide/usbx-events/image196.png)    | **Get dispositivo stack host** (ux_host_stack_device_get) |
| ![Icona di rimozione del dispositivo stack host](./media/user-guide/usbx-events/image197.png)    | **Rimozione del dispositivo stack host** (ux_host_stack_device_get) |
| ![Icona della risorsa gratuita del dispositivo stack host](./media/user-guide/usbx-events/image198.png)    | **Host Stack Device Resource Free** (ux_host_stack_device_resource_free) |
| ![Icona di creazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image199.png)    | **Creazione dell'istanza dell'endpoint** dello stack host (ux_host_stack_endpoint_instance_create) |
| ![Icona Host Stack Endpoint Instance Delete (Elimina istanza endpoint stack host)](./media/user-guide/usbx-events/image200.png)    | **Host Stack Endpoint Instance Delete** (ux_host_stack_endpoint_instance_delete) |
| ![Icona reimpostazione endpoint stack host](./media/user-guide/usbx-events/image201.png)    | **Reimpostazione endpoint stack host** (ux_host_stack_endpoint_reset) |
| ![Icona di interruzione del trasferimento dell'endpoint dello stack host](./media/user-guide/usbx-events/image202.png)    | **Interruzione trasferimento endpoint stack host** (ux_host_stack_endpoint_transfer_abort) |
| ![Icona di registrazione del controller host dello stack host host](./media/user-guide/usbx-events/image203.png)    | **Registro del controller host dello stack host** *(ux_host_stack_hcd_register)* |
| ![Icona di inizializzazione dello stack di host](./media/user-guide/usbx-events/image204.png)    | **Host Stack Initialize** *(ux_host_stack_initialize)* |
| ![Icona Get dell'endpoint dell'interfaccia dello stack host](./media/user-guide/usbx-events/image205.png)    | **Host Stack Interface Endpoint Get** *(ux_host_stack_interface_endpoint_get)* |
| ![Icona di creazione dell'istanza dell'interfaccia dello stack di host](./media/user-guide/usbx-events/image206.png)    | **Creazione dell'istanza dell'interfaccia** dello stack *host (ux_host_stack_interface_instance_create)* |
| ![Icona Host Stack Interface Instance Delete (Elimina istanza dell'interfaccia dello stack host)](./media/user-guide/usbx-events/image207.png)    | **Host Stack Interface Instance Delete** *(ux_host_stack_interface_instance_delete)* |
| ![Icona del set di interfacce dello stack di host](./media/user-guide/usbx-events/image208.png)    | **Host Stack Interface Set** *(ux_host_stack_interface_set)* |
| ![Icona Di selezione dell'impostazione dell'interfaccia dello stack di host](./media/user-guide/usbx-events/image209.png)    | **Selezione dell'impostazione dell'interfaccia** *dello stack host (ux_host_stack_interface_setting_select)* |
| ![Icona di creazione della nuova configurazione dello stack di host](./media/user-guide/usbx-events/image210.png)    | **Creazione nuova configurazione dello stack host** *(ux_host_stack_new_configuration_create)* |
| ![Icona di creazione del nuovo dispositivo dello stack di host](./media/user-guide/usbx-events/image211.png)    | **Creazione di un nuovo dispositivo stack host** *(ux_host_stack_new_device_create)* |
| ![Icona di creazione nuovo endpoint dello stack di host](./media/user-guide/usbx-events/image212.png)    | **Creazione di un nuovo endpoint dello stack** host *(ux_host_stack_new_endpoint_create)* |
| ![Icona del processo di modifica dell'hub radice dello stack host](./media/user-guide/usbx-events/image213.png)    | **Processo di modifica dell'hub radice** dello stack host *(ux_host_stack_rh_change_process)* |
| ![Icona di estrazione del dispositivo dell'hub radice dello stack host](./media/user-guide/usbx-events/image214.png)    | **Estrazione dispositivo hub radice stack** host *(ux_host_stack_rh_device_extraction)* |
| ![Icona di inserimento del dispositivo dell'hub radice dello stack host](./media/user-guide/usbx-events/image215.png)    | **Inserimento dispositivo hub radice stack** host *(ux_host_stack_rh_device_insertion)* |
| ![Icona della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image216.png)    | **Richiesta di trasferimento stack host** *(ux_host_stack_transfer_request)* |
| ![Icona Host Stack Transfer Request Abort (Interruzione richiesta di trasferimento stack host)](./media/user-guide/usbx-events/image217.png)    | **Host Stack Transfer Request Abort** *(ux_host_stack_transfer_request_abort)* |
| ![Icona di errore di U S B X](./media/user-guide/usbx-events/image218.png)    | **Errore USBX** *(ux_error)* |

## <a name="event-descriptions"></a>Descrizioni di eventi

Le pagine seguenti descrivono gli eventi di traccia USBX.

### <a name="device-class-cdc-activate"></a>Device Class Cdc Activate 

#### <a name="ux_device_class_cdc_activate"></a>ux_device_class_cdc_activate

**Icona** ![ Icona di attivazione di Classe dispositivo C D C](./media/user-guide/usbx-events/image1.png)

**Descrizione**

Questo evento rappresenta un evento Cdc Activate della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-cdc-deactivate"></a>Device Class Cdc Deactivate 

#### <a name="ux_device_class_cdc_deactivate"></a>ux_device_class_cdc_deactivate

**Icona** ![ Icona Disattiva classe dispositivo C D C](./media/user-guide/usbx-events/image2.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX Cdc Deactivate.

Campi di informazioni 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-cdc-read"></a>Classe dispositivo Cdc Read 

#### <a name="ux_device_class_cdc_read"></a>ux_device_class_cdc_read

**Icona** ![ Icona di lettura di Classe dispositivo C D C](./media/user-guide/usbx-events/image3.png)

**Descrizione**

Questo evento rappresenta un evento di lettura Cdc classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="device-class-cdc-write"></a>Classe dispositivo Cdc Write 

#### <a name="ux_device_class_cdc_write"></a>ux_device_class_cdc_write

**Icona** ![ Icona di scrittura C della classe di dispositivo C](./media/user-guide/usbx-events/image4.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura Cdc classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="device-class-dpump-activate"></a>Device Class Dpump Activate 

#### <a name="ux_device_class_dpump_activate"></a>ux_device_class_dpump_activate

**Icona** ![ Icona device class Dpump Activate](./media/user-guide/usbx-events/image5.png)

**Descrizione**

Questo evento rappresenta un evento Dpump Activate della classe del dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-dpump-deactivate"></a>Device Class Dpump Deactivate 

#### <a name="ux_device_class_dpump_deactivate"></a>ux_device_class_dpump_deactivate

**Icona** ![ Icona Disattiva Dpump classe dispositivo](./media/user-guide/usbx-events/image6.png)

**Descrizione**

Questo evento rappresenta un evento Dpump Deactivate della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-dpump-read"></a>Device Class Dpump Read 

#### <a name="ux_device_class_dpump_read"></a>ux_device_class_dpump_read

**Icona** ![ Icona lettura Dpump classe dispositivo](./media/user-guide/usbx-events/image7.png)

**Descrizione**

Questo evento rappresenta un evento di lettura Dpump classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Buffer.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="device-class-dpump-write"></a>Scrittura Dpump classe dispositivo 

#### <a name="ux_device_class_dpump_write"></a>ux_device_class_dpump_write

**Icona** ![ Icona di scrittura Dpump classe dispositivo](./media/user-guide/usbx-events/image8.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura Dpump classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-activate"></a>Device Class Hid Activate 

#### <a name="ux_device_class_hid_activate"></a>ux_device_class_hid_activate

**Icona** ![ Icona di hid activate della classe di dispositivi](./media/user-guide/usbx-events/image9.png)

**Descrizione**

Questo evento rappresenta un evento Hid Activate della classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-deactivate"></a>Device Class Hid Deactivate 

#### <a name="ux_device_class_hid_deactivate"></a>ux_device_class_hid_deactivate

**Icona** ![ Icona Disattiva classe dispositivo - Disattivazione](./media/user-guide/usbx-events/image10.png)

**Descrizione**

Questo evento rappresenta un evento Hid Deactivate della classe dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-descriptor-send"></a>Device Class Hid Descriptor Send 

#### <a name="ux_device_class_hid_descritpor_send"></a>ux_device_class_hid_descritpor_send

**Icona** ![ Icona di invio descrittore hid della classe di dispositivi](./media/user-guide/usbx-events/image11.png)

**Descrizione**

Questo evento rappresenta un evento Hid Descriptor Send della classe dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: tipo di descrittore.
- Campo informazioni 3: Indice delle richieste.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-event-get"></a>Device Class Hid Event Get 

#### <a name="ux_device_class_hid_event_get"></a>ux_device_class_hid_event_get

**Icona** ![ Icona Device Class Hid Event Get](./media/user-guide/usbx-events/image12.png)

**Descrizione**

Questo evento rappresenta un evento Get evento hid della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-event-set"></a>Device Class Hid Event Set 

#### <a name="ux_device_class_hid_event_set"></a>ux_device_class_hid_event_set

**Icona** ![ Icona del set di eventi Hid della classe di dispositivi](./media/user-guide/usbx-events/image13.png)

**Descrizione**

Questo evento rappresenta un set di eventi hid della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-report-get"></a>Device Class Hid Report Get 

#### <a name="ux_device_class_hid_report_get"></a>ux_device_class_hid_report_get

**Icona** ![ Icona Get del report hid della classe di dispositivi](./media/user-guide/usbx-events/image14.png)

**Descrizione**

Questo evento rappresenta un evento Get del report hid della classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: tipo di descrittore.
- Campo informazioni 3: Indice delle richieste.
- Campo informazioni 4: Non usato.

### <a name="device-class-hid-report-set"></a>Device Class Hid Report Set 

#### <a name="ux_device_class_hid_report_set"></a>ux_device_class_hid_report_set

**Icona** ![ Icona del set di report hid della classe di dispositivi](./media/user-guide/usbx-events/image15.png)

**Descrizione**

Questo evento rappresenta un evento del set di report hid della classe dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: tipo di descrittore.
- Campo informazioni 3: Indice delle richieste.
- Campo informazioni 4: Non usato.

### <a name="device-class-pima-activate"></a>Device Class Pima Activate

#### <a name="ux_device_class_pima_activate"></a>ux_device_class_pima_activate

**Icona** ![ Icona Device Class Pima Activate](./media/user-guide/usbx-events/image16.png)

**Descrizione**

Questo evento rappresenta un evento Pima Activate della classe di dispositivi USBX.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-deactivate"></a>Classe device Pima Deactivate 

#### <a name="ux_device_class_pima_deactivate"></a>ux_device_class_pima_deactivate

**Icona** ![ Icona Device Class Pima Deactivate](./media/user-guide/usbx-events/image17.png)

**Descrizione**

Questo evento rappresenta un evento Pima Deactivate della classe di dispositivi USBX.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-device-info-send"></a>Classe dispositivo Pima Device Info Send 

#### <a name="ux_device_class_pima_device_info_send"></a>ux_device_class_pima_device_info_send

**Icona** ![ Icona Device Class Pima Device Info Send](./media/user-guide/usbx-events/image18.png)

**Descrizione**

Questo evento rappresenta un evento di invio delle informazioni sul dispositivo pima della classe dispositivo USBX.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.

### <a name="device-class-pima-event-get"></a>Device Class Pima Event Get 

#### <a name="ux_device_class_pima_event_get"></a>ux_device_class_pima_event_get

**Icona** ![ Icona Device Class Pima Event Get](./media/user-guide/usbx-events/image19.png)

**Descrizione**

Questo evento rappresenta un evento Get di evento Pima della classe di dispositivi USBX.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Field 2: Evento Pima.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-event-set"></a>Device Class Pima Event Set 

#### <a name="ux_device_class_pima_event_set"></a>ux_device_class_pima_event_set

**Icona** ![ Icona Device Class Pima Event Set](./media/user-guide/usbx-events/image20.png)

**Descrizione**

Questo evento rappresenta un evento del set di eventi pima della classe di dispositivi USBX.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Field 2: Evento Pima.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-object-add"></a>Aggiunta dell'oggetto Pima della classe Device 

#### <a name="ux_device_class_pima_object_add"></a>ux_device_class_pima_object_add

**Icona** ![ Icona Aggiungi oggetto Pima della classe device](./media/user-guide/usbx-events/image21.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX Pima Object Add Event.

**Campi di informazioni** 

- Campo info 1: Istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-object-data-get"></a>Device Class Pima Object Data Get 

#### <a name="ux_device_class_pima_object_data_get"></a>ux_device_class_pima_object_data_get

**Icona** ![ Icona Device Class Pima Object Data Get](./media/user-guide/usbx-events/image22.png)

**Descrizione**

Questo evento rappresenta un evento Pima Object Data Get della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo info 1: Istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-object-data-send"></a>Classe device Pima Object Data Send 

#### <a name="ux_device_class_pima_object_data_send"></a>ux_device_class_pima_object_data_send

**Icona** ![ Icona Device Class Pima Object Data Send](./media/user-guide/usbx-events/image23.png)

**Descrizione**

Questo evento rappresenta un evento di invio dati oggetto pima della classe di dispositivo USBX.

**Campi di informazioni** 

- Campo info 1: Istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-object-delete"></a>Classe device Pima Object Delete 

#### <a name="ux_device_class_pima_object_delete"></a>ux_device_class_pima_object_delete

**Icona** ![ Icona Device Class Pima Object Delete](./media/user-guide/usbx-events/image24.png)

**Descrizione**

Questo evento rappresenta un evento usbx device class Pima Object Delete.

**Campi di informazioni** 

- Campo info 1: Istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="device-class-pima-object-handles-send"></a>La classe Device Pima gestisce l'invio 

#### <a name="ux_device_class_pima_object_handles_send"></a>ux_device_class_pima_object_handles_send

**Icona** ![ Icona Device Class Pima Object Handles Send](./media/user-guide/usbx-events/image25.png)

**Descrizione**

Questo evento rappresenta un evento send della classe di dispositivi USBX Pima.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: Archiviazione ID.
- Info Campo 3: codice in formato oggetto.
- Info Campo 4: Associazione di oggetti.

### <a name="device-class-pima-object-info-get"></a>Device Class Pima Object Info Get 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Icona** ![ Icona Device Class Pima Object Info Get](./media/user-guide/usbx-events/image26.png)

**Descrizione**

Questo evento rappresenta un evento Di info oggetto Pima della classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: handle di oggetto.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-pima-object-info-send"></a>Device Class Pima Object Info Send 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Icona** ![ Icona Device Class Pima Object Info Send](./media/user-guide/usbx-events/image27.png)

**Descrizione**

Questo evento rappresenta un evento di invio informazioni sull'oggetto Pima della classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-pima-objects-number-send"></a>Device Class Pima Objects Number Send 

#### <a name="ux_device_class_pima_object_number_send"></a>ux_device_class_pima_object_number_send

**Icona** ![ Icona Device Class Pima Objects Number Send](./media/user-guide/usbx-events/image28.png)

**Descrizione**

Questo evento rappresenta un evento UsbX Device Class Pima Object Number Send.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Archiviazione ID.
- Info Field 3: Object format code (Campo informazioni 3: codice formato oggetto).
- Campo informazioni 4: Associazione di oggetti.

### <a name="device-class-pima-partial-object-data-get"></a>Device Class Pima Partial Object Data Get

#### <a name="ux_device_class_pima_partial_object_data_get"></a>ux_device_class_pima_partial_object_data_get

**Icona** ![ Icona Device Class Pima Partial Object Data Get](./media/user-guide/usbx-events/image29.png)

**Descrizione**

Questo evento rappresenta un evento get partial object data della classe dispositivo USBX Pima.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: handle di oggetto.
- Campo informazioni 3: offset richiesto.
- Campo informazioni 4: lunghezza richiesta.

### <a name="device-class-pima-response-send"></a>Device Class Pima Response Send 

#### <a name="ux_device_class_pima_response_send"></a>ux_device_class_pima_response_send

**Icona** ![ Icona Device Class Pima Response Send (Invio risposta Pima classe dispositivo)](./media/user-guide/usbx-events/image30.png)

**Descrizione**

Questo evento rappresenta un evento di invio della risposta Pima della classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: codice di risposta.
- Info Field 3: parametro Number.
- Campo informazioni 4: parametro Pima 1.

### <a name="device-class-pima-storage-id-send"></a>Device Class Pima Archiviazione Id Send 

#### <a name="ux_device_class_pima_storage_id_send"></a>ux_device_class_pima_storage_id_send

**Icona** ![ Icona Device Class Pima Archiviazione Id Send](./media/user-guide/usbx-events/image31.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Pima Archiviazione evento di invio ID.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-pima-storage-info-send"></a>Device Class Pima Archiviazione Info Send 

#### <a name="ux_device_class_pima_storage_info_send"></a>ux_device_class_pima_storage_info_send

**Icona** ![ Icona Device Class Pima Archiviazione Info Send](./media/user-guide/usbx-events/image32.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Pima Archiviazione Info Send Event.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-activate"></a>Device Class Rndis Activate 

#### <a name="ux_device_class_rndis_activate"></a>ux_device_class_rndis_activate

**Icona** ![ Icona Device Class Rndis Activate (Attiva Rndis classe dispositivo)](./media/user-guide/usbx-events/image33.png)

**Descrizione**

Questo evento rappresenta un evento Rndis Activate della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-deactivate"></a>Device Class Rndis Deactivate 

#### <a name="ux_device_class_rndis_deactivate"></a>ux_device_class_rndis_deactivate

**Icona** ![ Icona Disattiva classe dispositivo](./media/user-guide/usbx-events/image34.png)

**Descrizione**

Questo evento rappresenta un evento Rndis Deactivate della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-message-keep-alive"></a>Classe dispositivo Rndis Message Keep Alive 

#### <a name="ux_device_class_rndis_msg_keep_alive"></a>ux_device_class_rndis_msg_keep_alive

**Icona** ![ Icona Keep-Alive del messaggio Rndis della classe dispositivo](./media/user-guide/usbx-events/image35.png)

**Descrizione**

Questo evento rappresenta un evento keep-alive Rndis message keep-alive della classe di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-message-query"></a>Query del messaggio Rndis della classe dispositivo 

#### <a name="ux_device_class_rndis_msg_keep_query"></a>ux_device_class_rndis_msg_keep_query

**Icona** ![ Icona di query del messaggio Rndis della classe dispositivo](./media/user-guide/usbx-events/image36.png)

**Descrizione**

Questo evento rappresenta un evento di query del messaggio Rndis della classe del dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: OID Rndis.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-message-reset"></a>Reimpostazione del messaggio Rndis della classe dispositivo 

#### <a name="ux_device_class_rndis_msg_reset"></a>ux_device_class_rndis_msg_reset

**Icona** ![ Icona di reimpostazione del messaggio Rndis della classe dispositivo](./media/user-guide/usbx-events/image37.png)

**Descrizione**

Questo evento rappresenta un evento Rndis Message Reset della classe del dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.

### <a name="device-class-rndis-message-set"></a>Device Class Rndis Message Set 

#### <a name="ux_device_class_rndis_msg_set"></a>ux_device_class_rndis_msg_set

**Icona** ![ Icona Device Class Rndis Message Set (Set di messaggi Rndis classe dispositivo)](./media/user-guide/usbx-events/image38.png)

**Descrizione**

Questo evento rappresenta un evento Rndis Message Set della classe di dispositivi USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: OID Rndis.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-packet-receive"></a>Device Class Rndis Packet Receive 

#### <a name="ux_device_class_rndis_packet_receive"></a>ux_device_class_rndis_packet_receive

**Icona** ![ Icona ricezione pacchetti Rndis classe dispositivo](./media/user-guide/usbx-events/image39.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione pacchetti Rndis classe dispositivo USBX.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-rndis-packet-transmit"></a>Trasmissione di pacchetti Rndis della classe dispositivo 

#### <a name="ux_device_class_rndis_packet_transmit"></a>ux_device_class_rndis_packet_transmit

**Icona** ![ Icona di trasmissione pacchetti Rndis della classe dispositivo](./media/user-guide/usbx-events/image40.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione pacchetti Rndis della classe dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-activate"></a>Attivazione della classe Archiviazione dispositivo 

#### <a name="ux_device_class_storage_activate"></a>ux_device_class_storage_activate

**Icona** ![ Icona Attiva Archiviazione classe dispositivo](./media/user-guide/usbx-events/image41.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione Activate Event.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-deactivate"></a>Disattivazione della classe Archiviazione dispositivo 

#### <a name="ux_device_class_storage_deactivate"></a>ux_device_class_storage_deactivate

**Icona** ![ Icona Disattiva Archiviazione dispositivo](./media/user-guide/usbx-events/image42.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione Deactivate Event.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-format"></a>Formato dell'Archiviazione dispositivo 

#### <a name="ux_device_class_storage_format"></a>ux_device_class_storage_format

**Icona** ![ Icona Formato Archiviazione dispositivo](./media/user-guide/usbx-events/image43.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione Formato evento.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-inquiry"></a>Richiesta di richiesta Archiviazione dispositivo 

#### <a name="ux_device_class_storage_inquiry"></a>ux_device_class_storage_inquiry

**Icona** ![ Icona Richiesta di Archiviazione dispositivo](./media/user-guide/usbx-events/image44.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione richiesta.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-mode-select"></a>Selezione della modalità Archiviazione dispositivo

#### <a name="ux_device_class_storage_mode_select"></a>ux_device_class_storage_mode_select

**Icona** ![ Icona di selezione Archiviazione classe dispositivo](./media/user-guide/usbx-events/image45.png)

**Descrizione**

Questo evento rappresenta un evento di selezione della Archiviazione dispositivo USBX.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-mode-sense"></a>Classe device Archiviazione Mode Sense 

#### <a name="ux_device_class_storage_mode_sense"></a>ux_device_class_storage_mode_sense

**Icona** ![ Icona di senso Archiviazione classe di dispositivo](./media/user-guide/usbx-events/image46.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione Mode Sense Event.

Campi di informazioni 

- nfo Campo 1: Istanza di classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-prevent-allow-media-removal"></a>Classe device Archiviazione Impedisci rimozione supporti 

#### <a name="ux_device_class_storage_prevent_allow_media_removal"></a>ux_device_class_storage_prevent_allow_media_removal

**Icona** ![ Icona Impedisci rimozione supporti Archiviazione classe dispositivo](./media/user-guide/usbx-events/image47.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione impedisci la rimozione di supporti.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-read"></a>Lettura della classe Archiviazione dispositivo 

#### <a name="ux_device_class_storage_read"></a>ux_device_class_storage_read

**Icona** ![ Icona Lettura della Archiviazione dispositivo](./media/user-guide/usbx-events/image48.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione lettura evento.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Settore.
- Campo informazioni 4: Settori numerici.

### <a name="device-class-storage-read-capacity"></a>Classe device Archiviazione capacità di lettura 

#### <a name="ux_device_class_storage_read_capacity"></a>ux_device_class_storage_read_capacity

**Icona** ![ Icona Della capacità Archiviazione di lettura della classe di dispositivi](./media/user-guide/usbx-events/image49.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione di capacità di lettura.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-read-format-capacity"></a>Capacità del formato Archiviazione dispositivo 

#### <a name="ux_device_class_storage_read_format_capacity"></a>ux_device_class_storage_read_format_capacity

**Icona** ![ Icona Della capacità Archiviazione classe di dispositivi per la lettura del formato](./media/user-guide/usbx-events/image50.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione read format capacity event.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-read-toc"></a>Classe device Archiviazione Lettura sommario 

#### <a name="ux_device_class_storage_read_toc"></a>ux_device_class_storage_read_toc

**Icona** ![ Icona Della classe di Archiviazione lettura del sommario](./media/user-guide/usbx-events/image51.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione evento di lettura del sommario.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-request-sense"></a>Classe device Archiviazione Request Sense 

#### <a name="ux_device_class_storage_request_sense"></a>ux_device_class_storage_request_sense

**Icona** ![ Icona Di classe Archiviazione richiesta di senso](./media/user-guide/usbx-events/image52.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione request sense event.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Info Field 3: Sense key (Campo informazioni 3: Chiave di senso).
- Campo informazioni 4: Codice.

### <a name="device-class-storage-start-stop"></a>Arresto dell'Archiviazione dispositivo 

#### <a name="ux_device_class_storage_start_stop"></a>ux_device_class_storage_start_stop

**Icona** ![ Classe di dispositivi Archiviazione'icona Avvia arresto](./media/user-guide/usbx-events/image53.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione start stop event.

**Campi di informazioni**

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-test-ready"></a>Classe device Archiviazione test ready 

#### <a name="ux_device_class_storage_test_ready"></a>ux_device_class_storage_test_ready

**Icona** ![ Icona Di classe Archiviazione test pronto](./media/user-guide/usbx-events/image54.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione evento pronto per il test.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-verify"></a>Verifica dell'Archiviazione dispositivo 

#### <a name="ux_device_class_storage_verify"></a>ux_device_class_storage_verify

**Icona** ![ Icona Verifica Archiviazione dispositivo](./media/user-guide/usbx-events/image55.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione evento Verify.

**Campi di informazioni** 

- Campo informazioni 1: Istanza classe.
- Campo informazioni 2: Lun.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-class-storage-write"></a>Scrittura della classe Archiviazione dispositivo 

#### <a name="ux_device_class_storage_write"></a>ux_device_class_storage_write

**Icona** ![ Icona Di scrittura Archiviazione dispositivo](./media/user-guide/usbx-events/image56.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX Archiviazione write event.

**Campi di informazioni** 

- Campo info 1: Istanza della classe.
- Info Field 2: Lun.
- Campo informazioni 3: Settore.
- Info Campo 4: Settori numerici.

### <a name="device-stack-alternate-setting-get"></a>Get dell'impostazione alternativa dello stack di dispositivi 

#### <a name="ux_device_class_alternate_setting_get"></a>ux_device_class_alternate_setting_get

**Icona** ![ Icona Get dell'impostazione alternativa dello stack di dispositivi](./media/user-guide/usbx-events/image57.png)

**Descrizione**

Questo evento rappresenta un evento Get dell'impostazione alternativa dello stack di dispositivi USBX.

**Campi di informazioni**

- Info Campo 1: Valore dell'interfaccia.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-alternate-setting-set"></a>Set di impostazioni alternative dello stack di dispositivi 

#### <a name="ux_device_class_alternate_setting_set"></a>ux_device_class_alternate_setting_set

**Icona** ![ Icona del set di impostazioni alternative dello stack di dispositivi](./media/user-guide/usbx-events/image58.png)

**Descrizione**

Questo evento rappresenta un evento set di impostazioni alternativo dello stack di dispositivi USBX.

**Campi di informazioni**
- Info Campo 1: Valore dell'interfaccia.
- Info Campo 2: valore di impostazione alternativo.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-class-register"></a>Registro classi dello stack di dispositivi 

#### <a name="ux_device_stack_class_register"></a>ux_device_stack_class_register

**Icona** ![ Icona Device Stack Class Register (Registro classi stack di dispositivi)](./media/user-guide/usbx-events/image59.png)

**Descrizione**

Questo evento rappresenta un evento di registrazione della classe stack di dispositivi USBX.

**Campi di informazioni**

- Info Campo 1: Nome classe.
- Info Campo 2: Numero di interfaccia.
- Campo informazioni 3: parametro.
- Campo info 4: Non usato.

### <a name="device-stack-clear-feature"></a>Funzionalità di cancellazione dello stack di dispositivi 

#### <a name="ux_device_stack_clear_feature"></a>ux_device_stack_clear_feature

**Icona** ![ Icona della funzionalità di cancellazione dello stack di dispositivi](./media/user-guide/usbx-events/image60.png)

**Descrizione**

Questo evento rappresenta un evento della funzionalità di cancellazione dello stack di dispositivi USBX.

**Campi di informazioni**

- Info Campo 1: Tipo di richiesta.
- Info Campo 2: Valore della richiesta. Info Campo 3: Indice delle richieste.
- Campo info 4: Non usato.

### <a name="device-stack-configuration-get"></a>Ottenere la configurazione dello stack di dispositivi 

#### <a name="ux_device_stack_configuration_get-t"></a>ux_device_stack_configuration_get t

**Icona** ![ Icona Get della configurazione dello stack di dispositivi](./media/user-guide/usbx-events/image61.png)

**Descrizione**

Questo evento rappresenta un evento Get di configurazione dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo info 1: valore di configurazione.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-configuration-set"></a>Set di configurazione dello stack di dispositivi 

#### <a name="ux_device_stack_configuration_set"></a>ux_device_stack_configuration_set

**Icona** ![ Icona del set di configurazione dello stack di dispositivi](./media/user-guide/usbx-events/image62.png)

**Descrizione**

Questo evento rappresenta un evento del set di configurazione dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo info 1: valore di configurazione.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-connect"></a>Stack di dispositivi Connessione 

#### <a name="ux_device_stack_connect"></a>ux_device_stack_connect

**Icona** ![ Icona stack Connessione dispositivo](./media/user-guide/usbx-events/image63.png)

**Descrizione**

Questo evento rappresenta un evento USBX Device Stack Descriptor Send.

**Campi di informazioni**

- Info Campo 1: Non usato.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-descriptor-send"></a>Invio descrittore dello stack di dispositivi 

#### <a name="ux_device_stack_descriptor_send"></a>ux_device_stack_descriptor_send

**Icona** ![ Icona Device Stack Descriptor Send](./media/user-guide/usbx-events/image64.png)

**Descrizione**

Questo evento rappresenta un evento USBX Device Stack Descriptor Send.

**Campi di informazioni**

- Info Campo 1: Tipo di descrittore.
- Info Campo 2: Indice delle richieste.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-disconnect"></a>Disconnessione dello stack di dispositivi 

#### <a name="ux_device_stack_disconnect"></a>ux_device_stack_disconnect

**Icona** ![ Icona di disconnessione dello stack di dispositivi](./media/user-guide/usbx-events/image65.png)

**Descrizione**

Questo evento rappresenta un evento di disconnessione dello stack di dispositivi USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="device-stack-endpoint-stall"></a>Blocco dell'endpoint dello stack di dispositivi 

#### <a name="ux_device_stack_endpoint_stall"></a>ux_device_stack_endpoint_stall

**Icona** ![ Icona Di stallo dell'endpoint dello stack di dispositivi](./media/user-guide/usbx-events/image66.png)

**Descrizione**

Questo evento rappresenta un evento stallo dell'endpoint dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Endpoint.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-get-status"></a>Device Stack Get Status 

#### <a name="ux_device_stack_get_status"></a>ux_device_stack_get_status

**Icona** ![ Icona Get Status (Ottieni stato) dello stack di dispositivi](./media/user-guide/usbx-events/image67.png)

**Descrizione**

Questo evento rappresenta un evento di stato Get Status dello stack di dispositivi USBX.

**Campi di informazioni**

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-host-wakeup"></a>Riattivazione dell'host dello stack di dispositivi 

#### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

**Icona** ![ Icona di riattivazione dell'host dello stack di dispositivi](./media/user-guide/usbx-events/image68.png)

**Descrizione**

Questo evento rappresenta un evento di riattivazione host dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-initialize"></a>Inizializzazione dello stack di dispositivi 

#### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

**Icona** ![ Icona Device Stack Initialize (Inizializza stack di dispositivi)](./media/user-guide/usbx-events/image69.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-interface-delete"></a>Eliminazione dell'interfaccia dello stack di dispositivi 

#### <a name="ux_device_stack_interface_delete"></a>ux_device_stack_interface_delete

**Icona** ![ Icona di eliminazione dell'interfaccia dello stack di dispositivi](./media/user-guide/usbx-events/image70.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'interfaccia dello stack di dispositivi USBX.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-interface-get"></a>Device Stack Interface Get 

#### <a name="ux_device_stack_interface_get"></a>ux_device_stack_interface_get

**Icona** ![ Icona Get dell'interfaccia dello stack di dispositivi](./media/user-guide/usbx-events/image71.png)

**Descrizione**

Questo evento rappresenta un evento Get dell'interfaccia dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: valore dell'interfaccia.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-interface-set"></a>Set di interfacce dello stack di dispositivi 

#### <a name="ux_device_stack_interface_set"></a>ux_device_stack_interface_set

**Icona** ![ Icona del set di interfacce dello stack di dispositivi](./media/user-guide/usbx-events/image72.png)

**Descrizione**

Questo evento rappresenta un evento del set di interfacce dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: valore della richiesta. Campo informazioni 2: indice delle richieste.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-set-feature"></a>Funzionalità del set di stack di dispositivi 

#### <a name="ux_device_stack_set_feature"></a>ux_device_stack_set_feature

**Icona** ![ Icona della funzionalità Set di stack di dispositivi](./media/user-guide/usbx-events/image73.png)

**Descrizione**

Questo evento rappresenta un evento di funzionalità del set di stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: valore della richiesta. Campo informazioni 2: indice delle richieste.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-transfer-abort"></a>Interruzione del trasferimento dello stack di dispositivi 

#### <a name="ux_device_stack_transfer_abort"></a>ux_device_stack_transfer_abort

**Icona** ![ Icona di interruzione del trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image74.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del trasferimento dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Richiesta di trasferimento.
- Campo informazioni 2: codice di completamento.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-transfer-all-request-abort"></a>Device Stack Transfer All Request Abort 

#### <a name="ux_device_stack_transfer_all_request_abort"></a>ux_device_stack_transfer_all_request_abort

**Icona** ![ Icona Device Stack Transfer All Request Abort](./media/user-guide/usbx-events/image75.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione di tutte le richieste di trasferimento dello stack di dispositivi USBX.

**Campi di informazioni** 

- Campo informazioni 1: Endpoint.
- Campo informazioni 2: codice di completamento.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="device-stack-transfer-request"></a>Richiesta di trasferimento dello stack di dispositivi 

#### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

**Icona** ![ Icona Device Stack Transfer Request (Richiesta di trasferimento stack di dispositivi)](./media/user-guide/usbx-events/image76.png)

**Descrizione**

Questo evento rappresenta un evento di richiesta di trasferimento dello stack di dispositivi USBX.

**Campi di informazioni**

- Info Campo 1: Richiesta di trasferimento.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-asix-activate"></a>Classe host Asix Activate 

#### <a name="ux_host_class_asix_activate"></a>ux_host_class_asix_activate

**Icona** ![ Icona Asix Activate della classe host](./media/user-guide/usbx-events/image77.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Asix Activate.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-asix-deactivate"></a>Classe host Asix Deactivate 

#### <a name="ux_host_class_asix_deactivate"></a>ux_host_class_asix_deactivate

**Icona** ![ Icona Asix Deactivate della classe host](./media/user-guide/usbx-events/image78.png)

**Descrizione**

Questo evento rappresenta un evento Asix Deactivate della classe host USBX.

**Campi di informazioni** 

- Campo info 1: Istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-asix-interrupt-notification"></a>Notifica di interrupt asix della classe host 

#### <a name="ux_host_class_asix_interrupt_notification"></a>ux_host_class_asix_interrupt_notification

**Icona** ![ Icona Asix Interrupt Notification della classe host](./media/user-guide/usbx-events/image79.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Asix Interrupt Notification Event.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-asix-read"></a>Classe host Asix Read 

#### <a name="ux_host_class_asix_read"></a>ux_host_class_asix_read

**Icona** ![ Icona Asix Read della classe host](./media/user-guide/usbx-events/image80.png)

**Descrizione**

Questo evento rappresenta un evento di lettura Asix della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza richiesta.
- Campo info 4: Non usato.

### <a name="host-class-asix-write"></a>Classe host Asix Write 

#### <a name="ux_host_class_asix_write"></a>ux_host_class_asix_write

**Icona** ![ Icona Asix Write della classe host](./media/user-guide/usbx-events/image81.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura Asix della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza richiesta.
- Campo info 4: Non usato.

### <a name="host-class-audio-activate"></a>Attivazione audio della classe host 

#### <a name="ux_host_class_audio_activate"></a>ux_host_class_audio_activate

**Icona** ![ Icona Di attivazione audio della classe host](./media/user-guide/usbx-events/image82.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione audio della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-audio-control-value-get"></a>Ottenere il valore del controllo audio della classe host 

#### <a name="ux_host_class_audio_control_value_get"></a>ux_host_class_audio_control_value_get

**Icona** ![ Icona Get del valore del controllo audio della classe host](./media/user-guide/usbx-events/image83.png)

**Descrizione**

Questo evento rappresenta un evento Get del valore del controllo audio della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-audio-control-value-set"></a>Set di valori di controllo audio della classe host 

#### <a name="ux_host_class_audio_control_value_set"></a>ux_host_class_audio_control_value_set

**Icona** ![ Icona Del set di valori del controllo audio della classe host](./media/user-guide/usbx-events/image84.png)

**Descrizione**

Questo evento rappresenta un evento di elaborazione posticipata del driver di I/O NetX interno.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Controllo audio.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-audio-deactivate"></a>Disattivazione audio della classe host 

#### <a name="ux_host_class_audio_deactivate"></a>ux_host_class_audio_deactivate

**Icona** ![ Icona Disattiva audio classe host](./media/user-guide/usbx-events/image85.png)

**Descrizione**

Questo evento rappresenta un evento Audio Deactivate della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-audio-read"></a>Lettura audio della classe host 

#### <a name="ux_host_class_audio_read"></a>ux_host_class_audio_read

**Icona** ![ Icona Di lettura audio della classe host](./media/user-guide/usbx-events/image86.png)

**Descrizione**

Questo evento rappresenta un evento di lettura audio della classe host USBX.

- Campi di informazioni 
- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="host-class-audio-streaming-sampling-get"></a>Get del campionamento del flusso audio della classe host 

#### <a name="ux_host_class_audio_streaming_sampling_get"></a>ux_host_class_audio_streaming_sampling_get

**Icona** ![ Icona Get del campionamento di streaming audio della classe host](./media/user-guide/usbx-events/image87.png)

**Descrizione**

Questo evento rappresenta un evento Get di campionamento del flusso audio della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-audio-streaming-sampling-set"></a>Set di campionamento di streaming audio della classe host 

#### <a name="ux_host_class_audio_streaming_sampling_set"></a>ux_host_class_audio_streaming_sampling_set

**Icona** ![ Icona del set di campionamento di streaming audio della classe host](./media/user-guide/usbx-events/image88.png)

**Descrizione**

Questo evento rappresenta un evento set di campionamento di streaming audio della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Campionamento audio.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-audio-write"></a>Scrittura audio classe host 

#### <a name="ux_host_class_audio_write"></a>ux_host_class_audio_write

**Icona** ![ Icona di scrittura audio della classe host](./media/user-guide/usbx-events/image89.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura audio della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-activate"></a>Classe host Cdc Acm Activate 

#### <a name="ux_host_class_cdc_acm_activate"></a>ux_host_class_cdc_acm_activate

**Icona** ![ Icona di attivazione della classe host C D C A C M](./media/user-guide/usbx-events/image90.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione della classe host USBX Cdc Acm.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-deactivate"></a>Host Class Cdc Acm Deactivate 

#### <a name="ux_host_class_cdc_acm_deactivate"></a>ux_host_class_cdc_acm_deactivate

**Icona** ![ Host Class C D C A C M Deactivate icon (Classe host C D C A C M Disattiva)](./media/user-guide/usbx-events/image91.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione della classe host USBX Cdc Acm.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-abort-in-pipe"></a>Classe host Cdc Acm Ioctl Abort nella pipe 

#### <a name="ux_host_class_cdc_acm_ioctl_abort_in_pipe"></a>ux_host_class_cdc_acm_ioctl_abort_in_pipe

**Icona** ![ Classe host C D C A C M I O C T L Icona interrompi nella pipe](./media/user-guide/usbx-events/image92.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Abort In Pipe Event.

Campi di informazioni 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-abort-out-pipe"></a>Classe host Cdc Acm Ioctl Abort Out Pipe 

#### <a name="ux_host_class_cdc_acm_ioct_abort_out_pipe"></a>ux_host_class_cdc_acm_ioct_abort_out_pipe

**Icona** ! [[Classe host C D C A C M I O C T L Icona interrompi pipe](./media/user-guide/usbx-events/image93.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Abort Out Pipe Event.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-get-device-status"></a>Classe host Cdc Acm Ioctl Get Device Status 

#### <a name="ux_host_class_cdc_acm_ioctl_get_device_status"></a>ux_host_class_cdc_acm_ioctl_get_device_status

**Icona** ![ Classe host C D C A C M I O C T L Icona Ottieni stato dispositivo](./media/user-guide/usbx-events/image94.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Get Device Status Event.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Stato del dispositivo.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-get-line-coding"></a>Classe host Cdc Acm Ioctl Get Line Coding 

#### <a name="ux_host_class_cdc_acm_ioctl_get_line_coding"></a>ux_host_class_cdc_acm_ioctl_get_line_coding

**Icona** ![ Classe host C D C A C M I O C T L Icona Get Line Coding](./media/user-guide/usbx-events/image95.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Get Line Coding Event.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: parametro.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-notification-callback"></a>Callback di notifica Ioctl della classe host Cdc Acm

#### <a name="ux_host_class_cdc_acm_ioctl_notification_callback"></a>ux_host_class_cdc_acm_ioctl_notification_callback

**Icona** ![ Classe host C D C A C M I O C T L Icona callback di notifica](./media/user-guide/usbx-events/image96.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Notification Callback Event.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-send-break"></a>Interruzione di invio ioctl della classe host Cdc Acm 

#### <a name="ux_host_class_cdc_acm_ioctl_send_break"></a>ux_host_class_cdc_acm_ioctl_send_break

**Icona** ![ Classe host C D C A C M I O C T L Send Break](./media/user-guide/usbx-events/image97.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Send Break Event.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-set-line-coding"></a>Classe host Cdc Acm Ioctl Set Line Coding 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_coding"></a>ux_host_class_cdc_acm_ioctl_set_line_coding

**Icona** ![ La classe host C D C A C M I O C T L Imposta l'icona line ](./media/user-guide/usbx-events/image97.png) coding](./media/user-guide/usbx-events/image98.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Set Line Coding Event.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-ioctl-set-line-state"></a>Classe host Cdc Acm Ioctl Set Line State 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_state"></a>ux_host_class_cdc_acm_ioctl_set_line_state

**Icona** ![ Classe host C D C A C M I O C T L Imposta stato riga](./media/user-guide/usbx-events/image99.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Ioctl Set Line State Event.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-read"></a>Classe host Cdc Acm Read 

#### <a name="ux_host_class_cdc_acm_read"></a>ux_host_class_cdc_acm_read

**Icona** ![ Icona di lettura della classe host C D C A C M](./media/user-guide/usbx-events/image100.png)

**Descrizione**

Questo evento rappresenta un evento di lettura della classe host USBX Cdc Acm.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Campo info 3: Lunghezza richiesta.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-reception-start"></a>Inizio ricezione classe host Cdc Acm 

#### <a name="ux_host_class_cdc_acm_reception_start"></a>ux_host_class_cdc_acm_reception_start

**Icona** ![ Icona di avvio della ricezione della classe host C D C A C M](./media/user-guide/usbx-events/image101.png)

**Descrizione**

Questo evento rappresenta un evento di avvio della ricezione della classe host USBX Cdc Acm.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-reception-stop"></a>Arresto ricezione classe host Cdc Acm 

#### <a name="ux_host_class_cdc_acm_reception_stop"></a>ux_host_class_cdc_acm_reception_stop

**Icona** ![ Icona arresto ricezione classe host C D C A C M](./media/user-guide/usbx-events/image102.png)

**Descrizione**

Questo evento rappresenta un evento di arresto della ricezione della classe host USBX Cdc Acm.

**Campi di informazioni**

- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-cdc-acm-write"></a>Classe host Cdc Acm Write 

#### <a name="ux_host_class_acm_write"></a>ux_host_class_acm_write

**Icona** ![ Icona di scrittura della classe host C D C A C M](./media/user-guide/usbx-events/image103.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Cdc Acm Write Event.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Campo info 3: Lunghezza richiesta.
- Info Campo 4: Non usato.

### <a name="host-class-dpump-activate"></a>Classe host Dpump Activate 

#### <a name="ux_host_class_dpump_activate"></a>ux_host_class_dpump_activate

**Icona** ![ Icona Dpump Activate della classe host](./media/user-guide/usbx-events/image104.png)

**Descrizione**

Questo evento rappresenta un evento Dpump Activate della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-dpump-deactivate"></a>Classe host Dpump Deactivate 

#### <a name="ux_host_class_dpump_deactivate"></a>ux_host_class_dpump_deactivate

**Icona** ![ Icona Disattiva Dpump della classe host](./media/user-guide/usbx-events/image105.png)

**Descrizione**

Questo evento rappresenta un evento Dpump Deactivate della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-dpump-read"></a>Lettura Dpump della classe host 

#### <a name="ux_host_class_dpump_read"></a>ux_host_class_dpump_read

**Icona** ![ Icona di lettura Dpump della classe host](./media/user-guide/usbx-events/image106.png)

**Descrizione**

Questo evento rappresenta un evento di lettura Dpump della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="host-class-dpump-write"></a>Scrittura Dpump della classe host 

#### <a name="ux_host_class_dpump_write"></a>ux_host_class_dpump_write

**Icona** ![ Icona scrittura Dpump classe host](./media/user-guide/usbx-events/image107.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura Dpump della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Campo informazioni 3: lunghezza richiesta.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-activate"></a>Attivazione hid della classe host 

#### <a name="ux_host_class_hid_activate"></a>ux_host_class_hid_activate

**Icona** ![ Icona Hid Activate della classe host](./media/user-guide/usbx-events/image108.png)

**Descrizione**

Questo evento rappresenta un evento Hid Activate della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-client-register"></a>Registro del client Hid della classe host 

#### <a name="ux_host_class_hid_client_register"></a>ux_host_class_hid_client_register

**Icona** ![ Icona Hid Client Register (Registro client hid) della classe host](./media/user-guide/usbx-events/image109.png)

**Descrizione**

Questo evento rappresenta un evento di registro del client hid della classe host USBX.

**Campi di informazioni** 

- Info Field 1: Hid client name (Campo informazioni 1: Nome client hid).
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-deactivate"></a>Disattivazione hid della classe host 

#### <a name="ux_host_class_hid_deactivate"></a>ux_host_class_hid_deactivate

**Icona** ![ Icona Hid Deactivate della classe host](./media/user-guide/usbx-events/image110.png)

**Descrizione**

Questo evento rappresenta un evento Hid Deactivate della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-idle-get"></a>Hid Idle Get della classe host 

#### <a name="ux_host_class_hid_idle_get"></a>ux_host_class_hid_idle_get

**Icona** ![ Icona Hid Idle Get della classe host](./media/user-guide/usbx-events/image111.png)

**Descrizione**

Questo evento rappresenta un evento Hid Idle Get della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-idle-set"></a>Host Class Hid Idle Set 

#### <a name="ux_host_class_hid_idle_set"></a>ux_host_class_hid_idle_set

**Icona** ![ Icona Hid Idle Set della classe host](./media/user-guide/usbx-events/image112.png)

**Descrizione**

Questo evento rappresenta un evento hid idle set della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-keyboard-activate"></a>Attivazione tastiera hid della classe host 

#### <a name="ux_host_class_hid_keyboard_activate"></a>ux_host_class_hid_keyboard_activate

**Icona** ![ Icona di attivazione della tastiera hid della classe host](./media/user-guide/usbx-events/image113.png)

**Descrizione**

Questo evento rappresenta un evento hid keyboard activate della classe host USBX.

**Campi di informazioni**
<p>Campo informazioni 1: istanza della classe.
<p>Campo informazioni 2: istanza del client Hid.
<p>Campo informazioni 3: Non usato.
<p>Campo informazioni 4: Non usato.

### <a name="host-class-hid-keyboard-deactivate"></a>Disattivazione della tastiera hid della classe host 

#### <a name="ux_host_class_hid_keyboard_deactivate"></a>ux_host_class_hid_keyboard_deactivate

**Icona** ![ Icona di disattivazione della tastiera hid della classe host](./media/user-guide/usbx-events/image114.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione della tastiera hid della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza del client Hid.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-mouse-activate"></a>Attivazione mouse hid della classe host 

#### <a name="ux_host_class_hid_mouse_activate"></a>ux_host_class_hid_mouse_activate

**Icona** ![ Icona hid mouse activate della classe host](./media/user-guide/usbx-events/image115.png)

**Descrizione**

Questo evento rappresenta un evento Hid Mouse Activate della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza del client Hid.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-hid-mouse-deactivate"></a>Disattivazione del mouse hid della classe host 

#### <a name="ux_host_class_hid_mouse_deactivate"></a>ux_host_class_hid_mouse_deactivate

**Icona** ![ Icona di disattivazione del mouse hid della classe host](./media/user-guide/usbx-events/image116.png)

**Descrizione**

- Questo evento rappresenta un evento Hid Mouse Deactivate della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza del client Hid.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hid-remote-control-activate"></a>Classe host Hid Remote Control Activate 

#### <a name="ux_host_class_hid_remote_control_activate"></a>ux_host_class_hid_remote_control_activate

**Icona** ![ Icona di attivazione del controllo remoto hid della classe host](./media/user-guide/usbx-events/image117.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione del controllo remoto hid della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza del client Hid.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hid-remote-control-deactivate"></a>Classe host Hid Remote Control Deactivate 

#### <a name="ux_host_class_hid_remote_control_deactivate"></a>ux_host_class_hid_remote_control_deactivate

**Icona** ![ Icona Disattiva controllo remoto hid della classe host](./media/user-guide/usbx-events/image118.png)

**Descrizione**

Questo evento rappresenta un evento Hid Remote Control Deactivate della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza del client Hid.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hid-report-get"></a>Get report hid della classe host 

#### <a name="ux_host_class_hid_report_get"></a>ux_host_class_hid_report_get

**Icona** ![ Icona Del report Hid Get della classe host](./media/user-guide/usbx-events/image119.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Hid Report Get.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: report client.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hid-report-set"></a>Set di report hid della classe host 

#### <a name="ux_host_class_hid_report_set"></a>ux_host_class_hid_report_set

**Icona** ![ Icona Del set di report hid della classe host](./media/user-guide/usbx-events/image120.png)

**Descrizione** Questo evento rappresenta un set di report hid della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: report client.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hub-activate"></a>Attivazione dell'hub della classe host 

#### <a name="ux_host_class_hub_activate"></a>ux_host_class_hub_activate

**Icona** ![ Icona attiva dell'hub della classe host](./media/user-guide/usbx-events/image121.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione dell'hub della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hub-change-detect"></a>Rilevamento delle modifiche dell'hub della classe host 

#### <a name="ux_host_class_hub_change_detect"></a>ux_host_class_hub_change_detect

**Icona** ![ Icona Rilevamento modifiche hub classe host](./media/user-guide/usbx-events/image122.png)

**Descrizione**

Questo evento rappresenta un evento di rilevamento delle modifiche dell'hub della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hub-deactivate"></a>Disattivazione dell'hub della classe host 

#### <a name="ux_host_class_hub_deactivate"></a>ux_host_class_hub_deactivate

**Icona** ![ Icona Disattiva hub classe host](./media/user-guide/usbx-events/image123.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione dell'hub della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-hub-port-change-connection-process"></a>Processo di modifica della porta dell'hub della classe host 

#### <a name="ux_host_class_hub_change_connection_process"></a>ux_host_class_hub_change_connection_process

**Icona** ![ Icona Del processo di connessione per la modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image124.png)

**Descrizione**

Questo evento rappresenta un evento del processo di modifica della porta dell'hub della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Porta.
- Info Campo 3: Stato della porta.
- Campo info 4: Non usato.

### <a name="host-class-hub-port-change-enable-process"></a>Processo di abilitazione della modifica della porta dell'hub della classe host 

#### <a name="ux_host_class_hub_port_change_enable_process"></a>ux_host_class_hub_port_change_enable_process

**Icona** ![ Icona Abilita processo di abilitazione della modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image125.png)

**Descrizione**

Questo evento rappresenta un evento processo di abilitazione della modifica della porta dell'hub della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Porta.
- Info Campo 3: Stato della porta.
- Campo info 4: Non usato.

### <a name="host-class-hub-port-change-over-current-process"></a>Modifica della porta dell'hub della classe host rispetto al processo corrente 

#### <a name="ux_host_class_hub_port_change_over_current_process"></a>ux_host_class_hub_port_change_over_current_process

**Icona** ![ Icona Modifica della porta dell'hub della classe host rispetto al processo corrente](./media/user-guide/usbx-events/image126.png)

**Descrizione**

Questo evento rappresenta l'allocazione di un pacchetto tramite nx_packet_allocate.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Porta.
- Campo informazioni 3: Stato della porta.
- Campo informazioni 4: Non usato.

### <a name="host-class-hub-port-change-reset-process"></a>Processo di reimpostazione della porta dell'hub di classe host 

#### <a name="ux_host_class_hub_port_change_reset_process"></a>ux_host_class_hub_port_change_reset_process

**Icona** ![ Icona del processo di reimpostazione della modifica della porta dell'hub di classe host](./media/user-guide/usbx-events/image127.png)

**Descrizione**

Questo evento rappresenta un evento del processo di reimpostazione della modifica della porta dell'hub di classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: Hub. Campo informazioni 2: Porta.
- Campo informazioni 3: Stato della porta.
- Campo informazioni 4: Non usato.

### <a name="host-class-hub-port-change-suspend-process"></a>Processo di sospensione della modifica della porta dell'hub di classe host 

#### <a name="ux_host_class_hub_port_change_suspend_process"></a>ux_host_class_hub_port_change_suspend_process

**Icona** ![ Icona Sospendi processo di modifica della porta dell'hub di classe host](./media/user-guide/usbx-events/image128.png)

**Descrizione**

Questo evento rappresenta un evento del processo di sospensione della modifica della porta dell'hub di classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Porta.
- Campo informazioni 3: Stato della porta.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-activate"></a>Classe host Pima Activate 

#### <a name="ux_host_class_pima_activate"></a>ux_host_class_pima_activate

**Icona** ![ Icona di attivazione pima della classe host](./media/user-guide/usbx-events/image129.png)

**Descrizione**

Questo evento rappresenta un evento Pima Activate della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-deactivate"></a>Host Class Pima Deactivate 

#### <a name="ux_host_class_pima_deactivate"></a>ux_host_class_pima_deactivate

**Icona** ![ Icona Disattiva pima classe host](./media/user-guide/usbx-events/image130.png)

**Descrizione**

Questo evento rappresenta un evento Pima Deactivate della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-device-info-get"></a>Ottenere informazioni sul dispositivo Pima della classe host 

#### <a name="ux_host_class_pima_device_info_get"></a>ux_host_class_pima_device_info_get

**Icona** ![ Icona Ottieni informazioni sul dispositivo Pima della classe host](./media/user-guide/usbx-events/image131.png)

**Descrizione**

Questo evento rappresenta un evento Get info dispositivo Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: dispositivo Pima.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-device-reset"></a>Reimpostazione del dispositivo Pima della classe host 

#### <a name="ux_host_class_pima_device_reset"></a>ux_host_class_pima_device_reset

**Icona** ![ Icona di reimpostazione del dispositivo Pima della classe host](./media/user-guide/usbx-events/image132.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione del dispositivo Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-notification"></a>Notifica Pima della classe host 

#### <a name="ux_host_class_pima_notification"></a>ux_host_class_pima_notification

**Icona** ![ Icona di notifica Pima della classe host](./media/user-guide/usbx-events/image133.png)

**Descrizione**

Questo evento rappresenta un evento di notifica Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe. Campo informazioni 2: codice evento.
- Campo informazioni 3: ID transazione.
- Campo informazioni 4: Parametro1.

### <a name="host-class-pima-number-objects-get"></a>Oggetti numero pima della classe host Get 

#### <a name="ux_host_class_pima_number_objects_get"></a>ux_host_class_pima_number_objects_get

**Icona** ![ Icona Get degli oggetti numero pima della classe host](./media/user-guide/usbx-events/image134.png)

**Descrizione**

Questo evento rappresenta un evento Get Di oggetti numero pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-object-close"></a>Chiusura dell'oggetto Pima della classe host 

#### <a name="ux_host_class_pima_object_close"></a>ux_host_class_pima_object_close

**Icona** ![ Icona di chiusura dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image135.png)

**Descrizione**

Questo evento rappresenta un evento di chiusura dell'oggetto Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: oggetto.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-class-pima-object-copy"></a>Copia dell'oggetto Pima della classe host 

#### <a name="ux_host_class_pima_object_copy"></a>ux_host_class_pima_object_copy

**Icona** ![ Icona di copia dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image136.png)

**Descrizione**

Questo evento rappresenta un evento di copia dell'oggetto Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-pima-object-delete"></a>Eliminazione dell'oggetto Pima della classe host 

#### <a name="ux_host_class_pima_object_delete"></a>ux_host_class_pima_object_delete

**Icona** ![ Icona di eliminazione di oggetti Pima della classe host](./media/user-guide/usbx-events/image137.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'oggetto Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-pima-object-get"></a>Oggetto Pima della classe host Get 

#### <a name="ux_host_class_pima_object_get"></a>ux_host_class_pima_object_get

**Icona** ![ Icona Get dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image138.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni RARP tramite nx_rarp_info_get.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Campo informazioni 3: Oggetto.
- Campo info 4: Non usato.

### <a name="host-class-pima-object-info-get"></a>Ottenere informazioni sull'oggetto Pima della classe host 

#### <a name="ux_host_class_pima_object_info_get"></a>ux_host_class_pima_object_info_get

**Icona** ![ Icona Ottieni informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image139.png)

**Descrizione**

Questo evento rappresenta un evento get di informazioni sull'oggetto Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Campo informazioni 3: Oggetto.
- Campo info 4: Non usato.

### <a name="host-class-pima-object-info-send"></a>Classe host Pima Object Info Send 

#### <a name="ux_host_class_pima_object_info_send"></a>ux_host_class_pima_object_info_send

**Icona** ![ Icona di invio delle informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image140.png)

**Descrizione**

Questo evento rappresenta un evento di invio di informazioni sull'oggetto Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Oggetto.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-pima-object-move"></a>Spostamento di oggetti Pima della classe host 

#### <a name="ux_host_class_pima_object_move"></a>ux_host_class_pima_object_move

**Icona** ![ Icona di spostamento di oggetti Pima della classe host](./media/user-guide/usbx-events/image141.png)

**Descrizione**

Questo evento reprThis rappresenta un evento di spostamento di oggetti Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Campo informazioni 3: Oggetto.
- Campo info 4: Non usato.

### <a name="host-class-pima-object-send"></a>Classe host Pima Object Send 

#### <a name="ux_host_class_pima_object_move"></a>ux_host_class_pima_object_move

**Icona** ![ Icona di invio dell'oggetto Pima della classe host](./media/user-guide/usbx-events/image142.png)

**Descrizione**

Questo evento rappresenta un evento di invio di oggetti Pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Oggetto.
- Campo informazioni 3: Buffer di oggetti.
- Info Campo 4: Lunghezza dell'oggetto.

### <a name="host-class-pima-object-transfer-abort"></a>Interruzione del trasferimento di oggetti Pima della classe host 

#### <a name="ux_host_class_pima_object_transfer_abort"></a>ux_host_class_pima_object_transfer_abort

**Icona** ![ Icona interruzione trasferimento oggetti pima della classe host](./media/user-guide/usbx-events/image143.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del trasferimento di oggetti pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Campo informazioni 3: Oggetto.
- Campo info 4: Non usato.

### <a name="host-class-pima-read"></a>Classe host Pima Read 

#### <a name="ux_host_class_pima_read"></a>ux_host_class_pima_read

**Icona** ![ Icona Di lettura pima della classe host](./media/user-guide/usbx-events/image144.png)

**Descrizione**

Questo evento rappresenta un evento di lettura pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza dei dati.
- Campo info 4: Non usato.

### <a name="host-class-pima-request-cancel"></a>Classe host Pima Request Cancel 

#### <a name="ux_host_class_pima_request_cancel"></a>ux_host_class_pima_request_cancel

**Icona** ![ Icona Di annullamento della richiesta pima della classe host](./media/user-guide/usbx-events/image145.png)

**Descrizione**

Questo evento rappresenta un evento di annullamento della richiesta pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-pima-session-close"></a>Chiusura della sessione pima della classe host 

#### <a name="ux_host_class_pima_session_close"></a>ux_host_class_pima_session_close

**Icona** ![ Icona di chiusura della sessione pima della classe host](./media/user-guide/usbx-events/image146.png)

**Descrizione**

Questo evento rappresenta un evento di chiusura della sessione pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: sessione di Pima.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-pima-session-open"></a>Classe host Pima Session Open 

#### <a name="ux_host_class_pima_session_open"></a>ux_host_class_pima_session_open

**Icona** ![ Icona Host Class Pima Session Open](./media/user-guide/usbx-events/image147.png)

**Descrizione** Questo evento rappresenta un evento di apertura della sessione pima della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: sessione di Pima.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-pima-storage-ids-get"></a>Ottenere gli ID Archiviazione pima della classe host 

#### <a name="ux_host_class_pima_session_ids_get"></a>ux_host_class_pima_session_ids_get

**Icona** ![ Icona Get degli ID Archiviazione pima della classe host](./media/user-guide/usbx-events/image148.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Pima Archiviazione evento Get IDs.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- nfo Field 2: Archiviazione ID matrice.
- Info Campo 3: Archiviazione ID.
Info Campo 4: Non usato.

### <a name="host-class-pima-storage-info-get"></a>Classe host Pima Archiviazione Info Get 

#### <a name="ux_host_class_pima_storage_info_get"></a>ux_host_class_pima_storage_info_get

**Icona** ![ Icona di Pima Archiviazione Classe host Per ottenere informazioni](./media/user-guide/usbx-events/image149.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Pima Archiviazione Info Get Event.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: Archiviazione ID.
- Campo informazioni 3: Archiviazione.
- Info Campo 4: Non usato.

### <a name="host-class-pima-thumb-get"></a>Classe host Pima Thumb Get 

#### <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

**Icona** ![ Icona di Pima Thumb Get della classe host](./media/user-guide/usbx-events/image150.png)

**Descrizione**

Questo evento rappresenta l'inaccettabile connessione a un server TCP tramite nx_tcp_server_socket_unaccept.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: handle di oggetto.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-pima-write"></a>Classe host Pima Write 

#### <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

**Icona** ![ Icona di Pima Write della classe host](./media/user-guide/usbx-events/image151.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Pima Write.

**Campi di informazioni**

- Campo info 1: Istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza dei dati.
- Info Campo 4: Non usato.

### <a name="host-class-printer-activate"></a>Attivazione della stampante della classe host 

#### <a name="ux_host_class_printer_activate"></a>ux_host_class_printer_activate

**Icona** ![ Icona Attiva stampante classe host](./media/user-guide/usbx-events/image152.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione della stampante della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: puntatore all'istanza IP.
- Campo informazioni 2: puntatore al socket.
- Campo informazioni 3: tipo di servizio.
- Info Campo 4: Dimensioni della finestra di ricezione.

### <a name="host-class-printer-deactivate"></a>Disattivazione della stampante della classe host 

#### <a name="ux_host_class_printer_deactivate"></a>ux_host_class_printer_deactivate

**Icona** ![ Icona Disattiva stampante classe host](./media/user-guide/usbx-events/image153.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione della stampante della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-printer-name-get"></a>Ottenere il nome della stampante della classe host 

#### <a name="ux_host_class_printer_name_get"></a>ux_host_class_printer_name_get

**Icona** ![ Icona Get del nome della stampante della classe host](./media/user-guide/usbx-events/image154.png)

**Descrizione**

Questo evento rappresenta un evento Get nome stampante classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-class-printer-read"></a>Lettura stampante classe host 

#### <a name="ux_host_class_printer_read"></a>ux_host_class_printer_read

**Icona** ![ Icona Lettura stampante classe host](./media/user-guide/usbx-events/image155.png)

**Descrizione**

Questo evento rappresenta un evento di lettura della stampante della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza richiesta.
- Info Campo 4: Non usato.

### <a name="host-class-printer-soft-reset"></a>Reimpostazione soft della stampante della classe host 

#### <a name="ux_host_class_printer_soft_reset"></a>ux_host_class_printer_soft_reset

**Icona** ![ Icona reimpostazione del soft reset della stampante della classe host](./media/user-guide/usbx-events/image156.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione soft della stampante della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-printer-status-get"></a>Ottiene lo stato della stampante della classe host 

#### <a name="ux_host_class_printer_status_get"></a>ux_host_class_printer_status_get

**Icona** ![ Icona Get dello stato della stampante della classe host](./media/user-guide/usbx-events/image157.png)

**Descrizione**

Questo evento rappresenta un evento Get dello stato della stampante della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: stato della stampante.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-printer-write"></a>Scrittura stampante classe host 

#### <a name="ux_host_class_printer_write"></a>ux_host_class_printer_write

**Icona** ![ Icona scrittura stampante classe host](./media/user-guide/usbx-events/image158.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Printer Write.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza richiesta.
- Campo info 4: Non usato.

### <a name="host-class-prolific-activate"></a>Attivazione della classe host Disaserta 

#### <a name="ux_host_class_prolific_activate"></a>ux_host_class_prolific_activate 

**Icona** ![ Icona attivazione di Classi host Insod](./media/user-guide/usbx-events/image159.png)

**Descrizione**

Questo evento rappresenta un evento Activate della classe host USBX.

**Campi di informazioni** 

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-deactivate"></a>Disattivazione della classe host Inattiva 

#### <a name="ux_host_class_prolific_deactivate"></a>ux_host_class_prolific_deactivate 

**Icona** ![ Icona disattiva classe host](./media/user-guide/usbx-events/image160.png)

**Descrizione**

Questo evento rappresenta un evento Deactivate della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-abort-in-pipe"></a>Interruzione ioctl della classe host nella pipe 

#### <a name="ux_host_class_prolific_ioctl_abort_in_pipe"></a>ux_host_class_prolific_ioctl_abort_in_pipe

**Icona** ![ Icona dell'interruzione dell'interruzione della classe host I O C T L nella pipe](./media/user-guide/usbx-events/image161.png)

**Descrizione**

Questo evento rappresenta un evento ioctl Abort In Pipe della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Endpoint.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-abort-out-pipe"></a>Pipe di interruzione ioctl della classe host 

#### <a name="ux_host_class_prolific_ioctl_abort_out_pipe"></a>ux_host_class_prolific_ioctl_abort_out_pipe

**Icona** ![ Icona della pipe di interruzione dell'interruzione della pipe di I O C T L della classe host](./media/user-guide/usbx-events/image162.png)

**Descrizione**

Questo evento rappresenta un evento pipe di interruzione ioctl ioctl della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Endpoint.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-get-device-status"></a>Ioctl Get Device Status della classe host 

#### <a name="ux_host_class_prolific_ioctl_get_device_status"></a>ux_host_class_prolific_ioctl_get_device_status

**Icona** ![ Icona Di stato del dispositivo get di I O C T L della classe host](./media/user-guide/usbx-events/image163.png)

**Descrizione**

Questo evento rappresenta un evento Ioctl Get Device Status della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo Info 2: Stato del dispositivo.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-get-line-coding"></a>Codifica linea Ioctl Get line della classe host 

#### <a name="ux_host_class_prolific_ioctl_get_line_coding"></a>ux_host_class_prolific_ioctl_get_line_coding

**Icona** ![ Icona di codifica linea per la classe host Disartiemeta I O C T L Get Line](./media/user-guide/usbx-events/image164.png)

**Descrizione**

Questo evento rappresenta un evento ioctl Get Line Coding della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-purge"></a>Pulitura Ioctl della classe host 

#### <a name="ux_host_class_prolific_ioctl_purge"></a>ux_host_class_prolific_ioctl_purge

**Icona** ![ Icona pulitura ioctl della classe host](./media/user-guide/usbx-events/image165.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione Ioctl ioctl della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-report-device"></a>Dispositivo report Ioctl della classe host 

#### <a name="ux_host_class_prolific_ioctl_report_device"></a>ux_host_class_prolific_ioctl_report_device

**Icona** ![ Icona del dispositivo report I O C T L della classe host](./media/user-guide/usbx-events/image166.png)

**Descrizione**

Questo evento rappresenta un evento di modifica dello stato del dispositivo di report Ioctl della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-send-break"></a>Interruzione di invio Ioctl della classe host 

#### <a name="ux_host_class_prolific_ioctl_send_break"></a>ux_host_class_prolific_ioctl_send_break

**Icona** ![ Icona di interruzione di trasmissione di I O C T L della classe host](./media/user-guide/usbx-events/image167.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione di trasmissione Ioctl ioctl della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-set-line-coding"></a>Codifica riga per set ioctl della classe host 

#### <a name="ux_host_class_prolific_ioctl_set_line_coding"></a>ux_host_class_prolific_ioctl_set_line_coding

**Icona** ![ Icona della codifica linea impostata per la classe host Disartieme I O C T L impostata](./media/user-guide/usbx-events/image168.png)

**Descrizione**

Questo evento rappresenta un evento di codifica linea ioctl set ioctl classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-ioctl-set-line-state"></a>Stato linea set ioctl della classe host 

#### <a name="ux_host_class_prolific_ioctl_set_line_state"></a>ux_host_class_prolific_ioctl_set_line_state

**Icona** ![ Icona Di stato linea impostata classe host I O C T L](./media/user-guide/usbx-events/image169.png)

**Descrizione**

Questo evento rappresenta un evento stato linea set ioctl della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo info 2: parametro.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-read"></a>Lettura non in lettura della classe host 

#### <a name="ux_host_class_prolific_read"></a>ux_host_class_prolific_read

**Icona** ![ Icona Di lettura di classi host](./media/user-guide/usbx-events/image170.png)

**Descrizione**

Questo evento rappresenta una classe host USBX , un evento di lettura in modalità non consentita.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza richiesta.
- Campo info 4: Non usato.

### <a name="host-class-prolific-reception-start"></a>Inizio ricezione della classe host 

#### <a name="ux_host_class_prolific_reception_start"></a>ux_host_class_prolific_reception_start

**Icona** ![ Icona start ricezione della classe host](./media/user-guide/usbx-events/image171.png)

**Descrizione**

Questo evento rappresenta un evento di avvio della ricezione della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-reception-stop"></a>Arresto della ricezione della classe host 

#### <a name="ux_host_class_prolific_reception_stop"></a>ux_host_class_prolific_reception_stop

**Icona** ![ Icona arresto della ricezione della classe host](./media/user-guide/usbx-events/image172.png)

**Descrizione**

Questo evento rappresenta un evento di arresto della ricezione della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-prolific-write"></a>Scrittura non autorese della classe host 

#### <a name="ux_host_class_prolific_write"></a>ux_host_class_prolific_write

**Icona** ![ Icona di scrittura per classi host](./media/user-guide/usbx-events/image173.png)

**Descrizione**

Questo evento rappresenta una classe host USBX, un evento di scrittura di tipo non associato.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore ai dati.
- Info Campo 3: Lunghezza richiesta.
- Campo info 4: Non usato.

### <a name="host-class-storage-activate"></a>Attivazione della classe host Archiviazione 

#### <a name="ux_host_class_storage_activate"></a>ux_host_class_storage_activate

**Icona** ![ Icona Attiva Archiviazione classe host](./media/user-guide/usbx-events/image174.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione Activate Event.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-deactivate"></a>Classe host Archiviazione Deactivate 

#### <a name="ux_host_class_storage_deactivate"></a>ux_host_class_storage_deactivate

**Icona** ![ Icona Disattiva Archiviazione classe host](./media/user-guide/usbx-events/image175.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione evento Deactivate.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-media-capacity-get"></a>Classe host Archiviazione capacità multimediale get 

#### <a name="ux_host_class_storage_media_capacity_get"></a>ux_host_class_storage_media_capacity_get

**Icona** ![ Classe host Archiviazione'icona Ottieni capacità multimediale](./media/user-guide/usbx-events/image176.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione evento Get della capacità multimediale.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-media-format-capacity-get"></a>Classe host Archiviazione Media Format Capacity Get

#### <a name="ux_host_class_storage_media_format_capacity_get"></a>ux_host_class_storage_media_format_capacity_get

**Icona** ![ Icona Della classe host Archiviazione Media Format Capacity Get](./media/user-guide/usbx-events/image177.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione evento Get della capacità del formato multimediale.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

#### <a name="host-class-storage-media-mount"></a>Classe host Archiviazione supporto montaggio 

#### <a name="ux_host_class_storage_media_mount"></a>ux_host_class_storage_media_mount

**Icona** ![ Classe host Archiviazione'icona Montaggio multimediale](./media/user-guide/usbx-events/image178.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione evento di montaggio multimediale.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Settore.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-media-open"></a>Classe host Archiviazione Media Open 

#### <a name="ux_host_class_storage_media_open"></a>ux_host_class_storage_media_open

**Icona** ![ Classe host Archiviazione'icona Apri supporti](./media/user-guide/usbx-events/image179.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione evento Media Open.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Supporti.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-media-read"></a>Classe host Archiviazione Media Read 

#### <a name="ux_host_class_storage_media_read"></a>ux_host_class_storage_media_read

**Icona** ![ Icona Di lettura Archiviazione classe host](./media/user-guide/usbx-events/image180.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione di lettura multimediale.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Inizio del settore.
- Info Campo 3: Numero di settori.
- Info Campo 4: Puntatore ai dati.

### <a name="host-class-storage-media-write"></a>Scrittura di supporti Archiviazione classe host 

#### <a name="ux_host_class_storage_media_write"></a>ux_host_class_storage_media_write

**Icona** ![ Icona Di scrittura Archiviazione classe host](./media/user-guide/usbx-events/image181.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione di scrittura multimediale.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: Inizio del settore.
- Info Campo 3: Numero di settori.
- Info Campo 4: Puntatore ai dati.

### <a name="host-class-storage-request-sense"></a>Senso di richiesta Archiviazione classe host 

#### <a name="ux_host_class_storage_request_sense"></a>ux_host_class_storage_request_sense

**Icona** ![ Icona Del senso Archiviazione classe host](./media/user-guide/usbx-events/image182.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione request sense.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-start-stop"></a>Arresto della Archiviazione host 

#### <a name="ux_host_class_storage_start_stop"></a>ux_host_class_storage_start_stop

**Icona** ![ Icona Avvia arresto Archiviazione classe host](./media/user-guide/usbx-events/image183.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione evento start stop.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Field 2: Start stop signal (Campo informazioni 2: Avvia segnale di arresto).
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-class-storage-unit-ready-test"></a>Classe host Archiviazione unit test pronto 

#### <a name="ux_host_class_storage_unit_ready_test"></a>ux_host_class_storage_unit_ready_test

**Icona** ![ Icona Della classe host Archiviazione Unit Ready Test](./media/user-guide/usbx-events/image184.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Archiviazione di test unit ready.

**Campi di informazioni**

- Campo informazioni 1: istanza della classe.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-stack-class-instance-create"></a>Creazione dell'istanza della classe stack host 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Icona** ![ Icona Crea istanza classe stack host](./media/user-guide/usbx-events/image185.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza della classe host USBX.

**Campi di informazioni**

- Campo informazioni 1: classe.
- Campo informazioni 2: Istanza della classe.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="host-stack-class-instance-destroy"></a>Eliminazione dell'istanza della classe stack host 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Icona** ![ Icona Eliminazione dell'istanza della classe stack host](./media/user-guide/usbx-events/image186.png)

**Descrizione**

Questo evento rappresenta un evento destroy dell'istanza della classe stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: classe.
- Campo informazioni 2: Istanza della classe.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-configuration-delete"></a>Eliminazione della configurazione dello stack host 

#### <a name="ux_host_class_configuration_delete"></a>ux_host_class_configuration_delete

**Icona** ![ Icona Elimina configurazione stack host](./media/user-guide/usbx-events/image187.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione della configurazione dello stack host USBX.

**Campi di informazioni**

- Campo info 1: Configurazione.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-configuration-enumerate"></a>Enumerazione della configurazione dello stack host 

#### <a name="ux_host_stack_configuration_enumerate"></a>ux_host_stack_configuration_enumerate

**Icona** ![ Icona enumerare la configurazione dello stack host](./media/user-guide/usbx-events/image188.png)

**Descrizione**

Questo evento rappresenta un evento enumerato di configurazione dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="stack-configuration-instance-create"></a>Creazione dell'istanza di configurazione dello stack 

#### <a name="ux_host_stack_configuration_instance_create"></a>ux_host_stack_configuration_instance_create

**Icona** ![ Icona Crea istanza di configurazione stack](./media/user-guide/usbx-events/image189.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza di configurazione dello stack di host USBX.

**Campi di informazioni**

- Campo info 1: Configurazione.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-configuration-instance-delete"></a>Eliminazione dell'istanza di configurazione dello stack host 

#### <a name="ux_host_stack_configuration_instance_delete"></a>ux_host_stack_configuration_instance_delete

**Icona** ![ Icona Di eliminazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image190.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'istanza di configurazione dello stack host USBX.

**Campi di informazioni**

- Campo info 1: Configurazione.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-configuration-set"></a>Set di configurazione dello stack di host 

#### <a name="ux_host_stack_configuration_set"></a>ux_host_stack_configuration_set

**Icona** ![ Icona del set di configurazione dello stack di host](./media/user-guide/usbx-events/image191.png)

**Descrizione**

Questo evento rappresenta un evento del set di configurazione dello stack host USBX.

**Campi di informazioni**

- Campo info 1: Configurazione.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-device-address-set"></a>Set di indirizzi del dispositivo stack host 

#### <a name="ux_host_stack_device_address_set"></a>ux_host_stack_device_address_set

**Icona** ![ Icona Del set di indirizzi del dispositivo stack host](./media/user-guide/usbx-events/image192.png)

**Descrizione**

Questo evento rappresenta un evento del set di indirizzi del dispositivo stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo Info 2: Indirizzo del dispositivo.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-device-configuration-get"></a>Ottenere la configurazione del dispositivo stack host 

#### <a name="ux_host_stack_device_configuration_get"></a>ux_host_stack_device_configuration_get

**Icona** ![ Icona Get della configurazione del dispositivo dello stack di host](./media/user-guide/usbx-events/image193.png)

**Descrizione**

Questo evento rappresenta un evento Get di configurazione del dispositivo stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- nfo Campo 2: Configurazione.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-device-configuration-select"></a>Selezione configurazione dispositivo stack host 

#### <a name="ux_host_stack_device_configuration_select"></a>ux_host_stack_device_configuration_select

**Icona** ![ Icona Di selezione della configurazione del dispositivo dello stack host](./media/user-guide/usbx-events/image194.png)

**Descrizione**

Questo evento rappresenta un evento di selezione della configurazione del dispositivo dello stack di host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo Info 2: Configurazione.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-device-descriptor-read"></a>Lettura descrittore dispositivo stack host 

#### <a name="ux_host_stack_device_descriptor_read"></a>ux_host_stack_device_descriptor_read

**Icona** ![ Icona Di lettura descrittore dispositivo stack host](./media/user-guide/usbx-events/image195.png)

**Descrizione**

Questo evento rappresenta un evento di lettura del descrittore del dispositivo dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="host-stack-device-get"></a>Get del dispositivo stack host 

#### <a name="ux_host_stack_device_get"></a>ux_host_stack_device_get

**Icona** ![ Icona Ottieni dispositivo stack host](./media/user-guide/usbx-events/image196.png)

**Descrizione**

Questo evento rappresenta un evento Get dispositivo stack host USBX.

**Campi di informazioni**

- Info Campo 1: Indice del dispositivo.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-device-remove"></a>Rimozione del dispositivo stack host 

#### <a name="ux_host_stack_device_remove"></a>ux_host_stack_device_remove

**Icona** ![ Icona di rimozione del dispositivo stack host](./media/user-guide/usbx-events/image197.png)

**Descrizione**

Questo evento rappresenta un evento di rimozione del dispositivo stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Hcd.
- Campo informazioni 2: Padre.
- Campo informazioni 3: Indice delle porte.
- Campo informazioni 4: Dispositivo.

### <a name="host-stack-device-resource-free"></a>Risorse del dispositivo stack host gratuite 

#### <a name="ux_host_stack_device_resource_free"></a>ux_host_stack_device_resource_free

**Icona** ![ Icona della risorsa gratuita del dispositivo stack host](./media/user-guide/usbx-events/image198.png)

**Descrizione**

Questo evento rappresenta un evento gratuito della risorsa del dispositivo stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-endpoint-instance-create"></a>Creazione dell'istanza dell'endpoint dello stack host 

#### <a name="ux_host_stack_endpoint_instance_create"></a>ux_host_stack_endpoint_instance_create

**Icona** ![ Icona di creazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image199.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza dell'endpoint host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-endpoint-instance-delete"></a>Eliminazione dell'istanza dell'endpoint dello stack host 

#### <a name="ux_host_stack_endpoint_instance_delete"></a>ux_host_stack_endpoint_instance_delete

**Icona** ![ Icona Host Stack Endpoint Instance Delete (Elimina istanza endpoint stack host)](./media/user-guide/usbx-events/image200.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'istanza dell'endpoint dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-endpoint-reset"></a>Reimpostazione dell'endpoint dello stack host 

#### <a name="ux_host_stack_endpoint_reset"></a>ux_host_stack_endpoint_reset

**Icona** ![ Icona reimpostazione endpoint stack host](./media/user-guide/usbx-events/image201.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione dell'endpoint dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-endpoint-transfer-abort"></a>Interruzione trasferimento endpoint stack host 

#### <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

**Icona** ![ Icona di interruzione del trasferimento dell'endpoint dello stack host](./media/user-guide/usbx-events/image202.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione trasferimento endpoint stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Endpoint.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-host-controller-register"></a>Registro del controller host dello stack host host 

#### <a name="ux_host_stack_hcd_register"></a>ux_host_stack_hcd_register

**Icona** ![ Icona di registrazione del controller host dello stack host host](./media/user-guide/usbx-events/image203.png)

**Descrizione**

Questo evento rappresenta un registro controller host dello stack host USBX.

**Campi di informazioni**

- Info Field 1: Hcd Name.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-initialize"></a>Inizializzazione dello stack host 

#### <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

**Icona** ![ Icona di inizializzazione dello stack di host](./media/user-guide/usbx-events/image204.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-interface-endpoint-get"></a>Host Stack Interface Endpoint Get 

#### <a name="interface_-tcp-retry-entry"></a>Interface_ di ripetizione dei tentativi TCP

**Icona** ![ Icona Get dell'endpoint dell'interfaccia dello stack host](./media/user-guide/usbx-events/image205.png)

**Descrizione**

Questo evento rappresenta un evento di ripetizione dei tentativi TCP NetX interno.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Indice dell'endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-interface-instance-create"></a>Creazione dell'istanza dell'interfaccia dello stack host 

#### <a name="ux_host_stack_interface_instance_create"></a>ux_host_stack_interface_instance_create

**Icona** ![ Icona di creazione dell'istanza dell'interfaccia dello stack di host](./media/user-guide/usbx-events/image206.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza dell'interfaccia host USBX.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-interface-instance-delete"></a>Eliminazione dell'istanza dell'interfaccia dello stack host 

#### <a name="ux_host_stack_interface_instance_delete"></a>ux_host_stack_interface_instance_delete

**Icona** ![ Icona Host Stack Interface Instance Delete (Elimina istanza dell'interfaccia dello stack host)](./media/user-guide/usbx-events/image207.png)

**Descrizione**

Questo evento rappresenta un evento delete dell'istanza dell'interfaccia host USBX.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-interface-set"></a>Host Stack Interface Set 

#### <a name="ux_host_stack_interface_set"></a>ux_host_stack_interface_set

**Icona** ![ Icona del set di interfacce dello stack di host](./media/user-guide/usbx-events/image208.png)

**Descrizione**

Questo evento rappresenta un evento del set di interfacce host USBX.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-interface-setting-select"></a>Selezione dell'impostazione dell'interfaccia dello stack host 

#### <a name="ux_host_stack_interface_setting_select"></a>ux_host_stack_interface_setting_select

**Icona** ![ Icona Di selezione dell'impostazione dell'interfaccia dello stack di host](./media/user-guide/usbx-events/image209.png)

**Descrizione**

Questo evento rappresenta un evento select dell'impostazione dell'interfaccia host USBX.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-new-configuration-create"></a>Creazione nuova configurazione dello stack host 

#### <a name="ux_host_stack_new_configuration_create"></a>ux_host_stack_new_configuration_create

**Icona** ![ Icona di creazione della nuova configurazione dello stack di host](./media/user-guide/usbx-events/image210.png)

**Descrizione**
 
Questo evento rappresenta un evento di creazione nuova configurazione dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo informazioni 2: Configurazione.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-new-device-create"></a>Creazione di un nuovo dispositivo nello stack di host 

#### <a name="ux_host_stack_new_device_create"></a>ux_host_stack_new_device_create

**Icona** ![ Icona di creazione del nuovo dispositivo dello stack di host](./media/user-guide/usbx-events/image211.png)

**Descrizione**
 
 Questo evento rappresenta un evento di creazione di un nuovo dispositivo stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Hcd.
- Campo informazioni 2: Proprietario del dispositivo.
- Campo informazioni 3: Indice delle porte.
- Campo informazioni 4: Dispositivo.

### <a name="host-stack-new-endpoint-create"></a>Creazione di un nuovo endpoint nello stack host 

#### <a name="ux_host_stack_new_endpoint_create"></a>ux_host_stack_new_endpoint_create

**Icona** ![ Icona di creazione nuovo endpoint dello stack di host](./media/user-guide/usbx-events/image212.png)

**Descrizione**
 
Questo evento rappresenta un evento di creazione nuovo endpoint dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Interfaccia.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-root-hub-change-process"></a>Processo di modifica dell'hub radice dello stack host 

#### <a name="ux_host_stack_rh_change_process"></a>ux_host_stack_rh_change_process

**Icona** ![ Icona del processo di modifica dell'hub radice dello stack host](./media/user-guide/usbx-events/image213.png)

**Descrizione**
 
Questo evento rappresenta un processo di modifica dell'hub radice dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Indice delle porte.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-root-hub-device-extraction"></a>Estrazione del dispositivo dell'hub radice dello stack host 

#### <a name="ux_host_stack_rh_device_extraction"></a>ux_host_stack_rh_device_extraction

**Icona** ![ Icona di estrazione del dispositivo dell'hub radice dello stack host](./media/user-guide/usbx-events/image214.png)

**Descrizione**

Questo evento rappresenta un evento di estrazione dispositivo dell'hub radice dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Hcd.
- Campo informazioni 2: Indice delle porte.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-root-hub-device-insertion"></a>Inserimento dispositivo hub radice stack host 

#### <a name="ux_host_stack_rh_device_insertion"></a>ux_host_stack_rh_device_insertion

**Icona** ![ Icona di inserimento del dispositivo dell'hub radice dello stack host](./media/user-guide/usbx-events/image215.png)

**Descrizione**

Questo evento rappresenta l'inserimento di un dispositivo hub radice dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Hcd.
- Campo informazioni 2: Indice delle porte.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="host-stack-transfer-request"></a>Richiesta di trasferimento dello stack host 

#### <a name="ux_host_stack_transfer_request"></a>ux_host_stack_transfer_request

**Icona** ![ Icona della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image216.png)

**Descrizione**

Questo evento rappresenta una richiesta di trasferimento stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Richiesta di trasferimento.
- Campo informazioni 4: Non usato.

### <a name="host-stack-transfer-request-abort"></a>Interruzione della richiesta di trasferimento dello stack host 

#### <a name="internal-io-driver-get-status"></a>Ottenere lo stato del driver di I/O interno

**Icona** ![ Icona Host Stack Transfer Request Abort (Interruzione richiesta di trasferimento stack host)](./media/user-guide/usbx-events/image217.png)

**Descrizione**

Questo evento rappresenta un'interruzione della richiesta di trasferimento dello stack host USBX.

**Campi di informazioni**

- Campo informazioni 1: Dispositivo.
- Campo informazioni 2: Endpoint.
- Campo informazioni 3: Richiesta di trasferimento.
- Campo informazioni 4: Non usato.

### <a name="usbx-error"></a>Errore USBX 

#### <a name="ux_error"></a>ux_error

**Icona** ![ Icona di errore di U S B X](./media/user-guide/usbx-events/image218.png)

**Descrizione**

Questo evento rappresenta un evento di errore USBX.

**Campi di informazioni**

- Campo informazioni 1: errore USBX.
- Campo informazioni 2: Nome errore.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.