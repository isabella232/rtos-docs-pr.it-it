---
title: Capitolo 6 - Azure RTOS a tolleranza di errore fileX
description: Questo capitolo contiene una descrizione del modulo a tolleranza di errore fileX di Azure RTOS progettato per mantenere l'integrità file system se il supporto perde potenza o viene espulso durante un'operazione di scrittura file.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 66bffa2dbf52bc458bfaf124aa006a79e810100ac2e926c17444daf090519e66
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783749"
---
# <a name="chapter-6---azure-rtos-filex-fault-tolerant-module"></a>Capitolo 6 - Azure RTOS a tolleranza di errore fileX

Questo capitolo contiene una descrizione del modulo a tolleranza di errore fileX di Azure RTOS progettato per mantenere l'integrità file system se il supporto perde potenza o viene espulso durante un'operazione di scrittura file.

## <a name="filex-fault-tolerant-module-overview"></a>Panoramica del modulo a tolleranza di errore FileX

Quando un'applicazione scrive dati in un file, FileX aggiorna sia i cluster di dati che le informazioni di sistema. Questi aggiornamenti devono essere completati come operazione atomica per mantenere le informazioni file system coerenti. Ad esempio, quando si accoda dati a un file, FileX deve trovare un cluster disponibile nel supporto, aggiornare la catena FAT, aggiornare la lunghezza nella voce di directory ed eventualmente aggiornare il numero di cluster iniziale nella voce di directory. Un'interruzione dell'alimentazione o un'espulsione di supporti può interrompere la sequenza di aggiornamenti, che lascia lo stato file system incoerente. Se lo stato incoerente non viene corretto, i dati aggiornati possono andare persi e a causa di un danno alle informazioni di sistema, la successiva operazione di file system può danneggiare altri file o directory nel supporto.

Il modulo a tolleranza di errore FileX funziona con i passaggi di inserimento nel journal necessari per aggiornare un *file* prima che questi passaggi siano applicati al file system. Se l'aggiornamento del file ha esito positivo, queste voci di log vengono rimosse. Tuttavia, se l'aggiornamento del file viene interrotto, le voci di log vengono archiviate nel supporto. Al successivo montaggio del supporto, FileX rileva queste voci di log dall'operazione di scrittura precedente (non completata). In questi casi, FileX può eseguire il ripristino da un errore tramite il rollback delle modifiche già apportate al file system o riapplicando le modifiche necessarie per completare l'operazione precedente. In questo modo, il modulo a tolleranza di errore FileX mantiene file system'integrità se il supporto perde energia durante un'operazione di aggiornamento.

> [!IMPORTANT]
> *Il modulo a tolleranza di errore FileX non è progettato per impedire file system danneggiamento causato dal danneggiamento dei supporti fisici con dati validi al suo interno.*

> [!IMPORTANT]
> *Dopo che il modulo FileX Fault Tolerant protegge un supporto, il supporto non deve essere montato da fileX con tolleranza di errore abilitato. In questo modo, le voci di log nel file system essere incoerenti con le informazioni di sistema sul supporto. Se il modulo FileX Fault Tolerant tenta di elaborare le voci di log dopo l'aggiornamento del supporto da un altro file system, la procedura di ripristino potrebbe non riuscire, lasciando l'intero file system in uno stato imprevedibile.*

## <a name="use-of-the-fault-tolerant-module"></a>Uso del modulo fault tolerant

La funzionalità Tolleranza di errore FileX è disponibile per tutti i file system FAT supportati da FileX, inclusi FAT12, FAT16, FAT32 ed exFAT. Per abilitare la funzionalità a tolleranza di errore, FileX deve essere compilato con il **simbolo FX_ENABLE_FAULT_TOLERANT** definito. In fase di esecuzione, l'applicazione avvia il servizio a tolleranza di errore **_chiamando fx_fault_tolerant_enable_*_ immediatamente*** dopo la chiamata a _ fx_media_open . Dopo aver abilitato la tolleranza di errore, tutte le operazioni di scrittura dei file nei supporti designati sono protette. Per impostazione predefinita, il modulo a tolleranza di errore non è abilitato.

