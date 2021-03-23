---
title: Considerazioni sulle classi USBX DPUMP
description: USBX contiene una classe DPUMP per l'host e il lato dispositivo.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9960b391418fa2f9203e761115bcba71cc3619e8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823978"
---
# <a name="chapter-3-usbx-dpump-class-considerations"></a>Capitolo 3: considerazioni sulla classe DPUMP di USBX

USBX contiene una classe DPUMP per l'host e il lato dispositivo. Questa classe non è una classe standard, ma piuttosto un esempio in cui viene illustrato come creare un dispositivo semplice utilizzando due pipe bulk e inviando i dati in queste due pipe. La classe DPUMP può essere usata per avviare una classe personalizzata o per i dispositivi RS232 legacy.

Diagramma di flusso DPUMP USB:

![Diagramma di flusso DPUMP USB](./media/usbx-host-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-host-class"></a>Classe host USBX DPUMP

Il lato host della classe DPUMP ha due funzioni, una per l'invio dei dati e una per la ricezione dei dati:

- `ux_host_class_dpump_write`
- `ux_host_class_dpump_read`

Entrambe le funzioni sono bloccate per semplificare l'applicazione DPUMP. Se è necessario che entrambe le pipe (IN e OUT) siano in esecuzione contemporaneamente, l'applicazione sarà necessaria per creare un thread di trasmissione e un thread di ricezione.

Il prototipo per la funzione di scrittura è il seguente.

```C
UINT ux_host_class_dpump_write(UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,  
    ULONG *actual_length)
```

Dove:

- DPUMP è l'istanza della classe
- data_pointer è il puntatore al buffer da inviare
- requested_length è la lunghezza da inviare
- actual_length è la lunghezza inviata dopo il completamento del trasferimento, correttamente o parzialmente.

Il prototipo per la funzione di ricezione è simile.

```C
UINT ux_host_class_dpump_read(
    UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

Di seguito è riportato un esempio della classe host DPUMP in cui un'applicazione scrive un pacchetto sul lato dispositivo e riceve lo stesso pacchetto nella ricezione:

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

## <a name="usbx-dpump-device-class"></a>Classe USBX DPUMP Device

La classe Device DPUMP usa un thread, che viene avviato al momento della connessione all'host USB. Il thread attende un pacchetto in arrivo nell'endpoint in blocco. Quando viene ricevuto un pacchetto, il contenuto viene copiato in blocco nel buffer dell'endpoint e viene inviata una transazione sull'endpoint, in attesa che l'host invii una richiesta di lettura da questo endpoint. In questo modo viene fornito un meccanismo di loopback tra le operazioni bulk e bulk negli endpoint.
