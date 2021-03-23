---
title: Capitolo 3-Descrizione dei servizi client DHCP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi client DHCP di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f143a443221ae08848316a458a630a0790108198
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822022"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-client-services"></a>Capitolo 3-Descrizione dei servizi client DHCP di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi client DHCP di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dhcp_create**: *creare un'istanza DHCP*
- **nx_dhcp_clear_broadcast_flag**: *Cancella flag broadcast nei messaggi client*
- **nx_dhcp_delete**: *eliminare un'istanza DHCP*
- **nx_dhcp_force_renew**: *inviare un messaggio di rinnovo forzato*
- **nx_dhcp_packet_pool_set**: *impostare il pool di pacchetti client DHCP*
- **nx_dhcp_decline**: inviare un *messaggio di rifiuto al server*
- **nx_dhcp_release**: inviare un *messaggio di rilascio al server*
- **nx_dhcp_reinitialize**: *Cancella parametri della rete client DHCP*
- **nx_dhcp_request_client_ip**: *specificare un indirizzo IP specifico*
- **nx_dhcp_send_request**: *inviare un messaggio DHCP al server*
- **nx_dhcp_start**: *avviare l'elaborazione del client DHCP*
- **nx_dhcp_stop**: *arrestare l'elaborazione del client DHCP*
- **nx_dhcp_set_interface_index**: *impostare l'interfaccia per l'esecuzione del client DHCP*
- **nx_dhcp_server_address_get**: *ottenere l'indirizzo IP del server DHCP*
- **nx_dhcp_state_change_notify**: *impostare la funzione di callback quando viene modificato lo stato DHCP*
- **nx_dhcp_user_option_retrieve**: *recuperare l'opzione DHCP specificata*
- **nx_dhcp_user_option_convert**: *conversione di quattro byte in ULONG*

Servizi client DHCP specifici dell'interfaccia:
 
- **nx_dhcp_interface_clear_broadcast_flag**: *Cancella il flag broadcast nei messaggi client sull'interfaccia specificata*
- **nx_dhcp_interface_enable**: *Abilita l'interfaccia per l'esecuzione di DHCP sull'interfaccia specificata*
- **nx_dhcp_interface_disable**: *disabilitare l'interfaccia per l'esecuzione di DHCP sull'interfaccia specificata*
- **nx_dhcp_interface_decline**: *inviare il messaggio di rifiuto al server sull'interfaccia specificata*
- **nx_dhcp_interface_force_renew**: *inviare un messaggio Force Renew sull'interfaccia specificata*
- **nx_dhcp_interface_reinitialize**: *Cancella i parametri di rete del client DHCP nell'interfaccia specificata*
- **nx_dhcp_interface_release**: *inviare un messaggio di rilascio al server sull'interfaccia specificata*
- **nx_dhcp_interface_request_client_ip**: *specificare un indirizzo IP specifico nell'interfaccia specificata*
- **nx_dhcp_interface_send_request**: *inviare un messaggio DHCP al server sull'interfaccia specificata*
- **nx_dhcp_interface_server_address_get**: *ottenere l'indirizzo IP del server DHCP nell'interfaccia specificata*
- **nx_dhcp_interface_start**: *avviare l'elaborazione del client DHCP sull'interfaccia specificata*
- **nx_dhcp_interface_stop**: *arrestare l'elaborazione del client DHCP sull'interfaccia specificata*
- **nx_dhcp_interface_state_change_notify**: *impostare la funzione di callback quando lo stato DHCP viene modificato sull'interfaccia specificata*
- **nx_dhcp_interface_user_option_retrieve**: *recuperare l'opzione DHCP specificata nell'interfaccia specificata*

Servizi client DHCP se è stato definito NX_DHCP_CLIENT_RESORE_STATE:

- **nx_dhcp_resume**: *Riprendi stato client DHCP stabilito in precedenza*
- **nx_dhcp_suspend**: *sospendere l'elaborazione dello stato del client DHCP*
- **nx_dhcp_client_get_record**: *creare un record dello stato del client DHCP*
- **nx_dhcp_client_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP*
- **nx_dhcp_client_update_time_remaining**: *aggiornare il tempo rimanente nello stato DHCP corrente*

Servizi client DHCP specifici dell'interfaccia se NX_DHCP_CLIENT_RESORE_STATE è definito:

