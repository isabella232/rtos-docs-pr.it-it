---
title: Informazioni su Azure RTO USBX
description: Azure RTO USBX è un host USB a prestazioni elevate, un dispositivo e uno stack embedded on-the-go (OTG), Azure RTO USBX è completamente integrato con Azure RTO ThreadX e disponibile per tutti i processori supportati da RTO threadX di Azure.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 87eb6ee9f8733db3201280d377aa832b87131871
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824374"
---
# <a name="overview-of-azure-rtos-usbx"></a>Panoramica di Azure RTO USBX

Azure RTO USBX è un host USB a prestazioni elevate, un dispositivo e uno stack embedded on-the-go (OTG). Azure RTO USBX è completamente integrato con Azure RTO ThreadX e disponibile per tutti i processori supportati da ThreadX. Analogamente a ThreadX, Azure RTO USBX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni con Deep embedded che richiedono un'interfaccia con i dispositivi USB.

## <a name="host-device-otg--extensive-class-support"></a>Host, Device, OTG & supporto completo per le classi

Lo stack di protocolli USB per host/dispositivo di Azure RTO USBX è una soluzione USB incorporata di livello industriale progettata specificamente per applicazioni molto incorporate e in tempo reale. Azure RTO USBX offre supporto per host, dispositivi e OTG, oltre a un supporto completo per le classi. Azure RTO USBX è completamente integrato con ThreadX Real-Time sistema operativo, Azure RTO FileX Embedded FAT file system, Azure RTO NetX e Azure RTO NetX Duo Embedded TCP/IP. Tutti questi componenti, combinati con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTO USBX la scelta ideale per le applicazioni di Internet delle cose incorporate più complesse che richiedono la connettività USB.

### <a name="small-footprint"></a>Footprint ridotto

Azure RTO USBX ha un footprint minimo ristretto di 10,5 KB di FLASH e 5,1 KB di RAM per il supporto CDC/ACM del dispositivo USBX di Azure RTO. L'host USBX di Azure RTO richiede almeno 18 KB di FLASH e 25 KB di RAM per il supporto CDC/ACM.

Per la funzionalità TCP sono necessari altri 10 KB a 13 KB di memoria per l'area di istruzione. L'utilizzo della RAM USBX di Azure RTO in genere varia da 2,6 KB a 3,6 KB oltre alla memoria del pool di pacchetti, definita dall'applicazione.

Analogamente a ThreadX, le dimensioni di Azure RTO USBX vengono ridimensionate automaticamente in base ai servizi effettivamente utilizzati dall'applicazione. In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.

### <a name="fast-execution"></a>Esecuzione rapida

Azure RTO USBX è progettato per la velocità e prevede un livello minimo di chiamata di funzione interna e il supporto per la cache e l'utilizzo DMA. Questa e una filosofia di progettazione orientata alle prestazioni generale consentono ad Azure RTO USBX di ottenere le prestazioni più veloci possibile.

### <a name="simple-easy-to-use"></a>Semplice e facile da usare

Azure RTO USBX è semplice da usare. L'API USBX di Azure RTO è intuitiva e altamente funzionale. I nomi delle API sono costituiti da parole reali e non da "zuppa alfabetica" o nomi altamente abbreviati, così comuni in altri prodotti file system. Tutte le API USBX di Azure RTO hanno un "ux_" leader e seguono una convenzione di denominazione sostantivo-verbo. Inoltre, esiste una coerenza funzionale nell'API. Tutte le API che sospendono, ad esempio, hanno un timeout facoltativo che funziona in modo identico per le API.

### <a name="usb-interoperability-verification"></a>Verifica dell'interoperabilità USB

Lo stack di dispositivi USBX di Azure RTO è stato testato rigorosamente con l'USB se lo strumento di test standard USBCV per garantire la conformità completa con le specifiche USB e l'interoperabilità con sistemi host diversi.
Inoltre, Azure RTO USBX OTG stack è stato verificato e certificato da Independent test lab Allion in Taiwan.

### <a name="usb-host-controller-support"></a>Supporto del controller host USB

Azure RTO USBX supporta gli standard USB principali come OHCI e EHCI. Inoltre, Azure RTO USBX supporta controller host USB discreti proprietari da Atmel, microchip, Philips, Renesas, ST, TI e altri fornitori. Azure RTO USBX supporta anche più controller host nella stessa applicazione.
Supporto del controller del dispositivo USB Azure RTO USBX supporta i controller di dispositivo USB più diffusi da dispositivi analoghi, Atmel, microchip, NXP, Philips, Renesas, ST, TI e altri fornitori.

### <a name="extensive-host-class-support"></a>Supporto completo per le classi host

