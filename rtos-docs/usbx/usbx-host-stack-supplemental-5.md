---
title: USBX OTG
description: USBX supporta le funzionalità di OTG di USB quando un controller USB compatibile con OTG è disponibile nella progettazione dell'hardware.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3349059f168b145629ca9bf030ddb141350ca760
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823930"
---
# <a name="chapter-5-usbx-otg"></a>Capitolo 5: USBX OTG

USBX supporta le funzionalità di OTG di USB quando un controller USB compatibile con OTG è disponibile nella progettazione dell'hardware.

USBX supporta OTG nello stack USB principale. Per il funzionamento di OTG, tuttavia, è necessario un controller USB specifico. Le funzioni del controller USBX OTG si trovano nella directory ***usbx_otg*** . La versione corrente di USBX supporta solo il LPC3131 NXP con le funzionalità complete di OTG.

Le funzioni regolari del driver del controller (host o dispositivo) sono ancora disponibili nella usbx_device_controllers USBX standard e usbx_host_controllers ma la directory ***usbx_otg*** contiene le funzioni OTG specifiche associate al controller USB.

Sono disponibili quattro categorie di funzioni per un controller OTG oltre alle normali funzioni host/dispositivo.

- Funzioni specifiche di VBUS
- Avvio e arresto del controller
- Gestione ruoli USB
- Gestori di interrupt

## <a name="vbus-functions"></a>Funzioni VBUS

Ogni controller deve disporre di un VBUS Manager per modificare lo stato di VBUS in base ai requisiti di risparmio energia. In genere questa funzione esegue solo l'attivazione o la disattivazione di VBUS

## <a name="start-and-stop-the-controller"></a>Avviare e arrestare il controller

Diversamente da quanto avviene con un'implementazione USB normale, il gruppo OTG richiede che l'host e/o lo stack del dispositivo siano attivati e disattivati in caso di modifica del ruolo.

## <a name="usb-role-manager"></a>Gestione ruoli USB

Il gestore dei ruoli USB riceve i comandi per modificare lo stato del dispositivo USB. Ci sono diversi Stati che richiedono transizioni da e verso quelle specificate nella tabella seguente.

| State                    | Valore | Descrizione                                           |
| ------------------------ | ----- | ----------------------------------------------------- |
| UX_OTG_IDLE            | 0     | Il dispositivo è inattivo. Non connesso ad alcun elemento |
| UX_OTG_IDLE_TO_HOST  | 1     | Il dispositivo è connesso a un connettore di tipo             |
| UX_OTG_IDLE_TO_SLAVE | 2     | Il dispositivo è connesso al connettore di tipo B             |
| UX_OTG_HOST_TO_IDLE  | 3     | Il dispositivo host è stato disconnesso                          |
| UX_OTG_HOST_TO_SLAVE | 4     | Scambio di ruoli da host a slave                          |
| UX_OTG_SLAVE_TO_IDLE | 5     | Il dispositivo slave è disconnesso                          |
| UX_OTG_SLAVE_TO_HOST | 6     | Scambio di ruoli da slave a host                          |

## <a name="interrupt-handlers"></a>Gestori di interrupt

Sia i driver di host che i driver del controller del dispositivo per OTG necessitano di gestori di interrupt diversi per monitorare i segnali oltre gli interrupt USB tradizionali, in particolare i segnali dovuti a SRP e VBUS.

Come inizializzare un controller USB OTG. Per esempio, viene usato NXP LPC3131.

```C
/* Initialize the LPC3131 OTG controller. */
status = ux_otg_lpc3131_initialize(0x19000000, lpc3131_vbus_function,
    tx_demo_change_mode_callback);
```

In questo esempio si inizializza il LPC3131 in modalità OTG passando una funzione VBUS e un callback per la modifica della modalità (da host a slave o viceversa).

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

Il valore della modalità passato può includere i valori seguenti.

- UX_OTG_MODE_IDLE
- UX_OTG_MODE_SLAVE
- UX_OTG_MODE_HOST

L'applicazione può sempre controllare l'aspetto del dispositivo esaminando la variabile.

```C
ux_system_otg ->ux_system_otg_device_type
```

I valori possibili sono i seguenti.

- UX_OTG_DEVICE_A
- UX_OTG_DEVICE_B
- UX_OTG_DEVICE_IDLE

Un dispositivo host USB OTG può sempre richiedere uno scambio di ruolo inviando il comando.

```C
/* Ask the stack to perform a HNP swap with the device. We relinquish the host role to A device. */

ux_host_stack_role_swap(storage ->ux_host_class_storage_device);
```

Per un dispositivo slave, non esiste alcun comando da emettere, ma il dispositivo slave può impostare uno stato per modificare il ruolo, che verrà prelevato dall'host quando emette una GET_STATUS e lo scambio verrà avviato.

```C
/* We are a B device, ask for role swap. The next GET_STATUS from the host will get the status change and do the HNP. */

ux_system_otg ->ux_system_otg_slave_role_swap_flag =
    UX_OTG_HOST_REQUEST_FLAG;
```