- **nx_dhcp_client_interface_get_record**: *creare un record dello stato del client DHCP nell'interfaccia specificata*
- **nx_dhcp_client_interface_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP sull'interfaccia specificata*
- **nx_dhcp_client_interface_update_time_remaining**: *aggiornare l'ora rimanente nello stato DHCP corrente sull'interfaccia specificata*

## <a name="nx_dhcp_create"></a>nx_dhcp_create

Creare un'istanza DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza DHCP per l'istanza IP creata in precedenza. Per impostazione predefinita, l'interfaccia primaria è abilitata per l'esecuzione di DHCP. L'input del nome, sebbene non usato nell'implementazione di NetX duo del client DHCP, deve rispettare i criteri RFC 1035 per i nomi host. La lunghezza totale non deve superare i 255 caratteri, le etichette separate da punti devono iniziare con una lettera e terminare con una lettera o un numero e possono contenere trattini ma nessun altro carattere non alfanumerico.

Se l'applicazione desidera eseguire un'altra interfaccia DHCP registrata con l'istanza IP (usando *nx_ip_interface_attach*), l'applicazione può chiamare *NX_DHCP_SET_INTERFACE_INDEX* per eseguire DHCP solo su tale interfaccia oppure *nx_dhcp_interface_enable* per eseguire DHCP su tale interfaccia. Per ulteriori informazioni, vedere la descrizione di questi servizi.

>[!NOTE]
> L'applicazione deve verificare che il payload del pool di pacchetti client DHCP sia in grado di supportare la dimensione minima dei messaggi DHCP specificata dalla RFC 2131 sezione 2 (548 byte di dati del messaggio DHCP più le intestazioni UDP, IP e frame di rete fisica).

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP. 
- **ip_ptr**: puntatore all'istanza IP creata in precedenza.  
- **name_ptr**: puntatore al nome host per l'istanza DHCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) creazione DHCP riuscita
- **NX_DHCP_INVALID_NAME**: (0xA8) nome host non valido
- **NX_DHCP_INVALID_PAYLOAD**: payload (0x9C) troppo piccolo per il messaggio DHCP
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Create a DHCP instance.  */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created.  */
```

## <a name="nx_dhcp_interface_enable"></a>nx_dhcp_interface_enable

Abilitare l'interfaccia specificata per l'esecuzione di DHCP 

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita l'interfaccia specificata per l'esecuzione di DHCP. Per impostazione predefinita, l'interfaccia primaria è abilitata per il client DHCP. A questo punto, è possibile avviare DHCP su questa interfaccia chiamando *nx_dhcp_interface_start* o per avviare DHCP in tutte le interfacce abilitate *nx_dhcp_start*.

>[!NOTE] 
> L'applicazione deve prima registrare questa interfaccia con l'istanza IP, usando *nx_ip_interface_attach.*

Per aggiungere questa interfaccia all'elenco delle interfacce abilitate, è inoltre necessario che sia disponibile un'interfaccia client DHCP "record". Per impostazione predefinita NX_DHCP_CLIENT_MAX_RECORDS viene definito su 1. Impostare questa opzione sul numero massimo di interfacce previste per eseguire simultaneamente il client DHCP. In genere NX_DHCP_CLIENT_MAX_RECORDS corrisponderà NX_MAX_PHYSICAL_INTERFACES; Tuttavia, se un dispositivo ha più interfacce fisiche rispetto a quanto previsto per l'esecuzione del client DHCP, può risparmiare memoria impostando NX_DHCP_CLIENT_MAX_RECORDS su un valore inferiore a quello specificato. Non esiste un mapping uno-a-uno delle interfacce fisiche con i record dell'interfaccia client DHCP.

La differenza tra questo servizio e *nx_dhcp_set_interface_index* è la seconda che imposta una sola interfaccia per eseguire DHCP, mentre questo servizio aggiunge semplicemente l'interfaccia specificata all'elenco di interfacce client abilitate per DHCP.

Per disabilitare un'interfaccia per DHCP, l'applicazione può chiamare il

servizio *nx_dhcp_interface_disable* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.  
- **interface_index**: Indice dell'interfaccia per abilitare DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Abilitazione DHCP riuscita
- **NX_DHCP_NO_RECORDS_AVAILABLE**: (0XA7) non sono disponibili record per un'altra interfaccia da abilitare per DHCP
- Interfaccia **NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface.  NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled.  */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1.  */
```

