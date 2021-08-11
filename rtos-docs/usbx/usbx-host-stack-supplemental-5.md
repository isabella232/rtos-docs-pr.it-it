---
title: USBX OTG
description: USBX supporta le funzionalità OTG di USB quando nella progettazione hardware è disponibile un controller USB conforme a OTG.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bb9a0b98ed3f843ee690dfe419a3684562f1255e6839ddb06ded9d8f6023adcc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798266"
---
# <a name="chapter-5-usbx-otg"></a>Capitolo 5: USBX OTG

USBX supporta le funzionalità OTG di USB quando nella progettazione hardware è disponibile un controller USB conforme a OTG.

USBX supporta OTG nello stack USB principale. Per il funzionamento di OTG, tuttavia, è necessario un controller USB specifico. Le funzioni del controller USBX OTG sono disponibili nella directory ***usbx_otg.*** La versione corrente di USBX supporta solo NXP LPC3131 con funzionalità OTG complete.

Le normali funzioni del driver del controller (host o dispositivo) sono ancora disponibili nelle usbx_device_controllers e usbx_host_controllers USBX standard, ma la directory ***usbx_otg*** contiene le funzioni OTG specifiche associate al controller USB.

Sono disponibili quattro categorie di funzioni per un controller OTG oltre alle normali funzioni host/dispositivo.

- Funzioni specifiche di VBUS
- Avvio e arresto del controller
- Gestione ruoli USB
- Gestori di interrupt

## <a name="vbus-functions"></a>Funzioni VBUS

Ogni controller deve disporre di un gestore VBUS per modificare lo stato di VBUS in base ai requisiti di risparmio energia. In genere questa funzione esegue solo l'attivazione o la disattivazione di VBUS

## <a name="start-and-stop-the-controller"></a>Avviare e arrestare il controller

A differenza di una normale implementazione USB, OTG richiede che l'host e/o lo stack del dispositivo siano attivati e disattivati quando il ruolo cambia.

## <a name="usb-role-manager"></a>Gestione ruoli USB

Il gestore dei ruoli USB riceve i comandi per modificare lo stato dell'USB. Esistono diversi stati che necessitano di transizioni da e verso quelli indicati nella tabella seguente.

| State                    | Valore | Descrizione                                           |
| ------------------------ | ----- | ----------------------------------------------------- |
| UX_OTG_IDLE            | 0     | Il dispositivo è inattivo. Non connesso a nulla |
| UX_OTG_IDLE_TO_HOST  | 1     | Il dispositivo è connesso con un connettore di tipo A             |
| UX_OTG_IDLE_TO_SLAVE | 2     | Il dispositivo è connesso con il connettore di tipo B             |
| UX_OTG_HOST_TO_IDLE  | 3     | Il dispositivo host è stato disconnesso                          |
| UX_OTG_HOST_TO_SLAVE | 4     | Scambio di ruolo da host a slave                          |
| UX_OTG_SLAVE_TO_IDLE | 5     | Il dispositivo slave è disconnesso                          |
| UX_OTG_SLAVE_TO_HOST | 6     | Scambio di ruoli da slave a host                          |

## <a name="interrupt-handlers"></a>Gestori di interrupt

Sia i driver host che i driver del controller di dispositivo per OTG devono essere gestori di interrupt diversi per monitorare i segnali oltre gli interrupt USB tradizionali, in particolare i segnali dovuti a SRP e VBUS.

Come inizializzare un controller OTG USB. Qui viene utilizzato NXP LPC3131 come esempio.

```C
/* Initialize the LPC3131 OTG controller. */
status = ux_otg_lpc3131_initialize(0x19000000, lpc3131_vbus_function,
    tx_demo_change_mode_callback);
```

In questo esempio viene inizializzato LPC3131 in modalità OTG passando una funzione VBUS e un callback per la modifica della modalità (da host a slave o viceversa).

La funzione di callback deve semplicemente registrare la nuova modalità e riattivare un thread in sospeso per agire sul nuovo stato.

```C
void tx_demo_change_mode_callback(ULONG mode)
{
    /* Simply save the otg mode. */
    otg_mode = mode;

    /* Wake up the thread that is waiting. */
    ux_utility_semaphore_put(&mode_change_semaphore);
}
```

Il valore della modalità passato può avere i valori seguenti.

- UX_OTG_MODE_IDLE
- UX_OTG_MODE_SLAVE
- UX_OTG_MODE_HOST

L'applicazione può sempre controllare che cos'è il dispositivo esaminando la variabile .

```C
ux_system_otg ->ux_system_otg_device_type
```

I valori possono essere uno dei seguenti.

- UX_OTG_DEVICE_A
- UX_OTG_DEVICE_B
- UX_OTG_DEVICE_IDLE

Un dispositivo host OTG USB può sempre richiedere uno scambio di ruolo emettendo il comando .

```C
/* Ask the stack to perform a HNP swap with the device. We relinquish the host role to A device. */

ux_host_stack_role_swap(storage ->ux_host_class_storage_device);
```

Per un dispositivo slave, non è necessario eseguire alcun comando, ma il dispositivo slave può impostare uno stato per modificare il ruolo, che verrà prelevato dall'host quando emettere un GET_STATUS e verrà quindi avviato lo scambio.

```C
/* We are a B device, ask for role swap. The next GET_STATUS from the host will get the status change and do the HNP. */

ux_system_otg ->ux_system_otg_slave_role_swap_flag =
    UX_OTG_HOST_REQUEST_FLAG;
```
