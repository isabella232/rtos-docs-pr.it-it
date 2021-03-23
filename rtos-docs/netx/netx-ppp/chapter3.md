---
title: Capitolo 3-Descrizione dei servizi di Azure RTO NetX Point-to-Point Protocol (PPP)
description: Questo capitolo contiene una descrizione di tutti i servizi di Azure RTO NetX PPP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f24d7366d27a8223b069a54ef7b93f6b3e38bf3a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822556"
---
# <a name="chapter-3---description-of-azure-rtos-netx-point-to-point-protocol-ppp-services"></a>Capitolo 3-Descrizione dei servizi di Azure RTO NetX Point-to-Point Protocol (PPP)

Questo capitolo contiene una descrizione di tutti i servizi di Azure RTO NetX PPP (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_ppp_byte_receive**: *ricezione di un byte da ISR seriale*
- **nx_ppp_chap_challenge**: *genera una richiesta CHAP*
- **nx_ppp_chap_enable**: *abilitare l'autenticazione CHAP*
- **nx_ppp_create**: *creare un'istanza di PPP*
- **nx_ppp_delete**: *eliminare un'istanza di PPP*
- **nx_ppp_dns_address_get**: *ottenere l'indirizzo IP DNS*
- **nx_ppp_dns_address_set**:*impostare l'indirizzo IP del server DNS*
- **nx_ppp_secondary_dns_address_get**: *ottenere l'indirizzo IP del server DNS secondario*
- **nx_ppp_secondary_dns_address_set**: *impostare l'indirizzo IP del server Secondary_DNS*
- **nx_ppp_interface_index_get**: *ottenere l'indice dell'interfaccia IP*
- **nx_ppp_ip_address_assign**: *assegnare gli indirizzi IP per protocollo IPCP*
- **nx_ppp_link_down_notify**: *notifica applicazione al collegamento in basso*
- **nx_ppp_link_up_notify**: *notifica applicazione al collegamento*
- **nx_ppp_nak_authentication_notify**: *notifica l'applicazione se viene ricevuta l'autenticazione NAK*
- **nx_ppp_pap_enable**: *Abilita autenticazione PAP*
- **nx_ppp_ping_request**: *inviare una richiesta echo LCP*
- **nx_ppp_raw_string_send**: *Invia stringa non PPP*
- **nx_ppp_restart**: *riavvio dell'elaborazione PPP*
- **nx_ppp_start**: *avviare l'elaborazione PPP*
- **nx_ppp_status_get**: *ottenere lo stato PPP corrente*
- **nx_ppp_stop**: *arrestare l'elaborazione PPP*
- **nx_ppp_packet_receive**: *ricevere il pacchetto PPP*
- **nx_ppp_packet_send_set**: *impostare la funzione di invio pacchetti PPP*

## <a name="nx_ppp_byte_receive"></a>nx_ppp_byte_receive

Ricevi un byte da ISR seriale

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_byte_receive(NX_PPP *ppp_ptr, UCHAR byte);
```

### <a name="description"></a>Descrizione

Questo servizio viene in genere chiamato dalla routine ISR (Serial driver interrupt Service) dell'applicazione per trasferire un byte ricevuto a PPP. Quando viene chiamato, questa routine inserisce il byte ricevuto in un buffer di byte circolare e invia una notifica al thread PPP appropriato per l'elaborazione.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **byte**: byte ricevuti dal dispositivo seriale

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) ricezione byte PPP riuscita.
- **NX_PPP_BUFFER_FULL**: (0xB1) il buffer seriale PPP è già pieno.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Thread, ISRs

### <a name="example"></a>Esempio

```c
/* Notify “my_ppp” of a received byte. */
status =  nx_ppp_byte_receive(&my_ppp, new_byte);

/* If status is NX_SUCCESS the received byte was successfully
   buffered. */
```

## <a name="nx_ppp_chap_challenge"></a>nx_ppp_chap_challenge

Genera una richiesta CHAP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_chap_challenge(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una richiesta CHAP dopo che la connessione PPP è già in esecuzione. In questo modo l'applicazione è in grado di verificare l'autenticità della connessione periodicamente. Se la verifica ha esito negativo, il collegamento PPP viene chiuso.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avviata verifica PPP riuscita.
- **NX_PPP_FAILURE**: (0XB0) la richiesta PPP non è valida. il protocollo CHAP è stato abilitato solo per la risposta.
- **NX_NOT_IMPLEMENTED**: (0x80) la logica CHAP è stata disabilitata tramite NX_PPP_DISABLE_CHAP.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Initiate a PPP challenge for instance “my_ppp”. */
status =  nx_ppp_chap_challenge(&my_ppp);

/* If status is NX_SUCCESS a CHAP challenge “my_ppp” was successfully 
initiated. */
```

## <a name="nx_ppp_chap_enable"></a>nx_ppp_chap_enable

Abilitare l'autenticazione CHAP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_chap_enable(NX_PPP *ppp_ptr, 
                        UINT (*get_challenge_values)(CHAR *rand_value,CHAR *id,CHAR *name),
                        UINT (*get_responder_values)(CHAR *system,CHAR *name,CHAR *secret),
                        UINT (*get_verification_values)(CHAR *system,CHAR *name,CHAR *secret)); 
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il protocollo CHAP (Challenge-Handshake Authentication Protocol) per l'istanza di PPP specificata.