## <a name="nx_dhcp_interface_disable"></a>nx_dhcp_interface_disable

Disabilitare l'interfaccia specificata per eseguire DHCP 

### <a name="prototype"></a>Prototipo

```c

UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio Disabilita l'interfaccia specificata per l'esecuzione di DHCP. Reinizializza il client DHCP su questa interfaccia.

Per riavviare il client DHCP, l'applicazione deve riabilitare l'interfaccia utilizzando *nx_dhcp_interface_enable* e riavviare DHCP chiamando *nx_dhcp_interface_start*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.  
- **interface_index**: Indice dell'interfaccia in cui disabilitare DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) creazione DHCP riuscita
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Disable DHCP on a secondary interface. */

status =  nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled.  */
```
## <a name="nx_dhcp_clear_broadcast_flag"></a>nx_dhcp_clear_broadcast_flag

Imposta il flag di trasmissione DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a>Descrizione

Questo servizio imposta o cancella il flag di trasmissione l'intestazione del messaggio DHCP per tutte le interfacce abilitate per DHCP. Per alcuni messaggi DHCP, ad esempio DISCOVER, il flag broadcast è impostato su broadcast perché il client non dispone di un indirizzo IP.

valori clear_flag: 

- **NX_TRUE**: il flag broadcast è cancellato (richiesta unicast risposta)
- **NX_FALSE**: flag broadcast impostato (risposta broadcast richiesta)

Questo servizio è destinato ai client DHCP che devono passare attraverso un router per accedere al server DHCP, in cui il router rifiuta l'invio di messaggi broadcast.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP  
- **clear_flag**: valore su cui impostare il flag di trasmissione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) impostazione del flag completata
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response).  */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a>nx_dhcp_interface_clear_broadcast_flag

Imposta o deseleziona il flag broadcast sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr, 
                                            UINT interface_index, 
                                            UINT clear_flag);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione host client DHCP di impostare o deselezionare il flag di trasmissione nei messaggi client DHCP per il server DHCP sull'interfaccia specificata. Per ulteriori informazioni, vedere **nx_dhcp_clear_broadcast_flag**.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP
- **interface_index**: Indice dell'interfaccia per impostare il flag di trasmissione
- **clear_flag**: valore su cui impostare il flag di trasmissione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) impostazione del flag completata
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface.  */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_delete"></a>nx_dhcp_delete

Eliminare un'istanza DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza DHCP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'eliminazione DHCP è riuscita.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete a DHCP instance.  */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted.  */
```

## <a name="nx_dhcp_-force_renew"></a>nx_dhcp_ force_renew

Invia un messaggio di rinnovo forzato 

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione host di inviare un messaggio di rinnovo forzato su tutte le interfacce abilitate per DHCP. Il client DHCP deve trovarsi in uno stato associato. Questa funzione imposta lo stato su RENEW, in modo che il client DHCP tenterà di eseguire il rinnovo prima della scadenza del timeout T1.

Per inviare un rinnovo forzato a un'interfaccia specifica quando più interfacce sono abilitate per DHCP, usare *nx_dhcp_interface_force_renew*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) ha inviato il rinnovo forzato.
- **NX_DHCP_NOT_BOUND**: (0x94) indirizzo IP client non associato.  
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send a force renew message from the Client.  */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_interface_force_renew"></a>nx_dhcp_interface_force_renew

Invia un messaggio Force Renew sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr, 
                                   UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione host di inviare un messaggio Force Renew sull'interfaccia di input purché tale interfaccia sia stata abilitata per DHCP (vedere *nx_dhcp_interface_enable*). Il client DHCP nell'interfaccia specificata deve essere in uno stato associato. Questa funzione imposta lo stato su RENEW, in modo che il client DHCP tenterà di eseguire il rinnovo prima della scadenza del timeout T1.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) ha inviato il rinnovo forzato.  
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send a force renew message to the server on interface 1.  */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);


/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_packet_pool_set"></a>nx_dhcp_packet_pool_set

Impostare il pool di pacchetti client DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione di creare il pool di pacchetti client DHCP passando un puntatore a un pool di pacchetti creato in precedenza in questa chiamata al servizio. Per utilizzare questa funzionalità, l'applicazione host deve definire NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL. Una volta definito, il servizio *nx_dhcp_create* non creerà il pool di pacchetti del client. 

>[!NOTE] 
> Per l'applicazione è consigliabile utilizzare i valori predefiniti per il payload del pool di pacchetti client DHCP, definito come NX_DHCP_PACKET_PAYLOAD in *nxd_dhcp_client. h* quando si crea il pool di pacchetti.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.  
- **packet_pool_ptr**: puntatore al pool di pacchetti creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il pool di pacchetti client DHCP è impostato
- **NX_NOT_ENABLED**: il servizio (0x14) non è abilitato
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_DHCP_INVALID_PAYLOAD: il payload (0x9C) è troppo piccolo

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
                                 NX_DHCP_PACKET_PAYLOAD, pointer, 
                                 (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool.  */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set.  */

```