L'host USBX di Azure RTO fornisce supporto per le classi più diffuse, tra cui ASIX, AUDIO, CDC/ACM, CDC/ECM, GSER, HID (tastiera, mouse e controllo remoto), HUB, PIMA (PTP/MTP), stampanti, PROLIFICo e archiviazione.

### <a name="extensive-usb-device-class-support"></a>Supporto esteso per le classi di dispositivi USB

Il dispositivo USBX di Azure RTO fornisce supporto per le classi più diffuse, tra cui CDC/ACM, CDC/ECM, DFU, HID, PIMA (PTP/MTP) (w/MTP), RNDIS e archiviazione. È disponibile anche il supporto per le classi personalizzate.

### <a name="pictbridge-support"></a>Supporto PictBridge

Azure RTO USBX supporta l'implementazione di PictBridge completa sia nell'host che nel dispositivo. PictBridge si trova nella parte superiore della classe Azure RTO USBX PIMA (PTP/MTP) su entrambi i lati. Lo standard PictBridge consente la connessione di una fotocamera digitale o di uno smartphone direttamente a una stampante senza PC, consentendo la stampa diretta a determinate stampanti compatibili con PictBridge. Quando una fotocamera o un telefono è connesso a una stampante, la stampante è l'host USB e la fotocamera è il dispositivo USB. Con la tecnologia PictBridge, tuttavia, la fotocamera viene visualizzata come host e i comandi vengono gestiti dalla fotocamera. La fotocamera è il server di archiviazione, ovvero la stampante il client di archiviazione. La fotocamera è il client di stampa e la stampante è naturalmente il server di stampa. PictBridge utilizza USB come livello di trasporto, ma si basa su PTP (Picture Transfer Protocol) per il protocollo di comunicazione.

### <a name="custom-class-support"></a>Supporto per classi personalizzate

L'host e il dispositivo USBX di Azure RTO supportano le classi personalizzate. Una classe personalizzata di esempio è disponibile nella distribuzione USBX di Azure RTO. Questa semplice classe di data pump è denominata DPUMP e può essere usata come modello per le classi di applicazioni personalizzate.
Tecnologia avanzata Azure RTO USBX host e dispositivi supportano le classi personalizzate. Una classe personalizzata di esempio è disponibile nella distribuzione USBX di Azure RTO. Azure RTO USBX è una tecnologia avanzata che include:

* Supporto per host, dispositivi e OTG
* Supporto USB basso, completo e ad alta velocità
* Scalabilità automatica
* Completamente integrato con ThreadX, Azure RTO FileX e Azure RTO NetX
* Metriche delle prestazioni facoltative
* Supporto per l'analisi del sistema TraceX di Azure RTO

### <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTO USBX ha un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto IP e UDP di base. Azure RTO USBX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Di conseguenza, Azure RTO USBX è una delle soluzioni USB più diffuse per i dispositivi di Internet delle cose embedded. Il nostro vantaggio di time-to-Market coerente è basato su:

* Documentazione relativa alla qualità: esaminare le guide per gli utenti dei dispositivi e degli host USBX di Azure RTO e vedere per se stessi.
* Disponibilità del codice sorgente completa
* API di facile utilizzo
* Set di funzionalità completo e avanzato

## <a name="one-simple-license"></a>Una licenza semplice

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

## <a name="full-highest-quality-source-code"></a>Codice sorgente completo di qualità elevata

Nel corso degli anni, il codice sorgente NetX di Azure RTO ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.

### <a name="supports-most-popular-architectures"></a>Supporta le architetture più diffuse

Azure RTO USBX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, inclusi i seguenti:

* **Dispositivi analoghi**: SHARC, Blackfin, CM4xx
* **Andina Core**: RISC-V
* **Ambiqmicro**: Apollo MCU
* **ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M
* **Cadenza**: Xtensa, diamante
* **CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi
* **Cypress**: RISC-V
* **Silice**: ESI-RISC
* **Infineon**: XMC1000, XMC4000, Tricore
* **Intel & Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10
* **Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32
* **Microsemi**: RISC-V
* **NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4
* **Renesas**: SH, HS, V850, RX, RZ, Synergy Silicon Labs: EFM32
* **Synopsys**: Arc 600, 700, Arc em, Arc HS
* **St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7
* **TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C
* **Wave computing**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class **Xilinx**: Microblaze, PowerPC 405, Zynq, Zynq UltraSCALE

## <a name="azure-rtos-usbx-apis"></a>API USBX di Azure RTO

### <a name="azure-rtos-usbx-host-api"></a>API host USBX di Azure RTO

L'API dell'host USBX di Azure RTO è un'API intuitiva e coerente, seguendo una convenzione di denominazione dei verbi sostantivi. Tutte le API hanno ux_host_ * per identificare facilmente come USBX. Le API di blocco hanno un timeout di thread facoltativo.

