---
title: Capitolo 1 - Introduzione a Azure RTOS FileX
description: Azure RTOS FileX è un supporto in formato FAT completo e un sistema di gestione dei file per applicazioni con incorporazione approfondita.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 48fab21d78ede88e84db11a4f30574ce2061d145820b819ec7846203e297f42a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782981"
---
# <a name="chapter-1---introduction-to-azure-rtos-filex"></a>Capitolo 1 - Introduzione a Azure RTOS FileX

Azure RTOS FileX è un supporto in formato FAT completo e un sistema di gestione dei file per applicazioni con incorporazione approfondita. Questo capitolo presenta FileX, che descrive le applicazioni e i vantaggi.

## <a name="filex-unique-features"></a>Funzionalità univoche di FileX

Azure RTOS FileX supporta un numero illimitato di dispositivi multimediali contemporaneamente, inclusi dischi RAM, gestori FLASH e dispositivi fisici effettivi. Supporta formati FAT (File Allocation Table) a 12, 16 e 32 bit e supporta anche la tabella di allocazione file estesa (exFAT), l'allocazione di file contigui ed è altamente ottimizzata per dimensioni e prestazioni. FileX include anche il supporto a tolleranza di errore, le funzioni di callback di apertura/chiusura dei supporti e di scrittura di file.

Progettato per soddisfare la crescente necessità di dispositivi FLASH, FileX usa gli stessi metodi di progettazione e codifica di ThreadX. Come tutti i prodotti Microsoft, FileX viene distribuito con codice sorgente ANSI C completo e non ha diritti di esecuzione.

### <a name="product-highlights"></a>Evidenziazioni del prodotto

- Supporto completo del processore ThreadX
- Nessuna royalty
- Completare il codice sorgente ANSI C
- Prestazioni in tempo reale
- Supporto tecnico reattivo
- Oggetti FileX illimitati (supporti, directory e file)
- Creazione/eliminazione dinamica di oggetti FileX
- Utilizzo flessibile della memoria
- Ridimensiona automaticamente le dimensioni
- Dimensioni dell'area di istruzione di footprint ridotto (fino a 6 KByte): 6-30.000
- Integrazione completa con ThreadX
- Neutro endiano
- Driver di I/O FileX di facile implementazione
- Supporto FAT a 12, 16 e 32 bit
- Supporto di exFAT
- Supporto dei nomi file lunghi
- Cache delle voci FAT interna
- Supporto dei nomi Unicode
- Allocazione di file contigui
- Settore consecutivo e lettura/scrittura del cluster
- Cache del settore logico interno
- La dimostrazione del disco RAM viene eseguita automaticamente
- Funzionalità del formato multimediale
- Rilevamento e ripristino degli errori
- Opzioni a tolleranza di errore
- Statistiche sulle prestazioni incorporate
- Supporto autonomo (nessun Azure RTOS)

## <a name="safety-certifications"></a>Certificazioni di sicurezza

### <a name="tv-certification"></a>Certificazione TÜV

FileX è stato certificato da SGS-TÜV Saar per l'uso in sistemi critici per la sicurezza, in base a IEC-61508 e IEC-62304. La certificazione conferma che FileX può essere usato nello sviluppo di software correlato alla sicurezza per i più elevati livelli di integrità della sicurezza dei sistemi International Electrotechnical Commission (IEC) 61508 e IEC 62304, per "Sicurezza funzionale dei sistemi elettrici, elettronici e programmabili correlati alla sicurezza elettronica". SGS-TÜV Saar, costituita da un'iniziativa congiunta di Germania SGS-Group e TÜV Saarland, è diventata la principale società indipendente e accreditata per il test, il controllo, la verifica e la certificazione di software incorporato per sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, incluso IEC 62304, vengono usati per garantire la sicurezza funzionale dei dispositivi medici elettrici, elettronici e programmabili correlati alla sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali e sistemi di controllo delle linee di trasporto.

SGS-TÜV Saar ha certificato FileX da usare nei sistemi automobilistici critici per la sicurezza, in base allo standard ISO 26262. Inoltre, FileX è certificato per il livello di integrità della sicurezza automobilistica (ASIL) D, che rappresenta il livello più alto di certificazione ISO 26262.

Inoltre, SGS-TÜV Saar ha certificato FileX da usare nelle applicazioni critiche per la sicurezza, in base allo standard EN 50128 fino a SW-SIL 4.

