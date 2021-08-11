---
title: Capitolo 3 - Descrizione dei Azure RTOS NetX Point-to-Point Protocol (PPP)
description: Questo capitolo contiene una descrizione di tutti Azure RTOS servizi PPP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 980348b5c50acfb82b2d8fda8786a1d48bf59c69e7949b6f62b64515b59bf42d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798759"
---
# <a name="chapter-3---description-of-azure-rtos-netx-point-to-point-protocol-ppp-services"></a>Capitolo 3 - Descrizione dei Azure RTOS NetX Point-to-Point Protocol (PPP)

Questo capitolo contiene una descrizione di tutti Azure RTOS servizi PPP NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_ppp_byte_receive:** *ricevere un byte da ISR seriale*
- **nx_ppp_chap_challenge**: *Generare una richiesta CHAP*
- **nx_ppp_chap_enable:** abilitare *l'autenticazione CHAP*
- **nx_ppp_create**: *Creare un'istanza PPP*
- **nx_ppp_delete**: *Eliminare un'istanza PPP*
- **nx_ppp_dns_address_get:** Ottenere *l'indirizzo IP DNS*
- **nx_ppp_dns_address_set:***Impostare l'indirizzo IP del server DNS*
- **nx_ppp_secondary_dns_address_get:** Ottenere *l'indirizzo IP del server DNS secondario*
- **nx_ppp_secondary_dns_address_set:** impostare *l'Secondary_DNS IP del server*
- **nx_ppp_interface_index_get:** Ottenere *l'indice dell'interfaccia IP*
- **nx_ppp_ip_address_assign**: *Assegnare indirizzi IP per IPCP*
- **nx_ppp_link_down_notify**: *Notificare l'applicazione al collegamento verso il basso*
- **nx_ppp_link_up_notify:** *Inviare una notifica all'applicazione al collegamento*
- **nx_ppp_nak_authentication_notify:** *Inviare una notifica all'applicazione se viene ricevuta la naK di autenticazione*
- **nx_ppp_pap_enable**: Abilitare *l'autenticazione PAP*
- **nx_ppp_ping_request**: *Inviare una richiesta echo LCP*
- **nx_ppp_raw_string_send:** *Inviare una stringa non PPP*
- **nx_ppp_restart**: *Riavviare l'elaborazione PPP*
- **nx_ppp_start**: Avviare *l'elaborazione PPP*
- **nx_ppp_status_get:** *ottenere lo stato PPP corrente*
- **nx_ppp_stop:** *Arrestare l'elaborazione PPP*
- **nx_ppp_packet_receive:** *Ricevere un pacchetto PPP*
- **nx_ppp_packet_send_set:** *Impostare la funzione di invio pacchetti PPP*

## <a name="nx_ppp_byte_receive"></a>nx_ppp_byte_receive

Ricevere un byte da ISR seriale

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_byte_receive(NX_PPP *ppp_ptr, UCHAR byte);
```

### <a name="description"></a>Descrizione

Questo servizio viene in genere chiamato dal driver seriale ISR (Interrupt Service Routine) dell'applicazione per trasferire un byte ricevuto in PPP. Quando viene chiamata, questa routine inserisce il byte ricevuto in un buffer di byte circolare e invia una notifica al thread PPP appropriato per l'elaborazione.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **byte:** byte ricevuto dal dispositivo seriale

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Ricezione di byte PPP completata.
- **NX_PPP_BUFFER_FULL:** il buffer seriale PPP (0xB1) è già pieno.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Thread, ISR

### <a name="example"></a>Esempio

```c
/* Notify “my_ppp” of a received byte. */
status =  nx_ppp_byte_receive(&my_ppp, new_byte);

/* If status is NX_SUCCESS the received byte was successfully
   buffered. */
