---
title: Capitolo 3 - Descrizione dei Azure RTOS client DHCP NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS DHCP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 50902d37f823302910b1b219658dcbf1a41406f480c14795ffceea6e733a0848
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799541"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-client-services"></a>Capitolo 3 - Descrizione dei Azure RTOS client DHCP NetX

Questo capitolo contiene una descrizione di tutti i Azure RTOS DHCP NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dhcp_create**: *Creare un'istanza DHCP*

- **nx_dhcp_clear_broadcast_flag:** Cancellare il flag broadcast nei messaggi client

- **nx_dhcp_delete**: *Eliminare un'istanza DHCP*

- **nx_dhcp_decline:** Inviare *un messaggio di rifiuto al server*

- **nx_dhcp_force_renew:** *Inviare un messaggio di rinnovo forzato*

- **nx_dhcp_packet_pool_set:** *impostare il pool di pacchetti del client DHCP*

- **nx_dhcp_release:** Inviare *un messaggio di versione al server*

- **nx_dhcp_reinitialize:** Cancellare *i parametri di rete del client DHCP*

- **nx_dhcp_request_client_ip:** specificare *un indirizzo IP specifico*

- **nx_dhcp_send_request:** *Inviare un messaggio DHCP al server*

- **nx_dhcp_server_address_get:** recuperare *l'indirizzo del server DHCP del client DHCP*

- **nx_dhcp_set_interface_index**: *specificare l'interfaccia di rete client*

- **nx_dhcp_start**: Avviare *l'elaborazione DHCP*

- **nx_dhcp_state_change_notify:** *notificare all'applicazione la modifica dello stato DHCP*

- **nx_dhcp_stop:** *arrestare l'elaborazione DHCP*

- **nx_dhcp_user_option_retrieve:** Recupera *l'opzione DHCP*

- **nx_dhcp_user_option_convert:** convertire *quattro byte in ULONG*

Interfaccia servizi client DHCP specifici:

- **nx_dhcp_interface_clear_broadcast_flag:** cancella *il flag broadcast nei messaggi client sull'interfaccia specificata*

- **nx_dhcp_interface_enable**: abilitare *l'interfaccia per eseguire DHCP sull'interfaccia specificata*

- **nx_dhcp_interface_disable:** *disabilitare l'interfaccia per l'esecuzione di DHCP nell'interfaccia specificata*

- **nx_dhcp_interface_decline:** *Inviare un messaggio di rifiuto al server nell'interfaccia specificata*

- **nx_dhcp_interface_force_renew**: *Inviare un messaggio di rinnovo forzato sull'interfaccia specificata*

- **nx_dhcp_interface_reinitialize:** cancellare *i parametri di rete del client DHCP nell'interfaccia specificata*

- **nx_dhcp_interface_release:** *Inviare un messaggio di versione al server nell'interfaccia specificata*

- **nx_dhcp_interface_request_client_ip**: *specificare un indirizzo IP specifico nell'interfaccia specificata*

- **nx_dhcp_interface_send_request**: *Inviare un messaggio DHCP al server nell'interfaccia specificata*

- **nx_dhcp_interface_server_address_get:** ottenere *l'indirizzo IP del server DHCP nell'interfaccia specificata*

- **nx_dhcp_interface_start**: *avviare l'elaborazione del client DHCP nell'interfaccia specificata*

- **nx_dhcp_interface_stop:** *arrestare l'elaborazione del client DHCP nell'interfaccia specificata*

- **nx_dhcp_interface_state_change_notify**: impostare *la funzione di callback quando lo stato DHCP cambia nell'interfaccia specificata*

- **nx_dhcp_interface_user_option_retrieve:** *recuperare l'opzione DHCP specificata nell'interfaccia specificata*

Servizi client DHCP se NX_DHCP_CLIENT_RESORE_STATE definito:

- **nx_dhcp_resume:** riprendere *lo stato del client DHCP stabilito in precedenza*

- **nx_dhcp_suspend**: *Sospendere l'elaborazione dello stato del client DHCP*

- **nx_dhcp_client_get_record**: *creare un record dello stato del client DHCP*

- **nx_dhcp_client_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP*

- **nx_dhcp_client_update_time_remaining**: *aggiornare il tempo rimanente nello stato DHCP corrente*

Interfaccia servizi client DHCP specifici se NX_DHCP_CLIENT_RESORE_STATE definito:

