---
title: Informazioni Azure RTOS USBX
description: Azure RTOS USBX è un host USB ad alte prestazioni, un dispositivo e uno stack incorporato (OTG), Azure RTOS USBX è completamente integrato con Azure RTOS ThreadX e disponibile per tutti i processori supportati da Azure RTOS ThreadX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 3c214a49f7dd1af20c20f07412fb072dd785b16f
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754829"
---
# <a name="overview-of-azure-rtos-usbx"></a>Panoramica di Azure RTOS USBX

Azure RTOS USBX è un host USB ad alte prestazioni, un dispositivo e uno stack incorporato OTG (On-the-Go). Azure RTOS USBX è completamente integrato con Azure RTOS ThreadX ed è disponibile per tutti i processori supportati da ThreadX. Analogamente a ThreadX, Azure RTOS USBX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni con deep embedded che richiedono un'interfaccia con dispositivi USB.

## <a name="host-device-otg--extensive-class-support"></a>Supporto completo per host, dispositivi & OTG

Azure RTOS stack di protocolli USB incorporato usb host/dispositivo USB è una soluzione USB incorporata di livello industriale progettata specificamente per applicazioni IoT, in tempo reale e con deep embedded. Azure RTOS USBX offre supporto per host, dispositivi e OTG, nonché supporto completo per le classi. Azure RTOS USBX è completamente integrato con il sistema operativo ThreadX Real-Time, gli stack TCP/IP incorporati Azure RTOS FileX file system, Azure RTOS NetX e Azure RTOS NetX Duo incorporati. Tutto questo, in combinazione con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rende Azure RTOS USBX la scelta ideale per le applicazioni IoT incorporate più complesse che richiedono la connettività USB.

### <a name="usbx-memory-footprint"></a>Footprint della memoria USBX

Azure RTOS USBX ha un footprint minimo notevolmente ridotto di 10,5 KB di MEMORIA FLASH e 5,1 KB di RAM per il supporto di Azure RTOS USBX Device CDC/ACM. Azure RTOS'host USBX richiede almeno 18 KB di MEMORIA FLASH e 25 KB di RAM per il supporto CDC/ACM.

Per la funzionalità TCP sono necessari altri 10 KB o 13 KB di memoria dell'area di istruzioni. Azure RTOS'utilizzo della RAM USBX è in genere compreso tra 2,6 KB e 3,6 KB più la memoria del pool di pacchetti, definita dall'applicazione.

Analogamente a ThreadX, le dimensioni di Azure RTOS USBX vengono ridimensionate automaticamente in base ai servizi effettivamente usati dall'applicazione. Questo elimina virtualmente la necessità di parametri di configurazione e compilazione complessi, semplificando le operazioni per lo sviluppatore.

### <a name="usb-interoperability-verification"></a>Verifica dell'interoperabilità USB

Azure RTOS USBX Device Stack è stato rigorosamente testato con lo strumento di test standard USB IF USBCV per garantire la conformità completa con le specifiche USB e l'interoperabilità con sistemi host diversi.
Inoltre, Azure RTOS stack USBX OTG è stato verificato e certificato dal lab di test indipendente Allion a Taiwan.

### <a name="usb-host-controller-support"></a>Supporto del controller host USB

Azure RTOS USBX supporta i principali standard USB come OHCI e EHCI. Inoltre, Azure RTOS USBX supporta controller host USB discreti proprietari di Atmel, Microchip, Philips, Renesas, ST, TI e altri fornitori. Azure RTOS USBX supporta anche più controller host nella stessa applicazione.
Supporto del controller del dispositivo USB Azure RTOS USBX supporta i controller di dispositivo USB più diffusi da dispositivi analogici, Atmel, Microchip, NXP, Philips, Renesas, ST, TI e altri fornitori.

### <a name="extensive-host-class-support"></a>Supporto completo delle classi host

Azure RTOS'host USBX offre il supporto per le classi più comuni, tra cui ASIX, AUDIO, CDC/ACM, CDC/ECM, GSER, HID (tastiera, mouse e controllo remoto), HUB, PIMA (PTP/MTP), PRINTER, LESS E STORAGE.

### <a name="extensive-usb-device-class-support"></a>Supporto completo della classe di dispositivi USB

Azure RTOS dispositivo USBX offre il supporto per le classi più comuni, tra cui CDC/ACM, CDC/ECM, DFU, HID, PIMA (PTP/MTP) (w/MTP), RNDIS e STORAGE. È disponibile anche il supporto per le classi personalizzate.

### <a name="pictbridge-support"></a>Supporto di Pictbridge

Azure RTOS USBX supporta l'implementazione completa di Pictbridge sia nell'host che nel dispositivo. Pictbridge si trova sopra Azure RTOS classe USBX PIMA (PTP/MTP) su entrambi i lati. Lo standard PictBridge consente la connessione di una fotocamera digitale o di uno smartphone direttamente a una stampante senza PC, consentendo la stampa diretta su determinate stampanti con supporto di Pictbridge. Quando una fotocamera o un telefono è connesso a una stampante, la stampante è l'host USB e la fotocamera è il dispositivo USB. Tuttavia, con Pictbridge, la fotocamera apparirà come l'host e i comandi vengono guidati dalla fotocamera. La fotocamera è il server di archiviazione, la stampante del client di archiviazione. La fotocamera è il client di stampa e la stampante è naturalmente il server di stampa. Pictbridge usa USB come livello di trasporto, ma si basa su PTP (Picture Transfer Protocol) per il protocollo di comunicazione.

