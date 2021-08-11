---
title: Capitolo 6 - Utilizzo della classe USBX CDC-ECM
description: USBX contiene una classe CDC-ECM per il lato host e dispositivo. Questa classe è progettata per essere usata con NetX, in particolare la classe USBX CDC-ECM funge da driver per NetX. Per questo motivo non sono elencate API CDC-ECM nel capitolo 5.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 7328b8c3537acac1ef02fced32b0c2731065aea0c6e2742a96f0644e9a8045f0
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798351"
---
# <a name="chapter-6---usbx-cdc-ecm-class-usage"></a>Capitolo 6 - Utilizzo della classe USBX CDC-ECM

USBX contiene una classe CDC-ECM per il lato host e dispositivo. Questa classe è progettata per essere usata con NetX, in particolare la classe USBX CDC-ECM funge da driver per NetX. Per questo motivo non sono elencate API CDC-ECM nel capitolo 5.

Dopo l'inizializzazione di NetX e USBX e la ricerca di un'istanza di un dispositivo CDC-ECM da parte di USBX, l'applicazione usa esclusivamente NetX per comunicare con il dispositivo. L'inizializzazione segue il modello illustrato nell'esempio seguente.

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
