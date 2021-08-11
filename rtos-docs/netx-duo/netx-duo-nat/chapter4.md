---
title: Capitolo 4 - Descrizione dei servizi NAT
description: Questo capitolo contiene una descrizione di tutti i servizi API NAT di NetX Duo in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: dbe2cb25607162b62b048251927bdc7671c5884d2a3b45b6b24bae539e08d24a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797296"
---
# <a name="chapter-4---description-of-nat-services"></a>Capitolo 4 - Descrizione dei servizi NAT

Questo capitolo contiene una descrizione di tutti i servizi API NAT di NetX Duo (elencati di seguito) in ordine alfabetico.

> [!NOTE]
> Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_nat_create"></a>nx_nat_create

Creare un server NAT

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server NAT.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT da creare
- **ip_ptr puntatore all'istanza** IP
- **global_interface_index** Indicizzare l'interfaccia di rete globale
- **dynamic_cache_memory** Area di memoria del puntatore alla tabella NAT
- **dynamic_cache_size** Dimensioni dell'area di memoria per la tabella NAT

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** server NAT (0x00) creato correttamente
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido
- NX_NAT_PARAM_ERROR (0xD01) Input non puntatore non valido
- NX_NAT_CACHE_ERROR (0xD02) Input puntatore cache non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
#define NX_NAT_ENTRY_CACHE_SIZE 20480

static UCHAR nat_cache[NX_NAT_ENTRY_CACHE_SIZE];
UINT global_interface_index = 0;

/* Create a NAT Server and cache with a global interface index. */
status = nx_nat_create(nat_ptr, ip_ptr, global_interface_index,
    nat_cache, NX_NAT_ENTRY_CACHE_SIZE);

/* If status = NX_SUCCESS, the NAT instance was successfully
    created. */
```

## <a name="nx_nat_delete"></a>nx_nat_delete

Eliminare un server NAT

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_delete(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un server NAT creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT da eliminare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) NAT eliminato correttamente
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Delete the NAT instance. */
status = nx_nat_delete (nat_ptr);

/* If the NAT instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_nat_enable"></a>nx_nat_enable

Abilitare l'istanza IP per NAT

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_enable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita l'istanza IP per NAT ,ad esempio inoltrando i pacchetti ricevuti al server NAT.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) NAT abilitato correttamente
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Enable the NAT server. */
status = nx_nat_enable (nat_ptr);

/* If status = NX_SUCCESS, the IP instance was successfully enabled for NAT. */
```

## <a name="nx_nat_disable"></a>nx_nat_disable

Disabilitare l'istanza IP per NAT

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_disable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita NAT nell'istanza IP.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) NAT disabilitato correttamente
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Disable the NAT server. */
status = nx_nat_disable (nat_ptr);

/* If status = NX_SUCCESS the NAT operation successfully disable. */
```

## <a name="nx_nat_cache_notify_set"></a>nx_nat_cache_notify_set

Impostare una funzione di callback di notifica completa della cache

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)
    (NX_NAT_DEVICE *nat_ptr)));
```

### <a name="description"></a>Descrizione

Questo servizio registra il callback completo della cache con il puntatore a funzione di input cache_full_notify_cb che punta a una funzione di notifica completa della cache definita dall'utente.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT
- **cache_full_notify_cb** Puntatore alla funzione di notifica completa della cache

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La funzione di notifica completa della cache è stata impostata correttamente
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido
- NX_NAT_PARAM_ERROR (0xD01) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Set the cache full notify callback function to the NAT instance. */
status = nx_nat_cache_notify_set(nat_ptr, cache_full_notify_cb);

/* If status = NX_SUCCESS the callback function was successfully set. */
```

## <a name="nx_nat_inbound_entry_create"></a>nx_nat_inbound_entry_create

Creare una voce in ingresso nella tabella di conversione NAT

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr
    ULONG local_ip_address,
    USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

### <a name="description"></a>Descrizione

Questo servizio crea una voce in ingresso come statica (voce permanente, non scade mai) e la aggiunge alla tabella di conversione NAT. Queste voci vengono in genere create per i server host locali in cui viene avviata una connessione da un host nella rete esterna. Il server NAT verifica che la porta esterna non sia già in uso nella tabella di conversione o sia associata da un socket NetX Duo esistente dello stesso protocollo.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT
- **entry_ptr** Puntatore alla voce di traduzione
- **local_ip_address** Indirizzo IP host locale
- **external_port** Porta di destinazione nella rete esterna
- **local_port** Porta di origine (host locale)
- **protocollo** Protocollo di pacchetti (ad esempio TCP)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Voce creata correttamente
- **NX_NAT_PORT_UNAVAILABLE** (0xD0D) Porta esterna non valida
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido
- NX_NAT_PARAM_ERROR (0xD01) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Create an entry for an inbound TCP packet. */
status = nx_nat_inbound_entry_create(nat_ptr, entry_ptr,
    IP_ADDRESS(192,168,2,2), 5001, 5001,
    NX_PROTOCOL_TCP);

/* If status = NX_SUCCESS the entry was successfully created. */
```

## <a name="nx_nat_inbound_entry_delete"></a>nx_nat_inbound_entry_delete

Eliminare una voce in ingresso nella tabella di conversione NAT

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_inbound_entry_delete(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *delete_entry_ptr)
```

### <a name="description"></a>Descrizione

Questo servizio elimina la voce in ingresso specificata dalla tabella di conversione.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT
- **delete_entry_ptr** Puntatore alla voce di conversione NAT

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Voce eliminata correttamente
- **NX_NAT_ENTRY_NOT_FOUND** (0xD04) Voce non trovata
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido
- NX_NAT_ENTRY_TYPE_ERROR (0xD0C) Tipo di traduzione non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Delete the specified static entry from the translation table. */
status = nx_nat_inbound_entry_delete(nat_ptr, delete_entry_ptr);

/* If status = NX_SUCCESS the entry was successfully deleted. */
```