* ASIX
    - FLASH minimo 0,3 KB, 4 KB di RAM
    - Traccia automatica a livello di scalingSystem tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_asix_**
* AUDIO
    - FLASH minimo 1,2 KB, 4 KB di RAM
    - Scalabilità automatica
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_audio_**
* CDC/ACM
    - FLASH minimo 1,4 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_cdc_acm_**
* HID
    - FLASH minimo 0,3 KB, 4 KB di RAM
    - Tastiera, mouse e supporto remoto
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_hid_** 
* HUB
    - Minimo 1,7 KB di memoria, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_hub_**
* PIMA (PTP/MTP)
    - Minimo 0,9 KB di memoria, 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_pima_**
* STAMPANTE
    - Minimo 0,8 KB di memoria, 8 KB di RAM
    - Scalabilità automatica
    -  Traccia a livello di sistema tramite Azure RTO TraceX
    -  API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_printer_**
* PROLIFICO
    - FLASH minimo 1,5 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_prolific_**
* STORAG
    - FLASH minimo 5,6 KB, 4 KB di RAM
    - Scalabilità automatica<br> Integrato con Azure RTO FileX
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API host USBX di Azure RTO intuitive in questo formato: *ux_host_class_storage_**
* STACK host USB
    - Supporta molti controller host
    - FLASH minimo da 18 KB, 25 KB di RAM
    - Scalabilità automatica
    - Supporto per più controller host nella stessa piattaforma
    -  Supporto USB basso, completo e ad alta velocità
    -  Traccia a livello di sistema tramite Azure RTO TraceX
    -  API host USBX di Azure RTO intuitive in questo formato: *ux_host_stack_* * 
* OHCI, EHCI, controller host proprietari 

### <a name="azure-rtos-usbx-device-api"></a>API del dispositivo USBX di Azure RTO

L'API del dispositivo USBX di Azure RTO è un'API intuitiva e coerente che segue una convenzione di denominazione dei verbi sostantivi. Tutte le API hanno ux_device_ * per identificare facilmente come USBX. Le API di blocco hanno un timeout thread facoltativo. Per altri dettagli, vedere la [Guida dell'utente dell'host USBX di Azure RTO](usbx-host-stack-about.md) .

* CDC/ACM
    - Minimo 0,8 KB di memoria, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API intuitive del dispositivo USBX di Azure RTO in questo formato: * ux_device_class_cdc_acm_ * *.
* CDC/ECM
    - Minimo 1,5 KB di memoria, da 4 KB a 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX<br> API intuitive del dispositivo USBX di Azure RTO in questo formato: * ux_device_class_cdc_ecm_ * *.
* DFU
    - Minimo 1,1 KB di memoria, 2 KB di RAM
    -  Scalabilità automatica
    -  Traccia a livello di sistema tramite Azure RTO TraceX
    - API del dispositivo USBX di Azure RTO intuitive in questo formato: *ux_device_class_dfu_** 
* GSER
    - FLASH minimo 0,6 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API del dispositivo USBX di Azure RTO intuitive in questo formato: *ux_device_class_gser_**
* HID
    - Minimo 0,9 KB di memoria, 2 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API intuitive del dispositivo USBX di Azure RTO in questo formato: *ux_device_class_hid_** Pima (PTP/MTP)
    - Minimo 5,2 KB di memoria, 8 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API del dispositivo USBX di Azure RTO intuitive in questo formato: *ux_device_class_pima_** 
* STORAGE
    - FLASH minimo 2,3 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API del dispositivo USBX di Azure RTO intuitive in questo formato: *ux_device_class_storage_**
* RNDIS
    - Minimo 2,3 KB di memoria, da 4 KB a 8 KB di RAM
    - Scalabilità automatica
    - Integrazione con Azure RTO NetX e Azure RTO NetX DUO
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API del dispositivo USBX di Azure RTO intuitive in questo formato: *ux_device_class_rndls_**
* STACK di dispositivi USBX di Azure RTO
    - FLASH minimo 2,3 KB, 4 KB di RAM
    - Scalabilità automatica
    - Traccia a livello di sistema tramite Azure RTO TraceX
    - API del dispositivo USBX di Azure RTO intuitive in questo formato: *ux_device_class_storage_**
* CONTROLLER host proprietari

## <a name="next-steps"></a>Passaggi successivi

Per iniziare a usare l'host e lo stack di dispositivi USBX di Azure RTO, seguire il manuale dell'utente [dello stack host](usbx-host-stack-about.md) o il [manuale dell'utente dello stack di dispositivi](usbx-device-stack-about.md).