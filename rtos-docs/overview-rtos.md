---
title: Che cos'è Microsoft Azure RTO?
description: Azure RTO è un sistema operativo in tempo reale (RTO) per i dispositivi Internet e i dispositivi perimetrali basati su unità di microcontroller (MCU).
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 3b1c63135f6069652d7f66fc976b9d770a4dfeb2
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822502"
---
# <a name="what-is-microsoft-azure-rtos"></a>Che cos'è Microsoft Azure RTO

Azure RTO è un sistema operativo in tempo reale (RTO) per i dispositivi Internet e i dispositivi perimetrali basati su unità di microcontroller (MCU). Azure RTO è progettato per supportare i dispositivi con la massima costrizione (alimentato da batteria e con meno di 64 KB di memoria flash).
 
Azure RTO è già certificato per diversi standard di sicurezza. Sono incluse le certificazioni IEC 61508 SIL 4, IEC 62304 Class C e ISO 26262 ASIL D. Anche Azure RTO ThreadX è certificato 178.

Azure RTO offre un ambiente EAL4 + Common criteri di sicurezza con certificazione, inclusa la sicurezza completa a livello IP tramite IPsec e la sicurezza a livello di socket tramite TLS e DTLS. La libreria di crittografia software ha raggiunto la certificazione FIPS 140-2. Vengono inoltre sfruttate le funzionalità di crittografia hardware, la protezione della memoria tramite i moduli ThreadX e il supporto per le funzionalità di sicurezza TrustZone ARMv8-M di ARM.

## <a name="components-of-azure-rtos"></a>Componenti di Azure RTO

La piattaforma Azure RTO è la raccolta di soluzioni in fase di esecuzione, tra cui Azure RTO ThreadX, Azure RTO FileX, Azure RTO GUIX, Azure RTO NetX, Azure RTO NetX Duo e Azure RTO USBX.

### <a name="azure-rtos-threadx"></a>Azure RTOS ThreadX

Azure RTOS ThreadX è un sistema operativo in tempo reale (RTOS, Real-Time Operating System) avanzato, progettato in modo specifico per applicazioni profondamente incorporate. Tra i vari vantaggi offerti da Azure RTO ThreadX sono disponibili funzionalità di pianificazione avanzate, passaggio di messaggi, gestione degli interrupt e servizi di messaggistica. Azure RTO ThreadX offre molte funzionalità avanzate, tra cui l'architettura picokernel, la pianificazione delle soglie di precedenza, il concatenamento degli eventi e un set completo di servizi di sistema.

### <a name="azure-rtos-filex"></a>Azure RTOS FileX

Azure RTO FileX è una file system a prestazioni elevate compatibili con FAT. È completamente integrato con Azure RTO ThreadX ed è disponibile per tutti i processori supportati. Analogamente ad Azure RTO ThreadX, Azure RTO FileX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni di oggi profondamente incorporate che richiedono operazioni sui file. Azure RTO FileX supporta la maggior parte dei supporti fisici, tra cui RAM disk, USBX, SD CARD e NAND/NOR Flash Memory tramite Azure RTO LevelX.

### <a name="azure-rtos-guix"></a>Azure RTOS GUIX

Azure RTO GUIX è un pacchetto di interfaccia utente grafica di qualità professionale, creato per soddisfare le esigenze degli sviluppatori di sistemi embedded. Diversamente dalle alternative, Azure RTO GUIX è piccolo, veloce e facilmente portabile in qualsiasi configurazione hardware in grado di supportare l'output grafico. Azure RTO GUIX offre anche un'eccezionale attrattiva visiva e un'API intuitiva e potente per lo sviluppo di interfacce utente a livello di applicazione.

### <a name="azure-rtos-netx"></a>Azure RTOS NetX

Azure RTO NetX è un'implementazione a prestazioni elevate degli standard del protocollo TCP/IP. È completamente integrato con Azure RTO ThreadX ed è disponibile per tutti i processori supportati. Azure RTO NetX ha un'architettura piconet univoca. Combinato con un'API di copia zero, lo rende perfetto per le applicazioni di oggi profondamente incorporate che richiedono la connettività di rete.

### <a name="azure-rtos-netx-duo"></a>Azure RTOS NetX Duo

Azure RTO NetX Duo è uno stack di rete TCP/IP avanzato e di livello industriale progettato in modo specifico per applicazioni incorporate, in tempo reale e in tempo reale. Azure RTO NetX Duo è uno stack di rete IPv4 e IPv6 duale, mentre NetX è lo stack di rete IPv4 originale, essenzialmente un subset di Azure RTO NetX Duo.

### <a name="azure-rtos-usbx"></a>Azure RTOS USBX

Azure RTO USBX è un host USB a prestazioni elevate, un dispositivo e uno stack embedded on-the-go (OTG). È completamente integrato con ThreadX ed è disponibile per tutti i processori supportati da Azure RTO ThreadX. Analogamente ad Azure RTO ThreadX, Azure RTO USBX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per applicazioni con Deep embedded che richiedono un'interfaccia con i dispositivi USB.

### <a name="windows-tools"></a>Strumenti di Windows

Azure RTO GUIX Studio fornisce un ambiente di progettazione di applicazioni GUI completo, che facilita la creazione e la manutenzione di tutti gli elementi grafici nell'interfaccia utente grafica dell'applicazione. Azure RTO GUIX Studio genera automaticamente il codice C compatibile con la libreria RTO GUIX di Azure, pronto per essere compilato ed eseguito nella destinazione.

Azure RTO TraceX è uno strumento di analisi basato su host che offre agli sviluppatori una visualizzazione grafica degli eventi di sistema in tempo reale e consente loro di visualizzare e comprendere meglio il comportamento dei sistemi in tempo reale.

## <a name="in-the-context-of-azure-iot"></a>Nel contesto di Azure

Oltre a connettersi direttamente ad Azure o a connettersi indirettamente tramite Azure IoT Edge, Azure RTO è disponibile anche su dispositivi Azure Sphere. La combinazione di RTO e Azure Sphere di Azure offrirà insieme l'elaborazione e la protezione in tempo reale di livello più efficace in un unico dispositivo.