## <a name="nx_dhcp_request_client_ip"></a>nx_dhcp_request_client_ip

Imposta l'indirizzo IP richiesto per l'istanza DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr, 
                               ULONG client_ip_address, 
                               UINT skip_discover_message);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP per il client DHCP da richiedere dal server DHCP sulla prima interfaccia abilitata per DHCP nel record client DHCP. Se viene impostato il flag di *skip_discover_message* , il client DHCP Ignora il messaggio di individuazione e invia un messaggio di richiesta.

Per impostare la richiesta per un indirizzo IP specifico per i messaggi DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_request_client_ip* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.  
- **client_ip_address**: indirizzo IP da richiedere dal server DHCP
- **skip_discover_message**: 
    - Se true, il client DHCP invia un messaggio di richiesta
    - Se false, invia il messaggio di individuazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'indirizzo IP richiesto è impostato.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_DHCP_INVALID_IP_REQUEST: (0x9D) indirizzo IP NULL richiesto

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Set the DHCP Client requested IP address and skip the discover message.  */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */

```

## <a name="nx_dhcp_interface_request_client_ip"></a>nx_dhcp_interface_request_client_ip

Imposta l'indirizzo IP richiesto per l'istanza DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr, UINT  interface_index, 
                                         ULONG client_ip_address, UINT skip_discover_message);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP per il client DHCP da richiedere dal server DHCP sull'interfaccia specificata, se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*). Se viene impostato il flag di *skip_discover_message* , il client DHCP Ignora il messaggio di individuazione e invia un messaggio di richiesta.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.
- **Interface_index**: Indice dell'interfaccia su cui richiedere l'indirizzo IP
- **client_ip_address**: indirizzo IP da richiedere dal server DHCP
- **skip_discover_message**: Se true, il client DHCP invia un messaggio di richiesta; in caso contrario, invia il messaggio di individuazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'indirizzo IP richiesto è impostato.
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0.  */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */
```

## <a name="nx_dhcp_reinitialize"></a>nx_dhcp_reinitialize

Cancella i parametri della rete client DHCP 

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella i parametri della rete dell'applicazione host (indirizzo IP, indirizzo di rete e network mask) e cancella lo stato del client DHCP in tutte le interfacce abilitate per DHCP. Viene usato in combinazione con *nx_dhcp_stop* e *nx_dhcp_start* per "riavviare" la macchina a stati DHCP:

```c
nx_dhcp_stop(&my_dhcp);
nx_dhcp_reinitialize(&my_dhcp);
nx_dhcp_start(&my_dhcp);
```

Per reinizializzare il client DHCP in un'interfaccia specifica quando sono abilitate più interfacce per DHCP, usare il servizio *nx_dhcp_interface_reinitialize* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il protocollo DHCP è stato reinizializzato 
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Reinitialize the previously started DHCP client.  */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a>nx_dhcp_interface_reinitialize

Cancella i parametri di rete del client DHCP nell'interfaccia specificata 

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr, 
                                     UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella i parametri di rete (indirizzo IP, indirizzo di rete e network mask) nell'interfaccia specificata se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*). Per ulteriori informazioni, vedere *nx_dhcp_reinitialize* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza
- **interface_index**: Indice dell'interfaccia da reinizializzare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'interfaccia è stata reinizializzata
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Reinitialize the previously started DHCP client on interface 1.  */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a>nx_dhcp_release

