---
title: Capitolo 3-Descrizione dei servizi AutoIP NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi AutoIP di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 22cc06c32cc9f1857b32d1d2b44a506ea1652cfd
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822751"
---
# <a name="chapter-3---description-of-azure-rtos-netx-autoip-services"></a>Capitolo 3-Descrizione dei servizi AutoIP NetX di Azure RTO

Questo capitolo contiene una descrizione di tutti i servizi AutoIP di Azure RTO NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_auto_ip_create**: *creare un'istanza di AutoIP*
- **nx_auto_ip_delete**: *eliminare l'istanza di AutoIP*
- **nx_auto_ip_get_address**: *ottenere l'indirizzo AutoIP corrente*
- **nx_auto_ip_set_interface**: *impostare l'interfaccia IP per la necessità di un indirizzo AutoIP*
- **nx_auto_ip_start**: *Avvia elaborazione AutoIP*
- **nx_auto_ip_stop**: *Arresta elaborazione AutoIP*

## <a name="nx_auto_ip_create"></a>nx_auto_ip_create

Creare un'istanza di AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_create(NX_AUTO_IP *auto_ip_ptr, CHAR *name,
            NX_IP *ip_ptr, VOID *stack_ptr, ULONG stack_size,
            UINT priority);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza di AutoIP nell'istanza IP specificata.

- **auto_ip_ptr**: puntatore al blocco di controllo AutoIP.
- **nome**: nome dell'istanza di AutoIP.
- **ip_ptr**: puntatore all'istanza IP.
- **stack_ptr**: puntatore all'area dello stack di thread AutoIP.
- **stack_size**: dimensioni dell'area dello stack di thread AutoIP.
- **Priority**: priorità del thread AutoIP.

> [!NOTE]
> Se si usa DHCP, il thread DHCP deve avere una priorità più elevata rispetto al thread dell'istanza IP e al thread AutoIP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) creazione AutoIP riuscita.
- **NX_AUTO_IP_ERROR**: (0XA00) AutoIP crea errore.
- NX_PTR_ERROR: (0x16) non valido AutoIP, ip_ptr o puntatore dello stack.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_delete"></a>nx_auto_ip_delete

Elimina istanza AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza di AutoIP creata in precedenza nell'istanza IP specificata.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr**: puntatore al blocco di controllo AutoIP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione AutoIP riuscita.
- **NX_AUTO_IP_ERROR**: (0XA00) AutoIP eliminare l'errore.
- NX_PTR_ERROR (0x16): puntatore AutoIP non valido.
- NX_CALLER_ERROR (0x11): chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_delete(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully deleted. */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_get_address"></a>nx_auto_ip_get_address

Ottenere l'indirizzo AutoIP corrente

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_get_address(NX_AUTO_IP *auto_ip_ptr,
                            ULONG *local_ip_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo AutoIP attualmente configurato. Se non ne esiste uno, viene restituito un indirizzo IP 0.0.0.0.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr**: puntatore al blocco di controllo AutoIP.
- **local_ip_address**: destinazione per l'indirizzo IP restituito.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) operazione AutoIP riuscita Get.
- **NX_AUTO_IP_NO_LOCAL**: (0XA01) non sono presenti indirizzi AutoIP validi.
- NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, timer, thread, ISRs

### <a name="example"></a>Esempio

```c
ULONG local_address;

/* Get the AutoIP address resolved by the instance "auto_ip_0." */
status = nx_auto_ip_get_address(&auto_ip_0, &local_address);

/* If status is NX_SUCCESS the local IP address is in "local_address." */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_set_interface"></a>nx_auto_ip_set_interface

Impostare l'interfaccia di rete per AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_set_interface(NX_AUTO_IP *auto_ip_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indice per l'interfaccia di rete AutoIP esegue il probe per un indirizzo IP di rete. Il valore predefinito è zero (l'interfaccia di rete primaria). Applicabile solo per i dispositivi multihomed.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr**: puntatore al blocco di controllo AutoIP.
- **interface_index**: interfaccia per verificare l'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) set di interfacce AutoIP riuscito
- **NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0xA02) interfaccia di rete non valida 
- NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, timer, thread, ISRs

### <a name="example"></a>Esempio

```c
ULONG interface_index;

/* Set the network interface on which AutoIP probes for host address. */
status = nx_auto_ip_set_interface(&auto_ip_0, interface_index);

/* If status is NX_SUCCESS the network interface is valid and set in the AutoIP control block auto_ip_0. */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_start"></a>nx_auto_ip_start

Avvia elaborazione AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il protocollo AutoIP in un'istanza di AutoIP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr**: puntatore al blocco di controllo AutoIP.
- **starting_local_address**: indirizzo iniziale AutoIP facoltativo. Il valore IP_ADDRESS (0, 0, 0, 0) specifica che deve essere derivato un indirizzo AutoIP casuale. In caso contrario, se viene specificato un indirizzo AutoIP valido, NetX AutoIP tenterà di assegnare tale indirizzo.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avvio AutoIP riuscito.
- **NX_AUTO_IP_ERROR**: (0XA00) AutoIP errore di avvio.
- NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Start the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_start(&auto_ip_0, IP_ADDRESS(0,0,0,0));

/* If status is NX_SUCCESS an AutoIP instance was successfully started. */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop

## <a name="nx_auto_ip_stop"></a>nx_auto_ip_stop

Arresta elaborazione AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_stop(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta il protocollo AutoIP in un'istanza di AutoIP creata e avviata in precedenza. Questo servizio viene in genere usato quando l'indirizzo IP viene modificato tramite DHCP o manualmente in un indirizzo non AutoIP.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr**: puntatore al blocco di controllo AutoIP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) AutoIP arrestati correttamente.
- **NX_AUTO_IP_ERROR**: (0XA00) AutoIP errore irreversibile.
- NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_stop(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully stopped. */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start