Se vengono specificati i puntatori a funzione "***get_challenge_values**_" e "_ * _get_verification_values_* *", CHAP è richiesto da questa istanza di PPP. In caso contrario, l'autenticazione CHAP risponde solo alle richieste di verifica del peer.

Sono presenti diversi elementi di dati a cui viene fatto riferimento nelle funzioni di callback obbligatorie. Si prevede che il *segreto*, il *nome* e il *sistema* degli elementi di dati siano stringhe con terminazione NULL con una dimensione massima di NX_PPP_NAME_SIZE-1. È previsto che l'elemento dati *rand_value* sia una stringa con terminazione null con una dimensione massima di NX_PPP_VALUE_SIZE-1. L' *ID* dell'elemento dati è un tipo di carattere senza segno semplice.

>[!NOTE]
> Questa funzione deve essere chiamata dopo *nx_ppp_create* ma prima di nx_ip_create o *nx_ip_interface_attach*.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **get_challenge_values**: puntatore alla funzione dell'applicazione per recuperare i valori utilizzati per la richiesta di verifica. Si noti che i valori *rand_value*, *ID* e *Secret* devono essere copiati nelle destinazioni specificate.
- **get_responder_values**: puntatore alla funzione dell'applicazione che recupera i valori utilizzati per rispondere a una richiesta di verifica. Si noti che i valori di *sistema*, *nome* e *segreto* devono essere copiati nelle destinazioni specificate.
- **get_verification_values**: puntatore alla funzione dell'applicazione che recupera i valori utilizzati per verificare la risposta alla richiesta di verifica. Si noti che i valori di *sistema*,*nome* e *segreto* devono essere copiati nelle destinazioni specificate.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) abilitata autenticazione CHAP PPP riuscita
- **NX_NOT_IMPLEMENTED**: (0x80) la logica CHAP è stata disabilitata tramite NX_PPP_DISABLE_CHAP.
- NX_PTR_ERROR: (0x07) puntatore PPP o puntatore alla funzione di callback non valido. Si noti che se si specifica *get_challenge_values* , è necessario specificare anche la funzione *get_verification_values* .
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
CHAR    name_string[] = "username";
CHAR    rand_value_string[] = "123456";
CHAR    system_string[] = "system";
CHAR    secret_string[] = "secret";

/* Enable CHAP in both directions (CHAP challenger and CHAP responder) for 
“my_ppp”. */
status =  nx_ppp_chap_enable(&my_ppp,   get_challenge_values, 
                              get_responder_values,
                              get_verification_values);


/* If status is NX_SUCCESS, “my_ppp” has CHAP enabled. */
/* Define the CHAP enable routines.  */
UINT  get_challenge_values(CHAR *rand_value, CHAR *id, CHAR *name)
{
   UINT    i;
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   *id =  '1';  /* One byte  */
   for (i = 0; i< (NX_PPP_VALUE_SIZE-1); i++)
   {
      rand_value[i] =  rand_value_string[i];
   }
   rand_value[i] =  0;
   
   return(NX_SUCCESS);  
}


