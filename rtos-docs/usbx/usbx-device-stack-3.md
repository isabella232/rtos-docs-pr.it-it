---
title: Capitolo 3-componenti funzionali dello stack di dispositivi USBX
description: Questo capitolo contiene una descrizione dello stack di dispositivi USB embedded a prestazioni elevate di USBX da una prospettiva funzionale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: dc57f3e0f6aa6731f4aaedee8169313ca7276cff
ms.sourcegitcommit: 1aeca2f91960856d8cc24fef65f909639e527599
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/31/2021
ms.locfileid: "106082201"
---
# <a name="chapter-3---functional-components-of-usbx-device-stack"></a>Capitolo 3-componenti funzionali dello stack di dispositivi USBX

Questo capitolo contiene una descrizione dello stack di dispositivi USB embedded a prestazioni elevate di USBX da una prospettiva funzionale.

## <a name="execution-overview"></a>Panoramica dell'esecuzione

USBX per il dispositivo è costituito da diversi componenti.

- Inizializzazione
- Chiamate dell'interfaccia dell'applicazione
- Classi di dispositivi
- Stack dispositivo USB
- Controller del dispositivo
- Gestione VBUS

Il diagramma seguente illustra lo stack di dispositivi USBX.

![Stack di dispositivi USBX](media/usbx-device-stack/usbx-device-stack.png)

### <a name="initialization"></a>Inizializzazione

Per attivare USBX, è necessario chiamare la funzione ***ux_system_initialize*** . Questa funzione Inizializza le risorse di memoria di USBX.

Per attivare le funzionalità del dispositivo USBX, è necessario chiamare la funzione ***ux_device_stack_initialize*** . Questa funzione inizializza a sua volta tutte le risorse usate dallo stack di dispositivi USBX, ad esempio thread ThreadX, mutex e semafori.

L'inizializzazione dell'applicazione consente di attivare il controller del dispositivo USB e una o più classi USB. Contrariamente al lato host USB, il lato dispositivo può avere un solo driver del controller USB in esecuzione in qualsiasi momento. Quando le classi sono state registrate nello stack e la funzione di inizializzazione dei controller del dispositivo è stata chiamata, il bus è attivo e lo stack risponderà ai comandi di reimpostazione del bus e enumerazione host.

### <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione

In USBX sono disponibili due livelli di API.

- API dello stack di dispositivi USB
- API della classe dispositivo USB

In genere, un'applicazione USBX non deve chiamare alcuna API dello stack di dispositivi USB. La maggior parte delle applicazioni accederà solo alle API della classe USB.

### <a name="usb-device-stack-apis"></a>API dello stack di dispositivi USB

Le API dello stack di dispositivi sono responsabili della registrazione dei componenti del dispositivo USBX, ad esempio le classi e il Framework del dispositivo.

### <a name="usb-device-class-apis"></a>API della classe dispositivo USB

Le API della classe sono molto specifiche per ogni classe USB. La maggior parte delle API comuni per le classi USB fornisce servizi quali l'apertura e la chiusura di un dispositivo, la lettura e la scrittura in un dispositivo. Le API sono simili per natura al lato host.

## <a name="device-framework"></a>Framework del dispositivo

Il lato dispositivo USB è responsabile della definizione del Framework del dispositivo. Il Framework del dispositivo è suddiviso in tre categorie, come descritto nelle sezioni seguenti.

### <a name="definition-of-the-components-of-the-device-framework"></a>Definizione dei componenti del Framework del dispositivo

La definizione di ogni componente del Framework del dispositivo è correlata alla natura del dispositivo e alle risorse usate dal dispositivo. Di seguito sono riportate le categorie principali.

- Descrittore dispositivo
- Descrittore di configurazione
- Descrittore di interfaccia
- Descrittore dell'endpoint

