---
title: Che cos'Microsoft Azure RTOS?
description: Azure RTOS è un sistema operativo in tempo reale (RTOS) per dispositivi IoT e perimetrali basati su unità microcontroller (MKU).
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: b099a5f18accfbe467a2a8fa680c0c76666a9ff3
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754914"
---
# <a name="what-is-microsoft-azure-rtos"></a>Che cos'Microsoft Azure RTOS?

Azure RTOS è un sistema operativo in tempo reale (RTOS) per dispositivi Internet delle cose (IoT) e perimetrali basati su unità microcontroller (MKU). Azure RTOS è progettato per supportare i dispositivi più vincolati (alimentato a batteria e con meno di 64 KB di memoria flash).

Azure RTOS è precertificato per un'ampia gamma di standard di sicurezza. Sono incluse le certificazioni IEC 61508 SIL 4, IEC 62304 Classe C e ISO 26262 ASIL D. Azure RTOS ThreadX è certificato anche per DO-178.

Azure RTOS un ambiente certificato per la sicurezza con criteri comuni EAL4+, inclusa la sicurezza completa del livello IP tramite IPsec e la sicurezza del livello socket tramite TLS e DTLS. La nostra libreria di crittografia software ha ottenuto la certificazione FIPS 140-2. Vengono anche sfruttate le funzionalità di crittografia hardware, la protezione della memoria tramite Moduli ThreadX e il supporto per le funzionalità di sicurezza ARMv8-M trustZone di ARM.

## <a name="components-of-azure-rtos"></a>Componenti di Azure RTOS

La piattaforma Azure RTOS è la raccolta di soluzioni di run-time tra cui Azure RTOS ThreadX, Azure RTOS FileX, Azure RTOS GUIX, Azure RTOS NetX, Azure RTOS NetX Duo e Azure RTOS USBX.

### <a name="azure-rtos-threadx"></a>Azure RTOS ThreadX

Azure [RTOS ThreadX](threadx/overview-threadx.md) è un sistema operativo Real-Time (RTOS) avanzato progettato specificamente per applicazioni con deep embedded. Tra i diversi vantaggi offerti Azure RTOS ThreadX sono le funzionalità di pianificazione avanzate, il passaggio di messaggi, la gestione delle interruzioni e i servizi di messaggistica. Azure RTOS ThreadX offre molte funzionalità avanzate, tra cui l'architettura del picokernel, la pianificazione delle soglie di preemption, il concatenamento degli eventi e un set avanzato di servizi di sistema.

### <a name="azure-rtos-filex"></a>Azure RTOS FileX

Azure [RTOS FileX è](filex/overview-filex.md) un sistema compatibile con FAT ad file system. È completamente integrato con Azure RTOS ThreadX ed è disponibile per tutti i processori supportati. Come Azure RTOS ThreadX, Azure RTOS FileX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni attualmente incorporate che richiedono operazioni su file. Azure RTOS FileX supporta la maggior parte dei supporti fisici, tra cui dischi RAM, USBX, SD CARD e memorie flash NAND/NOR tramite Azure RTOS LevelX.

### <a name="azure-rtos-guix"></a>Azure RTOS GUIX

Azure [RTOS GUIX è](guix/overview-guix.md) un pacchetto di interfaccia utente grafica di qualità professionale, creato per soddisfare le esigenze degli sviluppatori di sistemi incorporati. A differenza delle alternative, Azure RTOS GUIX è di piccole dimensioni, veloce e facilmente portabile in praticamente qualsiasi configurazione hardware in grado di supportare l'output grafico. Azure RTOS GUIX offre anche un'eccezionale grafica accattivante e un'API intuitiva e potente per lo sviluppo dell'interfaccia utente a livello di applicazione.

### <a name="azure-rtos-netx"></a>Azure RTOS NetX

Azure [RTOS NetX è](netx/overview-netx.md) un'implementazione ad alte prestazioni degli standard del protocollo TCP/IP. È completamente integrato con Azure RTOS ThreadX ed è disponibile per tutti i processori supportati. Azure RTOS NetX ha un'architettura Piconet univoca. In combinazione con un'API senza copia, è la soluzione ideale per le applicazioni attualmente incorporate che richiedono la connettività di rete.

### <a name="azure-rtos-netx-duo"></a>Azure RTOS NetX Duo

Azure [RTOS NetX](netx-duo/overview-netx-duo.md) Duo è uno stack di rete TCP/IP di livello industriale avanzato progettato specificamente per applicazioni IoT, in tempo reale e con deep embedded. Azure RTOS NetX Duo è uno stack di rete IPv4 e IPv6 doppio, mentre NetX è lo stack di rete IPv4 originale, essenzialmente un subset di Azure RTOS NetX Duo.