Rilascia indirizzo IP con lease

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP inviando il messaggio di rilascio a tale server. Quindi reinizializza il client DHCP. Questo servizio viene applicato a tutte le interfacce abilitate per DHCP.

L'applicazione può riavviare il client DHCP chiamando *nx_dhcp_start*.

Per rilasciare un indirizzo al server DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_release*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) versione DHCP riuscita.  
- **NX_DHCP_NOT_BOUND**: (0X94) l'indirizzo IP non è stato concesso in lease, quindi non può essere rilasciato.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Release the previously leased IP address.  */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_interface_release"></a>nx_dhcp_interface_release

Rilasciare l'indirizzo IP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP sull'interfaccia specificata e reinizializza il client DHCP. Il client DHCP può essere riavviato chiamando *nx_dhcp_start*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) versione DHCP riuscita.
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- **NX_DHCP_NOT_BOUND**: (0X94) l'indirizzo IP non è stato concesso in lease, quindi non può essere rilasciato.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Release the previously leased IP address on interface 1.  */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_decline"></a>nx_dhcp_decline

Rifiuta indirizzo IP dal server DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rifiuta un indirizzo IP con lease dal server DHCP in tutte le interfacce abilitate per DHCP. Se viene definito NX_DHCP_CLIENT_ SEND_ ARP_PROBE, il client DHCP invierà un messaggio di rifiuto se rileva che l'indirizzo IP è già in uso. Per ulteriori informazioni sulla configurazione del probe ARP nel client DHCP NetX Duo, vedere **Probe ARP** nel capitolo 1.

L'applicazione può utilizzare questo servizio per rifiutare il proprio indirizzo IP se rileva che l'indirizzo è in uso in altri modi.

Questo servizio reinizializza il client DHCP in modo che possa essere riavviato chiamando *nx_dhcp_start*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il rifiuto è stato inviato  
- **NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

/* Decline the IP address offered by the DHCP server.  */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```

## <a name="nx_dhcp_interface_decline"></a>nx_dhcp_interface_decline

Rifiutare l'indirizzo IP dal server DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio invia il messaggio di rifiuto al server per rifiutare un indirizzo IP assegnato dal server DHCP. Reinizializza inoltre il client DHCP. Per ulteriori informazioni, vedere *nx_dhcp_decline* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **Interface_index**: Indice dell'interfaccia per rifiutare l'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) messaggio di rifiuto DHCP inviato  
- **NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Decline the IP address offered by the DHCP server on interface 2.  */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```
## <a name="nx_dhcp_send_request"></a>nx_dhcp_send_request

Invia messaggio DHCP al server

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);

```

### <a name="description"></a>Descrizione

Questo servizio invia il messaggio DHCP specificato al server DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP. Per inviare un messaggio di rilascio o di rifiuto, l'applicazione deve utilizzare rispettivamente i servizi di *nx_dhcp [_interface] _Release*() o *nx_dhcp_interface_decline ()* .

È necessario avviare il client DHCP per l'utilizzo di questo servizio, ad eccezione dell'invio del INFORM_REQUEST tipo di messaggio.

>[!NOTE]
> Questo servizio non è destinato all'applicazione host a "unità" della macchina a stati client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.  
- **dhcp_message_type**: richiesta messaggio (definita in *nxd_dhcp_client. h*)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) messaggio DHCP inviato  
- **NX_DHCP_NOT_STARTED**: (0x96) indice di interfaccia non valido
- **NX_DHCP_INVALID_MESSAGE**: (0x9B) tipo di messaggio non valido da inviare
- NX_PTR_ERROR: (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send the DHCP INFORM REQUEST message to the server.  */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_interface_send_request"></a>nx_dhcp_interface_send_request

Invia messaggio DHCP al server in un'interfaccia specifica

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr, 
                                    UINT interface_index, 
                                    UINT dhcp_message_type);
```

### <a name="description"></a>Descrizione

Questo servizio invia un messaggio al server DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP. Per inviare un messaggio di rilascio o di rifiuto, l'applicazione deve utilizzare rispettivamente i servizi di *nx_dhcp [_interface] _Release*() o *nx_dhcp_interface_decline ()* .

È necessario avviare il client DHCP per l'utilizzo di questo servizio, ad eccezione dell'invio del tipo di messaggio di richiesta di comunicazione DHCP.

