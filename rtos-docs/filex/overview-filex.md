---
title: Informazioni su Azure RTO FileX
description: Azure RTO FileX è un file system compatibile con le prestazioni elevate, che è compatibile con le tabelle di allocazione file (FAT), completamente integrato con Azure RTO ThreadX e disponibile per tutti i processori supportati. Analogamente ad Azure RTO ThreadX, Azure RTO FileX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni di oggi profondamente incorporate che richiedono operazioni di gestione file. FileX supporta la maggior parte dei supporti fisici, tra cui RAM, Azure RTO USBX, SD CARD e NAND/NOR Flash Memory tramite Azure RTO LevelX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: a3a20c8ced3426399ceedf6994c872ce7aec93c3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823225"
---
# <a name="overview-of-azure-rtos-filex"></a>Panoramica di Azure RTO FileX

Azure RTO FileX Embedded file system è la soluzione avanzata e di livello industriale di Azure RTO per i formati di file FAT Microsoft, progettata in modo specifico per applicazioni incorporate, in tempo reale e Internet. Azure RTO FileX supporta tutti i formati di file Microsoft, tra cui FAT12, FAT16, FAT32 e exFAT. FileX offre anche la tolleranza di errore facoltativa e il livellamento dell'utilizzo FLASH tramite un prodotto aggiuntivo denominato [Azure RTO LevelX](https://docs.microsoft.com/azure/rtos/levelx/). Tutti questi componenti combinati con un footprint ridotto, un'esecuzione rapida e una maggiore semplicità d'uso, rendono Azure RTO FileX la scelta ideale per le applicazioni per le cose incorporate più complesse.

## <a name="api-protocols"></a>Protocolli API

### <a name="azure-rtos-filex-api"></a>API FileX di Azure RTO