- **nx_dhcp_client_interface_get_record**: *creare un record dello stato del client DHCP nell'interfaccia specificata*

- **nx_dhcp_client_interface_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP nell'interfaccia specificata*

- **nx_dhcp_client_interface_update_time_remaining**: *aggiornare il tempo rimanente nello stato DHCP corrente nell'interfaccia specificata*

## <a name="nx_dhcp_create"></a>nx_dhcp_create

Creare un'istanza DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza DHCP per l'istanza IP creata in precedenza. Per impostazione predefinita, l'interfaccia primaria è abilitata per l'esecuzione di DHCP. L'input del nome, anche se non usato nell'implementazione NetX del client DHCP, deve seguire i criteri RFC 1035 per i nomi host. La lunghezza totale non deve superare i 255 caratteri, le etichette separate da punti devono iniziare con una lettera e terminare con una lettera o un numero e possono contenere trattini ma nessun altro carattere non alfanumerico.

Se l'applicazione desidera eseguire DHCP in un'altra interfaccia registrata con l'istanza IP ( *usando nx_ip_interface_attach*), l'applicazione può chiamare *nx_dhcp_set_interface_index* per eseguire DHCP solo su tale interfaccia o *nx_dhcp_interface_enable per* eseguire DHCP anche su tale interfaccia. Per altri dettagli, vedere la descrizione di questi servizi.

> [!NOTE]
> L'applicazione deve assicurarsi che il payload del pool di pacchetti del client DHCP possa supportare le dimensioni minime dei messaggi DHCP specificate dalla sezione 2 rfc 2131 (548 byte di dati dei messaggi DHCP più intestazioni UDP, IP e frame di rete fisica).

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  
- **ip_ptr** Puntatore all'istanza IP creata in precedenza.  
- **name_ptr** Puntatore al nome host per l'istanza DHCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione DHCP riuscita

- **NX_DHCP_INVALID_NAME** (0xA8) Nome host non valido

- **NX_DHCP_INVALID_PAYLOAD** (0x9C) Payload troppo piccolo per il messaggio DHCP

- NX_PTR_ERROR (0x16) Puntatore IP o DHCP non valido

### <a name="allowed-from"></a>Consentito da

**Thread,** Inizializzazione

### <a name="example"></a>Esempio

```C
/* Create a DHCP instance. */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created. */
```

## <a name="nx_dhcp_interface_enable"></a>nx_dhcp_interface_enable

Abilitare l'interfaccia specificata per l'esecuzione di DHCP 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio abilita l'interfaccia specificata per l'esecuzione di DHCP. Per impostazione predefinita, l'interfaccia primaria è abilitata per il client DHCP. A questo punto, DHCP può essere avviato su questa interfaccia chiamando *nx_dhcp_interface_start* o per avviare DHCP in tutte le interfacce *abilitate nx_dhcp_start*.

Si noti che l'applicazione deve prima registrare questa interfaccia con l'istanza IP, usando *nx_ip_interface_attach.*

Inoltre, deve essere disponibile un 'record' dell'interfaccia client DHCP per aggiungere questa interfaccia all'elenco di interfacce abilitate. Per impostazione NX_DHCP_CLIENT_MAX_RECORDS è definito su 1. Impostare questa opzione sul numero massimo di interfacce previste per l'esecuzione simultanea del client DHCP. In NX_DHCP_CLIENT_MAX_RECORDS sarà uguale a NX_MAX_PHYSICAL_INTERFACES; Tuttavia, se un dispositivo ha più interfacce fisiche di quelle previste per l'esecuzione del client DHCP, può risparmiare memoria impostando NX_DHCP_CLIENT_MAX_RECORDS su un valore inferiore a tale numero. Non esiste un mapping uno a uno delle interfacce fisiche con i record dell'interfaccia client DHCP.

La differenza tra questo servizio e *nx_dhcp_set_interface_index* è che quest'ultima imposta solo una singola interfaccia per eseguire DHCP, mentre questo servizio aggiunge semplicemente l'interfaccia specificata all'elenco di interfacce client abilitate per DHCP.

Per disabilitare un'interfaccia per DHCP, l'applicazione può chiamare il *nx_dhcp_interface_disable* dhcp.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  

- **interface_index** Indice dell'interfaccia su cui abilitare DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Abilitato DHCP riuscito

