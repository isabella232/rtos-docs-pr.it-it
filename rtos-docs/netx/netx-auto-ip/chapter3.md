---
title: Capitolo 3 - Descrizione dei Azure RTOS NetX AutoIP
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX AutoIP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 15a70416f9d4d1324d930820b09366a7e7cd6f4525872472cd88edfbb25ee155
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796872"
---
# <a name="chapter-3---description-of-azure-rtos-netx-autoip-services"></a>Capitolo 3 - Descrizione dei Azure RTOS NetX AutoIP

Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX AutoIP (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_auto_ip_create:** Creare *un'istanza di AutoIP*
- **nx_auto_ip_delete:** Eliminare *l'istanza di AutoIP*
- **nx_auto_ip_get_address:** ottenere *l'indirizzo AutoIP corrente*
- **nx_auto_ip_set_interface:** impostare *l'interfaccia IP che deve avere un indirizzo AutoIP*
- **nx_auto_ip_start**: Avviare *l'elaborazione AutoIP*
- **nx_auto_ip_stop:** *Arrestare l'elaborazione AutoIP*

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

- **auto_ip_ptr:** puntatore al blocco di controllo AutoIP.
- **name**: nome dell'istanza di AutoIP.
- **ip_ptr:** puntatore all'istanza IP.
- **stack_ptr:** puntatore all'area dello stack di thread AutoIP.
- **stack_size**: dimensioni dell'area dello stack di thread AutoIP.
- **priority:** priorità del thread AutoIP.

> [!NOTE]
> Se si usa DHCP, il thread DHCP deve avere una priorità più alta rispetto al thread dell'istanza IP e al thread AutoIP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione autoIP riuscita.
- **NX_AUTO_IP_ERROR:**(0xA00) Errore di creazione AutoIP.
- NX_PTR_ERROR: (0x16) AutoIP, ip_ptr o puntatore dello stack non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a>Vedere anche

nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_delete"></a>nx_auto_ip_delete

Eliminare un'istanza di AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza di AutoIP creata in precedenza nell'istanza IP specificata.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr:** puntatore al blocco di controllo AutoIP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione autoIP riuscita.
- **NX_AUTO_IP_ERROR:**(0xA00) Errore di eliminazione autoIP.
- NX_PTR_ERROR (0x16): puntatore AutoIP non valido.
- NX_CALLER_ERROR (0x11): chiamante di questo servizio non valido.

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

Questo servizio recupera l'indirizzo AutoIP attualmente di configurazione. Se non è presente, viene restituito un indirizzo IP 0.0.0.0.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr:** puntatore al blocco di controllo AutoIP.
- **local_ip_address:** destinazione per l'indirizzo IP mittente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Ottenere l'indirizzo AutoIP riuscito.
- **NX_AUTO_IP_NO_LOCAL**: (0xA01) Nessun indirizzo AutoIP valido.
- NX_PTR_ERROR: (0x16) Puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, timer, thread, ISR

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

Questo servizio imposta l'indice per l'interfaccia di rete che AutoIP proberà per un indirizzo IP di rete. Il valore predefinito è zero (l'interfaccia di rete primaria). Applicabile solo per i dispositivi multihomed.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr:** puntatore al blocco di controllo AutoIP.
- **interface_index:** interfaccia per l'indirizzo IP del probe per

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Set di interfacce AutoIP riuscito
- **NX_AUTO_IP_BAD_INTERFACE_INDEX:**(0xA02) Interfaccia di rete non valida 
- NX_PTR_ERROR: (0x16) Puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, timer, thread, ISR

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

Avviare l'elaborazione AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il protocollo AutoIP in un'istanza di AutoIP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr:** puntatore al blocco di controllo AutoIP.
- **starting_local_address:** indirizzo iniziale autoIP facoltativo. Il valore IP_ADDRESS(0,0,0,0) specifica che deve essere derivato un indirizzo AutoIP casuale. In caso contrario, se viene specificato un indirizzo AutoIP valido, NetX AutoIP tenta di assegnarlo.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Avvio automatico di AutoIP riuscito.
- **NX_AUTO_IP_ERROR:**(0xA00) AutoIP start error (Errore di avvio di AutoIP).
- NX_PTR_ERROR: (0x16) Puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

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

Arrestare l'elaborazione di AutoIP

### <a name="prototype"></a>Prototipo

```c
UINT nx_auto_ip_stop(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta il protocollo AutoIP in un'istanza di AutoIP creata e avviata in precedenza. Questo servizio viene in genere usato quando l'indirizzo IP viene modificato tramite DHCP o manualmente in un indirizzo non AutoIP.

### <a name="input-parameters"></a>Parametri di input

- **auto_ip_ptr:** puntatore al blocco di controllo AutoIP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Arresto autoIP riuscito.
- **NX_AUTO_IP_ERROR:**(0xA00) AutoIP stop error (Errore di arresto di AutoIP).
- NX_PTR_ERROR: (0x16) Puntatore AutoIP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

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