- API intuitiva e coerente
- Sostantivo-convenzione di denominazione dei verbi
- Tutte le API hanno *fx_* iniziali per identificare facilmente come FILEX
- Le API di blocco hanno un timeout thread facoltativo
- Callback facoltativi delle notifiche utente per le operazioni su file e file multimediali
- Per altri dettagli, vedere la [Guida dell'utente di Azure RTO FILEX](about-this-guide.md)

### <a name="media-services"></a>Servizi multimediali

- Supporto FAT 12/16/32 e exFAT
- FLASH 6KB minimo, 2,5 KB di RAM
- Servizi di accesso multimediale completi
- Numero illimitato di istanze dei supporti
- Interfaccia semplice di driver di settore logico in lettura/scrittura
- Supporto per più partizioni
- Cache del settore logico
- Cache di immissione FAT
- Supporto della tolleranza di errore facoltativa
- Aggiornamento FAT secondario posticipato
- Traccia a livello di sistema tramite Azure RTO TraceX
- API di accesso multimediale intuitive, tra cui:
  - fx_media_open
  - fx_media_close
  - fx_media_format
  - fx_media_space_available

### <a name="directory-services"></a>Servizi directory

- Fino a 256 di percorsi di byte
- Nomi di directory Long e 8,3 supportati
- Creazione & eliminazione della directory
- Esplorazione e attraversamento della directory
- Gestione degli attributi di directory
- Traccia a livello di sistema tramite Azure RTO TraceX
- API di accesso alla directory intuitive, tra cui:
  - fx_directory_create
  - fx_directory_delete
  - fx_directory_attributes_set
  - fx_directory_attributes_read
  - fx_directory_first_entry_find
  - fx_directory_next_entry_find

### <a name="file-services"></a>Servizi file

- Minimo 3.3 KB di memoria FLASH
- File aperti illimitati
- I file di sola lettura possono essere aperti più volte
- Nomi di directory Long e 8,3 supportati
- Supporto file contiguo
- Logica di ricerca veloce
- Pre-allocazione dei cluster
- Creazione, eliminazione e ridenominazione di file
- Lettura, scrittura e visualizzazione del file
- Gestione degli attributi di file
- Traccia a livello di sistema tramite Azure RTO TraceX
- API di accesso ai file intuitive, tra cui:
  - fx_file_create
  - fx_file_delete
  - fx_file_attributes_set
  - fx_file_attributes_read
  - fx_file_read
  - fx_file_seek
  - fx_file_write

## <a name="small-footprint"></a>Footprint ridotto

Azure RTO FileX Embedded file system dispone di un footprint minimo ristretto di 8,6 KB a 12 KB per il supporto di base per i file di lettura/scrittura. L'utilizzo minimo della RAM FileX di Azure RTO è nell'ordine di 1,8 KB per un'istanza del supporto e solo con una cache di settore logica a 512 byte. Come Azure RTO ThreadX, le dimensioni di Azure RTO FileX vengono ridimensionate automaticamente in base ai servizi usati dall'applicazione. In questo modo si elimina la necessità di una configurazione complicata e dei parametri di compilazione, semplificando le operazioni per lo sviluppatore.

## <a name="fast-execution"></a>Esecuzione rapida

Azure RTO FileX offre una cache di settore logica e una cache di immissione FAT. Le dimensioni di entrambi sono sotto il controllo diretto dell'applicazione. Azure RTO FileX offre inoltre un'allocazione del cluster contigua e una lettura e scrittura diretta del cluster consecutivi. Le richieste di lettura/scrittura di interi settori vengono eseguite direttamente tra il buffer dell'applicazione e il supporto, ovvero non viene eseguito alcun buffer intermedio. Questa e una filosofia di progettazione orientata alle prestazioni generale consentono ad Azure RTO FileX di ottenere le prestazioni più veloci possibile.

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTO FileX è una tecnologia avanzata, incluse le seguenti.

- Supporto FAT 12/16/32 e exFAT
- Supporto per più partizioni
- Scalabilità automatica
- Endian neutro
- Nome di file lungo e supporto di 8,3
- Supporto della tolleranza di errore facoltativa
- Cache del settore logico
- Cache di immissione FAT
- Pre-allocazione dei cluster
- Supporto file contiguo
- Metriche delle prestazioni facoltative
- Supporto per l'analisi del sistema TraceX di Azure RTO

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a>Livelli di utilizzo non/NAND (Azure RTO LevelX)

Azure RTO LevelX è il prodotto Microsoft NOR/NAND FLASH Wear Leveling. Azure RTO LevelX può essere usato insieme a FileX o come libreria di settore FLASH autonomo di lettura/scrittura diretta per l'applicazione.

## <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTO FileX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Di conseguenza, Azure RTO FileX è uno dei file system FAT più diffusi per i dispositivi di Internet delle cose embedded. Di seguito sono riportati alcuni motivi per un vantaggio di time-to-Market coerente:

- Documentazione sulla qualità: esaminare la [Guida dell'utente di Azure RTO FILEX](about-this-guide.md) e vedere per se stessi.
- Disponibilità del codice sorgente completa
- API di facile utilizzo
- Set di funzionalità completo e avanzato

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a>Pre-certificati da TUV e UL a molti standard di sicurezza

![SGS-TUV Saar](./media/overview-filex/partener-logo-sgs-tuv-saar-2.png)

Azure RTO FileX è stato certificato da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, secondo IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128. La certificazione conferma che FileX può essere usato nello sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici, elettrici e programmabili relativi alla sicurezza elettronica." SGS-TUV Saar, costituito da una joint venture del SGS-Group e del TUV del Regno Unito, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviari.

:::image type="content" source="media/overview-filex/cru-logo-certification.png" alt-text="Certificazione CRU UL":::

Azure RTO FileX è stato riconosciuto da UL per conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 sicurezza standard per il software in componenti programmabili. UL è una società globale, indipendente e scientifica per la sicurezza, con più di un secolo di competenze innovative per l'innovazione delle soluzioni di sicurezza, che vanno dall'adozione pubblica di energia elettrica ai progressi della sostenibilità, dell'energia rinnovabile e della nanotecnologia.

Gli artefatti (certificato, manuale di sicurezza, report di test e così via) associati alle certificazioni TUV e UL sono disponibili per la vendita.

Nei casi in cui l'applicazione necessita di ulteriore certificazione, un servizio di certificazione è disponibile tramite Microsoft per fornire la certificazione chiavi in volta a diversi standard usando la piattaforma hardware effettiva e persino coprendo il codice dell'applicazione.

## <a name="one-simple-license"></a>Una licenza semplice

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

## <a name="full-highest-quality-source-code"></a>Codice sorgente completo di qualità elevata

Nel corso degli anni, il codice sorgente di FileX ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.

## <a name="supports-most-popular-architectures"></a>Supporta le architetture più diffuse

Azure RTO FileX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, inclusi i seguenti:

**Dispositivi analoghi**: SHARC, Blackfin, CM4xx

**Andina Core**: RISC-V

**Ambiqmicro**: Apollo MCU

**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M

**Cadenza**: Xtensa, diamante

**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi

**Cypress**: RISC-V

**Silice**: ESI-RISC

**Infineon**: XMC1000, XMC4000, Tricore

**Intel**; **Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10

**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32

**Microsemi**: RISC-V

**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, V850, RX, RZ, Synergy

**Silicone** Lab: EFM32

**Synopsys**: Arc 600, 700, Arc em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C

**Elaborazione Wave**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class

**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE

*Tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*