- **NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) Nessun record disponibile per un'altra interfaccia da abilitato per DHCP

- **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore IP o DHCP non valido

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface. NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled. */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1. */
```

## <a name="nx_dhcp_interface_disable"></a>nx_dhcp_interface_disable

Disabilitare l'interfaccia specificata per l'esecuzione di DHCP 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita l'interfaccia specificata per l'esecuzione di DHCP. Reinizializza il client DHCP su questa interfaccia.

Per riavviare il client DHCP, l'applicazione deve ri abilitare nuovamente l'interfaccia *nx_dhcp_interface_enable* e riavviare DHCP *chiamando nx_dhcp_interface_start*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  

- **interface_index** Indice dell'interfaccia su cui disabilitare DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione DHCP riuscita

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP o IP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disable DHCP on a secondary interface.
. */

status = nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled. */
```

## <a name="nx_dhcp_clear_broadcast_flag"></a>nx_dhcp_clear_broadcast_flag

Impostare il flag di trasmissione DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a>Descrizione

Questo servizio imposta o cancella il flag di trasmissione l'intestazione del messaggio DHCP per tutte le interfacce abilitate per DHCP. Per alcuni messaggi DHCP (ad esempio DISCOVER) il flag di trasmissione è impostato per la trasmissione perché il client non dispone di un indirizzo IP.

__clear_flag__


- **NX_TRUE** flag broadcast viene cancellato (richiesta di risposta unicast)

- **NX_FALSE** flag broadcast è impostato (richiesta di risposta broadcast)

Questo servizio è destinato ai client DHCP che devono passare attraverso un router per raggiungere il server DHCP, in cui il router rifiuta l'inoltro dei messaggi trasmessi.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP  

- **clear_flag** Valore su cui impostare il flag di trasmissione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiornamento del flag di trasmissione completato

- NX_PTR_ERROR (0x16) Puntatore DHCP o IP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response). */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a>nx_dhcp_interface_clear_broadcast_flag

Imposta o cancella il flag di trasmissione nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT clear_flag);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione host client DHCP di impostare o cancellare il flag di trasmissione nei messaggi client DHCP per il server DHCP sull'interfaccia specificata. Per altri dettagli, **vedere nx_dhcp_clear_broadcast_flag**

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP

- **interface_index** Indice dell'interfaccia per impostare il flag di trasmissione  

- **clear_flag** Valore su cui impostare il flag di trasmissione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiornamento del flag di trasmissione completato

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP o IP non valido

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface. */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_delete"></a>nx_dhcp_delete

Eliminare un'istanza DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza DHCP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione DHCP riuscita.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete a DHCP instance. */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted. */
```

## <a name="nx_dhcp_-force_renew"></a>nx_dhcp_ force_renew

Inviare un messaggio di rinnovo forzato 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione host di inviare un messaggio di rinnovo forzato su tutte le interfacce abilitate per DHCP. Il client DHCP deve essere in uno stato BOUND. Questa funzione imposta lo stato su RENEW in modo che il client DHCP tatti il rinnovo prima della scadenza del timeout T1.

Per inviare un rinnovo forzato su un'interfaccia specifica quando più interfacce sono abilitate per DHCP, *usare nx_dhcp_interface_force_renew*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il rinnovo forzato è stato inviato correttamente.  

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send a force renew message from the Client. */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_interface_force_renew"></a>nx_dhcp_interface_force_renew

Inviare un messaggio di rinnovo forzato sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione host di inviare un messaggio di rinnovo forzato sull'interfaccia di input purché tale interfaccia sia stata abilitata per DHCP (vedere *nx_dhcp_interface_enable*). Il client DHCP nell'interfaccia specificata deve essere in uno stato BOUND. Questa funzione imposta lo stato su RENEW in modo che il client DHCP tatti il rinnovo prima della scadenza del timeout T1.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il rinnovo forzato è stato inviato correttamente.  

- **NX_DHCP_INTERFACE_NOT_ENABLED**  (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP o IP non valido

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send a force renew message to the server on interface 1. */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_packet_pool_set"></a>nx_dhcp_packet_pool_set

Impostare il pool di pacchetti del client DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr,
                            NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione di creare il pool di pacchetti client DHCP passando un puntatore a un pool di pacchetti creato in precedenza in questa chiamata al servizio. Per usare questa funzionalità, l'applicazione host deve definire NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL. Se definito, il *nx_dhcp_create* non creerà il pool di pacchetti del client. Si noti che è consigliabile che l'applicazione usi i valori predefiniti per il payload del pool di pacchetti client DHCP, definiti come NX_DHCP_PACKET_PAYLOAD in *nx_dhcp.h* durante la creazione del pool di pacchetti.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  

- **packet_pool_ptr** Puntatore al pool di pacchetti creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** pool di pacchetti client DHCP 0x00 (0x00)

- **NX_NOT_ENABLED** (0x14) non è abilitato

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_DHCP_INVALID_PAYLOAD payload (0x9C) è troppo piccolo

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
        NX_DHCP_PACKET_PAYLOAD, pointer, (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool. */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set. */
```

