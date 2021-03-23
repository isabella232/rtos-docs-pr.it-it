---
title: Capitolo 1-Introduzione ad Azure RTO FileX
description: Azure RTO FileX è un sistema di gestione di file e file multimediali di formato FAT completo per applicazioni con Deep embedded.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be7e6f9cd9fbc69ac0908d1de733dac1c4f73bf6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821422"
---
# <a name="chapter-1---introduction-to-azure-rtos-filex"></a>Capitolo 1-Introduzione ad Azure RTO FileX

Azure RTO FileX è un sistema di gestione di file e file multimediali di formato FAT completo per applicazioni con Deep embedded. Questo capitolo introduce FileX, che descrive le applicazioni e i vantaggi.

## <a name="filex-unique-features"></a>Funzionalità univoche di FileX

Azure RTO FileX supporta un numero illimitato di dispositivi multimediali allo stesso tempo, inclusi dischi RAM, gestione FLASH e dispositivi fisici effettivi. Supporta formati FAT (file allocation table) a 12, 16 e 32 bit, supporta inoltre la tabella di allocazione file estesa (exFAT), l'allocazione di file contigui ed è altamente ottimizzata per le dimensioni e le prestazioni. FileX include anche il supporto per la tolleranza di errore, le funzioni di apertura/chiusura e di callback dei file.

Progettato per soddisfare le crescenti esigenze di dispositivi FLASH, FileX usa gli stessi metodi di progettazione e codifica di ThreadX. Come tutti i prodotti Microsoft, FileX viene distribuito con il codice sorgente ANSI C completo e non dispone di royalties in fase di esecuzione.

### <a name="product-highlights"></a>Caratteristiche principali del prodotto

- Supporto completo del processore ThreadX
- Nessun royalties
- Completa codice sorgente ANSI C
- Prestazioni in tempo reale
- Supporto tecnico reattivo
- Oggetti FileX illimitati (supporti, directory e file)
- Creazione/eliminazione di oggetti FileX dinamici
- Utilizzo flessibile della memoria
- Ridimensiona automaticamente le dimensioni
- Dimensioni dell'area di istruzione con ingombro ridotto (fino a 6 KByte): 6-30K
- Completa l'integrazione con ThreadX
- Endian neutro
- Driver di I/O FileX di facile implementazione
- supporto FAT 12, 16 e 32 bit
- supporto di exFAT
- Supporto del nome file lungo
- Cache di immissione FAT interna
- Supporto del nome Unicode
- Allocazione file contigui
- Lettura/scrittura di un settore e di un cluster consecutivi
- Cache del settore logico interno
- La dimostrazione del disco RAM è stata avviata
- Funzionalità di formato multimediale
- Rilevamento e ripristino degli errori
- Opzioni a tolleranza di errore
- Statistiche sulle prestazioni predefinite
- Supporto autonomo (nessun RTO di Azure)

## <a name="safety-certifications"></a>Certificazioni di sicurezza

### <a name="tv-certification"></a>Certificazione TÜV

FileX è stato certificato da SGS-TÜV Saar per l'uso nei sistemi critici per la sicurezza, in base a IEC-61508 e IEC-62304. La certificazione conferma che FileX può essere usato nello sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati dei International Electrotechnical Commission (IEC) 61508 e IEC 62304, per la "protezione funzionale dei sistemi elettronici di sicurezza elettronica, elettronici e programmabili". SGS-TÜV Saar, costituito da una joint venture di SGS-Group della Germania e TÜV Saarland, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, incluso IEC 62304, vengono utilizzati per garantire la sicurezza funzionale di dispositivi medicali, sistemi di controllo dei processi, macchinari industriali e sistemi di controllo ferroviari.

SGS-TÜV Saar ha certificato FileX da usare nei sistemi autonomi per la sicurezza, in base allo standard ISO 26262. Inoltre, FileX è certificato per il livello di integrità di sicurezza (ASIL) di Automotive, che rappresenta il livello più elevato di certificazione ISO 26262.

Inoltre, SGS-TÜV Saar ha certificato FileX da usare nelle applicazioni ferroviarie critiche per la sicurezza, che soddisfano lo standard EN 50128 fino a SW-SIL 4.

![Logo SGS TUV Saar](./media/user-guide/sgs-tuv-saar-logo.png)

- IEC 61508 fino a SIL 4
- IEC 62304 fino alla classe di sicurezza SW C
- ISO 26262 ASIL D
- EN 50128 SW-SIL 4