Questo servizio non è destinato all'applicazione host a "unità" della macchina a stati client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.
- **Interface_index**: Indice dell'interfaccia su cui inviare il messaggio
- **dhcp_message_type**: richiesta messaggio (definita in nxd_dhcp_client. h)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) messaggio DHCP inviato  
- **NX_DHCP_NOT_STARTED**: (0x96) indice di interfaccia non valido
- **NX_DHCP_INVALID_MESSAGE**: (0x9B) tipo di messaggio non valido da inviare
- Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send the INFORM REQUEST message to the server on the primary interface.  */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_server_address_get"></a>nx_dhcp_server_address_get

Ottenere l'indirizzo IP del server DHCP del client DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr, 
                                ULONG server_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP. Il chiamante può utilizzare questo servizio solo dopo che il client DHCP è associato a un indirizzo IP assegnato dal server DHCP. L'applicazione host può usare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure è possibile usare il *_dhcp_state_change_notify* NX ed eseguire query sullo stato del client DHCP NX_DHCP_STATE_BOUND. Per ulteriori informazioni sull'impostazione della funzione di callback di modifica dello stato, vedere *nx_dhcp_state_change_notify* .

Per trovare il server DHCP in un'interfaccia specifica quando sono abilitate più interfacce per il client DHCP, usare il servizio *nx_dhcp_interface_server_address_get*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.
- **server_address**: puntatore all'indirizzo IP del server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) indirizzo server DHCP restituito
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) non sono abilitate interfacce per DHCP
- NX_PTR_ERROR: (0x16) puntatore di input non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Use the state change notify service to determine the Client transition to the bound state and get its DHCP server IP address.*/

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{
ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
        }

}
```

## <a name="nx_dhcp_interface_server_address_get"></a>nx_dhcp_interface_server_address_get

Ottenere l'indirizzo IP del server DHCP del client DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr, 
                                          UINT interface_index,
                                          ULONG server_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nell'interfaccia specificata se tale interfaccia è abilitata per DHCP. Il client DHCP deve essere nello stato associato. Dopo l'avvio del client DHCP su tale interfaccia, l'applicazione host può utilizzare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure utilizzare il callback di modifica dello stato del client DHCP ed eseguire una query sullo stato del client DHCP NX_DHCP_STATE_BOUND. Per ulteriori informazioni sull'impostazione della funzione di callback di modifica dello stato, vedere *nx_dhcp_state_change_notify* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.
- **Interface_index**: Indice dell'interfaccia per ottenere l'indirizzo IP
- **server_address**: puntatore all'indirizzo IP del server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) indirizzo server DHCP restituito
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) non sono abilitate interfacce per DHCP
- **NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. */

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

/* Get the DHCP server IP address on interface 1 */
if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
         status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                       &server_address);
        }
}
```

## <a name="nx_dhcp_set_interface_index"></a>nx_dhcp_set_interface_index

Impostare l'interfaccia di rete per l'istanza DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'interfaccia di rete per l'istanza DHCP per la connessione al server DHCP in quando viene eseguito il client DHCP configurato per una singola interfaccia di rete.

Per impostazione predefinita, il client DHCP viene eseguito sull'interfaccia principale. Per eseguire DHCP in un servizio secondario, utilizzare questo servizio per impostare l'interfaccia secondaria come interfaccia client DHCP. In precedenza, l'applicazione deve registrare l'interfaccia specificata nell'istanza IP utilizzando il servizio *nx_ip_interface_attach* .

>[!NOTE]
> Questo servizio è destinato alle applicazioni che intendono eseguire il client DHCP su una sola interfaccia. Per eseguire DHCP su più interfacce, vedere *nx_dhcp_interface_enable* per altri dettagli.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo DHCP.  
- **index**: Indice dell'interfaccia di rete del dispositivo

### <a name="return-values"></a>Valori restituiti