## <a name="nx_dhcp_request_client_ip"></a>nx_dhcp_request_client_ip

Impostare l'indirizzo IP richiesto per l'istanza DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr,
                                ULONG client_ip_address,
                                UINT skip_discover_message);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP che il client DHCP deve richiedere al server DHCP nella prima interfaccia abilitata per DHCP nel record client DHCP. Se il flag *skip_discover_message* è impostato, il client DHCP ignora il messaggio di individuazione e invia un messaggio di richiesta.

Per impostare la richiesta per un indirizzo IP specifico per i messaggi DHCP in un'interfaccia specifica, usare il *nx_dhcp_interface_request_client_ip* servizio.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  

- **client_ip_address** Indirizzo IP da richiedere dal server DHCP

- **skip_discover_message** Se true, il client DHCP invia un messaggio di richiesta  
Se false, invia il messaggio Discover.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IP richiesto è impostato.

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP o IP non valido

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida
 
### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the DHCP Client requested IP address and skip the discover message. */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_interface_request_client_ip"></a>nx_dhcp_interface_request_client_ip

Impostare l'indirizzo IP richiesto per l'istanza DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr,
                                        UINT interface_index,
                                        ULONG client_ip_address,
                                        UINT skip_discover_message);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP che il client DHCP deve richiedere al server DHCP sull'interfaccia specificata, se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*). Se il flag *skip_discover_message* è impostato, il client DHCP ignora il messaggio di individuazione e invia un messaggio di richiesta.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.

- **Interface_index** Indice dell'interfaccia su cui richiedere l'indirizzo IP

- **client_ip_address** Indirizzo IP da richiedere dal server DHCP

- **skip_discover_message** Se true, il client DHCP invia il messaggio di richiesta. altrimenti invia il messaggio Discover.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IP richiesto è impostato.

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP o IP non valido

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0. */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_reinitialize"></a>nx_dhcp_reinitialize

Cancellare i parametri di rete del client DHCP 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella i parametri di rete dell'applicazione host (indirizzo IP, indirizzo di rete e network mask) e cancella lo stato del client DHCP in tutte le interfacce abilitate per DHCP. Viene usato in combinazione *con* nx_dhcp_stop e *nx_dhcp_start* per "riavviare" la macchina a stati DHCP: 

nx_dhcp_stop(&my_dhcp);  
nx_dhcp_reinitialize(&my_dhcp);  
nx_dhcp_start(&my_dhcp);


Per reinizializzare il client DHCP su un'interfaccia specifica quando sono abilitate più interfacce per DHCP, usare il *nx_dhcp_interface_reinitialize* dhcp.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** reinizializzata (0x00) DHCP 

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Reinitialize the previously started DHCP client. */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a>nx_dhcp_interface_reinitialize

Cancellare i parametri di rete del client DHCP nell'interfaccia specificata 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio cancella i parametri di rete (indirizzo IP, indirizzo di rete e network mask) nell'interfaccia specificata se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*). Vedere *nx_dhcp_reinitialize* per altri dettagli.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza

- **interface_index** Indice dell'interfaccia da reinizializzare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** reinizializzata (0x00)

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Reinitialize the previously started DHCP client on interface 1. */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a>nx_dhcp_release

Rilasciare l'indirizzo IP con lease

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP inviando il messaggio RELEASE a tale server. Reinizializza quindi il client DHCP. Questo servizio viene applicato a tutte le interfacce abilitate per DHCP.

L'applicazione può riavviare il client DHCP *chiamando nx_dhcp_start*.