> [!IMPORTANT]
> *L'applicazione deve assicurarsi che il file system non sia accessibile prima di ***fx_fault_tolerant_enable** _chiamata. Se l'applicazione scrive dati nel file system prima dell'abilitazione a tolleranza di errore, l'operazione di scrittura potrebbe danneggiare il supporto se le operazioni di scrittura precedenti non sono state completate e il file system non è stato ripristinato usando log a tolleranza di errore entries._

## <a name="filex-fault-tolerant-module-log"></a>Log del modulo a tolleranza di errore FileX

Il log a tolleranza di errore FileX occupa un cluster logico in flash. L'indice al numero di cluster iniziale del cluster viene registrato nel settore di avvio del supporto, con un offset specificato dal simbolo **FX_FAULT_TOLERANT_BOOT_INDEX**. Per impostazione predefinita, questo simbolo è definito come 116. Questo percorso viene scelto perché è contrassegnato come riservato nella specifica FAT12/16/32 ed exFAT.

La figura 5, "Layout struttura log", mostra il layout generale della struttura del log. La struttura del log contiene tre sezioni: Intestazione log, Catena FAT e Voci di log.

> [!IMPORTANT]
> *Tutti i valori multi byte archiviati nelle voci di log sono in formato Little Endian.*

![Layout della struttura dei log](./media/user-guide/log-structure-layout.png)

**Figura 5. Layout della struttura dei log**

L'area Intestazione log contiene informazioni che descrivono l'intera struttura del log e illustrano in dettaglio ogni campo.

**TABELLA 8. Area dell'intestazione del log**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|ID|4|Identifica una struttura di log a tolleranza di errore FileX. La struttura del log viene considerata non valida se il valore ID non è 0x46544C52.|
|Dimensione totale|2|Indica le dimensioni totali (in byte) dell'intera struttura del log.|
|Checksum dell'intestazione|2|Checksum che converte l'area di intestazione del log. La struttura del log viene considerata non valida se i campi di intestazione non riescono a eseguire la verifica del checksum.|
|Numero di versione|2|Numeri di versione principale e secondaria a tolleranza di errore FileX.|
|Riservato|2|Per un'espansione futura.|

L'area Intestazione log è seguita dall'area Log catena FAT. La figura 9 contiene informazioni che descrivono come modificare la catena FAT. Questa area di log contiene informazioni sui cluster allocati a un file, sui cluster rimossi da un file e sulla posizione in cui l'inserimento/eliminazione deve essere e descrive ogni campo nell'area Log catena FAT.

**TABELLA 9. Area di log della catena FAT**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|Checksum del log della catena FAT|2|Checksum dell'intera area del log della catena FAT. L'area Fat Chain Log (Log catena FAT) viene considerata non valida se non supera la verifica del checksum.|
|Contrassegno|1|I valori di flag validi sono:<br/>0x01 catena FAT valida<br />0x02 viene usata la bitmap|
|Riservato|1|Riservate per utilizzo futuro|
|Punto di inserimento - Frontale|4|Cluster (appartenente alla catena FAT originale) a cui verrà collegata la catena appena creata.|
|Cluster head della nuova catena FAT|4|Primo cluster della catena FAT appena creata|
|Cluster head della catena FAT originale|4|Primo cluster della parte della catena FAT originale da rimuovere.|
|Punto di inserimento - Indietro|4|Cluster originale in cui si unisce la catena FAT appena creata.|
|Punto di eliminazione successivo|4|Questo campo assiste la procedura di pulizia della catena FAT.|

L'area Voci di log contiene voci di log che descrivono le modifiche necessarie per il ripristino in caso di errore. Nel modulo a tolleranza di errore FileX sono supportati tre tipi di voce di log: voce di log FAT; Voce del log della directory; e voce di log bitmap.

Le tre figure e le tre tabelle seguenti descrivono in dettaglio queste voci di log.

![Voce di log FAT](./media/user-guide/fat-log-entry.png)

**Figura 6. Voce di log FAT**

**TABELLA 10. Voce di log FAT**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
Type|2|Tipo di voce, deve essere FX_FAULT_TOLERANT_FAT_LOG_TYPE|
|Dimensione|2|Dimensioni di questa voce|
|Numero cluster|4|Numero cluster|
|Valore|4|Valore da scrivere nella voce FAT|

![Voce di log della directory](./media/user-guide/directory-log-entry.png)

**Figura 7. Voce di log della directory**

