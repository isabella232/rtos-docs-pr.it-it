---
title: Capitolo 6-modulo a tolleranza di errore FileX di Azure RTO
description: Questo capitolo contiene una descrizione del modulo a tolleranza d'errore FileX di Azure RTO progettato per mantenere file system integrità se il supporto perde energia o viene espulso durante un'operazione di scrittura di file.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 68a24f0345a2c4d3e824270699b00a2daab32f8e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822409"
---
# <a name="chapter-6---azure-rtos-filex-fault-tolerant-module"></a>Capitolo 6-modulo a tolleranza di errore FileX di Azure RTO

Questo capitolo contiene una descrizione del modulo a tolleranza d'errore FileX di Azure RTO progettato per mantenere file system integrità se il supporto perde energia o viene espulso durante un'operazione di scrittura di file.

## <a name="filex-fault-tolerant-module-overview"></a>Panoramica del modulo a tolleranza di errore FileX

Quando un'applicazione scrive i dati in un file, FileX aggiorna sia i cluster di dati che le informazioni di sistema. Questi aggiornamenti devono essere completati come operazione atomica per tenere coerenti le informazioni nel file system. Ad esempio, quando si accodano i dati a un file, FileX deve trovare un cluster disponibile nel supporto, aggiornare la catena FAT, aggiornare la lunghezza registrata nella voce della directory ed eventualmente aggiornare il numero del cluster iniziale nella voce di directory. L'interruzione dell'alimentazione o dell'espulsione dei supporti può interrompere la sequenza di aggiornamenti, che lascerà il file system in uno stato incoerente. Se lo stato non è coerente, i dati aggiornati possono andare perduti e, a causa di danni alle informazioni di sistema, l'operazione di file system successiva potrebbe danneggiare altri file o directory sul supporto.

Il modulo a tolleranza di errore FileX funziona eseguendo i passaggi di inserimento nel journal necessari per aggiornare un file *prima* di applicare questi passaggi al file System. Se l'aggiornamento del file ha esito positivo, queste voci di log vengono rimosse. Tuttavia, se l'aggiornamento del file viene interrotto, le voci di log vengono archiviate nel supporto. Alla successiva installazione del supporto, FileX rileva queste voci di log dall'operazione di scrittura precedente (non completata). In questi casi, FileX può eseguire il ripristino da un errore eseguendo il rollback delle modifiche già apportate al file system o riapplicando le modifiche necessarie per completare l'operazione precedente. In questo modo, il modulo a tolleranza di errore FileX mantiene l'integrità file system se il supporto perde energia durante un'operazione di aggiornamento.

> [!IMPORTANT]
> *Il modulo a tolleranza di errore FileX non è progettato per evitare file system danneggiamenti causati da un danneggiamento dei supporti fisici con dati validi.*

> [!IMPORTANT]
> *Quando il modulo a tolleranza di errore FileX protegge un supporto, il supporto non deve essere montato da un valore diverso da FileX con tolleranza di errore abilitata. In questo modo le voci di log del file system non saranno coerenti con le informazioni di sistema sui supporti. Se il modulo a tolleranza di errore FileX tenta di elaborare le voci di log dopo che il supporto è stato aggiornato da un altro file system, la procedura di ripristino potrebbe non riuscire, lasciando l'intero file system in uno stato imprevedibile.*

## <a name="use-of-the-fault-tolerant-module"></a>Uso del modulo a tolleranza di errore

La funzionalità di tolleranza di errore FileX è disponibile per tutti i file system FAT supportati da FileX, tra cui FAT12, FAT16, FAT32 e exFAT. Per abilitare la funzionalità di tolleranza di errore, è necessario compilare FileX con il simbolo **FX_ENABLE_FAULT_TOLERANT** definito. In fase di esecuzione, l'applicazione avvia il servizio a tolleranza di errore chiamando **_fx_fault_tolerant_enable_*_ immediatamente dopo la chiamata a _*_fx_media_open_**. Una volta abilitata la tolleranza di errore, tutte le operazioni di scrittura di file nel supporto designato sono protette. Per impostazione predefinita, il modulo a tolleranza di errore non è abilitato.