### <a name="custom-class-support"></a>Supporto delle classi personalizzate

Azure RTOS classi personalizzate di supporto per host e dispositivi USBX. Un esempio di classe personalizzata è disponibile nella Azure RTOS USBX. Questa semplice data pump è denominata DPUMP e può essere usata come modello per le classi di applicazioni personalizzate.
La tecnologia avanzata Azure RTOS host e dispositivo USBX supporta le classi personalizzate. Un esempio di classe personalizzata è disponibile nella Azure RTOS USBX. Azure RTOS USBX è una tecnologia avanzata che include:

* Supporto di host, dispositivi e OTG
* Supporto USB basso, pieno e ad alta velocità
* Scalabilità automatica
* Completamente integrato con ThreadX, Azure RTOS FileX e Azure RTOS NetX
* Metriche facoltative delle prestazioni
* Azure RTOS di analisi del sistema TraceX

## <a name="azure-rtos-usbx-apis"></a>Azure RTOS API USBX

### <a name="azure-rtos-usbx-host-api"></a>Azure RTOS'API host USBX

L Azure RTOS aPI host USBX è un'API intuitiva e coerente, che segue una convenzione di denominazione sostantivo-verbo. Tutte le API hanno una ux_host_* per identificarsi facilmente come USBX. Qualsiasi API di blocco ha un timeout del thread facoltativo.

* ASIX
    - MEMORIA FLASH minima di 0,3 KB, 4 KB di RAM
    - Ridimensionamento automatico Trace a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_asix_**
* AUDIO
    - MEMORIA FLASH minima di 1,2 KB, 4 KB di RAM
    - Scalabilità automatica
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_audio_**
* CDC/ACM
    - MEMORIA FLASH minima di 1,4 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_cdc_acm_**
* HID
    - MEMORIA FLASH minima di 0,3 KB, 4 KB di RAM
    - Tastiera, mouse e supporto remoto
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_hid_** 
* HUB
    - MEMORIA FLASH minima di 1,7 KB, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_hub_**
* PIMA (PTP/MTP)
    - MEMORIA FLASH minima di 0,9 KB, 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_pima_**
* Stampante
    - MEMORIA FLASH minima di 0,8 KB, 8 KB di RAM
    - Scalabilità automatica
    -  Traccia a livello di sistema tramite Azure RTOS TraceX
    -  Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_printer_**
* Prolifico
    - MEMORIA FLASH minima di 1,5 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_prolific_**
* STORAG
    - MEMORIA FLASH minima di 5,6 KB, 4 KB di RAM
    - Scalabilità automatica<br> Integrato con Azure RTOS FileX
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX nel formato seguente: *ux_host_class_storage_**
* USB Host STACK
    - Supporta molti controller host
    - Minimo 18 KB FLASH, 25 KB di RAM
    - Scalabilità automatica
    - Supporto per più controller host nella stessa piattaforma
    -  Supporto USB basso, pieno e ad alta velocità
    -  Traccia a livello di sistema tramite Azure RTOS TraceX
    -  Intuitive Azure RTOS API host USBX in questo formato: *ux_host_stack_* * 
* OHCI, EHCI, CONTROLLER HOST PROPRIETARI 

### <a name="azure-rtos-usbx-device-api"></a>Azure RTOS API dispositivo USBX

L Azure RTOS'API del dispositivo USBX è un'API intuitiva e coerente che segue una convenzione di denominazione sostantivo-verbo. Tutte le API dispongono di ux_device_* per identificarsi facilmente come USBX. Le API di blocco hanno un timeout del thread facoltativo. Per altre [informazioni, Azure RTOS guida dell'utente dell'host USBX.](usbx-host-stack-about.md)

* CDC/ACM
    - Minimo 0,8 KB FLASH, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX nel formato seguente: *ux_device_class_cdc_acm_**.
* CDC/ECM
    - MEMORIA FLASH minima da 1,5 KB, da 4 KB a 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX<br> Intuitive Azure RTOS api dei dispositivi USBX nel formato seguente: *ux_device_class_cdc_ecm_**.
* Dfu
    - Minimo 1,1 KB FLASH, 2 KB di RAM
    -  Scalabilità automatica
    -  Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS api dei dispositivi USBX nel formato seguente: *ux_device_class_dfu_** 
* GSER
    - Minimo 0,6 KB FLASH, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_gser_**
* HID
    - Minimo 0,9 KB FLASH, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_hid_** PIMA (PTP/MTP)
    - Minimo 5,2 KB FLASH, 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_pima_** 
* STORAGE
    - Minimo 2,3 KB FLASH, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS api dei dispositivi USBX nel formato *seguente: ux_device_class_storage_**
* RNDIS
    - MEMORIA FLASH minima da 2,3 KB, da 4 KB a 8 KB di RAM
    - Scalabilità automatica
    - Integrato con Azure RTOS NetX e Azure RTOS NetX DUO
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS api dei dispositivi USBX nel formato *seguente: ux_device_class_rndls_**
* Azure RTOS STACK di dispositivi USBX
    - Minimo 2,3 KB FLASH, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS api dei dispositivi USBX nel formato *seguente: ux_device_class_storage_**
* CONTROLLER HOST PROPRIETARI

## <a name="next-steps"></a>Passaggi successivi

Iniziare a lavorare con l'Azure RTOS host USBX e lo stack di dispositivi seguendo la Guida dell'utente di [Host Stack](usbx-host-stack-about.md) o Device Stack [User Guide](usbx-device-stack-about.md).