```

## <a name="nx_ppp_chap_challenge"></a>nx_ppp_chap_challenge

Generare una richiesta CHAP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_chap_challenge(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una richiesta CHAP dopo che la connessione PPP è già in esecuzione. In questo modo l'applicazione può verificare periodicamente l'autenticità della connessione. Se la richiesta di verifica non riesce, il collegamento PPP viene chiuso.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Richiesta PPP riuscita avviata.
- **NX_PPP_FAILURE:**(0xB0) Richiesta PPP non valida, CHAP è stato abilitato solo per la risposta.
- **NX_NOT_IMPLEMENTED:** la logica CHAP (0x80) è stata disabilitata tramite NX_PPP_DISABLE_CHAP.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Questo servizio abilita il Challenge-Handshake Authentication Protocol (CHAP) per l'istanza PPP specificata.

Se vengono specificati **i** puntatori get_challenge_values " e _"_ * _get_verification_values_**", CHAP è richiesto da questa istanza PPP. In caso contrario, CHAP risponde solo alle richieste di richiesta di richiesta del peer.

Di seguito sono riportati diversi elementi di dati nelle funzioni di callback necessarie. Il segreto, *il* *nome* e *il* sistema degli elementi di dati devono essere stringhe con terminazione NULL con una dimensione massima di NX_PPP_NAME_SIZE-1. L'elemento *rand_value* deve essere una stringa con terminazione NULL con una dimensione massima di NX_PPP_VALUE_SIZE-1. *L'ID* elemento dati è un semplice tipo di carattere senza segno.

>[!NOTE]
> Questa funzione deve essere chiamata *dopo* nx_ppp_create ma prima di nx_ip_create o *nx_ip_interface_attach*.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **get_challenge_values:** puntatore alla funzione dell'applicazione per recuperare i valori usati per la richiesta. Si noti che *i rand_value*, *id* e *secret* devono essere copiati nelle destinazioni fornite.
- **get_responder_values:** puntatore alla funzione dell'applicazione che recupera i valori usati per rispondere a una richiesta. Si noti che *i valori di sistema*, *name* e *secret* devono essere copiati nelle destinazioni fornite.
- **get_verification_values:** puntatore alla funzione dell'applicazione che recupera i valori usati per verificare la risposta di richiesta. Si noti che *i valori di sistema*,*name* e *secret* devono essere copiati nelle destinazioni fornite.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Abilitato PPP CHAP riuscito
- **NX_NOT_IMPLEMENTED:** la logica CHAP (0x80) è stata disabilitata tramite NX_PPP_DISABLE_CHAP.
- NX_PTR_ERROR: (0x07) Puntatore PPP o puntatore a funzione di callback non valido. Si noti che *get_challenge_values* specificato, è necessario specificare *anche get_verification_values* funzione.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

Creare un'istanza PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_create(NX_PPP *ppp_ptr, CHAR *name, NX_IP *ip_ptr, 
                    VOID *stack_memory_ptr, ULONG stack_size, 
                    UINT thread_priority, NX_PACKET_POOL *pool_ptr,
                    void (*ppp_invalid_packet_handler)(NX_PACKET *packet_ptr),
                    void (*ppp_byte_send)(UCHAR byte));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza PPP per l'istanza IP NetX specificata.

>[!NOTE]
> È in genere consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread PPP. Fare riferimento al servizio *nx_ip_create* per altre informazioni su come specificare la priorità del thread IP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **name**: nome di questa istanza PPP.
- **ip_ptr:** puntatore al blocco di controllo per l'istanza IP non ancora creata.
- **stack_memory_ptr:** puntatore all'inizio dell'area dello stack del thread PPP.
- **stack_size**: dimensione in byte nello stack del thread.
- **pool_ptr:** puntatore al pool di pacchetti predefinito.
- **thread_priority:** priorità dei thread PPP interni (1-31).
- **ppp_invalid_packet_handler:** puntatore a funzione al gestore dell'applicazione per tutti i pacchetti non PPP. NetX PPP in genere chiama questa routine durante l'inizializzazione. In questo caso l'applicazione può rispondere ai comandi del modem o, nel caso di Windows XP, l'applicazione PPP NetX può avviare PPP rispondendo con " CLIENT SERVER" al "CLIENT" iniziale inviato da Windows XP.
- **ppp_byte_send:** puntatore a funzione alla routine di output in byte seriale dell'applicazione.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione PPP riuscita.
- NX_PTR_ERROR: (0x07) Puntatore a funzione di output PPP, IP o byte non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create “my_ppp” for IP instance “my_ip”. */
status =  nx_ppp_create(&my_ppp, “my PPP”, &my_ip, stack_start, 1024, 2, 
                        &my_pool, my_invalid_packet_handler, my_out_byte);

/* If status is NX_SUCCESS the PPP instance was successfully
   created. */
```