![Logo SGS TUV Saar](./media/user-guide/sgs-tuv-saar-logo.png)

- IEC 61508 fino a SIL 4
- Da IEC 62304 a SW safety Class C
- ISO 26262 ASIL D
- EN 50128 SW-SIL 4

> [!IMPORTANT]
> Per altre informazioni sulle versioni di FileX certificate da TÜV o per la disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.

### <a name="ul-certification"></a>Certificazione UL

FileX è stato certificato da UL per la conformità con ul 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 603351 Annex R e UL 1998 standard di sicurezza per il software in componenti programmabili. Insieme a IEC/UL 60730-1, che ha i requisiti per "Controlli che usano software" nell'allegato H, Lo standard IEC 60335-1 descrive i requisiti per "Circuiti elettronici programmabili" nell'allegato R. IEC 60730 Annex H e IEC 60335-1 Annex R per la sicurezza dell'hardware e del software MCU usati in elettrodomestici come lavatrici, lavastoviglie, essiccatori, refrigeratori, refrigeratori e forni.

![C RU US 2](./media/user-guide/c-ru-us-logo.png)

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]
>*Per altre informazioni sulle versioni di FileX certificate dall'UL o per la disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.*

## <a name="powerful-services-of-filex"></a>Servizi potenti di FileX

### <a name="multiple-media-management"></a>Gestione di più supporti

FileX può supportare un numero illimitato di supporti fisici. Ogni istanza del supporto ha una propria area di memoria distinta e un driver associato specificato ***nella fx_media_open*** chiamata. La distribuzione predefinita di FileX viene fornita con un semplice driver di supporti RAM e un sistema dimostrativo che usa questo disco RAM.

### <a name="logical-sector-cache"></a>Cache del settore logico

Riducendo il numero di trasferimenti di interi settori, da e verso i supporti, la cache del settore logico FileX migliora significativamente le prestazioni. FileX gestisce una cache del settore logico per ogni supporto aperto. La profondità della cache del settore logico è determinata dalla quantità di memoria fornita a FileX con la fx_media_open ***API.***

### <a name="contiguous-file-support"></a>Supporto di file contigui

FileX offre supporto di file contigui tramite il servizio API ***fx_file_allocate*** migliorare e rendere deterministica l'ora di accesso ai file. Questa routine accetta la quantità di memoria richiesta e cerca una serie di cluster adiacenti per soddisfare la richiesta. Se vengono trovati, questi cluster vengono preallocato rendendoli parte della catena di cluster allocati del file. Quando si spostano supporti fisici, il supporto di file contigui FileX comporta un miglioramento significativo delle prestazioni e rende deterministico il tempo di accesso.

### <a name="dynamic-creation"></a>Creazione dinamica

FileX consente di creare risorse di sistema in modo dinamico. Ciò è particolarmente importante se l'applicazione ha più requisiti di configurazione dinamica o multipli. Inoltre, non sono previsti limiti predeterminati per il numero di risorse FileX che è possibile usare (supporti o file). Inoltre, il numero di oggetti di sistema non influisce sulle prestazioni.

## <a name="easy-to-use-api"></a>API facile da usare

FileX offre la migliore tecnologia di file system integrata in modo facile da comprendere e da usare. L'API (Application Programming Interface) FileX rende i servizi intuitivi e coerenti. Non sarà necessario decifrare i servizi di "alfabeto zuppe" troppo comuni con altri file system.

Per un elenco completo dei servizi FileX versione 5, vedere [Appendice A.](appendix-a.md)

## <a name="exfat-support"></a>Supporto di exFAT

exFAT (Extended File Allocation Table) è un file system progettato da Microsoft per consentire alle dimensioni dei file di superare i 2 GB, un limite imposto dai file system FAT32. È l'impostazione file system per le schede SD con capacità superiore a 32 GB. Le schede SD o le unità flash formattate con il formato FileX exFAT sono compatibili con Windows. exFAT supporta dimensioni di file fino a un exabyte (EB), ovvero circa un miliardo di GB.

Gli utenti che vogliono usare exFAT devono ricompilare la libreria FileX con il simbolo ***FX_ENABLE_EXFAT** _ definito. Quando si apre un supporto, FileX rileva il tipo di supporto. Se il supporto è formattato con exFAT, FileX legge e scrive il file system standard exFAT seguente. Per formattare i nuovi supporti con exFAT, usare il servizio _*_fx_media_exFAT_format_**. Per impostazione predefinita, exFAT non è abilitato.

