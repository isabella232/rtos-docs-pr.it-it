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
# <a name="chapter-9---azure-rtos-usbx-trace-events"></a>Capitolo 9: eventi di traccia di Azure RTO USBX

Questo capitolo contiene una descrizione degli eventi USBX di Azure RTO visualizzati da TraceX. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

Di seguito è riportato un elenco di eventi USBX visualizzati da TraceX.

| Icona                             | Significato                               |
| -------------------------------- | ------------------------------------- |
| ![Icona di attivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image1.png)    | **Classe dispositivo CDC Activate** *(ux_device_class_cdc_activate)* |
| ![Icona di disattivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image2.png)    | **Classe dispositivo CDC Deactivate** *(ux_device_class_cdc_deactivate)* |
| ![Icona di lettura della classe del dispositivo c D](./media/user-guide/usbx-events/image3.png)    | **Classe dispositivo CDC Read** *(ux_device_class_cdc_read)* |
| ![Icona di scrittura della classe del dispositivo c D C](./media/user-guide/usbx-events/image4.png)    | **Classe dispositivo-scrittura CDC** *(ux_device_class_cdc_write)* |
| ![Icona di attivazione della classe Device DPUMP](./media/user-guide/usbx-events/image5.png)    | **Classe dispositivo DPUMP Activate** *(ux_device_class_dpump_activate)* |
| ![Icona di disattivazione della classe Device DPUMP](./media/user-guide/usbx-events/image6.png)    | **Classe dispositivo DPUMP disattivare** *(ux_device_class_dpump_deactivate)* |
| ![Icona di lettura della classe del dispositivo DPUMP](./media/user-guide/usbx-events/image7.png)    | **Classe dispositivo DPUMP Read** *(ux_device_class_dpump_read)* |
| ![Icona di scrittura della classe Device DPUMP](./media/user-guide/usbx-events/image8.png)    | **Classe dispositivo DPUMP Write** *(ux_device_class_dpump_write)* |
| ![Icona di attivazione HID della classe dispositivo](./media/user-guide/usbx-events/image9.png)    | **Attivazione HID della classe dispositivo** *(ux_device_class_hid_activate)* |
| ![Icona di disattivazione HID della classe dispositivo](./media/user-guide/usbx-events/image10.png)    | **Disattivazione HID della classe dispositivo** *(ux_device_class_hid_deactivate)* |
| ![Icona di invio del descrittore HID della classe dispositivo](./media/user-guide/usbx-events/image11.png)    | **Classe dispositivo-invia descrittore HID** *(ux_device_class_hid_descriptor_send)* |
| ![Icona di Get dell'evento HID della classe dispositivo](./media/user-guide/usbx-events/image12.png)    | **Classe dispositivo HID Event Get** *(ux_device_class_hid_event_get)* |
| ![Icona del set di eventi HID della classe dispositivo](./media/user-guide/usbx-events/image13.png)    | **Set di eventi HID della classe Device** *(ux_device_class_hid_event_set)* |
| ![Icona di Get del report HID della classe dispositivo](./media/user-guide/usbx-events/image14.png)    | **Classe dispositivo HID report Get** *(ux_device_class_hid_report_get)* |
| ![Icona del set di report HID della classe dispositivo](./media/user-guide/usbx-events/image15.png)    | **Set di report HID della classe dispositivo** *(ux_device_class_hid_report_set)* |
| ![Icona di attivazione Pima della classe dispositivo](./media/user-guide/usbx-events/image16.png)    | **Classe dispositivo di attivazione Pima** *(ux_device_class_pima_activate)* |
| ![Icona di disattivazione della classe di dispositivo Pima](./media/user-guide/usbx-events/image17.png)    | **Classe dispositivo Pima Deactivate** *(ux_device_class_pima_deactivate)* |
| ![Icona di invio informazioni sul dispositivo Pima della classe dispositivo](./media/user-guide/usbx-events/image18.png)    | **Classe dispositivo Pima invio informazioni sul dispositivo** *(ux_device_class_pima_device_info_send)* |
| ![Icona di Get evento di classe dispositivo Pima](./media/user-guide/usbx-events/image19.png)    | **Classe dispositivo Pima evento Get** *(ux_device_class_pima_event_get)* |
| ![Icona del set di eventi Pima della classe Device](./media/user-guide/usbx-events/image20.png)    | **Set di eventi Pima della classe Device** *(ux_device_class_pima_event_set)* |
| ![Icona di aggiunta oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image21.png)    | **Classe dispositivo-Aggiunta oggetto Pima** *(ux_device_class_pima_object_add)* |
| ![Icona di visualizzazione dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image22.png)    | **Classe dispositivo dati oggetto Pima Get** *(ux_device_class_pima_object_data_get)* |
| ![Icona di invio dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image23.png)    | **Classe dispositivo-invio dati oggetti Pima** *(ux_device_class_pima_object_data_send)* |
| ![Icona di eliminazione oggetti Pima classe dispositivo](./media/user-guide/usbx-events/image24.png)    | **Classe dispositivo eliminazione oggetti Pima** *(ux_device_class_pima_object_delete)* |
| ![Icona di invio handle oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image25.png)    | **Classe dispositivo gestisce l'invio** *(ux_device_class_pima_object_handles_send)* |
| ![Icona di visualizzazione informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image26.png)    | **Classe dispositivo informazioni su oggetti Pima Get** *(ux_device_class_pima_object_info_get)* |
| ![Icona di invio informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image27.png)    | **Classe dispositivo-invio informazioni oggetto Pima** *(ux_device_class_pima_object_info_send)* |
| ![Icona di invio numero di oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image28.png)    | **Classe dispositivo numero oggetti Pima invio** *(ux_device_class_pima_objects_number_send)* |
| ![Icona di visualizzazione dati oggetto parziale classe dispositivo Pima](./media/user-guide/usbx-events/image29.png)    | **Classe dispositivo i dati dell'oggetto parziale Pima Get** *(ux_device_class_pima_partial_object_data_get)* |
| ![Icona di invio risposta Pima della classe dispositivo](./media/user-guide/usbx-events/image30.png)    | **Classe dispositivo-invio risposta Pima** *(ux_device_class_pima_response_send)*|
| ![Icona di archiviazione della classe dispositivo Pima archiviazione I D](./media/user-guide/usbx-events/image31.png)    | **Classe dispositivo ID archiviazione Pima** *(ux_device_class_pima_storage_id_send)* |
| ![Icona di invio info di archiviazione Pima della classe dispositivo](./media/user-guide/usbx-events/image32.png)    | **Classe dispositivo informazioni di archiviazione Pima invio** *(ux_device_class_pima_storage_info_send)* |
| ![Icona di attivazione della classe dispositivo R N D I S](./media/user-guide/usbx-events/image33.png)    | **Classe dispositivo RNDIS Activate** *(ux_device_class_rndis_activate)* |
| ![Icona di disattivazione della classe dispositivo R N D](./media/user-guide/usbx-events/image34.png)    | **Classe dispositivo RNDIS disattivare** *(ux_device_class_rndis_deactivate)* |
| ![Classe dispositivo R N D I messaggio keep Aliveicon](./media/user-guide/usbx-events/image35.png)    | **Classe dispositivo RNDIS messaggio keep-alive** *(ux_device_class_rndis_msg_keep_alive)* |
| ![Icona della query del messaggio di classe del dispositivo R N D I](./media/user-guide/usbx-events/image36.png)    | **Query del messaggio RNDIS della classe dispositivo** *(ux_device_class_rndis_msg_query)* |
| ![Icona di reimpostazione del messaggio di classe dispositivo R N D I](./media/user-guide/usbx-events/image37.png)    | **Classe dispositivo reimpostazione del messaggio RNDIS** *(ux_device_class_rndis_msg_reset)* |
| ![Icona del set di messaggi di classe dispositivo R N D I S](./media/user-guide/usbx-events/image38.png)    | **Set di messaggi RNDIS della classe dispositivo** *(ux_device_class_rndis_msg_set)* |
| ![Icona di ricezione pacchetti di classe dispositivo R N D I](./media/user-guide/usbx-events/image39.png)    | **Classe dispositivo RNDIS ricezione pacchetti** *(ux_device_class_rndis_packet_receive)* |
| ![Icona di trasmissione pacchetti della classe dispositivo R N D I](./media/user-guide/usbx-events/image40.png)    | **Classe dispositivo RNDIS trasmissione pacchetti** *(ux_device_class_rndis_packet_transmit)* |
| ![Icona di attivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image41.png)    | **Attivazione dell'archiviazione della classe dispositivo** *(ux_device_class_storage_activate)* |
| ![Icona di disattivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image42.png)    | **Disattivazione archiviazione classe dispositivo** *(ux_device_class_storage_deactivate)* |
| ![Icona del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image43.png)    | **Formato di archiviazione della classe dispositivo** *(ux_device_class_storage_format)* |
| ![Icona di richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image44.png)    | **Richiesta di archiviazione della classe dispositivo** *(ux_device_class_storage_inquiry)* |
| ![Icona di selezione modalità di archiviazione classe dispositivo](./media/user-guide/usbx-events/image45.png)    | **Selezione della modalità di archiviazione della classe dispositivo** *(ux_device_class_storage_mode_select)* |
| ![Icona di rilevamento della modalità di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image46.png)    | **Rilevamento della modalità di archiviazione della classe dispositivo** *(ux_device_class_storage_mode_sense)* |
| ![Archiviazione della classe dispositivo Impedisci l'uso dell'icona Consenti rimozione supporti](./media/user-guide/usbx-events/image47.png)    | L' **archiviazione delle classi di dispositivi impedisce la rimozione dei supporti** *(ux_device_class_storage_prevent_allow_media_removal)* |
| ![Icona di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image48.png)    | **Lettura archiviazione classe dispositivo** *(ux_device_class_storage_read)* |
| ![Icona capacità di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image49.png)    | **Capacità di lettura di archiviazione della classe dispositivo** *(ux_device_class_storage_read_capacity)* |
| ![Icona della capacità di lettura del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image50.png)    | **Capacità di lettura formato di archiviazione della classe dispositivo** *(ux_device_class_storage_read_format_capacity)* |
| ![Icona di lettura Sommario archiviazione classe dispositivo](./media/user-guide/usbx-events/image51.png)    | **Sommario di lettura della classe dispositivo archiviazione** *(ux_device_class_storage_read_toc)* |
| ![Icona del senso della richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image52.png)    | **Rilevamento delle richieste di archiviazione della classe dispositivo** *(ux_device_class_storage_request_sense)* |
| ![Icona di avvio dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image53.png)    | **Inizio arresto archiviazione classe dispositivo** *(ux_device_class_storage_start_stop)* |
| ![Icona dei test di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image54.png)    | **Pronto per il test di archiviazione della classe dispositivo** *(ux_device_class_storage_test_ready)* |
| ![Icona di verifica archiviazione classe dispositivo](./media/user-guide/usbx-events/image55.png)    | **Verifica archiviazione classe dispositivo** *(ux_device_class_storage_verify)* |
| ![Icona di scrittura archiviazione classe dispositivo](./media/user-guide/usbx-events/image56.png)    | **Scrittura archiviazione classe dispositivo** *(ux_device_class_storage_write)* |
| ![Icona del Get dell'impostazione alternativa dello stack del dispositivo](./media/user-guide/usbx-events/image57.png)    | **Impostazione alternativa stack del dispositivo Get** *(ux_device_stack_alternate_setting_get)* |
| ![Icona del set di impostazioni alternativo dello stack del dispositivo](./media/user-guide/usbx-events/image58.png)    | **Set di impostazioni alternativo dello stack del dispositivo** *(ux_device_stack_alternate_setting_set)* |
| ![Icona di registro classe stack del dispositivo](./media/user-guide/usbx-events/image59.png)    | **Registro classe stack del dispositivo** *(ux_device_stack_class_register)* |
| ![Icona della funzionalità cancellazione dello stack del dispositivo](./media/user-guide/usbx-events/image60.png)    | **Funzionalità di cancellazione dello stack del dispositivo** *(ux_device_stack_clear_feature)* |
| ![Icona di Get della configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image61.png)    | **Configurazione dello stack del dispositivo Get** *(ux_device_stack_configuration_get)* |
| ![Icona del set di configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image62.png)    | **Set di configurazione dello stack del dispositivo** *(ux_device_stack_configuration_set)* |
| ![Icona di connessione dello stack del dispositivo](./media/user-guide/usbx-events/image63.png)    | **Connessione stack del dispositivo** *(ux_device_stack_connect)* |
| ![Icona di invio del descrittore dello stack del dispositivo](./media/user-guide/usbx-events/image64.png)    | **Invio del descrittore dello stack del dispositivo** *(ux_device_stack_descriptor_send)* |
| ![Icona di disconnessione dello stack del dispositivo](./media/user-guide/usbx-events/image65.png)    | **Disconnessione dello stack del dispositivo** *(ux_device_stack_disconnect)* |
| ![Icona dello stallo dello stack dell'endpoint del dispositivo](./media/user-guide/usbx-events/image66.png)    | Blocco **endpoint dello stack del dispositivo** *(ux_device_stack_endpoint_stall)* |
| ![Icona dello stato di Get dello stack del dispositivo](./media/user-guide/usbx-events/image67.png)    | **Stato di Get dello stack del dispositivo** *(ux_device_stack_get_status)* |
| ![Icona di riattivazione host stack del dispositivo](./media/user-guide/usbx-events/image68.png)    | Riattivazione **host stack del dispositivo** *(ux_device_stack_host_wakeup)* |
| ![Icona di inizializzazione dello stack del dispositivo](./media/user-guide/usbx-events/image69.png)    | **Inizializzazione dello stack del dispositivo** *(ux_device_stack_initialize)* |
| ![Icona di eliminazione dell'interfaccia dello stack del dispositivo](./media/user-guide/usbx-events/image70.png)    | **Eliminazione interfaccia dello stack di dispositivi** *(ux_device_stack_interface_delete)* |
| ![Icona Ottieni interfaccia stack di dispositivi](./media/user-guide/usbx-events/image71.png)    | **Interfaccia stack del dispositivo Get** *(ux_device_stack_interface_get)* |
| ![Icona del set di interfacce dello stack di dispositivi](./media/user-guide/usbx-events/image72.png)    | **Set di interfacce dello stack di dispositivi** *(ux_device_stack_interface_set)* |
| ![Icona della funzionalità set di stack del dispositivo](./media/user-guide/usbx-events/image73.png)    | **Funzionalità set di stack del dispositivo** *(ux_device_stack_set_feature)* |
| ![Icona di interruzione del trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image74.png)    | **Interruzione trasferimento stack del dispositivo** *(ux_device_stack_transfer_abort)* |
| ![* Icona di interruzione della richiesta di trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image75.png)    | **Interruzione della richiesta di trasferimento dello stack del dispositivo** *(ux_device_stack_transfer_all_request_abort)* |
| ![Icona della richiesta di trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image76.png)    | **Richiesta di trasferimento dello stack del dispositivo** *(ux_device_stack_transfer_request)* |
| ![Icona di attivazione della classe host ASIX](./media/user-guide/usbx-events/image77.png)    | **Classe host ASIX Activate** *(ux_host_class_asix_activate)* |
| ![Icona ASIX della classe host disattiva](./media/user-guide/usbx-events/image78.png)    | **Classe host ASIX disattivare** *(ux_host_class_asix_deactivate)* |
| ![Icona della notifica di interrupt della classe host ASIX](./media/user-guide/usbx-events/image79.png)    | **Notifica di interrupt della classe host ASIX** *(ux_host_class_asix_interrupt_notification)* |
| ![Icona di lettura della classe host ASIX](./media/user-guide/usbx-events/image80.png)    | **Classe host ASIX Read** *(ux_host_class_asix_read)* |
| ![Icona di scrittura della classe host ASIX](./media/user-guide/usbx-events/image81.png)    | **Classe host ASIX Write** *(ux_host_class_asix_write)* |
| ![Icona di attivazione dell'audio della classe host](./media/user-guide/usbx-events/image82.png)    | **Attivazione audio classe host** *(ux_host_class_audio_activate)* |
| ![Icona Get del valore del controllo audio della classe host](./media/user-guide/usbx-events/image83.png)    | **Valore di controllo audio della classe host Get** *(ux_host_class_audio_control_value_get)* |
| ![Icona del set di valori del controllo audio della classe host](./media/user-guide/usbx-events/image84.png)    | **Impostazione del valore del controllo audio della classe host** *(ux_host_class_audio_control_value_set)* |
| ![Icona di disattivazione audio della classe host](./media/user-guide/usbx-events/image85.png)    | **Disattivazione audio della classe host** *(ux_host_class_audio_deactivate)* |
| ![Icona di lettura audio della classe host](./media/user-guide/usbx-events/image86.png)    | **Lettura audio classe host** *(ux_host_class_audio_read)* |
| ![Icona di Get del campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image87.png)    | **Ottenere il campionamento del flusso audio della classe host** *(ux_host_class_audio_streaming_sampling_get)* |
| ![Icona del set di campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image88.png)    | **Set di campionamento del flusso audio della classe host** *(ux_host_class_audio_streaming_sampling_set)* |
| ![Icona di scrittura audio della classe host](./media/user-guide/usbx-events/image89.png)    | **Scrittura audio della classe host** *(ux_host_class_audio_write)* |
| ![Icona di attivazione della classe host C D C A C M](./media/user-guide/usbx-events/image90.png)    | **Classe host CDC ACM Activate** *(ux_host_class_cdc_acm_activate)* |
| ![Classe host C D C A C M icona di disattivazione](./media/user-guide/usbx-events/image91.png)    | **Classe host CDC ACM Deactivate** *(ux_host_class_cdc_acm_deactivate)* |
| ![Classe host C D C A C M I O C T L nell'icona pipe](./media/user-guide/usbx-events/image92.png)    | **Classe host CDC per l'interruzione IOCTL ACM in pipe** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)* |
| ![Classe host C D C A C M I O C T L pulsante Interrompi barra verticale](./media/user-guide/usbx-events/image93.png)    | **Classe host CDC ACM, Interrompi pipe out pipe** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)* |
| ![Classe host C D C A C M I O C T L icona di stato del dispositivo Get](./media/user-guide/usbx-events/image94.png)    | **Classe host CDC ACM IOCTL per ottenere lo stato del dispositivo** *(ux_host_class_cdc_acm_ioctl_get_device_status)* |
| ![Classe host C D C A C M I O C T L ottenere l'icona di codifica della riga](./media/user-guide/usbx-events/image95.png)    | **Classe host CDC ACM IOCTL Get line Coding** *(ux_host_class_cdc_acm_ioctl_get_line_coding)* |
| ![Classe host C D C A C M I O C T L icona di callback di notifica](./media/user-guide/usbx-events/image96.png)    | **Callback delle notifiche IOCTL di classe host CDC ACM** *(ux_host_class_cdc_acm_ioctl_notification_callback)* |
| ![Classe host C D C A C M I O C T L invio icona di interruzioni](./media/user-guide/usbx-events/image97.png)    | **Classe host CDC ACM di invio** *(ux_host_class_cdc_acm_ioctl_send_break)* |
| ![Classe host C D C A C M I O C T L impostare l'icona di codifica della riga](./media/user-guide/usbx-events/image98.png)    | Codifica a linee del set di righe *(ux_host_class_cdc_acm_ioctl_set_line_coding)* della **classe host CDC ACM** . |
| ![Classe host C D C A C M I O C T L impostare lo stato della riga icona](./media/user-guide/usbx-events/image99.png)    | **Stato della riga set IOCTL di classe host CDC ACM** *(ux_host_class_cdc_acm_ioctl_set_line_state)* |
| ![Icona di lettura c M di classe host c D](./media/user-guide/usbx-events/image100.png)    | **Classe host CDC ACM Read** *(ux_host_class_cdc_acm_read)* |
| ![Icona di avvio della ricezione c M della classe host C D C](./media/user-guide/usbx-events/image101.png)    | **Classe host CDC ACM reception Start** *(ux_host_class_cdc_acm_reception_start)* |
| ![Icona di arresto della ricezione c M per la classe host C D C](./media/user-guide/usbx-events/image102.png)    | **Arresto della ricezione della classe host CDC ACM** *(ux_host_class_cdc_acm_reception_stop)* |
| ![Icona di scrittura della classe host C D C A C M](./media/user-guide/usbx-events/image103.png)    | **Classe host CDC ACM Write** *(ux_host_class_cdc_acm_write)* |
| ![Icona di attivazione della classe host DPUMP](./media/user-guide/usbx-events/image104.png)    | **Classe host DPUMP Activate** *(ux_host_class_dpump_activate)* |
| ![Icona DPUMP della classe host disattiva](./media/user-guide/usbx-events/image105.png)    | **Classe host DPUMP disattivare** *(ux_host_class_dpump_deactivate)* |
| ![Icona di lettura della classe host DPUMP](./media/user-guide/usbx-events/image106.png)    | **Classe host DPUMP Read** *(ux_host_class_dpump_read)* |
| ![Icona di scrittura della classe host DPUMP](./media/user-guide/usbx-events/image107.png)    | **Classe host DPUMP Write** *(ux_host_class_dpump_write)* |
| ![Icona di attivazione HID della classe host](./media/user-guide/usbx-events/image108.png)    | **Attivazione HID della classe host** *(ux_host_class_hid_activate)* |
| ![Icona di registro del client HID della classe host](./media/user-guide/usbx-events/image109.png)    | **Registro del client HID della classe host** *(ux_host_class_hid_client_register)* |
| ![Icona di disattivazione HID della classe host](./media/user-guide/usbx-events/image110.png)    | **Disattivazione HID della classe host** *(ux_host_class_hid_deactivate)* |
| ![Icona della classe host HID Idle Get](./media/user-guide/usbx-events/image111.png)    | **Classe host HID Idle Get** *(ux_host_class_hid_idle_get)* |
| ![Icona del set di inattività HID della classe host](./media/user-guide/usbx-events/image112.png)    | **Set di inattività HID della classe host** *(ux_host_class_hid_idle_set)* |
| ![Icona di attivazione della tastiera HID della classe host](./media/user-guide/usbx-events/image113.png)    | **Attiva tastiera HID della classe host** *(ux_host_class_hid_keyboard_activate)* |
| ![Icona di disattivazione tastiera HID della classe host](./media/user-guide/usbx-events/image114.png)    | **Disattiva la tastiera HID della classe host** *(ux_host_class_hid_keyboard_deactivate)* |
| ![Icona di attivazione della classe host HID mouse](./media/user-guide/usbx-events/image115.png)    | **Attivazione mouse HID classe host** *(ux_host_class_hid_mouse_activate)* |
| ![Icona di disattivazione della classe host HID mouse](./media/user-guide/usbx-events/image116.png)    | Deactivate *(ux_host_class_hid_mouse_deactivate)* della **classe host HID mouse** |
| ![Icona di attivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image117.png)    | **Attivazione del controllo remoto HID della classe host** *(ux_host_class_hid_remote_control_activate)* |
| ![Icona di disattivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image118.png)    | **Disattivazione del controllo remoto HID della classe host** *(ux_host_class_hid_remote_control_deactivate)* |
| ![Icona di Get del report HID della classe host](./media/user-guide/usbx-events/image119.png)    | **Classe host (report HID) Get** *(ux_host_class_hid_report_get)* |
| ![Icona del set di report HID della classe host](./media/user-guide/usbx-events/image120.png)    | **Set di report HID della classe host** *(ux_host_class_hid_report_set)* |
| ![Icona di attivazione dell'hub classe host](./media/user-guide/usbx-events/image121.png)    | **Attivazione Hub classe host** *(ux_host_class_hub_activate)* |
| ![Icona rilevamento modifiche Hub classe host](./media/user-guide/usbx-events/image122.png)    | **Rilevamento modifiche Hub classe host** *(ux_host_class_hub_change_detect)* |
| ![* Icona di disattivazione dell'hub classe host](./media/user-guide/usbx-events/image123.png)    | **Disattivazione dell'hub della classe host** *(ux_host_class_hub_deactivate)* |
| ![Icona del processo di connessione della porta dell'hub della classe host](./media/user-guide/usbx-events/image124.png)    | **Processo di connessione modifica porta hub classe host** *(ux_host_class_hub_port_change_connection_process)* |
| ![Icona di abilitazione del processo modifica porta hub classe host](./media/user-guide/usbx-events/image125.png)    | **Processo di abilitazione della porta dell'hub della classe host** *(ux_host_class_hub_port_change_enable_process)* |
| ![Icona modifica porta hub classe host sull'icona del processo corrente](./media/user-guide/usbx-events/image126.png)    | **Modifica della porta dell'hub della classe host per il processo corrente** *(ux_host_class_hub_port_change_over_current_process)* |
| ![Icona del processo di reimpostazione della porta dell'hub della classe host](./media/user-guide/usbx-events/image127.png)    | **Processo di reimpostazione della porta dell'hub della classe host** *(ux_host_class_hub_port_change_reset_process)* |
| ![Icona di sospensione del processo di modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image128.png)    | **Processo di sospensione delle modifiche della porta dell'hub della classe host** *(ux_host_class_hub_port_change_suspend_process)* |
| ![Icona di attivazione della classe host Pima](./media/user-guide/usbx-events/image129.png)    | **Classe host Pima Activate** *(ux_host_class_prima_activate)* |
| ![Icona di disattivazione della classe host Pima](./media/user-guide/usbx-events/image130.png)    | **Classe host Pima Deactivate** *(ux_host_class_pima_deactivate)* |
| ![Icona di informazioni sul dispositivo Pima della classe host](./media/user-guide/usbx-events/image131.png)    | **Classe host informazioni sul dispositivo Pima Get** *(ux_host_class_pima_device_info_get)* |
| ![Icona di reimpostazione del dispositivo Pima della classe host](./media/user-guide/usbx-events/image132.png)    | **Reimpostazione del dispositivo Pima della classe host** *(ux_host_class_pima_device_reset)* |
| ![Icona di notifica classe host Pima](./media/user-guide/usbx-events/image133.png)    | **Notifica classe host Pima** *(ux_host_class_pima_notification)* |
| ![Icona di visualizzazione degli oggetti numero Pima della classe host](./media/user-guide/usbx-events/image134.png)    | **Classe host numero Pima oggetti Get** *(ux_host_class_pima_num_objects_get)* |
| ![Icona di chiusura oggetto classe host Pima](./media/user-guide/usbx-events/image135.png)    | **Chiusura oggetto Pima classe host** *(ux_host_class_pima_object_close)* |
| ![Icona di copia dell'oggetto classe host Pima](./media/user-guide/usbx-events/image136.png)    | **Classe host copia oggetto Pima** *(ux_host_class_pima_object_copy)* |
| ![Icona di eliminazione oggetto classe host Pima](./media/user-guide/usbx-events/image137.png)    | **Classe host Elimina oggetto Pima** *(ux_host_class_pima_object_delete)* |
| ![Icona di Get oggetto della classe host Pima](./media/user-guide/usbx-events/image138.png)    | **Classe host (oggetto Pima) Get** *(ux_host_class_pima_object_get)* |
| ![Icona di visualizzazione delle informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image139.png)    | **Classe host, informazioni sull'oggetto Pima Get** *(ux_host_class_pima_object_info_get)* |
| ![Icona di invio info oggetto Pima classe host](./media/user-guide/usbx-events/image140.png)    | **Classe host-informazioni sull'oggetto Pima Send** *(ux_host_class_pima_object_info_send)* |
| ![Icona di spostamento oggetto classe host Pima](./media/user-guide/usbx-events/image141.png)    | **Spostamento oggetto classe host Pima** *(ux_host_class_pima_object_move)* |
| ![Icona di invio oggetto Pima classe host](./media/user-guide/usbx-events/image142.png)    | **Classe host per l'invio di oggetti Pima** *(ux_host_class_pima_object_send)* |
| ![Icona di interruzione trasferimento oggetti Pima classe host](./media/user-guide/usbx-events/image143.png)    | **Interruzione del trasferimento di oggetti Pima della classe host** *(ux_host_class_object_transfer_abort)* |
| ![Icona di lettura della classe host Pima](./media/user-guide/usbx-events/image144.png)    | **Classe host Pima Read** *(ux_host_class_pima_read)* |
| ![Icona di annullamento richiesta Pima della classe host](./media/user-guide/usbx-events/image145.png)    | **Classe host Pima richiesta Cancel** *(ux_host_class_pima_request_cancel)* |
| ![Icona di chiusura della sessione Pima della classe host](./media/user-guide/usbx-events/image146.png)    | **Chiusura della sessione Pima della classe host** *(ux_host_class_pima_session_close)* |
| ![Icona di apertura della sessione Pima della classe host](./media/user-guide/usbx-events/image147.png)    | La **sessione Pima della classe host è aperta** *(ux_host_class_pima_session_open)* |
| ![Icona di Get dell'ID di archiviazione Pima della classe host](./media/user-guide/usbx-events/image148.png)    | **Classe host (ID di archiviazione Pima) Get** *(ux_host_class_pima_storage_ids_get)* |
| ![Icona di informazioni di archiviazione per la classe host Pima](./media/user-guide/usbx-events/image149.png)    | **Classe host Pima info archiviazione Get** *(ux_host_class_pima_storage_info_get)* |
| ![Icona della classe host Pima Thumb Get](./media/user-guide/usbx-events/image150.png)    | **Classe host Pima Thumb Get** *(ux_host_class_pima_thumb_get)* |
| ![Icona di scrittura della classe host Pima](./media/user-guide/usbx-events/image151.png)    | **Classe host di scrittura Pima** *(ux_host_class_pima_write)* |
| ![Icona di attivazione della stampante della classe host](./media/user-guide/usbx-events/image152.png)    | **Attivazione della stampante della classe host** *(ux_host_class_printer_activate)* |
| ![Icona di disattivazione della stampante della classe host](./media/user-guide/usbx-events/image153.png)    | **Disattivazione della stampante della classe host** *(ux_host_class_printer_deactivate)* |
| ![Icona di visualizzazione del nome della stampante della classe host](./media/user-guide/usbx-events/image154.png)    | **Nome della stampante della classe host Get** *(ux_host_class_printer_name_get)* |
| ![Icona di lettura della stampante della classe host](./media/user-guide/usbx-events/image155.png)    |  **Lettura stampante classe host** *(ux_host_class_printer_read)* |
| ![Icona di ripristino soft della stampante della classe host](./media/user-guide/usbx-events/image156.png)    | **Reimpostazione soft della stampante della classe host** *(ux_host_class_printer_soft_reset)* |
| ![Icona di Get dello stato della stampante della classe host](./media/user-guide/usbx-events/image157.png)    | **Stato della stampante della classe host Get** *(ux_host_class_printer_status_get)* |
| ![Icona di scrittura della stampante della classe host](./media/user-guide/usbx-events/image158.png)    | **Scrittura della stampante della classe host** *(ux_host_class_printer_write)* |
| ![Icona di attivazione della classe host Prolific](./media/user-guide/usbx-events/image159.png)    | **Attiva la classe host Prolific** *(ux_host_class_prolific_activate)* |
| ![Icona di disattivazione della classe host](./media/user-guide/usbx-events/image160.png)    | **Classe host Deactivate** *(ux_host_class_prolific_deactivate)* |
| ![Icona della classe host I/O per le interruzioni in pipe](./media/user-guide/usbx-events/image161.png)    | **Classe host-interruzioni IOCTL in pipe** *(ux_host_class_prolific_ioctl_abort_in_pipe)* |
| ![Icona della classe host Prolific I O C T interrompe la pipe](./media/user-guide/usbx-events/image162.png)    | **Classe host con IOCTL Abort Abort pipe** *(ux_host_class_prolific_ioctl_abort_out_pipe)* |
| ![Icona dello stato del dispositivo per la classe host Prolific I O C T](./media/user-guide/usbx-events/image163.png)    | **Classe host prolifico IOCTL ottenere lo stato del dispositivo** *(ux_host_class_prolific_ioctl_get_device_status)* |
| ![Icona della codifica della riga per la classe host Prolific I O C](./media/user-guide/usbx-events/image164.png)    | **Classe host prolifico IOCTL Get line Coding** *(ux_host_class_prolific_ioctl_get_line_coding)* |
| ![Icona di ripulitura della classe host Prolific I O C T](./media/user-guide/usbx-events/image165.png)    | **Classe host ripulitura IOCTL** *(ux_host_class_prolific_ioctl_purge)* |
| ![Icona di modifica dello stato del dispositivo di report I O C per la classe host](./media/user-guide/usbx-events/image166.png)    | **Modifica dello stato del dispositivo del report IOCTL per la classe host** *(ux_host_class_prolific_ioctl_report_device_status_change)* |
| ![Icona di invio della classe host Prolific I O C T](./media/user-guide/usbx-events/image167.png)    | **Classe host prolifico di invio di IOCTL** *(ux_host_class_prolific_ioctl_send_break)* |
| ![Icona del codice a linee set di classe host Prolific I O C T L](./media/user-guide/usbx-events/image168.png)    | **Codifica della riga del set IOCTL della classe host** *(ux_host_class_prolific_ioctl_set_line_coding)* |
| ![Icona dello stato della linea di impostazione della classe host Prolific I O C T](./media/user-guide/usbx-events/image169.png)    | **Stato della riga set IOCTL prolifico della classe host** *(ux_host_class_prolific_ioctl_set_line_state)* |
| ![Icona lettura prolifica classe host](./media/user-guide/usbx-events/image170.png)    | **Lettura prolifica della classe host** *(ux_host_class_prolific_read)* |
| ![Icona di inizio della ricezione prolifico della classe host](./media/user-guide/usbx-events/image171.png)    | **Avvio della ricezione prolifico della classe host** *(ux_host_class_prolific_reception_start)* |
| ![Icona di arresto della ricezione della classe host Prolific](./media/user-guide/usbx-events/image172.png)    | **Arresto della ricezione prolifico della classe host** *(ux_host_class_prolific_reception_stop)* |
| ![Icona di scrittura della classe host Prolific](./media/user-guide/usbx-events/image173.png)    | **Classe host-scrittura prolifica** *(ux_host_class_prolific_write)* |
| ![Icona di attivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image174.png)    | **Attivazione dell'archiviazione della classe host** *(ux_host_class_storage_activate)* |
| ![Icona di disattivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image175.png)    | **Disattivazione dell'archiviazione della classe host** (*ux_host_class_storage_deactivate)* |
| ![Icona Ottieni capacità supporto di archiviazione classe host](./media/user-guide/usbx-events/image176.png)    | **Capacità del supporto di archiviazione della classe host Get** *(ux_host_class_storage_media_capacity_get)* |
| ![Icona per la capacità del formato del supporto di archiviazione della classe host](./media/user-guide/usbx-events/image177.png)    | **Classe host archiviazione della capacità formato supporto Get** *(ux_host_class_storage_media_format_capacity_get)* |
| ![Icona di montaggio dei supporti di archiviazione della classe host](./media/user-guide/usbx-events/image178.png)    | **Montaggio dei supporti di archiviazione della classe host** (ux_host_class_storage_media_mount) * |
| ![Icona Apri supporto di archiviazione classe host](./media/user-guide/usbx-events/image179.png)    | **Supporto di archiviazione della classe host aperto** *(ux_host_class_storage_media_open)* |
| ![Icona lettura supporti di archiviazione classe host](./media/user-guide/usbx-events/image180.png)    | **Lettura supporto di archiviazione classe host** *(ux_host_class_storage_media_read)* |
| ![Icona Scrivi supporto di archiviazione classe host](./media/user-guide/usbx-events/image181.png)    | **Scrittura dei supporti di archiviazione della classe host** *(ux_host_class_storage_media_write)* |
| ![Icona del rilevamento della richiesta di archiviazione della classe host](./media/user-guide/usbx-events/image182.png)    | **Rilevamento delle richieste di archiviazione della classe host** *(ux_host_class_storage_request_sense)* |
| ![Icona di avvio dell'archiviazione della classe host](./media/user-guide/usbx-events/image183.png)    | **Inizio arresto archiviazione classe host** *(ux_host_class_storage_start_stop)* |
| ![Icona del test pronto per l'unità di archiviazione della classe host](./media/user-guide/usbx-events/image184.png)    | **Test pronto per l'unità di archiviazione della classe host** *(ux_host_class_storage_activate)* |
| ![Icona di creazione dell'istanza della classe Stack host](./media/user-guide/usbx-events/image185.png)    | **Creazione istanza Classe stack host** *(ux_host_stack_class_instance_create)* |
| ![Icona di eliminazione istanza Classe stack host](./media/user-guide/usbx-events/image186.png)    | **Eliminazione istanza Classe stack host** *(ux_host_stack_class_instance_destroy)* |
| ![Icona di eliminazione della configurazione dello stack host](./media/user-guide/usbx-events/image187.png)    | **Eliminazione della configurazione dello stack host** *(ux_host_stack_configuration_delete)* |
| ![Icona di enumerazione della configurazione dello stack host](./media/user-guide/usbx-events/image188.png)    | **Enumerazione della configurazione dello stack host** *(ux_host_stack_configuration_enumerate)* |
| ![Icona di creazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image189.png)    | **Creazione dell'istanza di configurazione dello stack host** *(ux_host_stack_configuration_instance_create)* |
| ![Icona di eliminazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image190.png)    | **Eliminazione dell'istanza di configurazione dello stack host** *(ux_host_stack_configuration_instance_delete)* |
| ![Icona del set di configurazione dello stack host](./media/user-guide/usbx-events/image191.png)    | **Set di configurazione dello stack host** *(ux_host_stack_configuration_set)* |
| ![Icona del set di indirizzi del dispositivo dello stack host](./media/user-guide/usbx-events/image192.png)    | **Set di indirizzi dispositivo stack host** *(ux_host_stack_device_set)* |
| ![Icona get configurazione dispositivo stack host](./media/user-guide/usbx-events/image193.png)    | **Configurazione del dispositivo dello stack host Get** *(ux_host_stack_device_configuration_get)* |
| ![Icona di selezione configurazione dispositivo stack host](./media/user-guide/usbx-events/image194.png)    | **Selezione configurazione dispositivo stack host** *(ux_host_stack_device_configuration_select)* |
| ![Icona di lettura del descrittore del dispositivo dello stack host](./media/user-guide/usbx-events/image195.png)    | **Lettura descrittore dispositivo stack host** *(ux_host_stack_device_descriptor_read)* |
| ![Icona Ottieni dispositivo stack host](./media/user-guide/usbx-events/image196.png)    | Get (ux_host_stack_device_get) del **dispositivo dello stack host** |
| ![Icona Rimuovi dispositivo stack host](./media/user-guide/usbx-events/image197.png)    | **Rimozione dispositivo stack host** (ux_host_stack_device_get) |
| ![Icona della risorsa del dispositivo dello stack host](./media/user-guide/usbx-events/image198.png)    | **Risorsa dispositivo stack host disponibile** (ux_host_stack_device_resource_free) |
| ![Icona di creazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image199.png)    | **Creazione dell'istanza dell'endpoint dello stack host** (ux_host_stack_endpoint_instance_create) |
| ![Icona di eliminazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image200.png)    | **Eliminazione istanza endpoint dello stack host** (ux_host_stack_endpoint_instance_delete) |
| ![Icona di reimpostazione dell'endpoint dello stack host](./media/user-guide/usbx-events/image201.png)    | **Reimpostazione dell'endpoint dello stack host** (ux_host_stack_endpoint_reset) |
| ![Icona di interruzione del trasferimento dell'endpoint dello stack host](./media/user-guide/usbx-events/image202.png)    | **Interruzione trasferimento endpoint dello stack host** (ux_host_stack_endpoint_transfer_abort) |
| ![Icona registro del controller host dello stack host](./media/user-guide/usbx-events/image203.png)    | **Registro del controller host dello stack** host *(ux_host_stack_hcd_register)* |
| ![Icona di inizializzazione dello stack host](./media/user-guide/usbx-events/image204.png)    | **Inizializzazione stack host** *(ux_host_stack_initialize)* |
| ![Icona Ottieni endpoint interfaccia stack host](./media/user-guide/usbx-events/image205.png)    | Get *(ux_host_stack_interface_endpoint_get)* dell' **endpoint dell'interfaccia dello stack host** |
| ![Icona di creazione dell'istanza dell'interfaccia dello stack host](./media/user-guide/usbx-events/image206.png)    | **Creazione istanza interfaccia stack host** *(ux_host_stack_interface_instance_create)* |
| ![Icona di eliminazione istanza interfaccia stack host](./media/user-guide/usbx-events/image207.png)    | **Eliminazione istanza interfaccia stack host** *(ux_host_stack_interface_instance_delete)* |
| ![Icona del set di interfacce dello stack host](./media/user-guide/usbx-events/image208.png)    | **Set di interfacce dello stack host** *(ux_host_stack_interface_set)* |
| ![Icona di selezione dell'impostazione dell'interfaccia dello stack host](./media/user-guide/usbx-events/image209.png)    | **Impostazione dell'interfaccia dello stack host Select** *(ux_host_stack_interface_setting_select)* |
| ![Icona di creazione nuova configurazione dello stack host](./media/user-guide/usbx-events/image210.png)    | **Creazione dello stack host nuova configurazione** *(ux_host_stack_new_configuration_create)* |
| ![Icona di creazione nuovo dispositivo dello stack host](./media/user-guide/usbx-events/image211.png)    | **Stack host nuovo dispositivo creato** *(ux_host_stack_new_device_create)* |
| ![Icona di creazione nuovo endpoint dello stack host](./media/user-guide/usbx-events/image212.png)    | **Creazione di un nuovo endpoint dello stack host** *(ux_host_stack_new_endpoint_create)* |
| ![Icona del processo di modifica dell'hub radice dello stack host](./media/user-guide/usbx-events/image213.png)    | **Processo di modifica dell'hub radice dello stack host** *(ux_host_stack_rh_change_process)* |
| ![Icona di estrazione dispositivo hub radice dello stack host](./media/user-guide/usbx-events/image214.png)    | **Estrazione dispositivo hub radice stack host** *(ux_host_stack_rh_device_extraction)* |
| ![Icona di inserimento dispositivo hub radice stack host](./media/user-guide/usbx-events/image215.png)    | **Inserimento dispositivo hub radice stack host** *(ux_host_stack_rh_device_insertion)* |
| ![Icona della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image216.png)    | **Richiesta di trasferimento dello stack host** *(ux_host_stack_transfer_request)* |
| ![Icona di interruzione della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image217.png)    | **Interruzione richiesta trasferimento stack host** *(ux_host_stack_transfer_request_abort)* |
| ![Icona di errore U S B X](./media/user-guide/usbx-events/image218.png)    | **Errore USBX** *(ux_error)* |

## <a name="event-descriptions"></a>Descrizioni di eventi

Nelle pagine seguenti vengono descritti gli eventi di traccia USBX.

### <a name="device-class-cdc-activate"></a>Classe del dispositivo CDC Activate 

#### <a name="ux_device_class_cdc_activate"></a>ux_device_class_cdc_activate

**Icona** ![ di Icona di attivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image1.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione CDC di classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-cdc-deactivate"></a>Classe dispositivo CDC Deactivate 

#### <a name="ux_device_class_cdc_deactivate"></a>ux_device_class_cdc_deactivate

**Icona** ![ di Icona di disattivazione della classe del dispositivo c D](./media/user-guide/usbx-events/image2.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX CDC Deactivate.

Campi informazioni 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-cdc-read"></a>Classe dispositivo CDC Read 

#### <a name="ux_device_class_cdc_read"></a>ux_device_class_cdc_read

**Icona** ![ di Icona di lettura della classe del dispositivo c D](./media/user-guide/usbx-events/image3.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX evento CDC Read.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-cdc-write"></a>Classe dispositivo-scrittura CDC 

#### <a name="ux_device_class_cdc_write"></a>ux_device_class_cdc_write

**Icona** ![ di Icona di scrittura della classe del dispositivo c D C](./media/user-guide/usbx-events/image4.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura CDC della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-dpump-activate"></a>Classe dispositivo DPUMP attiva 

#### <a name="ux_device_class_dpump_activate"></a>ux_device_class_dpump_activate

**Icona** ![ di Icona di attivazione della classe Device DPUMP](./media/user-guide/usbx-events/image5.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione DPUMP di classe dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-dpump-deactivate"></a>DPUMP classe dispositivo disattiva 

#### <a name="ux_device_class_dpump_deactivate"></a>ux_device_class_dpump_deactivate

**Icona** ![ di Icona di disattivazione della classe Device DPUMP](./media/user-guide/usbx-events/image6.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX DPUMP disattivare un evento.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-dpump-read"></a>Classe dispositivo DPUMP Read 

#### <a name="ux_device_class_dpump_read"></a>ux_device_class_dpump_read

**Icona** ![ di Icona di lettura della classe del dispositivo DPUMP](./media/user-guide/usbx-events/image7.png)

**Descrizione**

Questo evento rappresenta un evento di lettura DPUMP di classe dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: buffer.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-dpump-write"></a>Classe dispositivo scrittura DPUMP 

#### <a name="ux_device_class_dpump_write"></a>ux_device_class_dpump_write

**Icona** ![ di Icona di scrittura della classe Device DPUMP](./media/user-guide/usbx-events/image8.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura DPUMP della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-activate"></a>Attivazione HID Classe dispositivo 

#### <a name="ux_device_class_hid_activate"></a>ux_device_class_hid_activate

**Icona** ![ di Icona di attivazione HID della classe dispositivo](./media/user-guide/usbx-events/image9.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione HID della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-deactivate"></a>Classe dispositivo HID disattiva 

#### <a name="ux_device_class_hid_deactivate"></a>ux_device_class_hid_deactivate

**Icona** ![ di Icona di disattivazione HID della classe dispositivo](./media/user-guide/usbx-events/image10.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione HID della classe di dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-descriptor-send"></a>Trasmissione del descrittore HID della classe dispositivo 

#### <a name="ux_device_class_hid_descritpor_send"></a>ux_device_class_hid_descritpor_send

**Icona** ![ di Icona di invio del descrittore HID della classe dispositivo](./media/user-guide/usbx-events/image11.png)

**Descrizione**

Questo evento rappresenta un evento di invio del descrittore HID della classe di dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: tipo di descrittore.
- Informazioni sul campo 3: indice della richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-event-get"></a>Classe dispositivo (Get) evento HID 

#### <a name="ux_device_class_hid_event_get"></a>ux_device_class_hid_event_get

**Icona** ![ di Icona di Get dell'evento HID della classe dispositivo](./media/user-guide/usbx-events/image12.png)

**Descrizione**

Questo evento rappresenta un evento di Get evento HID della classe di dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-event-set"></a>Set di eventi HID della classe dispositivo 

#### <a name="ux_device_class_hid_event_set"></a>ux_device_class_hid_event_set

**Icona** ![ di Icona del set di eventi HID della classe dispositivo](./media/user-guide/usbx-events/image13.png)

**Descrizione**

Questo evento rappresenta un set di eventi HID della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-report-get"></a>Classe dispositivo-report HID 

#### <a name="ux_device_class_hid_report_get"></a>ux_device_class_hid_report_get

**Icona** ![ di Icona di Get del report HID della classe dispositivo](./media/user-guide/usbx-events/image14.png)

**Descrizione**

Questo evento rappresenta un evento di Get del report HID della classe di dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: tipo di descrittore.
- Informazioni sul campo 3: indice della richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-hid-report-set"></a>Set di report HID della classe dispositivo 

#### <a name="ux_device_class_hid_report_set"></a>ux_device_class_hid_report_set

**Icona** ![ di Icona del set di report HID della classe dispositivo](./media/user-guide/usbx-events/image15.png)

**Descrizione**

Questo evento rappresenta un evento del set di report HID della classe di dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: tipo di descrittore.
- Informazioni sul campo 3: indice della richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-activate"></a>Classe dispositivo Pima Activate

#### <a name="ux_device_class_pima_activate"></a>ux_device_class_pima_activate

**Icona** ![ di Icona di attivazione Pima della classe dispositivo](./media/user-guide/usbx-events/image16.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione Pima della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-deactivate"></a>Classe dispositivo Pima disattivare 

#### <a name="ux_device_class_pima_deactivate"></a>ux_device_class_pima_deactivate

**Icona** ![ di Icona di disattivazione della classe di dispositivo Pima](./media/user-guide/usbx-events/image17.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione Pima della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-device-info-send"></a>Classe dispositivo-invio informazioni sul dispositivo Pima 

#### <a name="ux_device_class_pima_device_info_send"></a>ux_device_class_pima_device_info_send

**Icona** ![ di Icona di invio informazioni sul dispositivo Pima della classe dispositivo](./media/user-guide/usbx-events/image18.png)

**Descrizione**

Questo evento rappresenta un evento di invio informazioni sul dispositivo USBX di classe dispositivo.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.

### <a name="device-class-pima-event-get"></a>Classe dispositivo Pima evento Get 

#### <a name="ux_device_class_pima_event_get"></a>ux_device_class_pima_event_get

**Icona** ![ di Icona di Get evento di classe dispositivo Pima](./media/user-guide/usbx-events/image19.png)

**Descrizione**

Questo evento rappresenta un evento di Get evento Pima di classe Device USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo Info 2: evento Pima.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-event-set"></a>Set di eventi Pima della classe dispositivo 

#### <a name="ux_device_class_pima_event_set"></a>ux_device_class_pima_event_set

**Icona** ![ di Icona del set di eventi Pima della classe Device](./media/user-guide/usbx-events/image20.png)

**Descrizione**

Questo evento rappresenta un evento del set di eventi Pima della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo Info 2: evento Pima.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-object-add"></a>Classe dispositivo-aggiunta di oggetti Pima 

#### <a name="ux_device_class_pima_object_add"></a>ux_device_class_pima_object_add

**Icona** ![ di Icona di aggiunta oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image21.png)

**Descrizione**

Questo evento rappresenta un evento di aggiunta di un oggetto Pima di classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-object-data-get"></a>Classe dispositivo Pima dati oggetto Get 

#### <a name="ux_device_class_pima_object_data_get"></a>ux_device_class_pima_object_data_get

**Icona** ![ di Icona di visualizzazione dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image22.png)

**Descrizione**

Questo evento rappresenta un evento di Get di dati dell'oggetto Pima della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-object-data-send"></a>Trasmissione dati oggetto Pima classe dispositivo 

#### <a name="ux_device_class_pima_object_data_send"></a>ux_device_class_pima_object_data_send

**Icona** ![ di Icona di invio dati oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image23.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione dati oggetto Pima classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-object-delete"></a>Classe dispositivo-Elimina oggetto Pima 

#### <a name="ux_device_class_pima_object_delete"></a>ux_device_class_pima_object_delete

**Icona** ![ di Icona di eliminazione oggetti Pima classe dispositivo](./media/user-guide/usbx-events/image24.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione di oggetti Pima di classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-object-handles-send"></a>Classe dispositivo gestisce l'invio di oggetti Pima 

#### <a name="ux_device_class_pima_object_handles_send"></a>ux_device_class_pima_object_handles_send

**Icona** ![ di Icona di invio handle oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image25.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivi USBX che gestisce l'evento di invio.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: ID archiviazione.
- Informazioni sul campo 3: codice del formato dell'oggetto.
- Campo informazioni 4: associazione di oggetti.

### <a name="device-class-pima-object-info-get"></a>Classe dispositivo. informazioni sull'oggetto Pima Get 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Icona** ![ di Icona di visualizzazione informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image26.png)

**Descrizione**

Questo evento rappresenta un evento di informazioni di oggetto Pima per la classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-object-info-send"></a>Classe dispositivo-invio informazioni oggetto Pima 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Icona** ![ di Icona di invio informazioni oggetto Pima classe dispositivo](./media/user-guide/usbx-events/image27.png)

**Descrizione**

Questo evento rappresenta un evento di invio delle informazioni sull'oggetto Pima della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-objects-number-send"></a>Classe dispositivo numero oggetti Pima invio 

#### <a name="ux_device_class_pima_object_number_send"></a>ux_device_class_pima_object_number_send

**Icona** ![ di Icona di invio numero di oggetti Pima di classe dispositivo](./media/user-guide/usbx-events/image28.png)

**Descrizione**

Questo evento rappresenta un evento di invio di un numero di oggetto Pima di classe dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: ID archiviazione.
- Informazioni sul campo 3: codice del formato dell'oggetto.
- Campo dati 4: oggetto associato.

### <a name="device-class-pima-partial-object-data-get"></a>Classe dispositivo i dati dell'oggetto parziale Pima Get

#### <a name="ux_device_class_pima_partial_object_data_get"></a>ux_device_class_pima_partial_object_data_get

**Icona** ![ di Icona di visualizzazione dati oggetto parziale classe dispositivo Pima](./media/user-guide/usbx-events/image29.png)

**Descrizione**

Questo evento rappresenta un evento di Get parziale dei dati degli oggetti Pima della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Informazioni campo 3: offset richiesto.
- Informazioni campo 4: lunghezza richiesta.

### <a name="device-class-pima-response-send"></a>Classe dispositivo-invio risposta Pima 

#### <a name="ux_device_class_pima_response_send"></a>ux_device_class_pima_response_send

**Icona** ![ di Icona di invio risposta Pima della classe dispositivo](./media/user-guide/usbx-events/image30.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione della risposta Pima della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: codice di risposta.
- Campo info 3: parametro number.
- Informazioni sul campo 4: Pima parametro 1.

### <a name="device-class-pima-storage-id-send"></a>Classe dispositivo-invio ID archiviazione Pima 

#### <a name="ux_device_class_pima_storage_id_send"></a>ux_device_class_pima_storage_id_send

**Icona** ![ di Icona di invio ID archiviazione Pima della classe dispositivo](./media/user-guide/usbx-events/image31.png)

**Descrizione**

Questo evento rappresenta un evento di invio dell'ID di archiviazione Pima di classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-pima-storage-info-send"></a>Classe dispositivo-informazioni archiviazione Pima invio 

#### <a name="ux_device_class_pima_storage_info_send"></a>ux_device_class_pima_storage_info_send

**Icona** ![ di Icona di invio info di archiviazione Pima della classe dispositivo](./media/user-guide/usbx-events/image32.png)

**Descrizione**

Questo evento rappresenta un evento di invio di informazioni di archiviazione Pima di classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-activate"></a>Classe dispositivo RNDIS attiva 

#### <a name="ux_device_class_rndis_activate"></a>ux_device_class_rndis_activate

**Icona** ![ di Icona di attivazione della classe Device RNDIS](./media/user-guide/usbx-events/image33.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione RNDIS di classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-deactivate"></a>RNDIS classe dispositivo disattiva 

#### <a name="ux_device_class_rndis_deactivate"></a>ux_device_class_rndis_deactivate

**Icona** ![ di Icona di disattivazione della classe Device RNDIS](./media/user-guide/usbx-events/image34.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX RNDIS disattivare un evento.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-message-keep-alive"></a>Classe dispositivo RNDIS messaggio keep-alive 

#### <a name="ux_device_class_rndis_msg_keep_alive"></a>ux_device_class_rndis_msg_keep_alive

**Icona** ![ di Icona del messaggio keep alive di classe Device RNDIS](./media/user-guide/usbx-events/image35.png)

**Descrizione**

Questo evento rappresenta una classe di dispositivo USBX RNDIS messaggio keep alive.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-message-query"></a>Query del messaggio RNDIS della classe dispositivo 

#### <a name="ux_device_class_rndis_msg_keep_query"></a>ux_device_class_rndis_msg_keep_query

**Icona** ![ di Icona della query del messaggio RNDIS della classe dispositivo](./media/user-guide/usbx-events/image36.png)

**Descrizione**

Questo evento rappresenta un evento di query del messaggio RNDIS del messaggio USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: RNDIS OID.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-message-reset"></a>Classe dispositivo reimpostazione del messaggio RNDIS 

#### <a name="ux_device_class_rndis_msg_reset"></a>ux_device_class_rndis_msg_reset

**Icona** ![ di Icona di reimpostazione del messaggio RNDIS della classe dispositivo](./media/user-guide/usbx-events/image37.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione del messaggio RNDIS per la classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.

### <a name="device-class-rndis-message-set"></a>Set di messaggi RNDIS della classe dispositivo 

#### <a name="ux_device_class_rndis_msg_set"></a>ux_device_class_rndis_msg_set

**Icona** ![ di Icona del set di messaggi RNDIS della classe dispositivo](./media/user-guide/usbx-events/image38.png)

**Descrizione**

Questo evento rappresenta un evento del set di messaggi RNDIS della classe di dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: RNDIS OID.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-packet-receive"></a>Classe dispositivo RNDIS ricezione pacchetti 

#### <a name="ux_device_class_rndis_packet_receive"></a>ux_device_class_rndis_packet_receive

**Icona** ![ di Icona di ricezione del pacchetto della classe Device RNDIS](./media/user-guide/usbx-events/image39.png)

**Descrizione**

Questo evento rappresenta un evento di ricezione del pacchetto RNDIS di classe dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-rndis-packet-transmit"></a>Classe dispositivo trasmissione pacchetti RNDIS 

#### <a name="ux_device_class_rndis_packet_transmit"></a>ux_device_class_rndis_packet_transmit

**Icona** ![ di Icona di trasmissione dei pacchetti della classe Device RNDIS](./media/user-guide/usbx-events/image40.png)

**Descrizione**

Questo evento rappresenta un evento di trasmissione pacchetti RNDIS di classe dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-activate"></a>Attivazione dell'archiviazione della classe dispositivo 

#### <a name="ux_device_class_storage_activate"></a>ux_device_class_storage_activate

**Icona** ![ di Icona di attivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image41.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione dell'archiviazione della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-deactivate"></a>Disattivazione dell'archiviazione della classe dispositivo 

#### <a name="ux_device_class_storage_deactivate"></a>ux_device_class_storage_deactivate

**Icona** ![ di Icona di disattivazione dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image42.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione dell'archiviazione della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-format"></a>Formato di archiviazione della classe dispositivo 

#### <a name="ux_device_class_storage_format"></a>ux_device_class_storage_format

**Icona** ![ di Icona del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image43.png)

**Descrizione**

Questo evento rappresenta un evento del formato di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-inquiry"></a>Richiesta di archiviazione della classe dispositivo 

#### <a name="ux_device_class_storage_inquiry"></a>ux_device_class_storage_inquiry

**Icona** ![ di Icona di richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image44.png)

**Descrizione**

Questo evento rappresenta un evento di richiesta di archiviazione della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-mode-select"></a>Selezione della modalità di archiviazione della classe dispositivo

#### <a name="ux_device_class_storage_mode_select"></a>ux_device_class_storage_mode_select

**Icona** ![ di Icona di selezione modalità di archiviazione classe dispositivo](./media/user-guide/usbx-events/image45.png)

**Descrizione**

Questo evento rappresenta un evento di selezione della modalità di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-mode-sense"></a>Rilevamento della modalità di archiviazione della classe dispositivo 

#### <a name="ux_device_class_storage_mode_sense"></a>ux_device_class_storage_mode_sense

**Icona** ![ di Icona di rilevamento della modalità di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image46.png)

**Descrizione**

Questo evento rappresenta un evento del senso della modalità di archiviazione della classe del dispositivo USBX.

Campi informazioni 

- Campo NFO 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-prevent-allow-media-removal"></a>L'archiviazione delle classi di dispositivi impedisce la rimozione di supporti 

#### <a name="ux_device_class_storage_prevent_allow_media_removal"></a>ux_device_class_storage_prevent_allow_media_removal

**Icona** ![ di Archiviazione della classe dispositivo Impedisci l'uso dell'icona Consenti rimozione supporti](./media/user-guide/usbx-events/image47.png)

**Descrizione**

Questo evento rappresenta un'archiviazione della classe del dispositivo USBX Impedisci l'evento di rimozione dei supporti.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-read"></a>Lettura archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_read"></a>ux_device_class_storage_read

**Icona** ![ di Icona di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image48.png)

**Descrizione**

Questo evento rappresenta un evento di lettura di archiviazione della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo informazioni 3: settore.
- Campo dati 4: settori numerici.

### <a name="device-class-storage-read-capacity"></a>Capacità lettura archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_read_capacity"></a>ux_device_class_storage_read_capacity

**Icona** ![ di Icona capacità di lettura archiviazione classe dispositivo](./media/user-guide/usbx-events/image49.png)

**Descrizione**

Questo evento rappresenta un evento di capacità di lettura di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-read-format-capacity"></a>Capacità di lettura del formato di archiviazione della classe dispositivo 

#### <a name="ux_device_class_storage_read_format_capacity"></a>ux_device_class_storage_read_format_capacity

**Icona** ![ di Icona della capacità di lettura del formato di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image50.png)

**Descrizione**

Questo evento rappresenta un evento di capacità di lettura del formato di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-read-toc"></a>Sommario di lettura per archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_read_toc"></a>ux_device_class_storage_read_toc

**Icona** ![ di Icona di lettura Sommario archiviazione classe dispositivo](./media/user-guide/usbx-events/image51.png)

**Descrizione**

Questo evento rappresenta un evento di lettura del sommario di archiviazione della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-request-sense"></a>Senso richiesta archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_request_sense"></a>ux_device_class_storage_request_sense

**Icona** ![ di Icona del senso della richiesta di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image52.png)

**Descrizione**

Questo evento rappresenta un evento del senso della richiesta di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Informazioni sul campo 3: chiave Sense.
- Campo informazioni 4: codice.

### <a name="device-class-storage-start-stop"></a>Inizio arresto archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_start_stop"></a>ux_device_class_storage_start_stop

**Icona** ![ di Icona di avvio dell'archiviazione della classe dispositivo](./media/user-guide/usbx-events/image53.png)

**Descrizione**

Questo evento rappresenta un evento di avvio di archiviazione della classe del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-test-ready"></a>Il test di archiviazione della classe dispositivo è pronto 

#### <a name="ux_device_class_storage_test_ready"></a>ux_device_class_storage_test_ready

**Icona** ![ di Icona dei test di archiviazione della classe dispositivo](./media/user-guide/usbx-events/image54.png)

**Descrizione**

Questo evento rappresenta un evento pronto per il test di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-verify"></a>Verifica archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_verify"></a>ux_device_class_storage_verify

**Icona** ![ di Icona di verifica archiviazione classe dispositivo](./media/user-guide/usbx-events/image55.png)

**Descrizione**

Questo evento rappresenta un evento di verifica dell'archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-class-storage-write"></a>Scrittura archiviazione classe dispositivo 

#### <a name="ux_device_class_storage_write"></a>ux_device_class_storage_write

**Icona** ![ di Icona di scrittura archiviazione classe dispositivo](./media/user-guide/usbx-events/image56.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura di archiviazione della classe del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: lun.
- Campo informazioni 3: settore.
- Campo dati 4: settori numerici.

### <a name="device-stack-alternate-setting-get"></a>Impostazione alternativa stack del dispositivo Get 

#### <a name="ux_device_class_alternate_setting_get"></a>ux_device_class_alternate_setting_get

**Icona** ![ di Icona del Get dell'impostazione alternativa dello stack del dispositivo](./media/user-guide/usbx-events/image57.png)

**Descrizione**

Questo evento rappresenta un'impostazione alternativa di Get Event stack del dispositivo USBX.

**Campi informazioni**

- Info Field 1: valore di interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-alternate-setting-set"></a>Set di impostazioni alternativo dello stack del dispositivo 

#### <a name="ux_device_class_alternate_setting_set"></a>ux_device_class_alternate_setting_set

**Icona** ![ di Icona del set di impostazioni alternativo dello stack del dispositivo](./media/user-guide/usbx-events/image58.png)

**Descrizione**

Questo evento rappresenta un evento del set di impostazioni alternativo dello stack di dispositivi USBX.

**Campi informazioni**
- Info Field 1: valore di interfaccia.
- Informazioni sul campo 2: valore dell'impostazione alternativa.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-class-register"></a>Registro classe stack del dispositivo 

#### <a name="ux_device_stack_class_register"></a>ux_device_stack_class_register

**Icona** ![ di Icona di registro classe stack del dispositivo](./media/user-guide/usbx-events/image59.png)

**Descrizione**

Questo evento rappresenta un evento di registrazione della classe stack del dispositivo USBX.

**Campi informazioni**

- Info Field 1: nome della classe.
- Informazioni sul campo 2: numero di interfaccia.
- Campo info 3: parametro.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-clear-feature"></a>Funzionalità di cancellazione dello stack del dispositivo 

#### <a name="ux_device_stack_clear_feature"></a>ux_device_stack_clear_feature

**Icona** ![ di Icona della funzionalità cancellazione dello stack del dispositivo](./media/user-guide/usbx-events/image60.png)

**Descrizione**

Questo evento rappresenta un evento di funzionalità di cancellazione dello stack del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: tipo di richiesta.
- Informazioni sul campo 2: valore della richiesta. Informazioni sul campo 3: indice della richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-configuration-get"></a>Configurazione dello stack del dispositivo Get 

#### <a name="ux_device_stack_configuration_get-t"></a>ux_device_stack_configuration_get t

**Icona** ![ di Icona di Get della configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image61.png)

**Descrizione**

Questo evento rappresenta un evento Get della configurazione dello stack di dispositivi USBX.

**Campi informazioni** 

- Campo informazioni 1: valore di configurazione.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-configuration-set"></a>Set di configurazione dello stack del dispositivo 

#### <a name="ux_device_stack_configuration_set"></a>ux_device_stack_configuration_set

**Icona** ![ di Icona del set di configurazione dello stack del dispositivo](./media/user-guide/usbx-events/image62.png)

**Descrizione**

Questo evento rappresenta un evento del set di configurazione dello stack di dispositivi USBX.

**Campi informazioni** 

- Campo informazioni 1: valore di configurazione.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-connect"></a>Connessione stack del dispositivo 

#### <a name="ux_device_stack_connect"></a>ux_device_stack_connect

**Icona** ![ di Icona di connessione dello stack del dispositivo](./media/user-guide/usbx-events/image63.png)

**Descrizione**

Questo evento rappresenta un evento di invio del descrittore dello stack del dispositivo USBX.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-descriptor-send"></a>Invio del descrittore dello stack del dispositivo 

#### <a name="ux_device_stack_descriptor_send"></a>ux_device_stack_descriptor_send

**Icona** ![ di Icona di invio del descrittore dello stack del dispositivo](./media/user-guide/usbx-events/image64.png)

**Descrizione**

Questo evento rappresenta un evento di invio del descrittore dello stack del dispositivo USBX.

**Campi informazioni**

- Info Field 1: tipo di descrittore.
- Informazioni sul campo 2: indice della richiesta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-disconnect"></a>Disconnessione dello stack del dispositivo 

#### <a name="ux_device_stack_disconnect"></a>ux_device_stack_disconnect

**Icona** ![ di Icona di disconnessione dello stack del dispositivo](./media/user-guide/usbx-events/image65.png)

**Descrizione**

Questo evento rappresenta un evento di disconnessione dello stack del dispositivo USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-endpoint-stall"></a>Stallo dello stack dell'endpoint del dispositivo 

#### <a name="ux_device_stack_endpoint_stall"></a>ux_device_stack_endpoint_stall

**Icona** ![ di Icona dello stallo dello stack dell'endpoint del dispositivo](./media/user-guide/usbx-events/image66.png)

**Descrizione**

Questo evento rappresenta un evento di blocco dell'endpoint dello stack di dispositivi USBX.

**Campi informazioni** 

- Campo informazioni 1: endpoint.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-get-status"></a>Stato di Get dello stack del dispositivo 

#### <a name="ux_device_stack_get_status"></a>ux_device_stack_get_status

**Icona** ![ di Icona dello stato di Get dello stack del dispositivo](./media/user-guide/usbx-events/image67.png)

**Descrizione**

Questo evento rappresenta un evento di stato di Get dello stack di dispositivi USBX.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-host-wakeup"></a>Riattivazione host stack del dispositivo 

#### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

**Icona** ![ di Icona di riattivazione host stack del dispositivo](./media/user-guide/usbx-events/image68.png)

**Descrizione**

Questo evento rappresenta un evento di riattivazione host dello stack del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-initialize"></a>Inizializzazione dello stack del dispositivo 

#### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

**Icona** ![ di Icona di inizializzazione dello stack del dispositivo](./media/user-guide/usbx-events/image69.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione dello stack del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-interface-delete"></a>Eliminazione dell'interfaccia dello stack di dispositivi 

#### <a name="ux_device_stack_interface_delete"></a>ux_device_stack_interface_delete

**Icona** ![ di Icona di eliminazione dell'interfaccia dello stack del dispositivo](./media/user-guide/usbx-events/image70.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'interfaccia dello stack di dispositivi USBX.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-interface-get"></a>Interfaccia stack del dispositivo Get 

#### <a name="ux_device_stack_interface_get"></a>ux_device_stack_interface_get

**Icona** ![ di Icona Ottieni interfaccia stack di dispositivi](./media/user-guide/usbx-events/image71.png)

**Descrizione**

Questo evento rappresenta un evento Get dell'interfaccia dello stack di dispositivi USBX.

**Campi informazioni** 

- Info Field 1: valore di interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-interface-set"></a>Set di interfacce dello stack di dispositivi 

#### <a name="ux_device_stack_interface_set"></a>ux_device_stack_interface_set

**Icona** ![ di Icona del set di interfacce dello stack di dispositivi](./media/user-guide/usbx-events/image72.png)

**Descrizione**

Questo evento rappresenta un evento del set di interfacce dello stack di dispositivi USBX.

**Campi informazioni** 

- Campo informazioni 1: valore della richiesta. Informazioni sul campo 2: indice della richiesta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-set-feature"></a>Funzionalità set di stack del dispositivo 

#### <a name="ux_device_stack_set_feature"></a>ux_device_stack_set_feature

**Icona** ![ di Icona della funzionalità set di stack del dispositivo](./media/user-guide/usbx-events/image73.png)

**Descrizione**

Questo evento rappresenta un evento di funzionalità del set di stack di dispositivi USBX.

**Campi informazioni** 

- Campo informazioni 1: valore della richiesta. Informazioni sul campo 2: indice della richiesta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-transfer-abort"></a>Interruzione trasferimento stack del dispositivo 

#### <a name="ux_device_stack_transfer_abort"></a>ux_device_stack_transfer_abort

**Icona** ![ di Icona di interruzione del trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image74.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del trasferimento dello stack del dispositivo USBX.

**Campi informazioni** 

- Campo informazioni 1: richiesta di trasferimento.
- Informazioni sul campo 2: codice di completamento.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-transfer-all-request-abort"></a>Interruzione richiesta tutti i trasferimenti stack di dispositivi 

#### <a name="ux_device_stack_transfer_all_request_abort"></a>ux_device_stack_transfer_all_request_abort

**Icona** ![ di Icona di interruzione della richiesta di trasferimento dello stack di dispositivi](./media/user-guide/usbx-events/image75.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione della richiesta di trasferimento dello stack di dispositivi USBX.

**Campi informazioni** 

- Campo informazioni 1: endpoint.
- Informazioni sul campo 2: codice di completamento.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="device-stack-transfer-request"></a>Richiesta di trasferimento dello stack del dispositivo 

#### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

**Icona** ![ di Icona della richiesta di trasferimento dello stack del dispositivo](./media/user-guide/usbx-events/image76.png)

**Descrizione**

Questo evento rappresenta un evento di richiesta di trasferimento dello stack di dispositivi USBX.

**Campi informazioni**

- Campo informazioni 1: richiesta di trasferimento.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-asix-activate"></a>Classe host ASIX Activate 

#### <a name="ux_host_class_asix_activate"></a>ux_host_class_asix_activate

**Icona** ![ di Icona di attivazione della classe host ASIX](./media/user-guide/usbx-events/image77.png)

**Descrizione**

Questo evento rappresenta una classe host USBX ASIX Activate.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-asix-deactivate"></a>Classe host ASIX disattivare 

#### <a name="ux_host_class_asix_deactivate"></a>ux_host_class_asix_deactivate

**Icona** ![ di Icona ASIX della classe host disattiva](./media/user-guide/usbx-events/image78.png)

**Descrizione**

Questo evento rappresenta una classe host USBX ASIX disattivare un evento.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-asix-interrupt-notification"></a>Notifica di interrupt della classe host ASIX 

#### <a name="ux_host_class_asix_interrupt_notification"></a>ux_host_class_asix_interrupt_notification

**Icona** ![ di Icona della notifica di interrupt della classe host ASIX](./media/user-guide/usbx-events/image79.png)

**Descrizione**

Questo evento rappresenta un evento di notifica di interrupt ASIX di classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-asix-read"></a>Classe host ASIX Read 

#### <a name="ux_host_class_asix_read"></a>ux_host_class_asix_read

**Icona** ![ di Icona di lettura della classe host ASIX](./media/user-guide/usbx-events/image80.png)

**Descrizione**

Questo evento rappresenta un evento di lettura ASIX della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-asix-write"></a>Classe host ASIX Write 

#### <a name="ux_host_class_asix_write"></a>ux_host_class_asix_write

**Icona** ![ di Icona di scrittura della classe host ASIX](./media/user-guide/usbx-events/image81.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura ASIX della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-activate"></a>Attivazione audio classe host 

#### <a name="ux_host_class_audio_activate"></a>ux_host_class_audio_activate

**Icona** ![ di Icona di attivazione dell'audio della classe host](./media/user-guide/usbx-events/image82.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione audio della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-control-value-get"></a>Valore di controllo audio della classe host Get 

#### <a name="ux_host_class_audio_control_value_get"></a>ux_host_class_audio_control_value_get

**Icona** ![ di Icona Get del valore del controllo audio della classe host](./media/user-guide/usbx-events/image83.png)

**Descrizione**

Questo evento rappresenta un evento Get del valore di controllo audio della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-control-value-set"></a>Valore del controllo audio della classe host impostato 

#### <a name="ux_host_class_audio_control_value_set"></a>ux_host_class_audio_control_value_set

**Icona** ![ di Icona del set di valori del controllo audio della classe host](./media/user-guide/usbx-events/image84.png)

**Descrizione**

Questo evento rappresenta un evento di elaborazione posticipato del driver di I/O NetX interno.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: controllo audio.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-deactivate"></a>Disattivazione audio della classe host 

#### <a name="ux_host_class_audio_deactivate"></a>ux_host_class_audio_deactivate

**Icona** ![ di Icona di disattivazione audio della classe host](./media/user-guide/usbx-events/image85.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione audio della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-read"></a>Lettura audio classe host 

#### <a name="ux_host_class_audio_read"></a>ux_host_class_audio_read

**Icona** ![ di Icona di lettura audio della classe host](./media/user-guide/usbx-events/image86.png)

**Descrizione**

Questo evento rappresenta un evento di lettura audio della classe host USBX.

- Campi informazioni 
- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-streaming-sampling-get"></a>Raccolta di campionamento flusso audio della classe host Get 

#### <a name="ux_host_class_audio_streaming_sampling_get"></a>ux_host_class_audio_streaming_sampling_get

**Icona** ![ di Icona di Get del campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image87.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento del campionamento del flusso audio della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-streaming-sampling-set"></a>Set di campionamento del flusso audio della classe host 

#### <a name="ux_host_class_audio_streaming_sampling_set"></a>ux_host_class_audio_streaming_sampling_set

**Icona** ![ di Icona del set di campionamento del flusso audio della classe host](./media/user-guide/usbx-events/image88.png)

**Descrizione**

Questo evento rappresenta un evento del set di campionamento di flusso audio della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: campionamento audio.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-audio-write"></a>Scrittura audio della classe host 

#### <a name="ux_host_class_audio_write"></a>ux_host_class_audio_write

**Icona** ![ di Icona di scrittura audio della classe host](./media/user-guide/usbx-events/image89.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura audio della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-activate"></a>Classe host CDC ACM Activate 

#### <a name="ux_host_class_cdc_acm_activate"></a>ux_host_class_cdc_acm_activate

**Icona** ![ di Icona di attivazione della classe host C D C A C M](./media/user-guide/usbx-events/image90.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM Activate Event.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-deactivate"></a>Classe host CDC ACM Deactivate 

#### <a name="ux_host_class_cdc_acm_deactivate"></a>ux_host_class_cdc_acm_deactivate

**Icona** ![ di Classe host C D C A C M icona di disattivazione](./media/user-guide/usbx-events/image91.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM Deactivate event.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-abort-in-pipe"></a>Classe host CDC per l'interruzione IOCTL ACM nella pipe 

#### <a name="ux_host_class_cdc_acm_ioctl_abort_in_pipe"></a>ux_host_class_cdc_acm_ioctl_abort_in_pipe

**Icona** ![ di Classe host C D C A C M I O C T L interruzione nell'icona pipe](./media/user-guide/usbx-events/image92.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM IOCTL Abort nell'evento pipe.

Campi informazioni 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-abort-out-pipe"></a>Classe host CDC ACM ACM Interrompi pipe 

#### <a name="ux_host_class_cdc_acm_ioct_abort_out_pipe"></a>ux_host_class_cdc_acm_ioct_abort_out_pipe

**Icona** ! [[Classe host c D c A c M I O c T L pulsante Interrompi barra verticale](./media/user-guide/usbx-events/image93.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM IOCTL Interrompi pipe evento.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-get-device-status"></a>Classe host CDC ACM per l'ottenimento dello stato del dispositivo 

#### <a name="ux_host_class_cdc_acm_ioctl_get_device_status"></a>ux_host_class_cdc_acm_ioctl_get_device_status

**Icona** ![ di Classe host C D C A C M I O C T L icona di stato del dispositivo Get](./media/user-guide/usbx-events/image94.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM IOCTL Get Device Status Event.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: stato del dispositivo.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-get-line-coding"></a>Classe host CDC ACM per ottenere la codifica della riga 

#### <a name="ux_host_class_cdc_acm_ioctl_get_line_coding"></a>ux_host_class_cdc_acm_ioctl_get_line_coding

**Icona** ![ di Classe host C D C A C M I O C T L ottenere l'icona di codifica della riga](./media/user-guide/usbx-events/image95.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM per l'evento di codifica della riga.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-notification-callback"></a>Callback delle notifiche IOCTL di classe host CDC ACM

#### <a name="ux_host_class_cdc_acm_ioctl_notification_callback"></a>ux_host_class_cdc_acm_ioctl_notification_callback

**Icona** ![ di Classe host C D C A C M I O C T L icona di callback di notifica](./media/user-guide/usbx-events/image96.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM, evento di callback di notifica IOCTL.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-send-break"></a>Classe host CDC ACM di invio-Interrompi 

#### <a name="ux_host_class_cdc_acm_ioctl_send_break"></a>ux_host_class_cdc_acm_ioctl_send_break

**Icona** ![ di Classe host C D C A C M I O C T L invio icona di interruzioni](./media/user-guide/usbx-events/image97.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM di invio di un evento di rottura.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-set-line-coding"></a>Codifica della riga set IOCTL di classe host CDC ACM 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_coding"></a>ux_host_class_cdc_acm_ioctl_set_line_coding

**Icona** ![ di La classe host C D C A C M I O C T L impostare l'icona dell'icona di codifica della riga ](./media/user-guide/usbx-events/image97.png) ] (./media/user-guide/usbx-events/image98.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM per set di codifica della riga.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-ioctl-set-line-state"></a>Stato della riga set IOCTL di classe host CDC ACM 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_state"></a>ux_host_class_cdc_acm_ioctl_set_line_state

**Icona** ![ di Classe host C D C A C M I O C T L impostare lo stato della riga icona](./media/user-guide/usbx-events/image99.png)

**Descrizione**

Questo evento rappresenta un evento di stato della riga set di linee di USBX di classe host CDC ACM.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-read"></a>Classe host CDC ACM Read 

#### <a name="ux_host_class_cdc_acm_read"></a>ux_host_class_cdc_acm_read

**Icona** ![ di Icona di lettura c M di classe host c D](./media/user-guide/usbx-events/image100.png)

**Descrizione**

Questo evento rappresenta una classe host USBX, un evento di lettura di CDC ACM.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-reception-start"></a>Classe host CDC ACM reception Start 

#### <a name="ux_host_class_cdc_acm_reception_start"></a>ux_host_class_cdc_acm_reception_start

**Icona** ![ di Icona di avvio della ricezione c M della classe host C D C](./media/user-guide/usbx-events/image101.png)

**Descrizione**

Questo evento rappresenta un evento di avvio della ricezione USBX di CDC ACM di classe host.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-reception-stop"></a>Arresto della ricezione della classe host CDC ACM 

#### <a name="ux_host_class_cdc_acm_reception_stop"></a>ux_host_class_cdc_acm_reception_stop

**Icona** ![ di Icona di arresto della ricezione c M per la classe host C D C](./media/user-guide/usbx-events/image102.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM reception Event stop.

**Campi informazioni**

- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-cdc-acm-write"></a>Classe host CDC ACM Write 

#### <a name="ux_host_class_acm_write"></a>ux_host_class_acm_write

**Icona** ![ di Icona di scrittura della classe host C D C A C M](./media/user-guide/usbx-events/image103.png)

**Descrizione**

Questo evento rappresenta una classe host USBX CDC ACM Write Event.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-dpump-activate"></a>Classe host DPUMP Activate 

#### <a name="ux_host_class_dpump_activate"></a>ux_host_class_dpump_activate

**Icona** ![ di Icona di attivazione della classe host DPUMP](./media/user-guide/usbx-events/image104.png)

**Descrizione**

Questo evento rappresenta un evento DPUMP Activate della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-dpump-deactivate"></a>Classe host DPUMP disattivare 

#### <a name="ux_host_class_dpump_deactivate"></a>ux_host_class_dpump_deactivate

**Icona** ![ di Icona DPUMP della classe host disattiva](./media/user-guide/usbx-events/image105.png)

**Descrizione**

Questo evento rappresenta una classe host USBX DPUMP disattivare un evento.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-dpump-read"></a>Classe host DPUMP Read 

#### <a name="ux_host_class_dpump_read"></a>ux_host_class_dpump_read

**Icona** ![ di Icona di lettura della classe host DPUMP](./media/user-guide/usbx-events/image106.png)

**Descrizione**

Questo evento rappresenta un evento di lettura DPUMP della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-dpump-write"></a>Classe host DPUMP Write 

#### <a name="ux_host_class_dpump_write"></a>ux_host_class_dpump_write

**Icona** ![ di Icona di scrittura della classe host DPUMP](./media/user-guide/usbx-events/image107.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura DPUMP della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-activate"></a>Attivazione HID della classe host 

#### <a name="ux_host_class_hid_activate"></a>ux_host_class_hid_activate

**Icona** ![ di Icona di attivazione HID della classe host](./media/user-guide/usbx-events/image108.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione HID della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-client-register"></a>Registro del client HID della classe host 

#### <a name="ux_host_class_hid_client_register"></a>ux_host_class_hid_client_register

**Icona** ![ di Icona di registro del client HID della classe host](./media/user-guide/usbx-events/image109.png)

**Descrizione**

Questo evento rappresenta un evento di registrazione del client HID della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: nome client nascosto.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-deactivate"></a>Disattivazione HID della classe host 

#### <a name="ux_host_class_hid_deactivate"></a>ux_host_class_hid_deactivate

**Icona** ![ di Icona di disattivazione HID della classe host](./media/user-guide/usbx-events/image110.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione HID della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-idle-get"></a>Classe host HID Idle Get 

#### <a name="ux_host_class_hid_idle_get"></a>ux_host_class_hid_idle_get

**Icona** ![ di Icona della classe host HID Idle Get](./media/user-guide/usbx-events/image111.png)

**Descrizione**

Questo evento rappresenta una classe host USBX. evento di Get inattivo HID.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-idle-set"></a>Set inattivo HID classe host 

#### <a name="ux_host_class_hid_idle_set"></a>ux_host_class_hid_idle_set

**Icona** ![ di Icona del set di inattività HID della classe host](./media/user-guide/usbx-events/image112.png)

**Descrizione**

Questo evento rappresenta un evento set inattivo HID della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-keyboard-activate"></a>Attivazione della tastiera HID della classe host 

#### <a name="ux_host_class_hid_keyboard_activate"></a>ux_host_class_hid_keyboard_activate

**Icona** ![ di Icona di attivazione della tastiera HID della classe host](./media/user-guide/usbx-events/image113.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione della tastiera HID della classe host USBX.

**Campi informazioni**
<p>Campo informazioni 1: istanza della classe.
<p>Campo informazioni 2: istanza client nascosta.
<p>Campo info 3: non utilizzato.
<p>Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-keyboard-deactivate"></a>Disattiva la tastiera HID della classe host 

#### <a name="ux_host_class_hid_keyboard_deactivate"></a>ux_host_class_hid_keyboard_deactivate

**Icona** ![ di Icona di disattivazione tastiera HID della classe host](./media/user-guide/usbx-events/image114.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione della tastiera HID della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza client nascosta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-mouse-activate"></a>Attivazione mouse HID classe host 

#### <a name="ux_host_class_hid_mouse_activate"></a>ux_host_class_hid_mouse_activate

**Icona** ![ di Icona di attivazione della classe host HID mouse](./media/user-guide/usbx-events/image115.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione del mouse HID della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza client nascosta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-mouse-deactivate"></a>Disattivazione del mouse della classe host HID 

#### <a name="ux_host_class_hid_mouse_deactivate"></a>ux_host_class_hid_mouse_deactivate

**Icona** ![ di Icona di disattivazione della classe host HID mouse](./media/user-guide/usbx-events/image116.png)

**Descrizione**

- Questo evento rappresenta un evento di deattivazione del mouse HID della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza client nascosta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-remote-control-activate"></a>Attivazione del controllo remoto HID della classe host 

#### <a name="ux_host_class_hid_remote_control_activate"></a>ux_host_class_hid_remote_control_activate

**Icona** ![ di Icona di attivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image117.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione del controllo remoto HID della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza client nascosta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-remote-control-deactivate"></a>Disattivazione del controllo remoto HID della classe host 

#### <a name="ux_host_class_hid_remote_control_deactivate"></a>ux_host_class_hid_remote_control_deactivate

**Icona** ![ di Icona di disattivazione del controllo remoto HID della classe host](./media/user-guide/usbx-events/image118.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione del controllo remoto HID della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: istanza client nascosta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-report-get"></a>Classe host-report HID 

#### <a name="ux_host_class_hid_report_get"></a>ux_host_class_hid_report_get

**Icona** ![ di Icona di Get del report HID della classe host](./media/user-guide/usbx-events/image119.png)

**Descrizione**

Questo evento rappresenta una classe host USBX di report HID.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: report client.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hid-report-set"></a>Set di report HID della classe host 

#### <a name="ux_host_class_hid_report_set"></a>ux_host_class_hid_report_set

**Icona** ![ di Icona del set di report HID della classe host](./media/user-guide/usbx-events/image120.png)

**Descrizione** di Questo evento rappresenta un set di report HID della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: report client.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-activate"></a>Attivazione dell'hub classi host 

#### <a name="ux_host_class_hub_activate"></a>ux_host_class_hub_activate

**Icona** ![ di Icona di attivazione dell'hub classe host](./media/user-guide/usbx-events/image121.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione dell'hub della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-change-detect"></a>Rilevamento modifiche Hub classe host 

#### <a name="ux_host_class_hub_change_detect"></a>ux_host_class_hub_change_detect

**Icona** ![ di Icona rilevamento modifiche Hub classe host](./media/user-guide/usbx-events/image122.png)

**Descrizione**

Questo evento rappresenta un evento di rilevamento delle modifiche dell'hub della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-deactivate"></a>Disattivazione dell'hub della classe host 

#### <a name="ux_host_class_hub_deactivate"></a>ux_host_class_hub_deactivate

**Icona** ![ di Icona di disattivazione dell'hub classe host](./media/user-guide/usbx-events/image123.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione dell'hub della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-port-change-connection-process"></a>Processo di connessione per la modifica della porta dell'hub classe host 

#### <a name="ux_host_class_hub_change_connection_process"></a>ux_host_class_hub_change_connection_process

**Icona** ![ di Icona del processo di connessione della porta dell'hub della classe host](./media/user-guide/usbx-events/image124.png)

**Descrizione**

Questo evento rappresenta un evento del processo di connessione di modifica della porta dell'hub della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: porta.
- Informazioni sul campo 3: stato della porta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-port-change-enable-process"></a>Modifica della porta dell'hub della classe host Abilita processo 

#### <a name="ux_host_class_hub_port_change_enable_process"></a>ux_host_class_hub_port_change_enable_process

**Icona** ![ di Icona di abilitazione del processo modifica porta hub classe host](./media/user-guide/usbx-events/image125.png)

**Descrizione**

Questo evento rappresenta un evento del processo di attivazione della porta dell'hub della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: porta.
- Informazioni sul campo 3: stato della porta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-port-change-over-current-process"></a>Modifica della porta dell'hub della classe host per il processo corrente 

#### <a name="ux_host_class_hub_port_change_over_current_process"></a>ux_host_class_hub_port_change_over_current_process

**Icona** ![ di Icona modifica porta hub classe host sull'icona del processo corrente](./media/user-guide/usbx-events/image126.png)

**Descrizione**

Questo evento rappresenta l'allocazione di un pacchetto tramite nx_packet_allocate.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: porta.
- Informazioni sul campo 3: stato della porta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-port-change-reset-process"></a>Processo di reimpostazione della porta dell'hub della classe host 

#### <a name="ux_host_class_hub_port_change_reset_process"></a>ux_host_class_hub_port_change_reset_process

**Icona** ![ di Icona del processo di reimpostazione della porta dell'hub della classe host](./media/user-guide/usbx-events/image127.png)

**Descrizione**

Questo evento rappresenta un evento del processo di reimpostazione della porta dell'hub della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: Hub. Informazioni sul campo 2: porta.
- Informazioni sul campo 3: stato della porta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-hub-port-change-suspend-process"></a>Processo di sospensione delle modifiche della porta dell'hub della classe host 

#### <a name="ux_host_class_hub_port_change_suspend_process"></a>ux_host_class_hub_port_change_suspend_process

**Icona** ![ di Icona di sospensione del processo di modifica della porta dell'hub della classe host](./media/user-guide/usbx-events/image128.png)

**Descrizione**

Questo evento rappresenta un evento di sospensione del processo di modifica della porta dell'hub della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: porta.
- Informazioni sul campo 3: stato della porta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-activate"></a>Classe host Pima Activate 

#### <a name="ux_host_class_pima_activate"></a>ux_host_class_pima_activate

**Icona** ![ di Icona di attivazione della classe host Pima](./media/user-guide/usbx-events/image129.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-deactivate"></a>Classe host Pima Deactivate 

#### <a name="ux_host_class_pima_deactivate"></a>ux_host_class_pima_deactivate

**Icona** ![ di Icona di disattivazione della classe host Pima](./media/user-guide/usbx-events/image130.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-device-info-get"></a>Classe host informazioni sul dispositivo Pima Get 

#### <a name="ux_host_class_pima_device_info_get"></a>ux_host_class_pima_device_info_get

**Icona** ![ di Icona di informazioni sul dispositivo Pima della classe host](./media/user-guide/usbx-events/image131.png)

**Descrizione**

Questo evento rappresenta un evento di informazioni sul dispositivo Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: dispositivo Pima.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-device-reset"></a>Classe host reimpostazione del dispositivo Pima 

#### <a name="ux_host_class_pima_device_reset"></a>ux_host_class_pima_device_reset

**Icona** ![ di Icona di reimpostazione del dispositivo Pima della classe host](./media/user-guide/usbx-events/image132.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione del dispositivo Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-notification"></a>Notifica classe host Pima 

#### <a name="ux_host_class_pima_notification"></a>ux_host_class_pima_notification

**Icona** ![ di Icona di notifica classe host Pima](./media/user-guide/usbx-events/image133.png)

**Descrizione**

Questo evento rappresenta un evento di notifica Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe. Informazioni sul campo 2: codice evento.
- Informazioni sul campo 3: ID transazione.
- Informazioni sul campo 4: parametro1.

### <a name="host-class-pima-number-objects-get"></a>Classe host numero Pima oggetti Get 

#### <a name="ux_host_class_pima_number_objects_get"></a>ux_host_class_pima_number_objects_get

**Icona** ![ di Icona di visualizzazione degli oggetti numero Pima della classe host](./media/user-guide/usbx-events/image134.png)

**Descrizione**

Questo evento rappresenta un evento USBX della classe host di un numero Pima di oggetti.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-close"></a>Chiusura dell'oggetto Pima della classe host 

#### <a name="ux_host_class_pima_object_close"></a>ux_host_class_pima_object_close

**Icona** ![ di Icona di chiusura oggetto classe host Pima](./media/user-guide/usbx-events/image135.png)

**Descrizione**

Questo evento rappresenta un evento di chiusura dell'oggetto Pima per la classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-copy"></a>Classe host copia di oggetti Pima 

#### <a name="ux_host_class_pima_object_copy"></a>ux_host_class_pima_object_copy

**Icona** ![ di Icona di copia dell'oggetto classe host Pima](./media/user-guide/usbx-events/image136.png)

**Descrizione**

Questo evento rappresenta un evento di copia dell'oggetto Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-delete"></a>Classe host Elimina oggetto Pima 

#### <a name="ux_host_class_pima_object_delete"></a>ux_host_class_pima_object_delete

**Icona** ![ di Icona di eliminazione oggetto classe host Pima](./media/user-guide/usbx-events/image137.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione di oggetti Pima di classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-get"></a>Classe host (oggetto Pima) Get 

#### <a name="ux_host_class_pima_object_get"></a>ux_host_class_pima_object_get

**Icona** ![ di Icona di Get oggetto della classe host Pima](./media/user-guide/usbx-events/image138.png)

**Descrizione**

Questo evento rappresenta l'acquisizione di informazioni RARP tramite nx_rarp_info_get.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: oggetto.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-info-get"></a>Classe host. informazioni sull'oggetto Pima Get 

#### <a name="ux_host_class_pima_object_info_get"></a>ux_host_class_pima_object_info_get

**Icona** ![ di Icona di visualizzazione delle informazioni sull'oggetto Pima della classe host](./media/user-guide/usbx-events/image139.png)

**Descrizione**

Questo evento rappresenta una classe host USBX per le informazioni di Get dell'oggetto.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: oggetto.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-info-send"></a>Invio di informazioni sull'oggetto classe host Pima 

#### <a name="ux_host_class_pima_object_info_send"></a>ux_host_class_pima_object_info_send

**Icona** ![ di Icona di invio info oggetto Pima classe host](./media/user-guide/usbx-events/image140.png)

**Descrizione**

Questo evento rappresenta un evento di invio di informazioni sull'oggetto Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-move"></a>Spostamento oggetto classe host Pima 

#### <a name="ux_host_class_pima_object_move"></a>ux_host_class_pima_object_move

**Icona** ![ di Icona di spostamento oggetto classe host Pima](./media/user-guide/usbx-events/image141.png)

**Descrizione**

Questo evento reprThis di evento rappresenta un evento di spostamento dell'oggetto Pima di una classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: oggetto.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-object-send"></a>Classe host-invio oggetto Pima 

#### <a name="ux_host_class_pima_object_move"></a>ux_host_class_pima_object_move

**Icona** ![ di Icona di invio oggetto Pima classe host](./media/user-guide/usbx-events/image142.png)

**Descrizione**

Questo evento rappresenta un evento di invio di oggetti Pima di classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: oggetto.
- Campo info 3: buffer oggetti.
- Campo dati 4: lunghezza dell'oggetto.

### <a name="host-class-pima-object-transfer-abort"></a>Interruzione del trasferimento di oggetti Pima della classe host 

#### <a name="ux_host_class_pima_object_transfer_abort"></a>ux_host_class_pima_object_transfer_abort

**Icona** ![ di Icona di interruzione trasferimento oggetti Pima classe host](./media/user-guide/usbx-events/image143.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del trasferimento di oggetti Pima per la classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: oggetto.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-read"></a>Lettura classe host Pima 

#### <a name="ux_host_class_pima_read"></a>ux_host_class_pima_read

**Icona** ![ di Icona di lettura della classe host Pima](./media/user-guide/usbx-events/image144.png)

**Descrizione**

Questo evento rappresenta un evento di lettura Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni sul campo 3: lunghezza dei dati.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-request-cancel"></a>Annullamento della richiesta Pima della classe host 

#### <a name="ux_host_class_pima_request_cancel"></a>ux_host_class_pima_request_cancel

**Icona** ![ di Icona di annullamento richiesta Pima della classe host](./media/user-guide/usbx-events/image145.png)

**Descrizione**

Questo evento rappresenta un evento di annullamento della richiesta Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-session-close"></a>Chiusura della sessione Pima della classe host 

#### <a name="ux_host_class_pima_session_close"></a>ux_host_class_pima_session_close

**Icona** ![ di Icona di chiusura della sessione Pima della classe host](./media/user-guide/usbx-events/image146.png)

**Descrizione**

Questo evento rappresenta un evento di chiusura della sessione Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: sessione Pima.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-session-open"></a>Sessione Pima della classe host aperta 

#### <a name="ux_host_class_pima_session_open"></a>ux_host_class_pima_session_open

**Icona** ![ di Icona di apertura della sessione Pima della classe host](./media/user-guide/usbx-events/image147.png)

**Descrizione** di Questo evento rappresenta un evento di apertura della sessione Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: sessione Pima.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-storage-ids-get"></a>Classe host Pima ID archiviazione Get 

#### <a name="ux_host_class_pima_session_ids_get"></a>ux_host_class_pima_session_ids_get

**Icona** ![ di Icona di Get dell'ID di archiviazione Pima della classe host](./media/user-guide/usbx-events/image148.png)

**Descrizione**

Questo evento rappresenta un evento di Get dell'ID di archiviazione Pima della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo NFO 2: Array ID archiviazione.
- Informazioni campo 3: lunghezza ID archiviazione.
Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-storage-info-get"></a>Classe host-informazioni di archiviazione Pima Get 

#### <a name="ux_host_class_pima_storage_info_get"></a>ux_host_class_pima_storage_info_get

**Icona** ![ di Icona di informazioni di archiviazione per la classe host Pima](./media/user-guide/usbx-events/image149.png)

**Descrizione**

Questo evento rappresenta un evento USBX di archiviazione di informazioni di archiviazione Pima della classe host.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: ID archiviazione.
- Campo informazioni 3: archiviazione.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-thumb-get"></a>Classe host Pima Thumb Get 

#### <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

**Icona** ![ di Icona della classe host Pima Thumb Get](./media/user-guide/usbx-events/image150.png)

**Descrizione**

Questo evento rappresenta l'inaccettazione di una connessione al server TCP tramite nx_tcp_server_socket_unaccept.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: handle dell'oggetto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-pima-write"></a>Classe host scrittura Pima 

#### <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

**Icona** ![ di Icona di scrittura della classe host Pima](./media/user-guide/usbx-events/image151.png)

**Descrizione**

Questo evento rappresenta una classe host USBX Pima Write.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni sul campo 3: lunghezza dei dati.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-printer-activate"></a>Attivazione della stampante della classe host 

#### <a name="ux_host_class_printer_activate"></a>ux_host_class_printer_activate

**Icona** ![ di Icona di attivazione della stampante della classe host](./media/user-guide/usbx-events/image152.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione della stampante della classe host USBX.

**Campi informazioni**

- Info Field 1: puntatore all'istanza IP.
- Informazioni sul campo 2: puntatore al socket.
- Informazioni sul campo 3: tipo di servizio.
- Informazioni sul campo 4: dimensioni della finestra di ricezione.

### <a name="host-class-printer-deactivate"></a>Disattivazione della stampante della classe host 

#### <a name="ux_host_class_printer_deactivate"></a>ux_host_class_printer_deactivate

**Icona** ![ di Icona di disattivazione della stampante della classe host](./media/user-guide/usbx-events/image153.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione della stampante della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-printer-name-get"></a>Nome della stampante della classe host Get 

#### <a name="ux_host_class_printer_name_get"></a>ux_host_class_printer_name_get

**Icona** ![ di Icona di visualizzazione del nome della stampante della classe host](./media/user-guide/usbx-events/image154.png)

**Descrizione**

Questo evento rappresenta un evento Get della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-printer-read"></a>Lettura stampante classe host 

#### <a name="ux_host_class_printer_read"></a>ux_host_class_printer_read

**Icona** ![ di Icona di lettura della stampante della classe host](./media/user-guide/usbx-events/image155.png)

**Descrizione**

Questo evento rappresenta un evento di lettura della stampante della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-printer-soft-reset"></a>Ripristino soft della stampante della classe host 

#### <a name="ux_host_class_printer_soft_reset"></a>ux_host_class_printer_soft_reset

**Icona** ![ di Icona di ripristino soft della stampante della classe host](./media/user-guide/usbx-events/image156.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione del software della stampante della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-printer-status-get"></a>Stato della stampante della classe host Get 

#### <a name="ux_host_class_printer_status_get"></a>ux_host_class_printer_status_get

**Icona** ![ di Icona di Get dello stato della stampante della classe host](./media/user-guide/usbx-events/image157.png)

**Descrizione**

Questo evento rappresenta un evento Get dello stato della stampante della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: stato della stampante.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-printer-write"></a>Scrittura della stampante della classe host 

#### <a name="ux_host_class_printer_write"></a>ux_host_class_printer_write

**Icona** ![ di Icona di scrittura della stampante della classe host](./media/user-guide/usbx-events/image158.png)

**Descrizione**

Questo evento rappresenta una scrittura della stampante della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-activate"></a>Attivazione prolifica della classe host 

#### <a name="ux_host_class_prolific_activate"></a>ux_host_class_prolific_activate 

**Icona** ![ di Icona di attivazione della classe host Prolific](./media/user-guide/usbx-events/image159.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione prolifico della classe host USBX.

**Campi informazioni** 

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-deactivate"></a>Disattivazione della classe host 

#### <a name="ux_host_class_prolific_deactivate"></a>ux_host_class_prolific_deactivate 

**Icona** ![ di Icona di disattivazione della classe host](./media/user-guide/usbx-events/image160.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione prolifico della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-abort-in-pipe"></a>Classe host-interruzioni IOCTL in pipe 

#### <a name="ux_host_class_prolific_ioctl_abort_in_pipe"></a>ux_host_class_prolific_ioctl_abort_in_pipe

**Icona** ![ di Icona della classe host I/O per le interruzioni in pipe](./media/user-guide/usbx-events/image161.png)

**Descrizione**

Questo evento rappresenta una classe host USBX prolifica IOCTL Abort nell'evento pipe.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-abort-out-pipe"></a>Classe host-Interrompi IOCTL interruzione pipe 

#### <a name="ux_host_class_prolific_ioctl_abort_out_pipe"></a>ux_host_class_prolific_ioctl_abort_out_pipe

**Icona** ![ di Icona della classe host Prolific I O C T interrompe la pipe](./media/user-guide/usbx-events/image162.png)

**Descrizione**

Questo evento rappresenta una classe host USBX per l'evento di pipe Abort Abort.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-get-device-status"></a>Classe host prolifico IOCTL ottenere lo stato del dispositivo 

#### <a name="ux_host_class_prolific_ioctl_get_device_status"></a>ux_host_class_prolific_ioctl_get_device_status

**Icona** ![ di Icona dello stato del dispositivo per la classe host Prolific I O C T](./media/user-guide/usbx-events/image163.png)

**Descrizione**

Questo evento rappresenta una classe host USBX che prolifico IOCTL ottiene un evento di stato del dispositivo.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: stato del dispositivo.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-get-line-coding"></a>Classe host prolifico IOCTL Get line codifica 

#### <a name="ux_host_class_prolific_ioctl_get_line_coding"></a>ux_host_class_prolific_ioctl_get_line_coding

**Icona** ![ di Icona della codifica della riga per la classe host Prolific I O C](./media/user-guide/usbx-events/image164.png)

**Descrizione**

Questo evento rappresenta una classe host USBX prolifico IOCTL ottenere un evento di codifica della riga.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-purge"></a>Classe host-ripulitura IOCTL 

#### <a name="ux_host_class_prolific_ioctl_purge"></a>ux_host_class_prolific_ioctl_purge

**Icona** ![ di Icona per la ripulitura IOCTL della classe host](./media/user-guide/usbx-events/image165.png)

**Descrizione**

Questo evento rappresenta una classe host USBX prolifico evento IOCTL Purge.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-report-device"></a>Classe host-dispositivo di report IOCTL prolifico 

#### <a name="ux_host_class_prolific_ioctl_report_device"></a>ux_host_class_prolific_ioctl_report_device

**Icona** ![ di Icona del dispositivo di report I O C di classe host Prolific](./media/user-guide/usbx-events/image166.png)

**Descrizione**

Questo evento rappresenta un evento di modifica dello stato del dispositivo di report IOCTL per la classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-send-break"></a>Classe host prolifico invio di IOCTL 

#### <a name="ux_host_class_prolific_ioctl_send_break"></a>ux_host_class_prolific_ioctl_send_break

**Icona** ![ di Icona di invio della classe host Prolific I O C T](./media/user-guide/usbx-events/image167.png)

**Descrizione**

Questo evento rappresenta una classe host USBX prolifico evento di invio di interruzioni IOCTL.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-set-line-coding"></a>Codifica della riga del set IOCTL della classe host 

#### <a name="ux_host_class_prolific_ioctl_set_line_coding"></a>ux_host_class_prolific_ioctl_set_line_coding

**Icona** ![ di Icona del codice a linee set di classe host Prolific I O C T L](./media/user-guide/usbx-events/image168.png)

**Descrizione**

Questo evento rappresenta una classe host USBX, un evento di codifica della riga set IOCTL.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-ioctl-set-line-state"></a>Stato della riga set IOCTL della classe host Prolific 

#### <a name="ux_host_class_prolific_ioctl_set_line_state"></a>ux_host_class_prolific_ioctl_set_line_state

**Icona** ![ di Icona dello stato della linea di impostazione della classe host Prolific I O C T](./media/user-guide/usbx-events/image169.png)

**Descrizione**

Questo evento rappresenta un evento di stato riga set IOCTL per la classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: parametro.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-read"></a>Lettura prolifica classe host 

#### <a name="ux_host_class_prolific_read"></a>ux_host_class_prolific_read

**Icona** ![ di Icona lettura prolifica classe host](./media/user-guide/usbx-events/image170.png)

**Descrizione**

Questo evento rappresenta un evento di lettura prolifico della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-reception-start"></a>Inizio della ricezione prolifico della classe host 

#### <a name="ux_host_class_prolific_reception_start"></a>ux_host_class_prolific_reception_start

**Icona** ![ di Icona di inizio della ricezione prolifico della classe host](./media/user-guide/usbx-events/image171.png)

**Descrizione**

Questo evento rappresenta un evento di avvio della ricezione prolifico della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-reception-stop"></a>Arresto della ricezione della classe host Prolific 

#### <a name="ux_host_class_prolific_reception_stop"></a>ux_host_class_prolific_reception_stop

**Icona** ![ di Icona di arresto della ricezione della classe host Prolific](./media/user-guide/usbx-events/image172.png)

**Descrizione**

Questo evento rappresenta un evento di arresto della ricezione prolifico della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-prolific-write"></a>Scrittura prolifica della classe host 

#### <a name="ux_host_class_prolific_write"></a>ux_host_class_prolific_write

**Icona** ![ di Icona di scrittura della classe host Prolific](./media/user-guide/usbx-events/image173.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura prolifico della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: puntatore dati.
- Informazioni campo 3: lunghezza richiesta.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-activate"></a>Attivazione dell'archiviazione della classe host 

#### <a name="ux_host_class_storage_activate"></a>ux_host_class_storage_activate

**Icona** ![ di Icona di attivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image174.png)

**Descrizione**

Questo evento rappresenta un evento di attivazione dell'archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-deactivate"></a>Disattivazione dell'archiviazione della classe host 

#### <a name="ux_host_class_storage_deactivate"></a>ux_host_class_storage_deactivate

**Icona** ![ di Icona di disattivazione dell'archiviazione della classe host](./media/user-guide/usbx-events/image175.png)

**Descrizione**

Questo evento rappresenta un evento di disattivazione dell'archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-media-capacity-get"></a>Capacità del supporto di archiviazione della classe host Get 

#### <a name="ux_host_class_storage_media_capacity_get"></a>ux_host_class_storage_media_capacity_get

**Icona** ![ di Icona Ottieni capacità supporto di archiviazione classe host](./media/user-guide/usbx-events/image176.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento della capacità del supporto di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-media-format-capacity-get"></a>Classe host capacità formato supporti di archiviazione Get

#### <a name="ux_host_class_storage_media_format_capacity_get"></a>ux_host_class_storage_media_format_capacity_get

**Icona** ![ di Icona per la capacità del formato del supporto di archiviazione della classe host](./media/user-guide/usbx-events/image177.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento della capacità del formato multimediale di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

#### <a name="host-class-storage-media-mount"></a>Montaggio dei supporti di archiviazione della classe host 

#### <a name="ux_host_class_storage_media_mount"></a>ux_host_class_storage_media_mount

**Icona** ![ di Icona di montaggio dei supporti di archiviazione della classe host](./media/user-guide/usbx-events/image178.png)

**Descrizione**

Questo evento rappresenta un evento di montaggio dei supporti di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: settore.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-media-open"></a>Supporto di archiviazione della classe host aperto 

#### <a name="ux_host_class_storage_media_open"></a>ux_host_class_storage_media_open

**Icona** ![ di Icona Apri supporto di archiviazione classe host](./media/user-guide/usbx-events/image179.png)

**Descrizione**

Questo evento rappresenta un evento di apertura del supporto di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: supporto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-media-read"></a>Lettura supporti di archiviazione classe host 

#### <a name="ux_host_class_storage_media_read"></a>ux_host_class_storage_media_read

**Icona** ![ di Icona lettura supporti di archiviazione classe host](./media/user-guide/usbx-events/image180.png)

**Descrizione**

Questo evento rappresenta un evento di lettura del supporto di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: inizio settore.
- Informazioni sul campo 3: conteggio settori.
- Informazioni sul campo 4: puntatore dati.

### <a name="host-class-storage-media-write"></a>Scrittura dei supporti di archiviazione della classe host 

#### <a name="ux_host_class_storage_media_write"></a>ux_host_class_storage_media_write

**Icona** ![ di Icona Scrivi supporto di archiviazione classe host](./media/user-guide/usbx-events/image181.png)

**Descrizione**

Questo evento rappresenta un evento di scrittura del supporto di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: inizio settore.
- Informazioni sul campo 3: conteggio settori.
- Informazioni sul campo 4: puntatore dati.

### <a name="host-class-storage-request-sense"></a>Rilevamento delle richieste di archiviazione della classe host 

#### <a name="ux_host_class_storage_request_sense"></a>ux_host_class_storage_request_sense

**Icona** ![ di Icona del rilevamento della richiesta di archiviazione della classe host](./media/user-guide/usbx-events/image182.png)

**Descrizione**

Questo evento rappresenta un evento del senso della richiesta di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-start-stop"></a>Avvio arresto archiviazione classe host 

#### <a name="ux_host_class_storage_start_stop"></a>ux_host_class_storage_start_stop

**Icona** ![ di Icona di avvio dell'archiviazione della classe host](./media/user-guide/usbx-events/image183.png)

**Descrizione**

Questo evento rappresenta un evento di inizio arresto dell'archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Informazioni sul campo 2: avviare il segnale di arresto.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-class-storage-unit-ready-test"></a>Test pronto unità di archiviazione classe host 

#### <a name="ux_host_class_storage_unit_ready_test"></a>ux_host_class_storage_unit_ready_test

**Icona** ![ di Icona del test pronto per l'unità di archiviazione della classe host](./media/user-guide/usbx-events/image184.png)

**Descrizione**

Questo evento rappresenta un evento di test dell'unità di archiviazione della classe host USBX.

**Campi informazioni**

- Campo informazioni 1: istanza della classe.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-class-instance-create"></a>Creazione istanza Classe stack host 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Icona** ![ di Icona di creazione dell'istanza della classe Stack host](./media/user-guide/usbx-events/image185.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza della classe dello stack host USBX.

**Campi informazioni**

- Informazioni campo 1: classe.
- Campo informazioni 2: istanza della classe.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-class-instance-destroy"></a>Eliminazione istanza Classe stack host 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Icona** ![ di Icona di eliminazione istanza Classe stack host](./media/user-guide/usbx-events/image186.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'istanza della classe dello stack host USBX.

**Campi informazioni**

- Informazioni campo 1: classe.
- Campo informazioni 2: istanza della classe.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-configuration-delete"></a>Eliminazione della configurazione dello stack host 

#### <a name="ux_host_class_configuration_delete"></a>ux_host_class_configuration_delete

**Icona** ![ di Icona di eliminazione della configurazione dello stack host](./media/user-guide/usbx-events/image187.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione della configurazione dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: configurazione.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-configuration-enumerate"></a>Enumerazione della configurazione dello stack host 

#### <a name="ux_host_stack_configuration_enumerate"></a>ux_host_stack_configuration_enumerate

**Icona** ![ di Icona di enumerazione della configurazione dello stack host](./media/user-guide/usbx-events/image188.png)

**Descrizione**

Questo evento rappresenta un evento di enumerazione della configurazione dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="stack-configuration-instance-create"></a>Creazione dell'istanza di configurazione dello stack 

#### <a name="ux_host_stack_configuration_instance_create"></a>ux_host_stack_configuration_instance_create

**Icona** ![ di Icona di creazione dell'istanza di configurazione dello stack](./media/user-guide/usbx-events/image189.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza di configurazione dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: configurazione.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-configuration-instance-delete"></a>Eliminazione dell'istanza di configurazione dello stack host 

#### <a name="ux_host_stack_configuration_instance_delete"></a>ux_host_stack_configuration_instance_delete

**Icona** ![ di Icona di eliminazione dell'istanza di configurazione dello stack host](./media/user-guide/usbx-events/image190.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'istanza di configurazione dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: configurazione.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-configuration-set"></a>Set di configurazione dello stack host 

#### <a name="ux_host_stack_configuration_set"></a>ux_host_stack_configuration_set

**Icona** ![ di Icona del set di configurazione dello stack host](./media/user-guide/usbx-events/image191.png)

**Descrizione**

Questo evento rappresenta un evento del set di configurazione dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: configurazione.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-device-address-set"></a>Set di indirizzi dispositivo stack host 

#### <a name="ux_host_stack_device_address_set"></a>ux_host_stack_device_address_set

**Icona** ![ di Icona del set di indirizzi del dispositivo dello stack host](./media/user-guide/usbx-events/image192.png)

**Descrizione**

Questo evento rappresenta un evento del set di indirizzi del dispositivo dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Informazioni sul campo 2: indirizzo del dispositivo.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-device-configuration-get"></a>Get configurazione dispositivo stack host 

#### <a name="ux_host_stack_device_configuration_get"></a>ux_host_stack_device_configuration_get

**Icona** ![ di Icona get configurazione dispositivo stack host](./media/user-guide/usbx-events/image193.png)

**Descrizione**

Questo evento rappresenta un evento di ottenimento della configurazione del dispositivo dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo NFO 2: configurazione.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-device-configuration-select"></a>Selezione configurazione dispositivo stack host 

#### <a name="ux_host_stack_device_configuration_select"></a>ux_host_stack_device_configuration_select

**Icona** ![ di Icona di selezione configurazione dispositivo stack host](./media/user-guide/usbx-events/image194.png)

**Descrizione**

Questo evento rappresenta un evento di selezione della configurazione del dispositivo dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: configurazione.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-device-descriptor-read"></a>Lettura descrittore dispositivo stack host 

#### <a name="ux_host_stack_device_descriptor_read"></a>ux_host_stack_device_descriptor_read

**Icona** ![ di Icona di lettura del descrittore del dispositivo dello stack host](./media/user-guide/usbx-events/image195.png)

**Descrizione**

Questo evento rappresenta un evento di lettura del descrittore di dispositivo dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-device-get"></a>Get del dispositivo dello stack host 

#### <a name="ux_host_stack_device_get"></a>ux_host_stack_device_get

**Icona** ![ di Icona Ottieni dispositivo stack host](./media/user-guide/usbx-events/image196.png)

**Descrizione**

Questo evento rappresenta un evento di Get del dispositivo dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: Indice del dispositivo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-device-remove"></a>Rimozione dispositivo stack host 

#### <a name="ux_host_stack_device_remove"></a>ux_host_stack_device_remove

**Icona** ![ di Icona Rimuovi dispositivo stack host](./media/user-guide/usbx-events/image197.png)

**Descrizione**

Questo evento rappresenta un evento di rimozione del dispositivo dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: HCD.
- Campo informazioni 2: padre.
- Campo informazioni 3: Indice porta.
- Informazioni sul campo 4: dispositivo.

### <a name="host-stack-device-resource-free"></a>Risorsa dispositivo stack host disponibile 

#### <a name="ux_host_stack_device_resource_free"></a>ux_host_stack_device_resource_free

**Icona** ![ di Icona della risorsa del dispositivo dello stack host](./media/user-guide/usbx-events/image198.png)

**Descrizione**

Questo evento rappresenta un evento di risorsa del dispositivo stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-endpoint-instance-create"></a>Creazione dell'istanza dell'endpoint dello stack host 

#### <a name="ux_host_stack_endpoint_instance_create"></a>ux_host_stack_endpoint_instance_create

**Icona** ![ di Icona di creazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image199.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza dell'endpoint dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-endpoint-instance-delete"></a>Eliminazione dell'istanza dell'endpoint dello stack host 

#### <a name="ux_host_stack_endpoint_instance_delete"></a>ux_host_stack_endpoint_instance_delete

**Icona** ![ di Icona di eliminazione dell'istanza dell'endpoint dello stack host](./media/user-guide/usbx-events/image200.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'istanza dell'endpoint dello stack host USBX.

**Campi informazioni**

- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-endpoint-reset"></a>Reimpostazione dell'endpoint dello stack host 

#### <a name="ux_host_stack_endpoint_reset"></a>ux_host_stack_endpoint_reset

**Icona** ![ di Icona di reimpostazione dell'endpoint dello stack host](./media/user-guide/usbx-events/image201.png)

**Descrizione**

Questo evento rappresenta un evento di reimpostazione dell'endpoint dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-endpoint-transfer-abort"></a>Interruzione trasferimento endpoint stack host 

#### <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

**Icona** ![ di Icona di interruzione del trasferimento dell'endpoint dello stack host](./media/user-guide/usbx-events/image202.png)

**Descrizione**

Questo evento rappresenta un evento di interruzione del trasferimento dell'endpoint dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: endpoint.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-host-controller-register"></a>Registro del controller host dello stack host 

#### <a name="ux_host_stack_hcd_register"></a>ux_host_stack_hcd_register

**Icona** ![ di Icona registro del controller host dello stack host](./media/user-guide/usbx-events/image203.png)

**Descrizione**

Questo evento rappresenta un registro del controller host dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: nome HCD.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-initialize"></a>Inizializzazione stack host 

#### <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

**Icona** ![ di Icona di inizializzazione dello stack host](./media/user-guide/usbx-events/image204.png)

**Descrizione**

Questo evento rappresenta un evento di inizializzazione dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-interface-endpoint-get"></a>Ottenere l'endpoint dell'interfaccia dello stack host 

#### <a name="interface_-tcp-retry-entry"></a>Interface_ immissione tentativi TCP

**Icona** ![ di Icona Ottieni endpoint interfaccia stack host](./media/user-guide/usbx-events/image205.png)

**Descrizione**

Questo evento rappresenta un evento di ripetizione NetX TCP interno.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: Indice endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-interface-instance-create"></a>Creazione istanza interfaccia stack host 

#### <a name="ux_host_stack_interface_instance_create"></a>ux_host_stack_interface_instance_create

**Icona** ![ di Icona di creazione dell'istanza dell'interfaccia dello stack host](./media/user-guide/usbx-events/image206.png)

**Descrizione**

Questo evento rappresenta un evento di creazione dell'istanza dell'interfaccia dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-interface-instance-delete"></a>Eliminazione istanza interfaccia stack host 

#### <a name="ux_host_stack_interface_instance_delete"></a>ux_host_stack_interface_instance_delete

**Icona** ![ di Icona di eliminazione istanza interfaccia stack host](./media/user-guide/usbx-events/image207.png)

**Descrizione**

Questo evento rappresenta un evento di eliminazione dell'istanza dell'interfaccia dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-interface-set"></a>Set di interfacce dello stack host 

#### <a name="ux_host_stack_interface_set"></a>ux_host_stack_interface_set

**Icona** ![ di Icona del set di interfacce dello stack host](./media/user-guide/usbx-events/image208.png)

**Descrizione**

Questo evento rappresenta un evento set dell'interfaccia dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-interface-setting-select"></a>Impostazione dell'interfaccia dello stack host Select 

#### <a name="ux_host_stack_interface_setting_select"></a>ux_host_stack_interface_setting_select

**Icona** ![ di Icona di selezione dell'impostazione dell'interfaccia dello stack host](./media/user-guide/usbx-events/image209.png)

**Descrizione**

Questo evento rappresenta un'impostazione dell'evento Select dell'interfaccia dello stack host USBX.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-new-configuration-create"></a>Creazione della nuova configurazione dello stack host 

#### <a name="ux_host_stack_new_configuration_create"></a>ux_host_stack_new_configuration_create

**Icona** ![ di Icona di creazione nuova configurazione dello stack host](./media/user-guide/usbx-events/image210.png)

**Descrizione**
 
Questo evento rappresenta uno stack host USBX nuovo evento di creazione della configurazione.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: configurazione.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-new-device-create"></a>Stack host creazione nuovo dispositivo 

#### <a name="ux_host_stack_new_device_create"></a>ux_host_stack_new_device_create

**Icona** ![ di Icona di creazione nuovo dispositivo dello stack host](./media/user-guide/usbx-events/image211.png)

**Descrizione**
 
 Questo evento rappresenta un nuovo evento di creazione del dispositivo di stack host USBX.

**Campi informazioni**

- Campo informazioni 1: HCD.
- Informazioni sul campo 2: proprietario del dispositivo.
- Campo informazioni 3: Indice porta.
- Informazioni sul campo 4: dispositivo.

### <a name="host-stack-new-endpoint-create"></a>Creazione di un nuovo endpoint dello stack host 

#### <a name="ux_host_stack_new_endpoint_create"></a>ux_host_stack_new_endpoint_create

**Icona** ![ di Icona di creazione nuovo endpoint dello stack host](./media/user-guide/usbx-events/image212.png)

**Descrizione**
 
Questo evento rappresenta uno stack host USBX nuovo evento di creazione endpoint.

**Campi informazioni**

- Informazioni sul campo 1: interfaccia.
- Campo informazioni 2: endpoint.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-root-hub-change-process"></a>Processo di modifica dell'hub radice dello stack host 

#### <a name="ux_host_stack_rh_change_process"></a>ux_host_stack_rh_change_process

**Icona** ![ di Icona del processo di modifica dell'hub radice dello stack host](./media/user-guide/usbx-events/image213.png)

**Descrizione**
 
Questo evento rappresenta un processo di modifica dell'hub radice dello stack host USBX.

**Campi informazioni**

- Info Field 1: Port index.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-root-hub-device-extraction"></a>Estrazione dispositivo hub radice stack host 

#### <a name="ux_host_stack_rh_device_extraction"></a>ux_host_stack_rh_device_extraction

**Icona** ![ di Icona di estrazione dispositivo hub radice dello stack host](./media/user-guide/usbx-events/image214.png)

**Descrizione**

Questo evento rappresenta un evento di estrazione del dispositivo dell'hub radice dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: HCD.
- Informazioni sul campo 2: Indice porta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-root-hub-device-insertion"></a>Inserimento dispositivo hub radice stack host 

#### <a name="ux_host_stack_rh_device_insertion"></a>ux_host_stack_rh_device_insertion

**Icona** ![ di Icona di inserimento dispositivo hub radice stack host](./media/user-guide/usbx-events/image215.png)

**Descrizione**

Questo evento rappresenta l'inserimento di un dispositivo hub radice dello stack host USBX.

**Campi informazioni**

- Campo informazioni 1: HCD.
- Informazioni sul campo 2: Indice porta.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-transfer-request"></a>Richiesta di trasferimento dello stack host 

#### <a name="ux_host_stack_transfer_request"></a>ux_host_stack_transfer_request

**Icona** ![ di Icona della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image216.png)

**Descrizione**

Questo evento rappresenta una richiesta di trasferimento dello stack dell'host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: endpoint.
- Campo informazioni 3: richiesta di trasferimento.
- Campo informazioni 4: non utilizzato.

### <a name="host-stack-transfer-request-abort"></a>Interruzione richiesta trasferimento stack host 

#### <a name="internal-io-driver-get-status"></a>Stato Get driver I/O interno

**Icona** ![ di Icona di interruzione della richiesta di trasferimento dello stack host](./media/user-guide/usbx-events/image217.png)

**Descrizione**

Questo evento rappresenta un'interruzione della richiesta di trasferimento dello stack dell'host USBX.

**Campi informazioni**

- Informazioni sul campo 1: dispositivo.
- Campo informazioni 2: endpoint.
- Campo informazioni 3: richiesta di trasferimento.
- Campo informazioni 4: non utilizzato.

### <a name="usbx-error"></a>Errore USBX 

#### <a name="ux_error"></a>ux_error

**Icona** ![ di Icona di errore U S B X](./media/user-guide/usbx-events/image218.png)

**Descrizione**

Questo evento rappresenta un evento di errore USBX.

**Campi informazioni**

- Campo informazioni 1: errore USBX.
- Informazioni sul campo 2: nome dell'errore.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.