Per rilasciare un indirizzo al server DHCP su un'interfaccia specifica, usare il *servizio nx_dhcp_interface_release*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rilascio DHCP riuscito.  

- **NX_DHCP_NOT_BOUND** (0x94) L'indirizzo IP non è stato noleggiato, quindi non può essere rilasciato.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Release the previously leased IP address. */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_interface_release"></a>nx_dhcp_interface_release

Rilasciare l'indirizzo IP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP nell'interfaccia specificata e reinizializza il client DHCP. Il client DHCP può essere riavviato chiamando *nx_dhcp_start*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rilascio DHCP riuscito.

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- **NX_DHCP_NOT_BOUND** (0x94) L'indirizzo IP non è stato noleggiato, quindi non può essere rilasciato.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Release the previously leased IP address on interface 1. */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_decline"></a>nx_dhcp_decline

Rifiutare l'indirizzo IP dal server DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rifiuta un indirizzo IP con lease dal server DHCP in tutte le interfacce abilitate per DHCP. Se NX_DHCP_CLIENT_ SEND_ ARP_PROBE è definito, il client DHCP invierà un messaggio DECLINE se rileva che l'indirizzo IP è già in uso. Per altre informazioni sulla configurazione dei probe ARP nel client DHCP NetX, vedere probe **ARP** nel capitolo 1.

L'applicazione può usare questo servizio per rifiutare il proprio indirizzo IP se rileva che l'indirizzo è in uso con altri mezzi.

Questo servizio reinizializza il client DHCP in modo che possa essere riavviato chiamando *nx_dhcp_start*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rifiuto inviato correttamente  

- **NX_DHCP_NOT_STARTED** (0x96) L'istanza DHCP non è stata avviata

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Decline the IP address offered by the DHCP server. */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was 
   successfully trasnmitted. */
```

## <a name="nx_dhcp_interface_decline"></a>nx_dhcp_interface_decline

Rifiutare l'indirizzo IP dal server DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio invia il messaggio DECLINE al server per rifiutare un indirizzo IP assegnato dal server DHCP. Reinizializza anche il client DHCP. Per *altri nx_dhcp_decline,* vedere l'nx_dhcp_decline.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

- **Interface_index** Indice dell'interfaccia per rifiutare l'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** messaggio di rifiuto DHCP 0x00 (0x00)  

- **NX_DHCP_NOT_BOUND** client DHCP (0x94) non associato

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Decline the IP address offered by the DHCP server on interface 2. */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was
   successfully trasnmitted. */
```

## <a name="nx_dhcp_send_request"></a>nx_dhcp_send_request

Inviare un messaggio DHCP al server

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);
```

### <a name="description"></a>Descrizione

Questo servizio invia il messaggio DHCP specificato al server DHCP sulla prima interfaccia abilitata per DHCP presente nel record client DHCP. Per inviare un messaggio RELEASE o DECLINE, l'applicazione deve usare rispettivamente i servizi *nx_dhcp[_interface]_release*() *o nx_dhcp_interface_decline().*

Il client DHCP deve essere avviato per utilizzare questo servizio, ad eccezione dell'invio INFORM_REQUEST tipo di messaggio.

> [!NOTE] 
> Questo servizio non è destinato all'applicazione host per "unità" la macchina a stati client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  

- **dhcp_message_type** Richiesta di messaggio (definita in *nx_dhcp.h*)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) DHCP inviato  

- **NX_DHCP_NOT_STARTED** (0x96) Indice di interfaccia non valido

- **NX_DHCP_INVALID_MESSAGE** (0x9B) Tipo di messaggio non valido da inviare

- NX_PTR_ERROR (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send the DHCP INFORM REQUEST message to the server. */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_interface_send_request"></a>nx_dhcp_interface_send_request

Inviare un messaggio DHCP al server su un'interfaccia specifica

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr,
                                    UINT interface_index,
                                    UINT dhcp_message_type);
```

### <a name="description"></a>Descrizione

Questo servizio invia un messaggio al server DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP. Per inviare un messaggio RELEASE o DECLINE, l'applicazione deve usare rispettivamente i servizi *nx_dhcp[_interface]_release*() *o nx_dhcp_interface_decline().*

Il client DHCP deve essere avviato per utilizzare questo servizio, ad eccezione dell'invio del tipo di messaggio DHCP INFORM REQUEST.