## <a name="fault-tolerant-support"></a>Supporto a tolleranza di errore

Il modulo a tolleranza di errore FileX è progettato per evitare file system danneggiamento causato da interruzioni durante l'aggiornamento del file o della directory. Ad esempio, quando si accoda dati a un file, FileX deve aggiornare il contenuto del file, la voce di directory ed eventualmente le voci FAT. Se questa sequenza di aggiornamento viene interrotta ,ad esempio un problema di alimentazione o il supporto viene espulso al centro dell'aggiornamento), il file system si trova in uno stato incoerente, che può influire sull'integrità dell'intero file system, causando il danneggiamento di altri file.

Il modulo FileX Fault Tolerant funziona registrando tutti i passaggi necessari per aggiornare un file o una directory lungo il percorso. Questa voce di log viene archiviata nei supporti in settori dedicati (blocchi) che FileX può trovare e accedere. È possibile accedere al percorso dei dati del log anche senza un file system. Pertanto, nel caso in cui file system danneggiato, FileX è ancora in grado di trovare la voce di log e ripristinare il file system in uno stato valido.

Quando FileX aggiorna il file o la directory, vengono create voci di log. Al termine dell'operazione di aggiornamento, le voci di log vengono rimosse. Se le voci di log non sono state rimosse correttamente dopo un aggiornamento di file riuscito, se il processo di ripristino determina che il contenuto della voce di log corrisponde al file system, non è necessario eseguire alcuna operazione e le voci di log possono essere eliminate.

Nel caso in cui file system'operazione di aggiornamento sia stata interrotta, alla successiva installazione del supporto da Parte di FileX, il modulo fault tolerant analizza le voci di log. Le informazioni nelle voci di log consentono a FileX di eseguire il backup delle modifiche parziali già applicate al file system (nel caso in cui l'errore si verifica durante la fase iniziale dell'operazione di aggiornamento del file) oppure, se le voci di log contengono informazioni sulle operazioni di nuovo, FileX è in grado di applicare le modifiche necessarie per completare l'operazione precedente.

Questa funzionalità a tolleranza di errore è disponibile per tutti i file system FAT supportati da FileX, inclusi FAT12, FAT16, FAT32 ed exFAT. Per impostazione predefinita, la tolleranza di errore non è abilitata in FileX. Per abilitare la funzionalità a tolleranza di errore, FileX deve essere compilato con il simbolo FX_ENABLE_FAULT_TOLERANT  **e** **FX_FAULT_TOLERANT** definiti. In fase di esecuzione, l'applicazione avvia il servizio a tolleranza di errore **_chiamando fx_fault_tolerant_enable_**.
Dopo l'avvio del servizio, tutte le operazioni di scrittura di file e directory passano attraverso il modulo fault tolerant.

All'avvio del servizio a tolleranza di errore, rileva prima di tutto se il supporto è protetto dal modulo a tolleranza di errore. In caso contrario, FileX presuppone l'integrità del file system e avvia la protezione allocando blocchi liberi dal file system da usare per la registrazione e la memorizzazione nella cache. Se i log del modulo a tolleranza di errore vengono trovati nel file system, analizza le voci di log. FileX ripristina l'operazione precedente o ripristina l'operazione precedente, a seconda del contenuto delle voci di log. Il file system diventa disponibile dopo l'elaborazione di tutte le voci di log precedenti. Ciò garantisce che FIleX inizi da uno stato valido noto.

Dopo la protezione di un supporto nel modulo FileX Fault Tolerant, il supporto non verrà aggiornato con un altro file system. In questo modo, le voci di log nel file system incoerente con il contenuto della tabella FAT, la voce di directory. Se il supporto viene aggiornato da un altro file system prima di riportarlo in FileX con il modulo fault tolerant, il risultato non è definito.

## <a name="callback-functions"></a>Funzioni di callback

A FileX vengono aggiunte le tre funzioni di callback seguenti:

- Callback di Apertura file multimediali
- Callback di chiusura dei supporti
- Callback di scrittura file

Dopo la registrazione, queste funzioni invieranno una notifica all'applicazione quando si verificano tali eventi.

## <a name="easy-integration"></a>Integrazione semplice

FileX è facilmente integrato con qualsiasi dispositivo FLASH o multimediale. Il porting di FileX è semplice. Questa guida descrive in dettaglio il processo e il driver RAM del sistema dimostrativo è un ottimo punto di partenza.
