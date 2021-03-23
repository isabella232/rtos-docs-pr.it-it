---
title: Capitolo 6-uso della classe CDC-ECM USBX
description: USBX contiene una classe CDC-ECM per l'host e il lato dispositivo. Questa classe è progettata per essere usata con NetX, in particolare, la classe USBX CDC-ECM funge da driver per NetX. Questo è il motivo per cui non esistono API CDC-ECM elencate nel capitolo 5.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 18e7e075788623916de36cf911597230295b56c5
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824341"
---
# <a name="chapter-6---usbx-cdc-ecm-class-usage"></a><span data-ttu-id="15bbb-105">Capitolo 6-uso della classe CDC-ECM USBX</span><span class="sxs-lookup"><span data-stu-id="15bbb-105">Chapter 6 - USBX CDC-ECM Class Usage</span></span>

<span data-ttu-id="15bbb-106">USBX contiene una classe CDC-ECM per l'host e il lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="15bbb-106">USBX contains a CDC-ECM class for the host and device side.</span></span> <span data-ttu-id="15bbb-107">Questa classe è progettata per essere usata con NetX, in particolare, la classe USBX CDC-ECM funge da driver per NetX.</span><span class="sxs-lookup"><span data-stu-id="15bbb-107">This class is designed to be used with NetX, specifically, the USBX CDC-ECM class acts as the driver for NetX.</span></span> <span data-ttu-id="15bbb-108">Questo è il motivo per cui non esistono API CDC-ECM elencate nel capitolo 5.</span><span class="sxs-lookup"><span data-stu-id="15bbb-108">This is why there are no CDC-ECM APIs listed in Chapter 5.</span></span>

<span data-ttu-id="15bbb-109">Dopo l'inizializzazione di NetX e USBX e l'utilizzo di un'istanza di un dispositivo CDC-ECM da parte di USBX, l'applicazione usa esclusivamente NetX per comunicare con il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="15bbb-109">Once NetX and USBX are initialized and an instance of a CDC-ECM device is found by USBX, the application exclusively uses NetX to communicate with the device.</span></span> <span data-ttu-id="15bbb-110">L'inizializzazione segue il modello illustrato nell'esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="15bbb-110">Initialization follows the pattern shown in the example below.</span></span>

```c
UINT status;

/* The USB controller should be the last component initialized so that
everything is ready when data starts being received. */

/* Initialize USBX. */

ux_system_initialize(memory_pointer, UX_USBX_MEMORY_SIZE, UX_NULL, 0);

/* The code below is required for installing the host portion of USBX */
status = ux_host_stack_initialize(UX_NULL);

/* Register cdc_ecm class. */

status = ux_host_stack_class_register(_ux_system_host_class_cdc_ecm_name,
    ux_host_class_cdc_ecm_entry);

/* Perform the initialization of the network driver. */

_ux_network_driver_init();

/* Initialize NetX. Refer to NetX user guide for details to add initialization code. */

/* Register the platform-specific USB controller. */

status = ux_host_stack_hcd_register("controller_name", controller_entry, param1, param2);

/* Find the CDC-ECM class. */
class_cdc_ecm_get();

/* Now wait for the link to be up. */

while (cdc_ecm -> ux_host_class_cdc_ecm_link_state != UX_HOST_CLASS_CDC_ECM_LINK_STATE_UP)
    tx_thread_sleep(10);

/* At this point, everything has been initialized, and we've found a CDC-ECM device.
    Now NetX can be used to communicate with the device. */
```