UINT  get_responder_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;

   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

UINT  get_verification_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

```
## <a name="nx_ppp_create"></a>nx_ppp_create

Creare un'istanza di PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_create(NX_PPP *ppp_ptr, CHAR *name, NX_IP *ip_ptr, 
                    VOID *stack_memory_ptr, ULONG stack_size, 
                    UINT thread_priority, NX_PACKET_POOL *pool_ptr,
                    void (*ppp_invalid_packet_handler)(NX_PACKET *packet_ptr),
                    void (*ppp_byte_send)(UCHAR byte));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza di PPP per l'istanza IP di NetX specificata.

>[!NOTE]
> È in genere consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread PPP. Per ulteriori informazioni su come specificare la priorità del thread IP, fare riferimento al servizio *nx_ip_create* .

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **nome**: nome dell'istanza di PPP.
- **ip_ptr**: puntatore al blocco di controllo per l'istanza IP non ancora creata.
- **stack_memory_ptr**: puntatore all'inizio dell'area dello stack del thread PPP.
- **stack_size**: dimensioni in byte nello stack del thread.
- **pool_ptr**: puntatore al pool di pacchetti predefinito.
- **THREAD_PRIORITY**: priorità dei thread PPP interni (1-31).
- **ppp_invalid_packet_handler**: puntatore della funzione al gestore dell'applicazione per tutti i pacchetti non PPP. Il PPP NetX in genere chiama questa routine durante l'inizializzazione. Questo è il punto in cui l'applicazione può rispondere ai comandi del modem o, nel caso di Windows XP, l'applicazione NetX PPP può avviare PPP rispondendo con "SERVER CLIENT" al "CLIENT" iniziale inviato da Windows XP.
- **ppp_byte_send**: puntatore a funzione per la routine di output di byte seriale dell'applicazione.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) creazione PPP riuscita.
- NX_PTR_ERROR: (0x07) puntatore a funzione di output PPP, IP o byte non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create “my_ppp” for IP instance “my_ip”. */
status =  nx_ppp_create(&my_ppp, “my PPP”, &my_ip, stack_start, 1024, 2, 
                        &my_pool, my_invalid_packet_handler, my_out_byte);

/* If status is NX_SUCCESS the PPP instance was successfully
   created. */
```

## <a name="nx_ppp_delete"></a>nx_ppp_delete

Eliminare un'istanza di PPP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_delete(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina l'istanza di PPP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione PPP riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete PPP instance “my_ppp”. */
status =  nx_ppp_delete(&my_ppp);

/* If status is NX_SUCCESS the “my_ppp” was successfully deleted. */
```

## <a name="nx_ppp_dns_address_get"></a>nx_ppp_dns_address_get

Ottenere l'indirizzo IP DNS

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP DNS fornito dal peer. Se non è stato fornito alcun indirizzo IP dal peer, viene restituito un indirizzo IP 0.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **dns_address_ptr**: destinazione per l'indirizzo IP DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) indirizzo PPP riuscito Get.
- **NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c

ULONG  my_dns_address;

/* Get IP Server address supplied by peer. */
status =  nx_ppp_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the DNS IP address – 
   if the peer supplied one. */
```

## <a name="nx_ppp_secondary_dns_address_get"></a>nx_ppp_secondary_dns_address_get

Ottenere l'indirizzo IP del server DNS secondario

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_secondary_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP DNS secondario fornito dal peer nell'handshake protocollo IPCP. Se non è stato fornito alcun indirizzo IP dal peer, viene restituito un indirizzo IP 0.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **dns_address_ptr**: destinazione per l'indirizzo del server DNS secondario

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) indirizzo DNS riuscito Get.
- **NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c
ULONG  my_dns_address;

/* Get secondary DNS Server address supplied by peer. */
status =  nx_ppp_secondary_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the secondary DNS Server address – if the peer supplied one. */
```

## <a name="nx_ppp_dns_address_set"></a>nx_ppp_dns_address_set

Impostare l'indirizzo IP del server DNS primario

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP del server DNS. Se il peer invia una richiesta di opzione del server DNS nello stato protocollo IPCP, questo host fornirà le informazioni.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **dns_address**: indirizzo del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il set di indirizzi DNS è riuscito.
- **NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c

ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the DNS Server address provided if the peer requests one. */

```

