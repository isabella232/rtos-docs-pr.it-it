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
# <a name="chapter-3-usbx-dpump-class-considerations"></a><span data-ttu-id="2a4c6-103">Capitolo 3: considerazioni sulla classe DPUMP di USBX</span><span class="sxs-lookup"><span data-stu-id="2a4c6-103">Chapter 3: USBX DPUMP Class Considerations</span></span>

<span data-ttu-id="2a4c6-104">USBX contiene una classe DPUMP per l'host e il lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-104">USBX contains a DPUMP class for the host and device side.</span></span> <span data-ttu-id="2a4c6-105">Questa classe non è una classe standard, ma piuttosto un esempio in cui viene illustrato come creare un dispositivo semplice utilizzando due pipe bulk e inviando i dati in queste due pipe.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-105">This class is not a standard class in itself, but rather an example that illustrates how to create a simple device by using two bulk pipes and sending data back and forth on these two pipes.</span></span> <span data-ttu-id="2a4c6-106">La classe DPUMP può essere usata per avviare una classe personalizzata o per i dispositivi RS232 legacy.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-106">The DPUMP class could be used to start a custom class or for legacy RS232 devices.</span></span>

<span data-ttu-id="2a4c6-107">Diagramma di flusso DPUMP USB:</span><span class="sxs-lookup"><span data-stu-id="2a4c6-107">USB DPUMP flow chart:</span></span>

![Diagramma di flusso DPUMP USB](./media/usbx-host-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-host-class"></a><span data-ttu-id="2a4c6-109">Classe host USBX DPUMP</span><span class="sxs-lookup"><span data-stu-id="2a4c6-109">USBX DPUMP Host Class</span></span>

<span data-ttu-id="2a4c6-110">Il lato host della classe DPUMP ha due funzioni, una per l'invio dei dati e una per la ricezione dei dati:</span><span class="sxs-lookup"><span data-stu-id="2a4c6-110">The host side of the DPUMP Class has two functions, one for sending data and one for receiving data:</span></span>

- `ux_host_class_dpump_write`
- `ux_host_class_dpump_read`

<span data-ttu-id="2a4c6-111">Entrambe le funzioni sono bloccate per semplificare l'applicazione DPUMP.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-111">Both functions are blocking to make the DPUMP application easier.</span></span> <span data-ttu-id="2a4c6-112">Se è necessario che entrambe le pipe (IN e OUT) siano in esecuzione contemporaneamente, l'applicazione sarà necessaria per creare un thread di trasmissione e un thread di ricezione.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-112">If it is necessary to have both pipes (IN and OUT) running at the same time, the application will be required to create a transmit thread and a receive thread.</span></span>

<span data-ttu-id="2a4c6-113">Il prototipo per la funzione di scrittura è il seguente.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-113">The prototype for the writing function is as follows.</span></span>

```C
UINT ux_host_class_dpump_write(UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,  
    ULONG *actual_length)
```

<span data-ttu-id="2a4c6-114">Dove:</span><span class="sxs-lookup"><span data-stu-id="2a4c6-114">Where:</span></span>

- <span data-ttu-id="2a4c6-115">DPUMP è l'istanza della classe</span><span class="sxs-lookup"><span data-stu-id="2a4c6-115">dpump is the instance of the class</span></span>
- <span data-ttu-id="2a4c6-116">data_pointer è il puntatore al buffer da inviare</span><span class="sxs-lookup"><span data-stu-id="2a4c6-116">data_pointer is the pointer to the buffer to be sent</span></span>
- <span data-ttu-id="2a4c6-117">requested_length è la lunghezza da inviare</span><span class="sxs-lookup"><span data-stu-id="2a4c6-117">requested_length is the length to send</span></span>
- <span data-ttu-id="2a4c6-118">actual_length è la lunghezza inviata dopo il completamento del trasferimento, correttamente o parzialmente.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-118">actual_length is the length sent after completion of the transfer, either successfully or partially.</span></span>

<span data-ttu-id="2a4c6-119">Il prototipo per la funzione di ricezione è simile.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-119">The prototype for the receiving function is similar.</span></span>

```C
UINT ux_host_class_dpump_read(
    UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

<span data-ttu-id="2a4c6-120">Di seguito è riportato un esempio della classe host DPUMP in cui un'applicazione scrive un pacchetto sul lato dispositivo e riceve lo stesso pacchetto nella ricezione:</span><span class="sxs-lookup"><span data-stu-id="2a4c6-120">Here is an example of the host DPUMP class where an application writes a packet to the device side and receives the same packet on the reception:</span></span>

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

## <a name="usbx-dpump-device-class"></a><span data-ttu-id="2a4c6-121">Classe USBX DPUMP Device</span><span class="sxs-lookup"><span data-stu-id="2a4c6-121">USBX DPUMP Device Class</span></span>

<span data-ttu-id="2a4c6-122">La classe Device DPUMP usa un thread, che viene avviato al momento della connessione all'host USB.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-122">The device DPUMP class uses a thread, which is started upon connection to the USB host.</span></span> <span data-ttu-id="2a4c6-123">Il thread attende un pacchetto in arrivo nell'endpoint in blocco.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-123">The thread waits for a packet coming on the Bulk Out endpoint.</span></span> <span data-ttu-id="2a4c6-124">Quando viene ricevuto un pacchetto, il contenuto viene copiato in blocco nel buffer dell'endpoint e viene inviata una transazione sull'endpoint, in attesa che l'host invii una richiesta di lettura da questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-124">When a packet is received, it copies the content to the Bulk In endpoint buffer and posts a transaction on this endpoint, waiting for the host to issue a request to read from this endpoint.</span></span> <span data-ttu-id="2a4c6-125">In questo modo viene fornito un meccanismo di loopback tra le operazioni bulk e bulk negli endpoint.</span><span class="sxs-lookup"><span data-stu-id="2a4c6-125">This provides a loopback mechanism between the Bulk Out and Bulk In endpoints.</span></span>
