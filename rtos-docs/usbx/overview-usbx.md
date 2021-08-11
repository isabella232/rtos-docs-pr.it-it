---
title: Informazioni Azure RTOS USBX
description: Azure RTOS USBX è un host USB ad alte prestazioni, un dispositivo e uno stack incorporato (OTG), Azure RTOS USBX è completamente integrato con Azure RTOS ThreadX e disponibile per tutti i processori supportati da Azure RTOS ThreadX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 8950e7573bf705feb16de6ac1adb5f55559ea4b04b453944c5a24baddc6ae7b9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791449"
---
# <a name="overview-of-azure-rtos-usbx"></a>Panoramica di Azure RTOS USBX

Azure RTOS USBX è un host, un dispositivo e uno stack incorporato OTG (On-the-Go) USB ad alte prestazioni. Azure RTOS USBX è completamente integrato con Azure RTOS ThreadX ed è disponibile per tutti i processori supportati da ThreadX. Come ThreadX, Azure RTOS USBX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per applicazioni con incorporata profonda che richiedono un'interfaccia con dispositivi USB.

## <a name="host-device-otg--extensive-class-support"></a>Supporto completo per host, dispositivo, & OTG

Azure RTOS stack di protocolli USB incorporato per host/dispositivo USBX è una soluzione USB incorporata di livello industriale progettata specificamente per applicazioni IoT, real-time e deep embedded. Azure RTOS USBX offre supporto per host, dispositivi e OTG, oltre a un ampio supporto per le classi. Azure RTOS USBX è completamente integrato con il sistema operativo ThreadX Real-Time, gli stack TCP/IP incorporati Azure RTOS FileX file system, Azure RTOS NetX e Azure RTOS NetX Duo incorporati. Tutto questo, combinato con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTOS USBX la scelta ideale per le applicazioni IoT incorporate più complesse che richiedono connettività USB.

### <a name="usbx-memory-footprint"></a>Footprint di memoria USBX

Azure RTOS USBX ha un footprint minimo notevolmente ridotto di 10,5 KB di FLASH e 5,1 KB di RAM per Azure RTOS supporto CDC/ACM del dispositivo USBX. Azure RTOS host USBX richiede almeno 18 KB di FLASH e 25 KB di RAM per il supporto CDC/ACM.

Per la funzionalità TCP sono necessari da 10 a 13 KB aggiuntivi di memoria dell'area di istruzioni. Azure RTOS utilizzo della RAM USBX varia in genere da 2,6 KB a 3,6 KB più la memoria del pool di pacchetti, definita dall'applicazione.

Analogamente a ThreadX, le dimensioni di Azure RTOS USBX vengono ridimensionate automaticamente in base ai servizi effettivamente usati dall'applicazione. Questo elimina virtualmente la necessità di parametri di configurazione e compilazione complessi, semplificando le operazioni per lo sviluppatore.

### <a name="usb-interoperability-verification"></a>Verifica dell'interoperabilità USB

Azure RTOS stack di dispositivi USBX è stato rigorosamente testato con lo strumento di test standard USB IF USBCV per garantire la conformità completa con le specifiche USB e l'interoperabilità con sistemi host diversi.
Inoltre, Azure RTOS stack OTG USBX è stato verificato e certificato dal lab di test indipendente Allion in Taiwan.

### <a name="usb-host-controller-support"></a>Supporto del controller host USB

Azure RTOS USBX supporta i principali standard USB, ad esempio OHCI e EHCI. Inoltre, Azure RTOS USBX supporta controller host USB discreti proprietari di Atmel, Microchip, Philips, Renesas, ST, TI e altri fornitori. Azure RTOS USBX supporta anche più controller host nella stessa applicazione.
Il controller del dispositivo USB Azure RTOS USBX supporta i controller di dispositivo USB più diffusi di dispositivi analoghi, Atmel, Microchip, NXP, Philips, Renesas, ST, TI e altri fornitori.

### <a name="extensive-host-class-support"></a>Supporto completo delle classi host

Azure RTOS host USBX offre il supporto per le classi più comuni, tra cui ASIX, AUDIO, CDC/ACM, CDC/ECM, GSER, HID (tastiera, mouse e controllo remoto), HUB, PIMA (PTP/MTP), PRINTER, PROLIFIC e STORAGE.

### <a name="extensive-usb-device-class-support"></a>Supporto completo della classe di dispositivi USB

Azure RTOS dispositivo USBX offre supporto per le classi più comuni, tra cui CDC/ACM, CDC/ECM, DFU, HID, PIMA (PTP/MTP) (w/MTP), RNDIS e STORAGE. È disponibile anche il supporto per le classi personalizzate.

### <a name="pictbridge-support"></a>Supporto di Pictbridge

Azure RTOS USBX supporta l'implementazione completa di Pictbridge sia nell'host che nel dispositivo. Pictbridge si trova sopra Azure RTOS classe USBX PIMA (PTP/MTP) su entrambi i lati. Lo standard PictBridge consente la connessione di una fotocamera digitale o di uno smart phone direttamente a una stampante senza PC, consentendo la stampa diretta a determinate stampanti in grado di riconoscere Pictbridge. Quando una fotocamera o un telefono è connesso a una stampante, la stampante è l'host USB e la fotocamera è il dispositivo USB. Tuttavia, con Pictbridge, la fotocamera apparirà come l'host e i comandi vengono guidati dalla fotocamera. La fotocamera è il server di archiviazione, la stampante del client di archiviazione. La fotocamera è il client di stampa e la stampante è ovviamente il server di stampa. Pictbridge usa USB come livello di trasporto, ma si basa su PTP (Picture Transfer Protocol) per il protocollo di comunicazione.