## <a name="nx_ppp_delete"></a>nx_ppp_delete

Eliminare un'istanza PPP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_delete(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina l'istanza PPP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione PPP riuscita.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Questo servizio recupera l'indirizzo IP DNS fornito dal peer. Se il peer non ha fornito alcun indirizzo IP, viene restituito un indirizzo IP pari a 0.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **dns_address_ptr**: Destinazione per l'indirizzo IP DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Ottenere l'indirizzo PPP riuscito.
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP non ha completato la negoziazione con il peer.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

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

Questo servizio recupera l'indirizzo IP DNS secondario fornito dal peer nell'handshake IPCP. Se il peer non ha fornito alcun indirizzo IP, viene restituito un indirizzo IP pari a 0.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **dns_address_ptr:** destinazione per l'indirizzo del server DNS secondario

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Ottenere l'indirizzo DNS corretto.
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP non ha completato la negoziazione con il peer.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

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

Questo servizio imposta l'indirizzo IP del server DNS. Se il peer invia una richiesta di opzione server DNS nello stato IPCP, questo host fornirà le informazioni.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **dns_address:** indirizzo del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Set di indirizzi DNS riuscito.
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP non ha completato la negoziazione con il peer.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

Questo servizio imposta l'indirizzo IP del server DNS secondario. Se il peer invia una richiesta di opzione server DNS secondario nello stato IPCP, questo host fornirà le informazioni.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **dns_address:** indirizzo del server DNS secondario

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Set di indirizzi DNS riuscito. 
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP non ha completato la negoziazione con il peer.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

Questo servizio recupera l'indice dell'interfaccia IP associato a questa istanza PPP. Ciò è utile solo quando l'istanza PPP non è l'interfaccia primaria di un'istanza IP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **index_ptr:** destinazione per l'indice dell'interfaccia

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Ottiene l'indice PPP riuscito.
- **NX_IN_PROGRESS:**(0x37) PPP non ha completato l'inizializzazione.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

### <a name="example"></a>Esempio

```c
ULONG  my_index;

/* Get the interface index for this PPP instance. */
status =  nx_ppp_interface_index_get(&my_ppp, &my_index);

/* If status is NX_SUCCESS the “my_index” contains the IP interface index for
   this PPP instance. */

```
## <a name="nx_ppp_ip_address_assign"></a>nx_ppp_ip_address_assign

Assegnare indirizzi IP per IPCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_ip_address_assign(NX_PPP *ppp_ptr, ULONG local_ip_address, 
            ULONG peer_ip_address);
```

### <a name="description"></a>Descrizione

Questo servizio configura gli indirizzi IP locali e peer da usare nel protocollo IPCP (Internet Protocol Control Protocol). L'applicazione PPP deve richiamare questo servizio in un'istanza PPP con indirizzi IP validi per se stesso e l'altro peer.  Se nessun indirizzo valido viene registrato con un'istanza PPP, deve basarsi sul peer PPP per definirne l'indirizzo IP.


### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **local_ip_address**: indirizzo IP locale.
- **peer_ip_address**: indirizzo IP del peer.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Assegnazione di indirizzi PPP riuscita.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set IP addresses for “my_ppp”. */
status =  nx_ppp_ip_address_assign(&my_ppp, IP_ADDRESS(256,2,2,187), 
IP_ADDRESS(256,2,2,188));


/* If status is NX_SUCCESS the “my_ppp” has the IP addresses. */
```

## <a name="nx_ppp_link_down_notify"></a>nx_ppp_link_down_notify