> [!IMPORTANT]
> Per ulteriori informazioni sulle versioni di FileX certificate da TÜV o sulla disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.

### <a name="ul-certification"></a>Certificazione UL

FileX è stato certificato da UL per conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 603351 allegato R e UL 1998 standard di sicurezza per il software in componenti programmabili. Insieme a IEC/UL 60730-1, che presenta i requisiti per "controlli che usano software" nell'allegato H, lo standard IEC 60335-1 descrive i requisiti per "circuiti elettronici programmabili" nell'allegato R. IEC 60730 allegato H e IEC 60335-1 allegato R, indirizzare la sicurezza dell'hardware e del software MCU usati in Appliance, ad esempio macchine di lavaggio, lavastoviglie, essiccatori, frigoriferi, freezer e forni.

![C RU US 2](./media/user-guide/c-ru-us-logo.png)

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]
>*Per ulteriori informazioni sulle versioni di FileX certificate da UL o sulla disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.*

## <a name="powerful-services-of-filex"></a>Potenti servizi di FileX

### <a name="multiple-media-management"></a>Gestione di più supporti

FileX è in grado di supportare un numero illimitato di supporti fisici. Ogni istanza del supporto ha una propria area di memoria distinta e il driver associato specificato nella chiamata ***fx_media_open*** . La distribuzione predefinita di FileX viene fornita con un semplice driver multimediale RAM e un sistema dimostrativo che usa questo disco RAM.

### <a name="logical-sector-cache"></a>Cache del settore logico

Grazie alla riduzione del numero di trasferimenti interi del settore, sia da che da supporto, la cache del settore logico FileX migliora significativamente le prestazioni. FileX gestisce una cache di settore logica per ogni supporto aperto. La profondità della cache del settore logico è determinata dalla quantità di memoria fornita per FileX con la chiamata API ***fx_media_open*** .

### <a name="contiguous-file-support"></a>Supporto file contiguo

FileX offre supporto file contiguo tramite il servizio API ***fx_file_allocate*** per migliorare e rendere deterministico il tempo di accesso ai file. Questa routine prende la quantità di memoria richiesta e cerca una serie di cluster adiacenti per soddisfare la richiesta. Se tali cluster vengono trovati, vengono preallocati facendoli parte della catena di cluster allocati del file. Sullo sviluppo di supporti fisici, il supporto del file contiguo FileX produce un miglioramento significativo delle prestazioni e rende deterministico il tempo di accesso.

### <a name="dynamic-creation"></a>Creazione dinamica

FileX consente di creare risorse di sistema in modo dinamico. Questa operazione è particolarmente importante se l'applicazione presenta requisiti di configurazione multipli o dinamici. Inoltre, non esistono limiti predeterminati per il numero di risorse FileX che è possibile usare (file multimediali o file). Inoltre, il numero di oggetti di sistema non ha alcun effetto sulle prestazioni.

## <a name="easy-to-use-api"></a>API di facile utilizzo

FileX fornisce la tecnologia file system altamente incorporata in modo molto più facile da comprendere e facile da utilizzare. L'API (Application Programming Interface) FileX rende i servizi intuitivi e coerenti. Non sarà necessario decifrare i servizi di "Alphabet Soup", che sono tutti troppo comuni con altri file System.

Per un elenco completo dei servizi FileX versione 5, vedere [appendice a](appendix-a.md).

## <a name="exfat-support"></a>Supporto di exFAT

exFAT (Extended File Allocation Table) è una file system progettata da Microsoft per consentire il superamento di 2 GB di dimensioni dei file, un limite imposto dai file system FAT32. Si tratta del file system predefinito per schede SD con capacità superiore a 32 GB. Le schede SD o le unità flash formattate con il formato FileX exFAT sono compatibili con Windows. exFAT supporta le dimensioni dei file fino a un exabyte (EB), che è approssimativamente di 1 miliardo GB.

Gli utenti che desiderano utilizzare exFAT devono ricompilare la libreria FileX con il simbolo ***FX_ENABLE_EXFAT** _ definito. Quando si apre un supporto, FileX rileva il tipo di supporto. Se il supporto è formattato con exFAT, FileX legge e scrive il file system seguente exFAT standard. Per formattare nuovi supporti con exFAT, usare il servizio _ *_fx_media_exFAT_format_* *. Per impostazione predefinita, exFAT non è abilitato.

## <a name="fault-tolerant-support"></a>Supporto tolleranza di errore