> [!IMPORTANT]
> * L'applicazione deve assicurarsi che non sia stato eseguito l'accesso file system prima di ***fx_fault_tolerant_enable** _ chiamata. Se l'applicazione scrive i dati nel file system prima dell'abilitazione a tolleranza di errore, è possibile che l'operazione di scrittura danneggi i supporti se le operazioni di scrittura precedenti non sono state completate e il file system non è stato ripristinato utilizzando il entries._ registro a tolleranza di errore

## <a name="filex-fault-tolerant-module-log"></a>Registro modulo a tolleranza di errore FileX

Il log a tolleranza di errore FileX occupa un cluster logico in Flash. L'indice per il numero del cluster iniziale del cluster viene registrato nel settore di avvio del supporto, con un offset specificato dal simbolo **FX_FAULT_TOLERANT_BOOT_INDEX**. Per impostazione predefinita, questo simbolo è definito come 116. Questo percorso viene scelto perché è contrassegnato come riservato in FAT12/16/32 e exFAT Specification.

Nella figura 5 viene illustrato il layout generale della struttura dei log. La struttura di log contiene tre sezioni: intestazione del log, catena FAT e voci di log.

> [!IMPORTANT]
> *Tutti i valori multibyte archiviati nelle voci di log sono in formato little endian.*

![Layout struttura log](./media/user-guide/log-structure-layout.png)

**Figura 5. Layout struttura log**

L'area di intestazione del log contiene informazioni che descrivono l'intera struttura di log e illustrano ogni campo in dettaglio.

**TABELLA 8. Area di intestazione del log**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|ID|4|Identifica una struttura di log a tolleranza di errore FileX. La struttura di log viene considerata non valida se il valore ID non è 0x46544C52.|
|Dimensione totale|2|Indica la dimensione totale (in byte) dell'intera struttura di log.|
|Checksum dell'intestazione|2|Checksum che converte l'area dell'intestazione del log. La struttura di log viene considerata non valida se i campi di intestazione non superano la verifica del checksum.|
|Numero di versione|2|Numeri di versione principale e secondaria a tolleranza di errore FileX.|
|Riservato|2|Per l'espansione futura.|

L'area di intestazione del log è seguita dall'area log della catena FAT. La figura 9 contiene informazioni che descrivono la modalità di modifica della catena FAT. Questa area di log contiene informazioni sui cluster allocati a un file, i cluster rimossi da un file e il punto in cui l'inserimento/eliminazione deve essere e descrive ogni campo nell'area log della catena FAT.

**TABELLA 9. Area log della catena FAT**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|Checksum log catena FAT|2|Checksum dell'intera area di log della catena FAT. L'area log della catena FAT viene considerata non valida se la verifica del checksum non riesce.|
|Contrassegno|1|I valori validi per i flag sono:<br/>0x01 catena FAT valida<br />0x02 BITMAP in uso|
|Riservato|1|Riservate per utilizzo futuro|
|Punto di inserimento-anteriore|4|Il cluster, che appartiene alla catena FAT originale, in cui la catena appena creata verrà collegata a.|
|Cluster Head di una nuova catena FAT|4|Primo cluster della catena FAT appena creata|
|Cluster Head della catena FAT originale|4|Primo cluster della parte della catena FAT originale da rimuovere.|
|Punto di inserimento-indietro|4|Il cluster originale in cui si unisce la catena FAT appena creata in.|
|Punto di eliminazione successivo|4|Questo campo supporta la procedura di pulizia della catena FAT.|

L'area voci di log contiene le voci di log che descrivono le modifiche necessarie per il ripristino da un errore. Nel modulo a tolleranza di errore FileX sono supportati tre tipi di voce di log: voce di log FAT; Voce di log directory; e la voce di log bitmap.

Le seguenti tre figure e tre tabelle descrivono in dettaglio queste voci di log.

![Voce di log FAT](./media/user-guide/fat-log-entry.png)

**Figura 6. Voce di log FAT**

**TABELLA 10. Voce di log FAT**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
Type|2|Tipo di voce, deve essere FX_FAULT_TOLERANT_FAT_LOG_TYPE|
|Dimensione|2|Dimensioni di questa voce|
|Numero di cluster|4|Numero di cluster|
|Valore|4|Valore da scrivere nella voce FAT|

![Voce di log di directory](./media/user-guide/directory-log-entry.png)

**Figura 7. Voce di log di directory**