## <a name="nx_ppp_secondary_dns_address_set"></a>nx_ppp_secondary_dns_address_set

Impostare l'indirizzo IP del server DNS secondario

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_secondary_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP del server DNS secondario. Se il peer invia una richiesta di opzione del server DNS secondario nello stato protocollo IPCP, questo host fornirà le informazioni.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **dns_address**: indirizzo del server DNS secondario

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il set di indirizzi DNS è riuscito. 
- **NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_secondary_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the secondary DNS Server address provided if the peer requests one. */

```
## <a name="nx_ppp_interface_index_get"></a>nx_ppp_interface_index_get

Ottenere l'indice dell'interfaccia IP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_interface_index_get(NX_PPP *ppp_ptr, UINT *index_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indice dell'interfaccia IP associato a questa istanza di PPP. Questa operazione è utile solo quando l'istanza di PPP non è l'interfaccia principale di un'istanza IP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **index_ptr**: destinazione per l'indice dell'interfaccia

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) ottenere l'indice PPP riuscito.
- **NX_IN_PROGRESS**: (0x37) PPP non ha completato l'inizializzazione.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c
ULONG  my_index;

/* Get the interface index for this PPP instance. */
status =  nx_ppp_interface_index_get(&my_ppp, &my_index);

/* If status is NX_SUCCESS the “my_index” contains the IP interface index for
   this PPP instance. */

```
## <a name="nx_ppp_ip_address_assign"></a>nx_ppp_ip_address_assign

Assegnare indirizzi IP per protocollo IPCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_ip_address_assign(NX_PPP *ppp_ptr, ULONG local_ip_address, 
            ULONG peer_ip_address);
```

### <a name="description"></a>Descrizione

Questo servizio configura gli indirizzi IP locali e peer per l'utilizzo in Internet Protocol Control Protocol (protocollo IPCP). L'applicazione PPP dovrebbe richiamare questo servizio su un'istanza di PPP con indirizzi IP validi per se stesso e per l'altro peer.  Se non è stato registrato alcun indirizzo valido con un'istanza di PPP, deve basarsi sul peer PPP per definirne l'indirizzo IP.


### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **local_ip_address**: indirizzo IP locale.
- **peer_ip_address**: indirizzo IP del peer.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) assegnazione di indirizzi PPP riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set IP addresses for “my_ppp”. */
status =  nx_ppp_ip_address_assign(&my_ppp, IP_ADDRESS(256,2,2,187), 
IP_ADDRESS(256,2,2,188));


/* If status is NX_SUCCESS the “my_ppp” has the IP addresses. */
```

## <a name="nx_ppp_link_down_notify"></a>nx_ppp_link_down_notify