Notificare l'applicazione al collegamento verso il basso

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_link_down_notify(NX_PPP *ppp_ptr, 
                             VOID (*link_down_callback)(NX_PPP *ppp_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra il callback di notifica del collegamento verso il basso dell'applicazione con l'istanza PPP specificata. Se diverso da NULL, la funzione di callback di collegamento verso il basso dell'applicazione viene chiamata ogni volta che il collegamento viene arrestato.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **link_down_callback:** puntatore a funzione di notifica collegamento verso il basso dell'applicazione. Se NULL, la notifica di collegamento verso il basso è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Registrazione del callback di notifica del collegamento riuscito.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

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

Inviare una notifica all'applicazione al collegamento

### <a name="prototype"></a>Prototipo

```c
UINT nx_ppp_link_up_notify(NX_PPP *ppp_ptr, 
                           VOID (*link_up_callback)(NX_PPP *ppp_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio registra il callback di notifica di collegamento dell'applicazione con l'istanza PPP specificata. Se non NULL, la funzione di callback di collegamento dell'applicazione viene chiamata ogni volta che viene generato il collegamento.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **link_up_callback:** puntatore a funzione di notifica di collegamento dell'applicazione. Se NULL, la notifica di collegamento è disabilitata.**

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Collegamento riuscito della registrazione del callback di notifica.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

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

Notificare all'applicazione se l'autenticazione NAK è stata ricevuta

### <a name="prototype"></a>Prototipo

```c
UINT    nx_ppp_nak_authentication_notify(NX_PPP *ppp_ptr, 
                                         void (*nak_authentication_notify)(void));
```

### <a name="description"></a>Descrizione

Questo servizio registra il callback di notifica nak di autenticazione dell'applicazione con l'istanza PPP specificata. Se non NULL, questa funzione di callback viene chiamata ogni volta che l'istanza PPP riceve una naK durante l'autenticazione.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **nak_authentication_notify:** puntatore alla funzione chiamato quando l'istanza PPP riceve un NAK di autenticazione. Se NULL, la notifica è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Registrazione del callback di notifica completata.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

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

Abilitare l'autenticazione PAP

### <a name="prototype"></a>Prototipo

```c

UINT  nx_ppp_pap_enable(NX_PPP *ppp_ptr, 
                        UINT (*generate_login)(CHAR *name, CHAR *password),
                        UINT (*verify_login)(CHAR *name, CHAR *password));
```

### <a name="description"></a>Descrizione

Questo servizio abilita il Password Authentication Protocol (PAP) per l'istanza PPP specificata. Se il ***puntatore verify_login***" è specificato, PAP è richiesto da questa istanza PPP. In caso contrario, PAP risponde solo ai requisiti PAP del peer come specificato durante la negoziazione LCP.

Di seguito sono riportati diversi elementi di dati nelle funzioni di callback necessarie. Il nome *dell'elemento* dati deve essere una stringa con terminazione NULL con una dimensione massima di NX_PPP_NAME_SIZE-1. Si prevede anche *che la password* dell'elemento dati sia una stringa con terminazione NULL con una dimensione massima di NX_PPP_PASSWORD_SIZE-1.

>[!NOTE]
> Questa funzione deve essere chiamata *dopo* nx_ppp_create ma *prima* di nx_ip_create *o nx_ip_interface_attach*.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **generate_login:** puntatore alla funzione dell'applicazione che produce un *nome* e una *password* per l'autenticazione da parte del peer. Si noti che *i valori* di nome e *password* devono essere copiati nelle destinazioni fornite.
- **verify_login:** puntatore alla funzione dell'applicazione che verifica il *nome* e la *password* forniti dal peer. Questa routine deve confrontare il nome *e* la *password specificati.* Se questa routine restituisce NX_SUCCESS, il nome e la password sono corretti e PPP può procedere al passaggio successivo. In caso contrario, questa routine restituisce NX_PPP_ERROR e PPP attende semplicemente un altro nome e una password.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) PPP PAP abilitato.
- **NX_NOT_IMPLEMENTED:** la logica PAP (0x80) è stata disabilitata tramite NX_PPP_DISABLE_PAP.
- NX_PTR_ERROR: (0x07) Puntatore PPP o puntatore a funzione dell'applicazione non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

Inviare una richiesta ping LCP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_ping_request(NX_PPP *ppp_ptr, CHAR *data, 
                          UINT data_size, ULONG wait_opion);
```

### <a name="description"></a>Descrizione

Questo servizio invia una richiesta ping LCP e imposta un flag che indica che il dispositivo PPP è in attesa di una risposta echo. Il servizio viene restituito non appena viene inviata la richiesta. Non attende una risposta. 

Quando viene ricevuta una risposta echo corrispondente, l'attività thread PPP cancella il flag. Il dispositivo PPP deve aver completato la parte LCP della negoziazione PPP.

Questo servizio è utile per le configurazioni PPP in cui il polling dell'hardware per lo stato del collegamento potrebbe non essere immediatamente possibile.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **data:** puntatore ai dati da inviare nella richiesta echo.
- **data_size**: dimensioni dei dati da inviare wait_option tempo di attesa per l'invio del messaggio echo LCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Richiesta echo inviata correttamente.
- **NX_PPP_NOT_ESTABLISHED:** connessione PPP (0xB5) non stabilita.
- NX_PTR_ERROR: (0x07) Puntatore PPP o puntatore a funzione dell'applicazione non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread dell'applicazione

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

Inviare una stringa ASCII non elaborata

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_raw_sting_send(NX_PPP *ppp_ptr, CHAR *string_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una stringa ASCII non PPP direttamente all'interfaccia PPP. Viene in genere usato dopo che PPP riceve un pacchetto non PPP che contiene informazioni di controllo del modem.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **string_ptr:** puntatore alla stringa da inviare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Invio di stringa non elaborata PPP riuscito.
- NX_PTR_ERROR: (0x07) Puntatore PPP o puntatore di stringa non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Riavviare l'elaborazione PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_restart(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio riavvia l'elaborazione PPP. Viene in genere chiamato quando il collegamento deve essere nuovamente stabilito da un callback di collegamento verso il basso o da un messaggio modem non PPP che indica che la comunicazione è stata persa.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Riavvio PPP riuscito avviato.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Questo servizio avvia l'elaborazione PPP. Viene in genere chiamato dopo nx_ppp_stop() chiamato.

>[!NOTE]
> PPP avvia automaticamente l'elaborazione PPP quando il collegamento è abilitato.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Avvio PPP riuscito avviato. 
- **NX_PPP_ALREADY_STARTED**: (0xb9) PPP già avviato.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the PPP instance “my_ppp”.  */
status =  nx_ppp_start(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been started. */
```

## <a name="nx_ppp_status_get"></a>nx_ppp_status_get

Ottenere lo stato PPP corrente

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_status_get(NX_PPP *ppp_ptr, UINT *status_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio ottiene lo stato corrente dell'istanza PPP specificata.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **status_ptr**: destinazione per lo stato PPP, i valori di stato possibili sono i seguenti:
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
> Lo stato è valido solo se l'API restituisce NX_SUCCESS. Inoltre, se viene restituito uno dei valori *_FAILED stato, l'elaborazione PPP viene arrestata fino a quando non viene riavviata nuovamente dall'applicazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Richiesta di stato PPP riuscita.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

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

Questo servizio arresta l'elaborazione PPP. L'utente può anche chiamare nx_ppp_start() per avviare l'elaborazione PPP, se necessario.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Avvio PPP riuscito avviato. 
- **NX_PPP_ALREADY_STOPPED:**(0xb8) PPP già arrestato.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the PPP instance “my_ppp”.  */
status =  nx_ppp_stop(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been stopped. */
```
## <a name="nx_ppp_packet_receive"></a>nx_ppp_packet_receive

Ricevere un pacchetto PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_packet_receive(NX_PPP *ppp_ptr, NX_PACKET *packet_ptr);

```

### <a name="description"></a>Descrizione

Questo servizio riceve il pacchetto PPP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **packet_ptr:** puntatore al pacchetto PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Richiesta di stato PPP riuscita.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Receive the PPP packet of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_receive(&my_ppp, packet_ptr);

/* If status is NX_SUCCESS the PPP packet has received. */


```
## <a name="nx_ppp_packet_send_set"></a>nx_ppp_packet_send_set

Impostare la funzione di invio di pacchetti PPP

### <a name="prototype"></a>Prototipo

```c
UINT  nx_ppp_packet_send_set(NX_PPP *ppp_ptr, 
                             VOID (*nx_ppp_packet_send)(NX_PACKET *packet_ptr));

```

### <a name="description"></a>Descrizione

Questo servizio imposta il funciton di invio di pacchetti PPP.

### <a name="input-parameters"></a>Parametri di input

- **ppp_ptr:** puntatore al blocco di controllo PPP.
- **nx_ppp_packet_send:** routine per inviare un pacchetto PPP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Richiesta di stato PPP riuscita.
- NX_PTR_ERROR: (0x07) Puntatore PPP non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the PPP packet send function of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_send_set(&my_ppp, nx_ppp_packet_send);

/* If status is NX_SUCCESS the PPP packet send function has set. */


```