Questo servizio non è destinato all'applicazione host per "unità" la macchina a stati client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.

- **Interface_index** Indice dell'interfaccia su cui inviare il messaggio  

- **dhcp_message_type** Richiesta di messaggio (definita in *nx_dhcp.h)*

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) dhcp inviato  

- **NX_DHCP_NOT_STARTED** (0x96) Indice di interfaccia non valido

- **NX_DHCP_INVALID_MESSAGE** (0x9B) Tipo di messaggio non valido da inviare

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Non abilitata per DHCP

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send the INFORM REQUEST message to the server on the primary interface. */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_server_address_get"></a>nx_dhcp_server_address_get

Ottenere l'indirizzo IP del server DHCP del client DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr,
                                ULONG server_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nella prima interfaccia abilitata per DHCP trovata nel record client DHCP. Il chiamante può usare questo servizio solo dopo che il client DHCP è associato a un indirizzo IP assegnato dal server DHCP. L'applicazione host può usare il *servizio nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure può usare il *nx_dhcp_state_change_notify* ed eseguire query sullo stato del client DHCP NX_DHCP_STATE_BOUND. Vedere *nx_dhcp_state_change_notify* per altri dettagli sull'impostazione della funzione di callback della modifica dello stato.

Per trovare il server DHCP in un'interfaccia specifica quando sono abilitate più interfacce per il client DHCP, usare il nx_dhcp_interface_server_address_get *locale*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.

- **server_address** Puntatore all'indirizzo IP del server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) indirizzo del server DHCP restituito

- NX_PTR_ERROR (0x16) Puntatore di input non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
    }
```

## <a name="nx_dhcp_interface_server_address_get"></a>nx_dhcp_interface_server_address_get

Ottenere l'indirizzo IP del server DHCP del client DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            ULONG server_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP del server DHCP client DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP. Il client DHCP deve essere nello stato Associato. Dopo aver avviato il client DHCP su tale interfaccia, l'applicazione host può usare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure può usare il callback di modifica dello stato del client DHCP ed eseguire query sullo stato del client DHCP NX_DHCP_STATE_BOUND. Vedere *nx_dhcp_state_change_notify* per altri dettagli sull'impostazione della funzione di callback della modifica dello stato.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.

- **Interface_index** Indice dell'interfaccia per ottenere l'indirizzo IP  

- **server_address** Puntatore all'indirizzo IP del server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) indirizzo del server DHCP restituito

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) Nessuna interfaccia abilitata per DHCP

- **NX_DHCP_NOT_BOUND** (0x94) Client DHCP non associato

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    /* Get the DHCP server IP address on interface 1 */
    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                    &server_address);
    }
```

## <a name="nx_dhcp_set_interface_index"></a>nx_dhcp_set_interface_index

Impostare l'interfaccia di rete per l'istanza DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'interfaccia di rete per la connessione dell'istanza DHCP al server DHCP quando si esegue il client DHCP configurato per una singola interfaccia di rete.

Per impostazione predefinita, il client DHCP viene eseguito sull'interfaccia primaria. Per eseguire DHCP in un servizio secondario, usare questo servizio per impostare l'interfaccia secondaria come interfaccia client DHCP. L'applicazione deve registrare in precedenza l'interfaccia specificata nell'istanza IP usando *nx_ip_interface_attach* servizio.

Si noti che questo servizio è destinato alle applicazioni che intendono eseguire il client DHCP su una sola interfaccia. Per eseguire DHCP su più interfacce, vedere *nx_dhcp_interface_enable* per altri dettagli.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo DHCP.  

- **index** Indice dell'interfaccia di rete del dispositivo

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS(0x00)** l'interfaccia è stata impostata correttamente.

- **NX_INVALID_INTERFACE** (0x4C) Interfaccia di rete non valida

- **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Abilitata per DHCP