### <a name="custom-class-support"></a>Supporto delle classi personalizzate

Azure RTOS host USBX e Dispositivo supportano classi personalizzate. Un esempio di classe personalizzata è disponibile nella distribuzione Azure RTOS USBX. Questa semplice data pump è denominata DPUMP e può essere usata come modello per le classi di applicazione personalizzate.
La tecnologia avanzata Azure RTOS host USBX e il dispositivo supportano classi personalizzate. Un esempio di classe personalizzata è disponibile nella distribuzione Azure RTOS USBX. Azure RTOS USBX è una tecnologia avanzata che include:

* Supporto di host, dispositivi e OTG
* Supporto USB basso, pieno e ad alta velocità
* Scalabilità automatica
* Completamente integrato con ThreadX, Azure RTOS FileX e Azure RTOS NetX
* Metriche delle prestazioni facoltative
* Azure RTOS di analisi del sistema TraceX

## <a name="azure-rtos-usbx-apis"></a>Azure RTOS API USBX

### <a name="azure-rtos-usbx-host-api"></a>Azure RTOS'API host USBX

L Azure RTOS'API host USBX è un'API intuitiva e coerente, seguendo una convenzione di denominazione sostantivo-verbo. Tutte le API hanno ux_host_* per identificarsi facilmente come USBX. Qualsiasi API di blocco ha un timeout del thread facoltativo.

* ASIX
    - Minimo 0,3 KB FLASH, 4 KB di RAM
    - Ridimensionamento automatico Trace a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX nel formato seguente: *ux_host_class_asix_**
* AUDIO
    - Minimo 1,2 KB FLASH, 4 KB di RAM
    - Scalabilità automatica
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_audio_**
* CDC/ACM
    - Minimo 1,4 KB FLASH, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX nel formato seguente: *ux_host_class_cdc_acm_**
* HID
    - Minimo 0,3 KB FLASH, 4 KB di RAM
    - Tastiera, mouse e supporto remoto
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX nel formato seguente: *ux_host_class_hid_** 
* HUB
    - Minimo 1,7 KB FLASH, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_hub_**
* PIMA (PTP/MTP)
    - Minimo 0,9 KB FLASH, 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_pima_**
* Stampante
    - Minimo 0,8 KB FLASH, 8 KB di RAM
    - Scalabilità automatica
    -  Traccia a livello di sistema tramite Azure RTOS TraceX
    -  Intuitive Azure RTOS API host USBX nel formato seguente: *ux_host_class_printer_**
* Prolifico
    - Minimo 1,5 KB FLASH, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_prolific_**
* STORAG
    - Minimo 5,6 KB FLASH, 4 KB di RAM
    - Scalabilità automatica<br> Integrazione con Azure RTOS FileX
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API host USBX in questo formato: *ux_host_class_storage_**
* USB Host STACK
    - Supporta molti controller host
    - MEMORIA FLASH minima di 18 KB, 25 KB di RAM
    - Scalabilità automatica
    - Supporto per più controller host nella stessa piattaforma
    -  Supporto USB basso, pieno e ad alta velocità
    -  Traccia a livello di sistema tramite Azure RTOS TraceX
    -  Intuitive Azure RTOS API host USBX in questo formato: *ux_host_stack_* * 
* OHCI, EHCI, CONTROLLER HOST PROPRIETARI 

### <a name="azure-rtos-usbx-device-api"></a>Azure RTOS'API del dispositivo USBX

L Azure RTOS aPI dispositivo USBX è un'API intuitiva e coerente che segue una convenzione di denominazione sostantivo-verbo. Tutte le API hanno una ux_device_* per identificarsi facilmente come USBX. Le API di blocco hanno un timeout del thread facoltativo. Per altri Azure RTOS, vedere il Manuale [dell'utente dell'host USBX.](usbx-host-stack-about.md)

* CDC/ACM
    - MEMORIA FLASH minima di 0,8 KB, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_cdc_acm_**.
* CDC/ECM
    - Memoria FLASH minima da 1,5 KB, da 4 KB a 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX<br> Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_cdc_ecm_**.
* Dfu
    - MEMORIA FLASH minima di 1,1 KB, 2 KB di RAM
    -  Scalabilità automatica
    -  Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_dfu_** 
* GSER
    - MEMORIA FLASH minima di 0,6 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_gser_**
* HID
    - MEMORIA FLASH minima di 0,9 KB, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_hid_** PIMA (PTP/MTP)
    - MEMORIA FLASH minima di 5,2 KB, 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_pima_** 
* STORAGE
    - MEMORIA FLASH minima di 2,3 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_storage_**
* RNDIS
    - Memoria FLASH minima da 2,3 KB, da 4 KB a 8 KB di RAM
    - Scalabilità automatica
    - Integrato con Azure RTOS NetX e Azure RTOS NetX DUO
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_rndls_**
* Azure RTOS STACK di dispositivi USBX
    - MEMORIA FLASH minima di 2,3 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTOS TraceX
    - Intuitive Azure RTOS API del dispositivo USBX in questo formato: *ux_device_class_storage_**
* CONTROLLER host PROPRIETARI

## <a name="next-steps"></a>Passaggi successivi

Iniziare a lavorare con il Azure RTOS host USBX e lo stack di dispositivi seguendo il manuale dell'utente di [Host Stack](usbx-host-stack-about.md) o il Manuale [dell'utente di Device Stack.](usbx-device-stack-about.md)