Il modulo a tolleranza di errore FileX è progettato per evitare file system danneggiamenti causati da interruzioni durante l'aggiornamento del file o della directory. Ad esempio, quando si accodano i dati a un file, FileX deve aggiornare il contenuto del file, la voce della directory e possibilmente le voci FAT. Se questa sequenza di aggiornamento viene interrotta (ad esempio, il glitch dell'alimentazione o il supporto viene espulso durante l'aggiornamento), il file system è in uno stato incoerente, che può influire sull'integrità dell'intera file system, causando il danneggiamento di altri file.

Il modulo a tolleranza di errore FileX funziona registrando tutti i passaggi necessari per aggiornare un file o una directory lungo il percorso. Questa voce di log viene archiviata nei supporti in settori dedicati (blocchi) che FileX è in grado di trovare e accedere. È possibile accedere al percorso dei dati di log anche senza un file system appropriato. Pertanto, nel caso in cui il file system sia danneggiato, FileX è ancora in grado di trovare la voce di log e ripristinare il file system in uno stato valido.

Quando FileX aggiorna un file o una directory, vengono create voci di log. Al termine dell'operazione di aggiornamento, le voci di log vengono rimosse. Se le voci di log non sono state rimosse correttamente dopo l'aggiornamento di un file, se il processo di ripristino determina che il contenuto nella voce di log corrisponde alla file system, non è necessario eseguire alcuna operazione ed è possibile pulire le voci di log.

Nel caso in cui l'operazione di aggiornamento file system sia stata interrotta, la volta successiva che il supporto viene montato da FileX, il modulo a tolleranza di errore analizza le voci di log. Le informazioni contenute nelle voci di log consentono a FileX di eseguire il backup delle modifiche parziali già applicate al file system (nel caso in cui l'errore si verifica durante la fase iniziale dell'operazione di aggiornamento dei file) o se le voci di log contengono informazioni di riesecuzione, FileX è in grado di applicare le modifiche necessarie per completare l'operazione precedente.

Questa funzionalità a tolleranza di errore è disponibile per tutti i file system FAT supportati da FileX, tra cui FAT12, FAT16, FAT32 e exFAT. Per impostazione predefinita, la tolleranza di errore non è abilitata in FileX. Per abilitare la funzionalità di tolleranza di errore, è necessario compilare FileX con il simbolo  **FX_ENABLE_FAULT_TOLERANT** e **FX_FAULT_TOLERANT** definito. In fase di esecuzione, l'applicazione avvia il servizio a tolleranza di errore chiamando **_fx_fault_tolerant_enable_**.
Dopo l'avvio del servizio, tutte le operazioni di scrittura di file e directory passano attraverso il modulo a tolleranza di errore.

Poiché il servizio a tolleranza di errore viene avviato, viene innanzitutto rilevato se il supporto è protetto o meno nel modulo a tolleranza di errore. In caso contrario, FileX presuppone l'integrità del file system e avvia la protezione allocando blocchi liberi dall'file system da utilizzare per la registrazione e la memorizzazione nella cache. Se i log del modulo a tolleranza di errore si trovano nella file system, analizza le voci di log. FileX ripristina l'operazione precedente oppure esegue nuovamente l'operazione precedente, a seconda del contenuto delle voci di log. Il file system diventa disponibile dopo l'elaborazione di tutte le voci di registro precedenti. Ciò garantisce che FIleX inizi da uno stato valido noto.

Dopo che un supporto è stato protetto con il modulo a tolleranza di errore FileX, il supporto non verrà aggiornato con un altro file system. In questo modo le voci di log nel file system non saranno coerenti con il contenuto della tabella FAT, ovvero la voce di directory. Se il supporto viene aggiornato da un altro file system prima di spostarlo di nuovo in FileX con il modulo a tolleranza di errore, il risultato è indefinito.

## <a name="callback-functions"></a>Funzioni di callback

Le tre funzioni di callback seguenti vengono aggiunte a FileX:

- Callback aperto del supporto
- Callback chiusura supporti
- Callback di scrittura file

Dopo la registrazione, queste funzioni invieranno una notifica all'applicazione quando si verificano tali eventi.

## <a name="easy-integration"></a>Facile integrazione

FileX è facilmente integrato con praticamente qualsiasi dispositivo FLASH o multimediale. Il porting di FileX è semplice. Questa guida descrive il processo in modo dettagliato e il driver RAM del sistema dimostrativo rende un ottimo punto di partenza.
