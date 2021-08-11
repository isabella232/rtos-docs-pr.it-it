---
title: Considerazioni sulla classe DPUMP USBX
description: USBX contiene una classe DPUMP per il lato host e dispositivo.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 72aa9c1e2200049bf81d64543b690edd001c4ecf9c2cdeb4c3bea5f1b03aa5b8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802575"
---
# <a name="chapter-3-usbx-dpump-class-considerations"></a>Capitolo 3: Considerazioni sulla classe DPUMP USBX

USBX contiene una classe DPUMP per il lato host e dispositivo. Questa classe non è una classe standard di per sé, ma piuttosto un esempio che illustra come creare un dispositivo semplice usando due pipe bulk e inviando dati avanti e indietro su queste due pipe. La classe DPUMP può essere usata per avviare una classe personalizzata o per i dispositivi RS232 legacy.

Diagramma di flusso USB DPUMP:

![Diagramma di flusso DPUMP USB](./media/usbx-host-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-host-class"></a>Classe host DPUMP USBX

Il lato host della classe DPUMP ha due funzioni, una per l'invio di dati e una per la ricezione dei dati:

- `ux_host_class_dpump_write`
- `ux_host_class_dpump_read`

Entrambe le funzioni bloccano per semplificare l'applicazione DPUMP. Se è necessario che entrambe le pipe (IN e OUT) siano in esecuzione contemporaneamente, l'applicazione dovrà creare un thread di trasmissione e un thread di ricezione.

Il prototipo per la funzione di scrittura è il seguente.

```C
UINT ux_host_class_dpump_write(UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,  
    ULONG *actual_length)
```

Dove:

- dpump è l'istanza della classe
- data_pointer è il puntatore al buffer da inviare
- requested_length è la lunghezza da inviare
- actual_length è la lunghezza inviata dopo il completamento del trasferimento, corretta o parziale.

Il prototipo per la funzione ricevente è simile.

```C
UINT ux_host_class_dpump_read(
    UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

Di seguito è riportato un esempio della classe DPUMP host in cui un'applicazione scrive un pacchetto sul lato dispositivo e riceve lo stesso pacchetto alla ricezione:

```C
/* We start with a 'A' in buffer. */
current_char = 'A';

while(1)
{
    /* Initialize the write buffer. */
    ux_utility_memory_set(out_buffer, current_char,
        UX_HOST_CLASS_DPUMP_PACKET_SIZE);

    /* Increment the character in buffer. */
    current_char++;

    /* Check for upper alphabet limit. */
    if (current_char > 'Z')
        current_char = 'A';

    /* Write to the Data Pump Bulk out endpoint. */
    status = ux_host_class_dpump_write (dpump, out_buffer,
        UX_HOST_CLASS_DPUMP_PACKET_SIZE,
        &actual_length);

    /* Verify that the status and the amount of data is correct. */
    if ((status == UX_SUCCESS) && actual_length == UX_HOST_CLASS_DPUMP_PACKET_SIZE)
    {
        /* Read to the Data Pump Bulk out endpoint. */
        status = ux_host_class_dpump_read (dpump, in_buffer,
            UX_HOST_CLASS_DPUMP_PACKET_SIZE, &actual_length);
    }
}
```

## <a name="usbx-dpump-device-class"></a>Classe di dispositivo USBX DPUMP

La classe DPUMP del dispositivo usa un thread che viene avviato al momento della connessione all'host USB. Il thread attende un pacchetto in arrivo nell'endpoint bulk out. Quando un pacchetto viene ricevuto, copia il contenuto nel buffer dell'endpoint Bulk In e invia una transazione su questo endpoint, in attesa che l'host esezioni una richiesta di lettura da questo endpoint. In questo modo viene fornito un meccanismo di loopback tra gli endpoint Bulk Out e Bulk In.