**TABELLA 11. Voce di log della directory**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|Type|2|Tipo di voce, deve essere FX_FAULT_TOLERANT_DIRECTORY_LOG_TYPE|
|Dimensione|2|Dimensioni di questa voce|
|Offset di settore|4|Offset (in byte) nel settore in cui si trova questa directory.|
|Settore dei log|4|Settore in cui si trova la voce di directory|
|Dati del registro|Variabile|Contenuto della voce di directory|

![Voce di log bitmap](./media/user-guide/bitmap-log-entry.png)

**Figura 8. Voce di log bitmap**

**TABELLA 12. Voce di log bitmap**

|Campo|Dimensioni (in byte)|Descrizione|
|-----|--------------|-----------|
|Type|2|Tipo di voce, deve essere FX_FAULT_TOLERANT_BITMAP_LOG_TYPE|
|Dimensione|2|Dimensioni di questa voce|
|Numero cluster|4|Numero cluster|
|Valore|4|Valore da scrivere nella voce FAT|

## <a name="fault-tolerant-protection"></a>Protezione a tolleranza di errore

Dopo l'avvio, il modulo a tolleranza di errore FileX cerca prima di tutto un file di log a tolleranza di errore esistente nel supporto. Se non è possibile trovare un file di log valido, FileX considera il supporto non protetto. In questo caso FileX creerà un file di log a tolleranza di errore nel supporto.

> [!IMPORTANT]
> *FileX non è in grado di proteggere un file system se è stato danneggiato prima dell'avvio del modulo a tolleranza di errore FileX. *

Se viene individuato un file di log a tolleranza di errore, FileX verifica la presenza di voci di log esistenti. Un file di log senza voce di log indica che l'operazione precedente al file ha avuto esito positivo e che tutte le voci di log sono state rimosse. In questo caso l'applicazione può iniziare a usare il file system con protezione a tolleranza di errore.

Tuttavia, se vengono individuate voci di log, FileX deve completare l'operazione precedente sul file o annullare le modifiche già applicate al file system, annullando di fatto le modifiche. In entrambi i casi, dopo che le voci di log sono state applicate al file system, il file system viene ripristinato in uno stato coerente e l'applicazione può iniziare a usare nuovamente il file system.

Per i supporti protetti da FileX, durante l'operazione di aggiornamento dei file, la parte dei dati viene scritta direttamente nel supporto. Quando FileX scrive i dati, registra anche tutte le modifiche da applicare alle voci di directory, la tabella FAT. Queste informazioni vengono registrate nelle voci di log a tolleranza di file. Questo approccio garantisce che gli aggiornamenti al file system dopo la scrittura dei dati nel supporto. Se il supporto viene espulso durante la fase di scrittura dei dati, le informazioni file system non sono ancora state modificate. Di conseguenza, file system'interruzione non è interessata dall'interruzione.

Dopo che tutti i dati sono stati scritti correttamente nel supporto, FileX segue le informazioni nelle voci di log per applicare le modifiche alle informazioni di sistema, una voce alla volta. Dopo il commit di tutte le informazioni di sistema nel supporto, le voci di log vengono rimosse dal log a tolleranza di errore. A questo punto, FileX completa l'operazione di aggiornamento dei file.

Durante l'operazione di aggiornamento dei file, i file non vengono aggiornati sul posto. Il modulo a tolleranza di errore alloca un settore per i dati in cui scrivere i nuovi dati e quindi rimuove il settore che contiene i dati da sovrascrittura, aggiornando le voci FAT correlate per collegare il nuovo settore nel chian. Nelle situazioni in cui è necessario modificare i dati parziali in un cluster, FileX alloca sempre nuovi cluster, scrive tutti i dati dei cluster con i dati aggiornati nei nuovi cluster e quindi libera i cluster vecchi. Ciò garantisce che se l'aggiornamento del file viene interrotto, il file originale rimane intatto. L'applicazione deve tenere presente che, in base alla protezione a tolleranza di errore FileX, l'aggiornamento dei dati in un file richiede che il supporto abbia spazio libero sufficiente per contenere i nuovi dati prima che i settori con dati precedenti possano essere rilasciati. Se il supporto non ha spazio sufficiente per contenere i nuovi dati, l'operazione di aggiornamento non riesce.