- L'interfaccia **NX_SUCCESS**: (0x00) è stata impostata correttamente.
- **NX_INVALID_INTERFACE**: (0x4C) interfaccia di rete non valida
- Interfaccia **NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) abilitata per DHCP
- **NX_DHCP_NO_RECORDS_AVAILABLE**: (0XA7) nessun record disponibile per un altro 
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Set the DHCP Client interface to the secondary interface (index 1).  */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set.  */
```

## <a name="nx_dhcp_start"></a>nx_dhcp_start

Avviare l'elaborazione DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione DHCP su tutte le interfacce abilitate per DHCP. Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*

Per verificare quando l'istanza IP è associata a un indirizzo IP sull'interfaccia client DHCP, usare *nx_ip_status_check* per vedere Verificare che l'indirizzo IP sia valido.

Se sono presenti altre interfacce che eseguono già DHCP, il servizio non le influirà.

Per avviare DHCP in un'interfaccia specifica quando sono abilitate più interfacce, usare il servizio *nx_dhcp_interface_start* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avvio DHCP riuscito.  
- **NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the DHCP processing for this IP instance.  */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_interface_start"></a>nx_dhcp_interface_start

Avvia elaborazione DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP. Per ulteriori informazioni sull'abilitazione di un'interfaccia per DHCP, vedere *nx_dhcp_interface_enable*(). Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*

Se non sono presenti altre interfacce che eseguono il client DHCP, il servizio avvierà/riprenderà il thread del client DHCP e (ri) attiverà il timer del client DHCP.  
  
L'applicazione deve usare *nx_ip_status_check* per verificare se è stato ottenuto un indirizzo IP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **Interface_index**: Indice in cui avviare il client DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avvio DHCP riuscito. 
- **NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_state_change_notify"></a>nx_dhcp_state_change_notify

Imposta funzione di callback modifica stato DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_state_change_notify(NX_DHCP *dhcp_ptr, 
                                 VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, UCHAR new_state));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback specificata dhcp_state_change_notify per notificare a un'applicazione le modifiche dello stato DHCP. La funzione di callback fornisce lo stato di transizione del client DHCP.

Di seguito sono riportati i valori associati ai vari Stati DHCP:

- NX_DHCP_STATE_BOOT: 1
- NX_DHCP_STATE_INIT: 2
- NX_DHCP_STATE_SELECTING: 3
- NX_DHCP_STATE_REQUESTING: 4
- NX_DHCP_STATE_BOUND: 5
- NX_DHCP_STATE_RENEWING: 6
- NX_DHCP_STATE_REBINDING: 7
- NX_DHCP_STATE_FORCERENEW: 8
- NX_DHCP_STATE_ADDRESS_PROBING: 9

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **dhcp_state_change_notify**: puntatore alla funzione di callback modifica stato

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) set di callback riuscito.  
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Register the “my_state_change” function to be called on any DHCP state change, assuming DHCP has alreadybeen created.  */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_interface_state_change_notify"></a>nx_dhcp_interface_state_change_notify

Imposta la funzione di callback della modifica dello stato DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_state_change_notify(NX_DHCP *dhcp_ptr, UINT interface_index,
                                           VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                                                            UINT interface_index,
                                                                            UCHAR new_state));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback specificata per notificare a un'applicazione le modifiche dello stato DHCP. Gli argomenti di input funciton di callback sono l'indice dell'interfaccia e lo stato di transizione del client DHCP a tale interfaccia.

Per ulteriori informazioni sulle funzioni di modifica dello stato, vedere *nx_dhcp_state_change_notify*().

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **dhcp_interface_state_change_notify**: puntatore alla funzione di callback dell'applicazione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) set di callback riuscito.  
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Register the “my_state_change” function to be called on any DHCP state change,   
   assuming DHCP has alreadybeen created.  */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                  UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_stop"></a>nx_dhcp_stop

Arresta l'elaborazione DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe l'elaborazione DHCP su tutte le interfacce che hanno avviato l'elaborazione DHCP. Se non sono presenti interfacce che elaborano DHCP, il servizio sospende il thread del client DHCP e disattiva il timer del client DHCP.

Per arrestare DHCP in un'interfaccia specifica se sono abilitate più interfacce per DHCP, usare il servizio *nx_dhcp_interface_stop* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) arresto DHCP riuscito
- **NX_DHCP_NOT_STARTED**: (0X96) l'istanza DHCP non è stata avviata.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the DHCP processing for this IP instance.  */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_interface_stop"></a>nx_dhcp_interface_stop

Arresta l'elaborazione DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe l'elaborazione DHCP sull'interfaccia specificata se DHCP è già avviato. Se non sono presenti altre interfacce che eseguono DHCP, il thread e il timer DHCP verranno sospesi.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **Interface_index**: interfaccia in cui arrestare l'elaborazione DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) arresto DHCP riuscito
- **NX_DHCP_NOT_STARTED**: (0X96) DHCP non avviato.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_user_option_retrieve"></a>nx_dhcp_user_option_retrieve

Recupera un'opzione DHCP dall'ultima risposta server

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, UINT request_option, 
                                  UCHAR *destination_ptr, UINT *destination_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP. In caso di esito positivo, i dati dell'opzione vengono copiati nel buffer specificato.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.  
- **request_option**: opzione DHCP, come specificato dalle RFC. Vedere l'opzione NX_DHCP_OPTION in *nxd_dhcp_client. h*.
- **destination_ptr**: puntatore alla destinazione per la stringa di risposta.  
- **destination_size**: puntatore alla dimensione della destinazione e al ritorno, la destinazione in cui inserire il numero di byte restituiti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il recupero delle opzioni è riuscito.  
- **NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato.
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) non sono abilitate interfacce per DHCP
- **NX_DHCP_DEST_TO_SMALL**: (0x95) la destinazione è troppo piccola per mantenere la risposta.
- Impossibile trovare l'opzione **NX_DHCP_PARSE_ERROR**: (0x97) nella risposta del server.
- NX_PTR_ERROR: (0x16) puntatore di input non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
                                        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a>nx_dhcp_interface_user_option_retrieve

Recupera un'opzione DHCP dall'ultima risposta server sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT request_option, UCHAR *destination_ptr,
                                            UINT *destination_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nell'interfaccia specificata, se tale interfaccia è abilitata per DHCP. In caso di esito positivo, i dati dell'opzione vengono copiati nel buffer specificato.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **Interface_index**: Indice in cui recuperare l'opzione specificata
- **request_option**: opzione DHCP, come specificato dalle RFC. Vedere l'opzione NX_DHCP_OPTION: in *nxd_dhcp_client. h*.  
- **destination_ptr**: puntatore alla destinazione per la stringa di risposta.  
- **destination_size**: puntatore alla dimensione della destinazione e al ritorno, la destinazione in cui inserire il numero di byte restituiti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il recupero delle opzioni è riuscito.  
- **NX_DHCP_NOT_BOUND**: (0x94) indirizzo IP non assegnato
- **NX_DHCP_DEST_TO_SMALL**: il buffer (0x95) è troppo piccolo
- **NX_DHCP_PARSE_ERROR**: (0x97) l'opzione DHCP non è stata trovata nella risposta del server.
- NX_PTR_ERROR: (0x16) puntatore DHCP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
                                                  dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_user_option_convert"></a>nx_dhcp_user_option_convert

Converte quattro byte in ULONG

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio converte i quattro caratteri a cui punta "option_string_ptr" in un valore long senza segno. È particolarmente utile quando gli indirizzi IP sono  
presente.

### <a name="input-parameters"></a>Parametri di input

- **option_string_ptr**: puntatore a una stringa di opzione recuperata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **Valore**: valore dei primi quattro byte.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a>nx_dhcp_user_option_add_callback_set

Imposta la funzione di callback per l'aggiunta di opzioni fornite dall'utente

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
                                           UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                                                        UINT iface_index, 
                                                                        UINT message_type, 
                                                                        UCHAR *user_option_ptr, 
                                                                        UINT *user_option_length));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback specificata per aggiungere opzioni fornite dall'utente.

Se la funzione di callback specificata, le applicazioni possono aggiungere opzioni fornite dall'utente nel pacchetto per iface_index e message_type.

>[!NOTE] 
> Nella routine dell'utente. Le applicazioni devono seguire il formato delle opzioni DHCP quando si aggiungono le opzioni fornite dall'utente. La dimensione totale delle opzioni utente deve essere minore o uguale a user_option_length e aggiornare la user_option_length come lunghezza delle opzioni reali. Restituisce NX_TRUE se le opzioni di aggiunta sono state completate, in caso contrario restituire NX_FALSE.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.
- **dhcp_user_option_add**: puntatore alla funzione di aggiunta dell'opzione User.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) set di callback riuscito.
- NX_PTR_ERROR: (0x16) puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created.  */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered.  */

```