### <a name="azure-rtos-usbx"></a>Azure RTOS USBX

Azure [RTOS USBX](usbx/overview-usbx.md) è un host USB ad alte prestazioni, un dispositivo e uno stack incorporato OTG (On-The-Go). È completamente integrato con ThreadX ed è disponibile per tutti i processori supportati Azure RTOS ThreadX. Come Azure RTOS ThreadX, Azure RTOS USBX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni con deep embedded che richiedono un'interfaccia con dispositivi USB.

### <a name="windows-tools"></a>Windows strumenti

Azure [RTOS GUIX Studio](guix/about-guix-studio.md) offre un ambiente di progettazione dell'applicazione GUI completo, facilitando la creazione e la manutenzione di tutti gli elementi grafici nell'interfaccia utente grafica dell'applicazione. Azure RTOS GUIX Studio genera automaticamente codice C compatibile con la libreria GUIX di Azure RTOS, pronto per essere compilato ed eseguito nella destinazione.

Azure [RTOS TraceX](tracex/overview-tracex.md) è uno strumento di analisi basato su host che offre agli sviluppatori una visualizzazione grafica degli eventi di sistema in tempo reale e consente di visualizzare e comprendere meglio il comportamento dei sistemi in tempo reale.

## <a name="the-azure-rtos-advantage"></a>Vantaggio Azure RTOS
Azure RTOS offre i vantaggi seguenti rispetto ad altri sistemi operativi in tempo reale.

### <a name="most-deployed-rtos"></a>RTOS più distribuito

Azure RTOS ha più di 6,2 miliardi di distribuzioni in tutto il mondo, secondo la società leader di intelligence di mercato M2M, VDC Research. La popolarità di Azure RTOS è un punto di forza per l'affidabilità, la qualità, le dimensioni, le prestazioni, le funzionalità avanzate, la facilità d'uso e i vantaggi generali del time-to-market.

> *"Abbiamo seguito la crescita di THREADX nei mercati wireless e IoT fin dalla creazione dell'azienda e siamo sempre più soddisfatti della diffusione dell'adozione di THREADX nel settore".* – Chris Roré, Executive Vice President, VDC Research

### <a name="intuitive-and-consistent-api-design"></a>Progettazione di API intuitiva e coerente

* API intuitiva e coerente.
* Convenzione di denominazione sostantivo-verbo.
* Tutte le API hanno un prefisso iniziale, ad esempio *tx_* per ThreadX e *fx_* per FileX, per identificare facilmente il componente Azure RTOS a cui appartengono.
* Coerenza funzionale in tutte le API. Ad esempio, tutte le funzioni API che sospendono hanno un timeout facoltativo che funziona in modo identico.
* Molte API sono disponibili direttamente dagli ISR delle applicazioni.
- Callback di notifica utente facoltativi per operazioni su file e supporti.
* Modello di programmazione basato su eventi (API).

### <a name="high-efficiency"></a>Efficienza elevata

- Footprint del codice ridotto.
- Footprint del codice scalabile in base ai servizi usati.
- Precertificato da TUV e UL a IEC 61508 SIL 4, IEC 62304 Classe C, ISO 26262 ASIL D e EN 50128 SW-SIL4.
- Esecuzione rapida. Azure RTOS è progettato per la velocità e ha livelli minimi di chiamate di funzione interne per ottenere le prestazioni più veloci possibili.

### <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTOS facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Di conseguenza, Azure RTOS è uno dei sistemi operativi in tempo reale più diffusi per i dispositivi IoT incorporati, inclusi molti soc di Broadcom, Gainspan e così via. Il vantaggio del time-to-market coerente si basa su:

* Disponibilità completa del codice sorgente.
* API facile da usare.
* Set di funzionalità completo e avanzato.
* Documentazione sulla qualità.

### <a name="one-simple-license"></a>Una licenza semplice

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando vengono distribuiti in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

### <a name="full-highest-quality-source-code"></a>Codice sorgente completo e di alta qualità

Nel corso degli anni, Azure RTOS codice sorgente ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione di avere una funzione per ogni file semplifica la navigazione all'origine.

### <a name="pre-certified-by-tuv-and-ul-to-many-safety-standards"></a>Precertificato da TUV e UL per molti standard di sicurezza

Azure RTOS è stato certificato da SGS-TUV Saar per l'uso in sistemi critici per la sicurezza, in base a IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D ed EN 50128. La certificazione conferma che Azure RTOS può essere usato nello sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 ed EN 50128 per la "Sicurezza funzionale dei sistemi elettronici, elettronici e programmabili correlati alla sicurezza elettronica". SGS-TUV Saar, formata tramite un'azienda congiunta di germania SGS-Group e TUV Saarland, è diventata la principale società indipendente e accreditata per test, controllo, verifica e certificazione di software incorporato per sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard che ne derivano, inclusi IEC-62304, ISO 26262 ed EN 50128, vengono usati per garantire la sicurezza funzionale di dispositivi medici elettronici, elettronici e programmabili correlati alla sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo delle apparecchiature.