- **NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) Nessun record disponibile per un altro

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the DHCP Client interface to the secondary interface (index 1). */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set. */
```

## <a name="nx_dhcp_start"></a>nx_dhcp_start

Avviare l'elaborazione DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione DHCP in tutte le interfacce abilitate per DHCP. Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*

Per verificare quando l'istanza IP è associata a  un indirizzo IP nell'interfaccia client DHCP, usare nx_ip_status_check per verificare che l'indirizzo IP sia valido.

Se sono già presenti altre interfacce che eseguono DHCP, questo servizio non le influirà su di esse.

Per avviare DHCP su un'interfaccia specifica quando sono abilitate più interfacce, usare il *nx_dhcp_interface_start* servizio.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio DHCP riuscito.  

- **NX_DHCP_ALREADY_STARTED** dhcp (0x93) è già stato avviato.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the DHCP processing for this IP instance. */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_interface_start"></a>nx_dhcp_interface_start

Avviare l'elaborazione DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP. Vedere *nx_dhcp_interface_enable*() per altre informazioni sull'abilitazione di un'interfaccia per DHCP. Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*

Se non sono presenti altre interfacce che eseguono il client DHCP, questo servizio avvia/riprende il thread client DHCP e (ri)attiva il timer client DHCP.  
  
L'applicazione deve *usare nx_ip_status_check* per verificare se viene ottenuto un indirizzo IP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

- **Interface_index** Indice in base al quale avviare il client DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio DHCP riuscito.  

- **NX_DHCP_ALREADY_STARTED** (0x93) L'istanza DHCP è già stata avviata.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_state_change_notify"></a>nx_dhcp_state_change_notify

Impostare la funzione di callback per la modifica dello stato DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_state_change_notify(
          NX_DHCP *dhcp_ptr, 
          VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                           UCHAR new_state));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback specificata dhcp_state_change_notify per notificare a un'applicazione le modifiche dello stato DHCP. La funzione di callback fornisce lo stato in cui il client DHCP ha eseguito la transizione.

Di seguito sono riportati i valori associati ai vari stati DHCP:

| State                             | Valore |
|-----------------------------------|-------|
| NX \_ DHCP \_ STATE \_ BOOT             | 1     |
| NX \_ DHCP \_ STATE \_ INIT             | 2     |
| NX \_ DHCP \_ STATE \_ SELECTING        | 3     |
| RICHIESTA DELLO \_ STATO DHCP \_ \_ NX       | 4     |
| NX \_ DHCP \_ STATE \_ BOUND            | 5     |
| RINNOVO DELLO STATO DHCP NX \_ \_ \_         | 6     |
| RIASSOCIAZIONE DELLO \_ STATO DHCP \_ \_ NX        | 7     |
| NX_DHCP_STATE_FORCERENEW          | 8     |
| PROBE DEGLI \_ INDIRIZZI DI STATO DHCP NX \_ \_ \_ | 9     |


### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

- **dhcp_state_change_notify** Puntatore a funzione di callback della modifica dello stato

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostato di callback riuscito.  

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Register the “my_state_change” function to be called on any DHCP state change, 
   assuming DHCP has alreadybeen created. */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_interface_state_change_notify"></a>nx_dhcp_interface_state_change_notify

Impostare la funzione di callback di modifica dello stato DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_state_change_notify(
              NX_DHCP *dhcp_ptr, 
              UINT interface_index,
              VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                               UINT interface_index,
                                               UCHAR new_state));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback specificata per notificare a un'applicazione le modifiche dello stato DHCP. Gli argomenti di input del funciton callback sono l'indice dell'interfaccia e lo stato a cui il client DHCP ha eseguito la transizione su tale interfaccia.

Per altre informazioni sulle funzioni di modifica dello stato, *vedere* nx_dhcp_state_change_notify ().

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

- **dhcp_interface_state_change_notify** Puntatore a funzione di callback dell'applicazione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostato di callback riuscito.  

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

### <a name="allowed-from"></a>Consentito da

thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Register the “my_state_change” function to be called on any DHCP state 
   change, assuming DHCP has alreadybeen created. */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                 UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_stop"></a>nx_dhcp_stop

Arresta l'elaborazione DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'elaborazione DHCP in tutte le interfacce che hanno avviato l'elaborazione DHCP. Se non sono presenti interfacce che elaborano DHCP, questo servizio sospende il thread client DHCP e disattiva il timer client DHCP.

Per arrestare DHCP in un'interfaccia specifica se sono abilitate più interfacce per DHCP, usare il nx_dhcp_interface_stop *dhcp.*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto DHCP riuscito

- **NX_DHCP_NOT_STARTED** (0x96) L'istanza DHCP non è stata avviata.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the DHCP processing for this IP instance. */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_interface_stop"></a>nx_dhcp_interface_stop

Arrestare l'elaborazione DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'elaborazione DHCP sull'interfaccia specificata se DHCP è già stato avviato. Se non sono presenti altre interfacce che eseguono DHCP, il thread DHCP e il timer vengono sospesi.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

- **Interface_index** Interfaccia in cui arrestare l'elaborazione DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto DHCP riuscito

- **NX_DHCP_NOT_STARTED** dhcp (0x96) non avviato.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_user_option_retrieve"></a>nx_dhcp_user_option_retrieve

Recuperare un'opzione DHCP dall'ultima risposta del server

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nella prima interfaccia abilitata per DHCP trovata nel record client DHCP. Se l'operazione riesce, i dati dell'opzione vengono copiati nel buffer specificato.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.  

- **request_option** Opzione DHCP, come specificato dalle RFC. Vedere l'NX_DHCP_OPTION in *nx_dhcp.h.*

- **destination_ptr** Puntatore alla destinazione per la stringa di risposta.  

- **destination_size** Puntatore alla dimensione della destinazione e, al ritorno, alla destinazione in cui inserire il numero di byte restituiti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero dell'opzione riuscito.  

- **NX_DHCP_NOT_BOUND** client DHCP (0x94) non associato.

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) Nessuna interfaccia abilitata per DHCP

- **NX_DHCP_DEST_TO_SMALL** (0x95) La destinazione è troppo piccola per contenere la risposta.

- **NX_DHCP_PARSE_ERROR(0x97)** Opzione DHCP non trovata nella risposta del server.

- NX_PTR_ERROR (0x16) Puntatore di input non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a>nx_dhcp_interface_user_option_retrieve

Recupera un'opzione DHCP dall'ultima risposta del server nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                  UINT interface_index, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nell'interfaccia specificata, se tale interfaccia è abilitata per DHCP. Se l'operazione riesce, i dati dell'opzione vengono copiati nel buffer specificato.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

- **Interface_index** Indice in base al quale recuperare l'opzione specificata  

- **request_option** Opzione DHCP, come specificato dalle RFC. Vedere l'NX_DHCP_OPTION in *nx_dhcp.h.*  

- **destination_ptr** Puntatore alla destinazione per la stringa di risposta.  

- **destination_size** Puntatore alla dimensione della destinazione e, al ritorno, alla destinazione in cui inserire il numero di byte restituiti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero dell'opzione riuscito.  

- **NX_DHCP_NOT_BOUND(0x94)** IP non assegnato

- **NX_DHCP_DEST_TO_SMALL** buffer (0x95) è troppo piccolo

- **NX_DHCP_PARSE_ERROR(0x97)** Opzione DHCP non trovata nella risposta del server.

- NX_PTR_ERROR (0x16) Puntatore DHCP non valido.

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido.

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_user_option_convert"></a>nx_dhcp_user_option_convert

Convertire quattro byte in ULONG

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio converte i quattro caratteri a cui punta "option_string_ptr" in un valore long senza segno. È particolarmente utile quando sono presenti indirizzi IP.

### <a name="input-parameters"></a>Parametri di input

- **option_string_ptr** Puntatore alla stringa di opzione recuperata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **Valore** Valore dei primi quattro byte.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a>nx_dhcp_user_option_add_callback_set

Impostare la funzione di callback per l'aggiunta di opzioni fornite dall'utente

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
    UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                 UINT iface_index, 
                                 UINT message_type, 
                                 UCHAR *user_option_ptr, 
                                 UINT *user_option_length));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback specificata per l'aggiunta di opzioni fornite dall'utente.

Se la funzione di callback è specificata, le applicazioni possono aggiungere le opzioni fornite dall'utente nel pacchetto iface_index e message_type.

> [!NOTE]
> Nella routine dell'utente. Le applicazioni devono seguire il formato delle opzioni DHCP quando si aggiungono opzioni specificate dall'utente. Le dimensioni totali delle opzioni utente devono essere minori o uguali a user_option_length e aggiornare le user_option_length come lunghezza delle opzioni reali. Restituisce NX_TRUE se l'aggiunta delle opzioni ha esito positivo, altrimenti restituisce NX_FALSE.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza DHCP creata in precedenza.

- **dhcp_user_option_add** Puntatore all'opzione utente add function.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostato di callback riuscito.

- NX_PTR_ERROR (0x16) Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created. */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered. */
```