Invia notifica all'applicazione al collegamento

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_link_down_notify(NX_PPP *ppp_ptr, 
                             VOID (*link_down_callback)(NX_PPP *ppp_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra il callback di notifica per il collegamento dell'applicazione con l'istanza di PPP specificata. Se diverso da NULL, la funzione di callback del collegamento di un'applicazione viene chiamata ogni volta che il collegamento diventa inattivo.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **link_down_callback**: puntatore alla funzione di notifica collegamento all'applicazione. Se è NULL, la notifica del collegamento è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il collegamento alla registrazione di callback delle notifiche è riuscito.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c
/* Register “my_link_down_callback” to be called whenever the PPP
   link goes down. */
status =  nx_ppp_link_down_notify(&my_ppp, my_link_down_callback);


/* If status is NX_SUCCESS the function “my_link_down_callback” has been
   registered with this PPP instance. */

VOID my_link_down_callback(NX_PPP *ppp_ptr)
{

/* On link down, simply restart PPP.  */
    nx_ppp_restart(ppp_ptr);
} 
```
## <a name="nx_ppp_link_up_notify"></a>nx_ppp_link_up_notify

Invia notifica all'applicazione al collegamento

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_link_up_notify(NX_PPP *ppp_ptr, 
                           VOID (*link_up_callback)(NX_PPP *ppp_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio registra il callback delle notifiche di collegamento dell'applicazione con l'istanza di PPP specificata. Se diverso da NULL, la funzione di callback del collegamento dell'applicazione viene chiamata ogni volta che il collegamento viene visualizzato.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **link_up_callback**: puntatore alla funzione di notifica collegamento dell'applicazione. Se è NULL, la notifica di collegamento è disabilitata. * *

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) collegamento riuscito registrazione di callback di notifica.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c
/* Register “my_link_up_callback” to be called whenever the PPP
   link comes up. */
status =  nx_ppp_link_up_notify(&my_ppp, my_link_up_callback);


/* If status is NX_SUCCESS the function “my_link_up_callback” has been
   registered with this PPP instance. */

VOID my_link_up_callback(NX_PPP *ppp_ptr)
{
    /* On link up, the application my want to start sending/receiving
       UPD/TCP data.  */
}
```

## <a name="nx_ppp_nak_authentication_notify"></a>nx_ppp_nak_authentication_notify

Invia notifica all'applicazione se è stata ricevuta l'autenticazione NAK

### <a name="prototype"></a>Prototipo

```c
UINT    nx_ppp_nak_authentication_notify(NX_PPP *ppp_ptr, 
                                         void (*nak_authentication_notify)(void));
```

### <a name="description"></a>Descrizione

Questo servizio registra il callback di notifica di autenticazione NAK dell'applicazione con l'istanza di PPP specificata. Se diverso da NULL, questa funzione di callback viene chiamata ogni volta che l'istanza di PPP riceve un NAK durante authentiaction.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **nak_authentication_notify**: puntatore a funzione chiamato quando l'istanza di PPP riceve un NAK di autenticazione. Se è NULL, la notifica è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la registrazione del callback di notifica è riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c
/* Register “my_nak_auth_callback” to be called whenever the PPP
   receives a NAK during authentication. */
status =  nx_ppp_nak_authentication_notify(&my_ppp, my_nak_auth_callback);

/* If status is NX_SUCCESS the function “my_nak_auth_callback” has been
   registered with this PPP instance. */

VOID my_nak_auth_callback(NX_PPP *ppp_ptr)
{
   /* Handle the situation of receiving an authentication NAK */
}

```

## <a name="nx_ppp_pap_enable"></a>nx_ppp_pap_enable

Abilita autenticazione PAP

### <a name="prototype"></a>Prototipo

```c

UINT  nx_ppp_pap_enable(NX_PPP *ppp_ptr, 
                        UINT (*generate_login)(CHAR *name, CHAR *password),
                        UINT (*verify_login)(CHAR *name, CHAR *password));
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il Password Authentication Protocol (PAP) per l'istanza di PPP specificata. Se viene specificato il puntatore a funzione "***verify_login***", il Pap è richiesto da questa istanza di PPP. In caso contrario, PAP risponde solo ai requisiti PAP del peer, come specificato durante la negoziazione LCP.

Sono presenti diversi elementi di dati a cui viene fatto riferimento nelle funzioni di callback obbligatorie. È previsto che il *nome* dell'elemento dati sia una stringa con terminazione null con una dimensione massima di NX_PPP_NAME_SIZE-1. Anche la *password* dell'elemento dati deve essere una stringa con terminazione null con una dimensione massima pari a NX_PPP_PASSWORD_SIZE-1.

>[!NOTE]
> Questa funzione deve essere chiamata dopo *nx_ppp_create* ma prima di *nx_ip_create* o *nx_ip_interface_attach*.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **generate_login**: puntatore alla funzione dell'applicazione che produce un *nome* e una *password* per l'autenticazione da parte del peer. Si noti che i valori relativi al *nome* e alla *password* devono essere copiati nelle destinazioni specificate.
- **verify_login**: puntatore alla funzione dell'applicazione che verifica il *nome* e la *password* forniti dal peer. Questa routine deve confrontare il *nome* e la *password* specificati. Se questa routine restituisce NX_SUCCESS, il nome e la password sono corretti e il PPP può procedere al passaggio successivo. In caso contrario, questa routine restituisce NX_PPP_ERROR e PPP è semplicemente in attesa di un altro nome e password.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'abilitazione del Pap PPP è riuscita.
- **NX_NOT_IMPLEMENTED**: (0x80) la logica PAP è stata disabilitata tramite NX_PPP_DISABLE_PAP.
- NX_PTR_ERROR: (0x07) puntatore PPP o puntatore a funzione dell'applicazione non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
CHAR    name_string[] = "username";
CHAR    password_string[] =  "password";

/* Enable PAP for PPP instance “my_ppp”. */
status =  nx_ppp_pap_enable(&my_ppp, my_generate_login, my_verify_login);

/* If status is NX_SUCCESS the “my_ppp” now has PAP enabled. */

/* Define callback routines for PAP enable.  */

UINT  generate_login(CHAR *name, CHAR *password)
{

UINT    i;

for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
name[i] = name_string[i];
name[i] =  0;

for (i = 0; i< (NX_PPP_PASSWORD_SIZE-1); i++)
password[i] = password_string[i];
password_string[i] =  0;

return(NX_SUCCESS);  
}

UINT  verify_login(CHAR *name, CHAR *password)
{

/* Assume name and password are correct. Normally, 
a comparison would be made here!  */
printf("Name: %s, Password: %s\n", name, password);

return(NX_SUCCESS);  
}
```

## <a name="nx_ppp_ping_request"></a>nx_ppp_ping_request

Invia una richiesta ping LCP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_ping_request(NX_PPP *ppp_ptr, CHAR *data, 
                          UINT data_size, ULONG wait_opion);
```

### <a name="description"></a>Descrizione

Questo servizio invia una richiesta ping LCP e imposta un flag che il dispositivo PPP è in attesa di una risposta echo. Il servizio viene restituito non appena viene inviata la richiesta. Non attende una risposta. 

Quando viene ricevuta una risposta echo corrispondente, l'attività thread PPP cancellerà il flag. Il dispositivo PPP deve avere completato la parte LCP della negoziazione PPP.

Questo servizio è utile per i set di impostazioni PPP in cui il polling dell'hardware per lo stato dei collegamenti potrebbe non essere immediatamente possibile.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **Data**: puntatore ai dati da inviare nella richiesta echo.
- **DATA_SIZE**: dimensioni dei dati da inviare WAIT_OPTION tempo di attesa per l'invio del messaggio echo LCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la richiesta echo è stata inviata correttamente.
- **NX_PPP_NOT_ESTABLISHED**: (0xB5) connessione PPP non stabilita.
- NX_PTR_ERROR: (0x07) puntatore PPP o puntatore a funzione dell'applicazione non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread applicazione

### <a name="example"></a>Esempio

```c

CHAR    buffer[] = "username";
UINT    buffer_length =  strlen("username ");

/* Send an LCP ping request”. */
status =  nx_ppp_ping_request(&my_ppp, &buffer[0], buffer_length, 200);

/* If status is NX_SUCCESS the LCP echo request was successfully sent. Now wait to 
   receive a response. */

while(my_ppp.nx_ppp_lcp_echo_reply_id > 0)
{
    tx_thread_sleep(100);
}

/* Got a valid reply! */
```

## <a name="nx_ppp_raw_string_send"></a>nx_ppp_raw_string_send

Invia una stringa ASCII non elaborata

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_raw_sting_send(NX_PPP *ppp_ptr, CHAR *string_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una stringa ASCII non PPP direttamente dall'interfaccia PPP. Viene in genere usato dopo che PPP riceve un pacchetto non PPP che contiene le informazioni di controllo del modem.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **string_ptr**: puntatore alla stringa da inviare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'invio di una stringa non ELABORAta PPP è riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP o puntatore di stringa non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

/* Send “CLIENTSERVER” to “CLIENT” sent by Windows 98 before PPP is
initiated.  */
status =  nx_ppp_raw_string_send(&my_ppp, “CLIENTSERVER”);

/* If status is NX_SUCCESS the raw string was successfully Sent via PPP. */
```
## <a name="nx_ppp_restart"></a>nx_ppp_restart

Riavvia elaborazione PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_restart(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio riavvia l'elaborazione PPP. Viene in genere chiamato quando il collegamento deve essere ristabilito da un callback di collegamento disattivato o da un messaggio modem non PPP che indica che la comunicazione è stata persa.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il riavvio PPP riuscito è stato avviato.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Restart the PPP instance “my_ppp”.  */
status =  nx_ppp_restart(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been restarted. */
```

## <a name="nx_ppp_start"></a>nx_ppp_start

Avviare l'elaborazione PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_start(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione PPP. Viene in genere chiamato dopo la chiamata di nx_ppp_stop ().

>[!NOTE]
> PPP avvia automaticamente l'elaborazione PPP quando il collegamento è abilitato.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avviata PPP riuscita avviata. 
- **NX_PPP_ALREADY_STARTED**: (0XB9) PPP già avviato.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the PPP instance “my_ppp”.  */
status =  nx_ppp_start(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been started. */
```

## <a name="nx_ppp_status_get"></a>nx_ppp_status_get

Ottieni stato PPP corrente

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_status_get(NX_PPP *ppp_ptr, UINT *status_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio ottiene lo stato corrente dell'istanza di PPP specificata.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **STATUS_PTR**: destinazione per lo stato PPP, di seguito sono riportati i valori di stato possibili:
    - **NX_PPP_STATUS_ESTABLISHED**
    - **NX_PPP_STATUS_LCP_IN_PROGRESS**
    - **NX_PPP_STATUS_LCP_FAILED**
    - **NX_PPP_STATUS_PAP_IN_PROGRESS**
    - **NX_PPP_STATUS_PAP_FAILED**
    - **NX_PPP_STATUS_CHAP_IN_PROGRESS**
    - **NX_PPP_STATUS_CHAP_FAILED**
    - **NX_PPP_STATUS_IPCP_IN_PROGRESS**
    - **NX_PPP_STATUS_IPCP_FAILED**

>[!NOTE]
> Lo stato è valido solo se l'API restituisce NX_SUCCESS. Inoltre, se viene restituito uno dei valori di stato * _FAILED, l'elaborazione PPP viene arrestata in modo efficace fino al riavvio dell'applicazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) richiesta di stato PPP riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="example"></a>Esempio

```c
UINT ppp_status;
UINT status;


/* Get the current status of PPP instance “my_ppp”.  */
status =  nx_ppp_status_get(&my_ppp, &ppp_status);

/* If status is NX_SUCCESS the current internal PPP status is contained in
   “ppp_status”. */
```
## <a name="nx_ppp_stop"></a>nx_ppp_stop

Avviare l'elaborazione PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_stop(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe l'elaborazione PPP. L'utente può anche chiamare nx_ppp_start () per avviare l'elaborazione PPP, se necessario.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avviata PPP riuscita avviata. 
- **NX_PPP_ALREADY_STOPPED**: (0XB8) PPP è già stato arrestato.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the PPP instance “my_ppp”.  */
status =  nx_ppp_stop(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been stopped. */
```
## <a name="nx_ppp_packet_receive"></a>nx_ppp_packet_receive

Ricevi pacchetto PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_packet_receive(NX_PPP *ppp_ptr, NX_PACKET *packet_ptr);

```

### <a name="description"></a>Descrizione

Questo servizio riceve il pacchetto PPP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **packet_ptr**: puntatore al pacchetto PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) richiesta di stato PPP riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Receive the PPP packet of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_receive(&my_ppp, packet_ptr);

/* If status is NX_SUCCESS the PPP packet has received. */


```
## <a name="nx_ppp_packet_send_set"></a>nx_ppp_packet_send_set

Impostare la funzione di invio pacchetti PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_packet_send_set(NX_PPP *ppp_ptr, 
                             VOID (*nx_ppp_packet_send)(NX_PACKET *packet_ptr));

```

### <a name="description"></a>Descrizione

Questo servizio imposta il funciton di invio del pacchetto PPP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr**: puntatore al blocco di controllo PPP.
- **nx_ppp_packet_send**: routine per l'invio del pacchetto PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) richiesta di stato PPP riuscita.
- NX_PTR_ERROR: (0x07) puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the PPP packet send function of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_send_set(&my_ppp, nx_ppp_packet_send);

/* If status is NX_SUCCESS the PPP packet send function has set. */


```