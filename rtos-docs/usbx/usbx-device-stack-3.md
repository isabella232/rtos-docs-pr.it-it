---
title: Capitolo 3 - Componenti funzionali dello stack di dispositivi USBX
description: Questo capitolo contiene una descrizione dello stack di dispositivi USB incorporato USBX ad alte prestazioni dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 104badcbf1ec682cd8b09008578ba91768834d694473ecccf59e35637dfd9f3c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791355"
---
# <a name="chapter-3---functional-components-of-usbx-device-stack"></a>Capitolo 3 - Componenti funzionali dello stack di dispositivi USBX

Questo capitolo contiene una descrizione dello stack di dispositivi USB incorporato USBX ad alte prestazioni dal punto di vista funzionale.

## <a name="execution-overview"></a>Panoramica dell'esecuzione

USBX per il dispositivo è costituito da diversi componenti.

- Inizializzazione
- Chiamate all'interfaccia dell'applicazione
- Classi di dispositivi
- Stack di dispositivi USB
- Controller del dispositivo
- Gestione VBUS

Il diagramma seguente illustra lo stack di dispositivi USBX.

![Stack di dispositivi USBX](media/usbx-device-stack/usbx-device-stack.png)

### <a name="initialization"></a>Inizializzazione

Per attivare USBX, è necessario ***chiamare*** ux_system_initialize funzione. Questa funzione inizializza le risorse di memoria di USBX.

Per attivare le funzionalità dei dispositivi USBX, è necessario ***chiamare ux_device_stack_initialize*** funzione. Questa funzione a sua volta inizializza tutte le risorse usate dallo stack di dispositivi USBX, ad esempio thread ThreadX, mutex e semafori.

È l'inizializzazione dell'applicazione ad attivare il controller del dispositivo USB e una o più classi USB. Diversamente dal lato host USB, sul lato dispositivo può essere in esecuzione un solo driver controller USB in qualsiasi momento. Quando le classi sono state registrate nello stack e la funzione di inizializzazione del controller del dispositivo è stata chiamata, il bus è attivo e lo stack risponderà ai comandi di enumerazione host e reimpostazione del bus.

### <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione

Esistono due livelli di API in USBX.

- API dello stack di dispositivi USB
- API della classe di dispositivi USB

In genere, un'applicazione USBX non deve chiamare alcuna API dello stack di dispositivi USB. La maggior parte delle applicazioni accederà solo alle API di classe USB.

### <a name="usb-device-stack-apis"></a>API dello stack di dispositivi USB

Le API dello stack di dispositivi sono responsabili della registrazione dei componenti del dispositivo USBX, ad esempio le classi e il framework di dispositivi.

### <a name="usb-device-class-apis"></a>API della classe di dispositivi USB

Le API di classe sono molto specifiche per ogni classe USB. La maggior parte delle API comuni per le classi USB fornisce servizi come l'apertura/chiusura di un dispositivo e la lettura e la scrittura in un dispositivo. Le API sono di natura simile al lato host.

## <a name="device-framework"></a>Framework di dispositivi

Il lato dispositivo USB è responsabile della definizione del framework di dispositivi. Il framework di dispositivi è suddiviso in tre categorie, come descritto nelle sezioni seguenti.

### <a name="definition-of-the-components-of-the-device-framework"></a>Definizione dei componenti di Device Framework

La definizione di ogni componente del framework di dispositivi è correlata alla natura del dispositivo e alle risorse utilizzate dal dispositivo. Di seguito sono riportate le categorie principali.

- Descrittore del dispositivo
- Descrittore di configurazione
- Descrittore di interfaccia
- Descrittore dell'endpoint

USBX supporta la definizione dei componenti del dispositivo sia per la velocità elevata che per la velocità completa (la velocità bassa viene considerata come la velocità completa). Ciò consente al dispositivo di operare in modo diverso quando è connesso a un host ad alta velocità o a velocità completa. Le differenze tipiche sono le dimensioni di ogni endpoint e la potenza utilizzata dal dispositivo.

La definizione del componente del dispositivo assume la forma di una stringa di byte che segue la specifica USB. La definizione è contigua e l'ordine in cui il framework è rappresentato in memoria sarà uguale a quello restituito all'host durante l'enumerazione.

Di seguito è riportato un esempio di framework di dispositivo per un disco flash USB ad alta velocità.

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

### <a name="definition-of-the-strings-of-the-device-framework"></a>Definizione delle stringhe del framework di dispositivi

Le stringhe sono facoltative in un dispositivo. Il loro scopo è quello di inserire l'host USB in informazioni sul produttore del dispositivo, sul nome del prodotto e sul numero di revisione tramite stringhe Unicode.

Le stringhe principali sono indici incorporati nei descrittori di dispositivo. È possibile incorporare indici di stringhe aggiuntivi in singole interfacce.

Supponendo che il framework di dispositivi precedente abbia tre indici di stringa incorporati nel descrittore di dispositivo, la definizione del framework di stringhe potrebbe essere simile a questo codice di esempio.

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

Se è necessario usare stringhe diverse per ogni velocità, è necessario usare indici diversi perché gli indici sono indipendenti dalla velocità.

La codifica della stringa è basata su UNICODE. Per altre informazioni sullo standard di codifica UNICODE, vedere la pubblicazione seguente:

*Standard Unicode, codifica dei caratteri a livello mondiale, versione 1., volumi 1 e 2, The Unicode Consortium, Addison-Wesley Publishing Company, Reading MA.*

### <a name="definition-of-the-languages-supported-by-the-device-for-each-string"></a>Definizione delle lingue supportate dal dispositivo per ogni stringa

USBX è in grado di supportare più lingue anche se l'inglese è l'impostazione predefinita. La definizione di ogni linguaggio per i descrittori di stringa è sotto forma di una matrice di definizioni di linguaggi definiti come segue.

```c
#define LANGUAGE_ID_FRAMEWORK_LENGTH 2
UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

Per supportare altre lingue, è sufficiente aggiungere la definizione a byte doppio del codice della lingua dopo il codice inglese predefinito. Il codice della lingua è stato definito da Microsoft nel documento.

*Developing International Software for Windows 95 and Windows NT, Nadine Kano, Microsoft Press, Redmond WA*

## <a name="vbus-manager"></a>VBUS Manager

Nella maggior parte dei progetti di dispositivi USB, VBUS non fa parte del core del dispositivo USB, ma è connesso a un GPIO esterno, che monitora il segnale di linea.

Di conseguenza, le vbus devono essere gestite separatamente dal driver del controller di dispositivo.

È l'applicazione a fornire al controller del dispositivo l'indirizzo dell'I/O VBUS. Le VBUS devono essere inizializzate prima dell'inizializzazione del controller del dispositivo.

A seconda della specifica della piattaforma per il monitoraggio vbus, è possibile consentire al driver del controller di gestire i segnali VBUS dopo l'inizializzazione dell'I/O vbus o, se non è possibile, l'applicazione deve fornire il codice per la gestione delle VBUS.

Se l'applicazione vuole gestire la vbus da sola, l'unico requisito è chiamare la funzione ***ux_device_stack_disconnect*** quando rileva che un dispositivo è stato estratto. Non è necessario informare il controller quando viene inserito un dispositivo perché il controller si riattiva quando viene rilevato il segnale di asserzione/deassert BUS RESET.