:::image type="content" source="media/partener-logo-sgs-tuv-saar.png" alt-text="Certificazione SGS-TUV":::

Azure RTOS è stato riconosciuto da UL per la conformità con UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R e UL 1998 standard di sicurezza per software in componenti programmabili. UL è una società globale indipendente e di scienze di sicurezza con più di un secolo di esperienza nell'innovazione delle soluzioni di sicurezza, dall'adozione pubblica dell'elettricità alle innovazioni in materia di sostenibile, energia sostenibile e nanotecnologia.

:::image type="content" source="media/cru-logo-certification.png" alt-text="Certificazione UL CRU":::

Artifacts le certificazioni TUV e UL (Certificate, Safety Manual, Test Report e così via) associate alle certificazioni TUV e UL.

Nei casi in cui l'applicazione richiede una certificazione aggiuntiva, microsoft offre un servizio di certificazione per fornire la certificazione chiavi in volta a vari standard usando la piattaforma hardware effettiva e coprendo anche il codice dell'applicazione. Per altre informazioni sul servizio di certificazione, contattare Microsoft.

### <a name="eal4-common-criteria-security-certification"></a>Certificazione di sicurezza EAL4+ Common Criteria

Azure RTOS ha ottenuto la certificazione di sicurezza EAL4+ Common Criteria. Target of Evaluation (TOE) include Azure RTOS ThreadX, Azure RTOS NetX Duo, Azure RTOS NetX Secure TLS e Azure RTOS NetX MQTT. Rappresenta i protocolli IoT più comuni richiesti da sensori, dispositivi, router perimetrali e gateway con deep embedded.

:::image type="content" source="media/eal-logo-certification.png" alt-text="Certificazione EAL":::

La struttura di valutazione della sicurezza IT usata per la certificazione di sicurezza Microsoft Azure RTOS SC è Brightsight BV e l'autorità di certificazione è SERTIT.

### <a name="fips-140-2-validated"></a>FIPS 140-2 convalidato

Azure RTOS librerie di crittografia hanno ottenuto la certificazione FIPS 140-2 (Federal Information Processing Standardization 140-2) per il software, che specifica i requisiti per i moduli di crittografia. FIPS 140-2 richiede che tutte le agenzie governative federali e i reparti che usano la sicurezza basata su crittografia soddisfino standard specifici correlati alla complessità e alle funzionalità di crittografia. Questi standard di sicurezza basati su crittografia sono riconosciuti anche in Canada e nell'Unione Europa.

Il lab di valutazione di Information Security usato per Azure RTOS crypto è stato atsec e l'autorità di certificazione è [Il National Institute of Standards and Technology (NIST).](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394)

### <a name="supports-most-popular-architectures"></a>Supporta le architetture più comuni

Azure RTOS sui microprocessori a 32/64 bit più diffusi, out-of-the-box, completamente testati e completamente supportati, incluse le architetture avanzate seguenti.

- **Dispositivi analogici:** SHARC, Blackfin, CM4xx

- **Andes Core**: RISC-V

- **Ambiqmicro:** MKU Apollo

- **ARM:** ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64 bit/R4/R5, TrustZone ARMv8-M

- **Cadenza:** Xtensa, Diamond

- **CEVA:** PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi

- **Cypress**: RISC-V

- **EnSilica:** eSi-RISC

- **Infineon:** XMC1000, XMC4000, TriCore

- **Intel; Intel FPGA:** x36/Pentium, XScale, NIOS II, Ciclone, Arria 10

- **Microchip:** AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32

- **Microsemi**: RISC-V

- **NXP:** LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4

- **Renesas:** SH, HS, V850, RX, RZ, Synergy

- **Silicon Labs**: EFM32

- **Synopsys:** ARC 600, 700, ARC EM, ARC HS

- **ST:** STM32, ARM7, ARM9, Cortex-M3/M4/M7

- **Tl:** C5xxx, C6xxx, Stellaris, Sitara, Tiva-C

- **Wave Computing:** MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class

- **Xilinx:** MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE

*Tutte le cifre relative a tempi e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*

## <a name="in-the-context-of-azure-iot"></a>Nel contesto di Azure IoT

Oltre a connettersi direttamente a Azure IoT o connettersi indirettamente tramite Azure IoT Edge, Azure RTOS è disponibile anche Azure Sphere dispositivi. La combinazione di Azure RTOS e Azure Sphere l'elaborazione in tempo reale e la sicurezza migliori in un unico dispositivo.