USBX supporta la definizione dei componenti del dispositivo sia per la velocità elevata che per quella completa (la velocità ridotta viene gestita allo stesso modo della velocità massima). Ciò consente al dispositivo di funzionare in modo diverso quando si è connessi a un host ad alta velocità o a velocità intera. Le differenze tipiche sono le dimensioni di ogni endpoint e la potenza usata dal dispositivo.

La definizione del componente del dispositivo assume il formato di una stringa di byte che segue la specifica USB. La definizione è contigua e l'ordine in cui il Framework è rappresentato in memoria sarà uguale a quello restituito all'host durante l'enumerazione.

Di seguito è riportato un esempio di un Framework di dispositivi per un disco flash USB ad alta velocità.

```c
#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60
UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02, 0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50, 0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};
```

### <a name="definition-of-the-strings-of-the-device-framework"></a>Definizione delle stringhe del Framework del dispositivo

Le stringhe sono facoltative in un dispositivo. Il loro scopo è consentire all'host USB di conoscere il produttore del dispositivo, il nome del prodotto e il numero di revisione tramite stringhe Unicode.

Le stringhe principali sono indici incorporati nei descrittori di dispositivo. Gli indici di stringhe aggiuntive possono essere incorporati in interfacce singole.

Supponendo che il Framework del dispositivo precedente includa tre indici stringa incorporati nel descrittore del dispositivo, la definizione di Framework di stringa potrebbe essere simile a questo codice di esempio

```c
/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string
*/

#define STRING_FRAMEWORK_LENGTH 38
UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72, 0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};
```

Se per ogni velocità è necessario usare stringhe diverse, è necessario usare indici diversi perché gli indici sono indipendenti dalla velocità.

La codifica della stringa è basata su UNICODE. Per ulteriori informazioni sullo standard di codifica UNICODE, fare riferimento alla pubblicazione seguente:

*Lo standard Unicode, la codifica dei caratteri in tutto il mondo, la versione 1., i volumi 1 e 2, Unicode Consortium, Addison-Wesley Publishing Company, Reading MA.*

### <a name="definition-of-the-languages-supported-by-the-device-for-each-string"></a>Definizione delle lingue supportate dal dispositivo per ogni stringa

USBX è in grado di supportare più lingue, anche se la lingua inglese è quella predefinita. La definizione di ogni lingua per i descrittori di stringa è sotto forma di una matrice di definizioni di linguaggi definita come indicato di seguito.

```c
#define LANGUAGE_ID_FRAMEWORK_LENGTH 2
UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

Per supportare altre lingue, è sufficiente aggiungere la definizione a doppio byte del codice della lingua dopo il codice inglese predefinito. Il codice della lingua è stato definito da Microsoft nel documento.

*Sviluppo di software internazionale per Windows 95 e Windows NT, Nadine Kano, Microsoft Press, Redmond WA*

## <a name="vbus-manager"></a>Gestione VBUS

Nella maggior parte delle progettazioni di dispositivi USB, VBUS non fa parte del dispositivo USB core, ma piuttosto connesso a un GPIO esterno, che monitora il segnale di linea.

Di conseguenza, VBUS deve essere gestito separatamente dal driver del controller del dispositivo.

Spetta all'applicazione fornire il controller del dispositivo con l'indirizzo del VBUS IO. VBUS deve essere inizializzato prima dell'inizializzazione del controller del dispositivo.

A seconda della specifica della piattaforma per il monitoraggio di VBUS, è possibile consentire al driver del controller di gestire i segnali VBUS dopo che l'i/o VBUS è stato inizializzato o, se ciò non è possibile, l'applicazione deve fornire il codice per la gestione di VBUS.

Se l'applicazione desidera gestire VBUS autonomamente, l'unico requisito consiste nel chiamare la funzione ***ux_device_stack_disconnect*** quando viene rilevato che un dispositivo è stato estratto. Non è necessario informare il controller quando viene inserito un dispositivo perché il controller verrà riattivato quando viene rilevato il segnale di reimpostazione del BUS di asserzione/deasserzione.
