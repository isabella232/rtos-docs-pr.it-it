---
title: Capitolo 4-Descrizione dei servizi NAT
description: Questo capitolo contiene una descrizione di tutti i servizi API NAT NetX Duo in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8bdbdfcb2da6425fb99cadc7b2f6815dedc12953
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821755"
---
# <a name="chapter-4---description-of-nat-services"></a>Capitolo 4-Descrizione dei servizi NAT

Questo capitolo contiene una descrizione di tutti i servizi API NAT NetX Duo (elencati di seguito) in ordine alfabetico.

> [!NOTE]
> Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

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
- **puntatore ip_ptr** all'istanza IP
- **global_interface_index** Indicizzare l'interfaccia di rete globale
- **dynamic_cache_memory** Area memoria puntatore alla tabella NAT
- **dynamic_cache_size** Dimensioni dell'area di memoria per la tabella NAT

### <a name="return-values"></a>Valori restituiti

- Server NAT **NX_SUCCESS** (0x00) creato correttamente
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
- NX_NAT_PARAM_ERROR (0xD01) non è stato inserito alcun puntatore non valido
- Input del puntatore della cache NX_NAT_CACHE_ERROR (0xD02) non valido

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

Questo servizio Elimina un server NAT creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT da eliminare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) NAT eliminato correttamente
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

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

Questo servizio Abilita l'istanza IP per NAT (ad esempio, inoltra i pacchetti ricevuti al server NAT).

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT

### <a name="return-values"></a>Valori restituiti

- NAT **NX_SUCCESS** (0x00) correttamente abilitato
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

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

Questo servizio Disabilita NAT nell'istanza IP.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT

### <a name="return-values"></a>Valori restituiti

- NAT **NX_SUCCESS** (0x00) disabilitato
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Disable the NAT server. */
status = nx_nat_disable (nat_ptr);

/* If status = NX_SUCCESS the NAT operation successfully disable. */
```

## <a name="nx_nat_cache_notify_set"></a>nx_nat_cache_notify_set

Impostare una funzione di callback notifica completa della cache

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)
    (NX_NAT_DEVICE *nat_ptr)));
```

### <a name="description"></a>Descrizione

Questo servizio registra il callback completo della cache con il puntatore alla funzione di input cache_full_notify_cb che punta a una funzione di notifica completa della cache definita dall'utente.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT
- **cache_full_notify_cb** Puntatore alla funzione di notifica completa della cache

### <a name="return-values"></a>Valori restituiti

- Funzione di notifica completa della cache **NX_SUCCESS** (0x00) impostata correttamente
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
- NX_NAT_PARAM_ERROR (0xD01) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Set the cache full notify callback function to the NAT instance. */
status = nx_nat_cache_notify_set(nat_ptr, cache_full_notify_cb);

/* If status = NX_SUCCESS the callback function was successfully set. */
```

## <a name="nx_nat_inbound_entry_create"></a>nx_nat_inbound_entry_create

Creare una voce in ingresso nella tabella NAT Translation

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr
    ULONG local_ip_address,
    USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

### <a name="description"></a>Descrizione

Questo servizio crea una voce in ingresso come statica (voce permanente senza scadenza) e la aggiunge alla tabella di traduzione NAT. Queste voci vengono in genere create per i server host locali in cui viene avviata una connessione da un host nella rete esterna. Il server NAT verifica che la porta esterna non sia già in uso nella tabella di traduzione o che sia associata a un socket NetX duo già esistente dello stesso protocollo.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT
- **entry_ptr** Puntatore alla voce di traslazione
- **local_ip_address** Indirizzo IP host locale
- **external_port** Porta di destinazione nella rete esterna
- **local_port** Porta di origine (host locale)
- **protocollo** di Protocollo Packet (ad esempio, TCP)

### <a name="return-values"></a>Valori restituiti

- Creazione della voce **NX_SUCCESS** (0x00) completata
- **NX_NAT_PORT_UNAVAILABLE** (0xD0D) porta esterna non valida
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
- NX_NAT_PARAM_ERROR (0xD01) non è stato inserito alcun puntatore non valido

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

Eliminare una voce in ingresso nella tabella NAT Translation

### <a name="prototype"></a>Prototipo

```C
UINT nx_nat_inbound_entry_delete(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *delete_entry_ptr)
```

### <a name="description"></a>Descrizione

Questo servizio Elimina la voce in ingresso specificata dalla tabella di conversione.

### <a name="input-parameters"></a>Parametri di input

- **nat_ptr** Puntatore all'istanza NAT
- **delete_entry_ptr** Puntatore alla voce di traduzione NAT

### <a name="return-values"></a>Valori restituiti

- La voce **NX_SUCCESS** (0x00) è stata eliminata
- La voce **NX_NAT_ENTRY_NOT_FOUND** (0xD04) non è stata trovata
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
- Tipo di traduzione NX_NAT_ENTRY_TYPE_ERROR (0xD0C) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Delete the specified static entry from the translation table. */
status = nx_nat_inbound_entry_delete(nat_ptr, delete_entry_ptr);

/* If status = NX_SUCCESS the entry was successfully deleted. */
```