**TABELLA 11. Voce di log di directory**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|Type|2|Tipo di voce, deve essere FX_FAULT_TOLERANT_DIRECTORY_LOG_TYPE|
|Dimensione|2|Dimensioni di questa voce|
|Offset settore|4|Offset (in byte) nel settore in cui si trova questa directory.|
|Settore di log|4|Settore in cui si trova la voce della directory|
|Dati del registro|Variabile|Contenuto della voce di directory|

![Voce di log bitmap](./media/user-guide/bitmap-log-entry.png)

**Figura 8. Voce di log bitmap**

**TABELLA 12. Voce di log bitmap**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|Type|2|Tipo di voce, deve essere FX_FAULT_TOLERANT_BITMAP_LOG_TYPE|
|Dimensione|2|Dimensioni di questa voce|
|Numero di cluster|4|Numero di cluster|
|Valore|4|Valore da scrivere nella voce FAT|

## <a name="fault-tolerant-protection"></a>Protezione con tolleranza di errore

Dopo l'avvio del modulo a tolleranza di errore FileX, viene innanzitutto eseguita la ricerca di un file di log a tolleranza di errore esistente nel supporto. Se non è possibile trovare un file di log valido, FileX considera i supporti non protetti. In questo caso FileX creerà un file di log a tolleranza di errore nel supporto.

> [!IMPORTANT]
> * FileX non è in grado di proteggere un file system se è stato danneggiato prima dell'avvio del modulo a tolleranza di errore FileX. *

Se si trova un file di log a tolleranza di errore, FileX controlla le voci di log esistenti. Un file di log senza voce di log indica che l'operazione di file precedente è stata completata e che tutte le voci di log sono state rimosse. In questo caso l'applicazione può iniziare a usare la file system con protezione a tolleranza di errore.

Tuttavia, se vengono individuate le voci di log, FileX deve completare l'operazione precedente sui file oppure ripristinare le modifiche già applicate al file system, annullare le modifiche in modo efficace. In entrambi i casi, dopo aver applicato le voci di log al file system, il file system viene ripristinato in uno stato coerente e l'applicazione può iniziare a usare nuovamente il file system.

Per il supporto protetto da FileX, durante l'operazione di aggiornamento dei file la parte relativa ai dati viene scritta direttamente nei supporti. Quando FileX scrive i dati, registra anche tutte le modifiche necessarie per l'applicazione alle voci di directory e alla tabella FAT. Queste informazioni vengono registrate nelle voci di log a tolleranza di file. Questo approccio garantisce che gli aggiornamenti al file system si verifichino dopo che i dati sono stati scritti nei supporti. Se il supporto viene espulso durante la fase di scrittura dei dati, le informazioni cruciali file system non sono ancora state modificate. Di conseguenza, il file system non è influenzato dall'interruzione.

Dopo che tutti i dati sono stati scritti correttamente nel supporto, FileX segue le informazioni contenute nelle voci di log per applicare le modifiche alle informazioni di sistema, una voce alla volta. Dopo aver eseguito il commit di tutte le informazioni di sistema sul supporto, le voci di log vengono rimosse dal log a tolleranza di errore. A questo punto, FileX completa l'operazione di aggiornamento del file.

Durante l'operazione di aggiornamento dei file, i file non vengono aggiornati sul posto. Il modulo a tolleranza di errore alloca un settore per i dati in cui scrivere i nuovi dati, quindi rimuove il settore che contiene i dati da sovrascrivere, aggiornando le voci FAT correlate per collegare il nuovo settore in chian. Per le situazioni in cui è necessario modificare i dati parziali in un cluster, FileX alloca sempre nuovi cluster, scrive tutti i dati dei vecchi cluster con dati aggiornati nei nuovi cluster, quindi libera i cluster precedenti. In questo modo si garantisce che se l'aggiornamento del file viene interrotto, il file originale è intatto. L'applicazione deve tenere presente che, con la protezione a tolleranza di errore di FileX, l'aggiornamento dei dati in un file richiede che i supporti dispongano di spazio libero sufficiente per contenere nuovi dati prima che possano essere rilasciati i settori con dati obsoleti. Se il supporto non dispone di spazio sufficiente per contenere nuovi dati, l'operazione di aggiornamento ha esito negativo.
