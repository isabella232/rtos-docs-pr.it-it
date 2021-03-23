---
title: Appendice A-Descrizione della funzionalità di stato di ripristino
description: L'NX_DHCP_CLIENT_RESTORE_STATE opzione di configurazione del client Azure RTO NetX DHDP consente a un sistema di ripristinare un record client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be8b5dc4885951bee3dba38af6fe5e21b81aa767
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822712"
---
# <a name="appendix-a---description-of-the-restore-state-feature"></a>Appendice A-Descrizione della funzionalità di stato di ripristino

L'NX_DHCP_CLIENT_RESTORE_STATE opzione di configurazione del client Azure RTO NetX DHDP consente a un sistema di ripristinare un record client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.

Quando questa opzione è abilitata, l'applicazione può sospendere e riprendere il thread del client DHCP. È inoltre disponibile un servizio per aggiornare il client DHCP con il tempo trascorso tra la sospensione e la ripresa del thread.

## <a name="restoring-the-dhcp-client-between-reboots"></a>Ripristino del client DHCP tra i riavvii

Prima di ripristinare un client DHCP dopo il riavvio, un client DHCP creato in precedenza che deve raggiungere lo stato associato e a cui viene assegnato un indirizzo IP dal server DHCP. Prima che venga disattivato, l'applicazione DHCP deve quindi salvare il record client DHCP corrente nella memoria non volatile. Per tenere traccia del tempo trascorso durante questo stato di spegnimento, è inoltre necessario che sia presente un "Time Keeper" indipendente. Durante l'accensione, l'applicazione crea una nuova istanza del client DHCP, quindi la aggiorna con il record client DHCP creato in precedenza. Il tempo trascorso viene ottenuto dal "Time Keeper" e quindi applicato al tempo rimanente per il lease del client DHCP. Si noti che questo può causare la modifica degli Stati da parte del client DHCP, ad esempio dal limite al rinnovo. A questo punto, l'applicazione può riprendere il client DHCP.

Se il tempo trascorso durante il spegnimento imposta lo stato del client DHCP in uno stato di rinnovo o riassociazione, il client DHCP avvierà automaticamente i messaggi DHCP che richiedono il rinnovo o il riassociazione del lease di indirizzi IP. Se l'indirizzo IP è scaduto, il client DHCP cancellerà automaticamente l'indirizzo IP nell'istanza IP e avvierà il processo DHCP dallo stato INIT, richiedendo un nuovo indirizzo IP.

In questo modo il client DHCP può operare tra i riavvii come se non fosse interrotto.

Di seguito è riportata un'illustrazione di questa funzionalità. Si presuppone che il client DHCP sia in esecuzione solo sull'interfaccia primaria.

```C
/* On the power up, create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) for the DHCP Client/application
   in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCP_CLIENT_RECORD client_nv_record;


if (/* The application checks if there is a previously saved DHCP Client record. */)
{


  /* No previously saved Client record. Start the DHCP Client in the INIT state. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  do
  {
  
    /* Wait for DHCP to assign the IP address. */
  } while (status != NX_SUCCESS);

  /* We have a valid IP address. */

  /* At some point decide we power down the system. */

  /* Save the Client state data which we will subsequently need to restore the DHCP  
     Client. */
  status = nx_dhcp_client_get_record(&dhcp_0, &client_nv_record);         

  /* Copy this memory to non-volatile memory (not shown). */

  /* Delete the IP and DHCP Client instances before powering down. */
  nx_dhcp_delete(&dhcp_0);

  nx_ip_delete(&ip_0);

  /* Ready to power down, having released other resources as necessary. */

}
else
{

  /* The application has determined there is a previously saved record. We will 
     restore it to the current DHCP Client instance. */

  /* Get the previous Client state data from non-volatile memory. */

  /* Apply the record to the current Client instance. This will also 
     update the IP instance with IP address, mask etc. */
  status = nx_dhcp_client_restore_record(&dhcp_0, &client_nv_record, time_elapsed);   

     if (status != NX_SUCCESS)
      return;

     /* We are ready to resume the DHCP Client thread and use the assigned IP address. */
     status = nx_dhcp_resume(&dhcp_0);

     if (status != NX_SUCCESS)
      return;

}
```

## <a name="resuming-the-dhcp-client-thread-after-suspension"></a>Ripresa del thread client DHCP dopo la sospensione 

Per sospendere un thread client DHCP senza spegnere, l'applicazione chiama *nx_dhcp_suspend* su un client DHCP che ha raggiunto lo stato associato e che ha un indirizzo IP valido. Quando è pronto per riprendere il client DHCP, chiama prima di tutto *nx_dhcp_client_update_time_remaining* per aggiornare il tempo rimanente nel lease di indirizzi DHCP (ottenendo il tempo trascorso da un custode del tempo indipendente). Chiama quindi il *nx_dhcp_resume* per riprendere il thread del client DHCP.

Se il tempo trascorso imposta lo stato del client DHCP in uno stato di rinnovo o riassociazione, il client DHCP avvierà automaticamente i messaggi DHCP che richiedono il rinnovo o il riassociazione del lease di indirizzi IP. Se l'indirizzo IP è scaduto, il client DHCP cancellerà automaticamente l'indirizzo IP e inizierà il processo DHCP dallo stato INIT, richiedendo un nuovo indirizzo IP.

Di seguito viene illustrato l'uso di questa funzionalità.

```C
/* Create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) typically in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

  /* Start the DHCP Client. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  while(1)
  {
   
    /* Wait for DHCP to obtain an IP address. */
  }

  /* Do tasks with the IP address e.g. send pings to another host on the 
     network... */
  status =  nx_icmp_ping(…);

  if (status !=NX_SUCCESS)
          printf("Failed %d byte Ping!\n", length);

  /* At some later time, suspend the DHCP Client e.g. the device is going to low 
   power mode (sleep) so we do not want any threads to wake it up. */

  nx_dhcp_suspend(&dhcp_0);  

  /* During this suspended state, an independent timer is keeping track of the
     elapsed time. */


  /* At some point, we are ready to resume the DHCP Client thread. */

  /* Update the DHCP Client lease time remaining with the time elapsed. */
  status = nx_dhcp_client_update_time_remaining(&dhcp_0, time_elapsed);   

  if (status != NX_SUCCESS)
       return;

  /* We now can resume the DHCP Client thread. */
  status = nx_dhcp_resume(&dhcp_0);

  if (status != NX_SUCCESS)
       return;

  /* Resume tasks e.g. ping another host. */
  status =  nx_icmp_ping(…);

}
```

Di seguito è riportato un elenco di servizi per il ripristino dello stato di un client DHCP dalla memoria e per la sospensione e la ripresa del client DHCP.

## <a name="nx_dhcp_client_get_record"></a>nx_dhcp_client_get_record

Creare un record dello stato corrente del client DHCP

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_ client_get_record(NX_DHCP *dhcp_ptr, 
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio salva il client DHCP in esecuzione nella prima interfaccia abilitata per DHCP trovato nell'istanza del client DHCP al record a cui fa riferimento record_ptr. Ciò consente all'applicazione client DHCP di ripristinare lo stato del client DHCP dopo, ad esempio, un spegnimento e un riavvio.

Per salvare un record client DHCP in un'interfaccia specifica se è abilitata più di un'interfaccia per DHCP, usare il servizio *nx_dhcp_interface_client_get_record* .

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

- **record_ptr** Puntatore al record client DHCP

### <a name="return-values"></a>Valori restituiti

- Record client di **NX_SUCCESS** (0x0) creato

- Client di **NX_DHCP_NOT_BOUND** (0x94) non in stato associato

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) non sono abilitate interfacce per DHCP

- **NX_PTR_ERROR** (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_get_record(dhcp_ptr, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_interface_client_get_record"></a>nx_dhcp_interface_client_get_record

Crea un record dello stato del client DHCP corrente sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_interface_client_get_record(NX_DHCP *dhcp_ptr, 
                                 UINT interface_index,
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio salva il client DHCP in esecuzione nell'interfaccia specificata nel record a cui punta record_ptr. Ciò consente all'applicazione client DHCP di ripristinare lo stato del client DHCP dopo, ad esempio, un spegnimento e un riavvio.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

- **interface_index** Indice in corrispondenza del quale ottenere il record

- **record_ptr** Puntatore al record client DHCP

### <a name="return-values"></a>Valori restituiti

- Record client di **NX_SUCCESS** (0x0) creato

- Client di **NX_DHCP_NOT_BOUND** (0x94) non in stato associato

- Indice di interfaccia **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0X9A) non valido

- NX_PTR_ERROR (0x16) puntatore DHCP non valido.

- L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state on interface 1. */
status=  nx_dhcp_interface_client_get_record(dhcp_ptr, 1, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_-client_restore_record"></a>nx_dhcp_ client_restore_record

Ripristinare il client DHCP da un record salvato in precedenza

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_client_restore_record(NX_DHCP *dhcp_ptr, 
                                    NX_DHCP_CLIENT_RECORD       
                                    *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione di ripristinare il client DHCP da una sessione precedente utilizzando il record client DHCP a cui punta record_ptr. L'input time_elapsed viene applicato al tempo rimanente per il lease del client DHCP.

A tale scopo, è necessario che l'applicazione client DHCP abbia creato un record del client DHCP prima dell'accensione e abbia salvato tale record nella memoria non volatile.

Se è abilitata più di un'interfaccia per il client DHCP, questo servizio viene applicato alla prima interfaccia valida presente nell'istanza del client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

- **record_ptr** Puntatore al record client DHCP

- **time_elapsed** Tempo di sottrazione dal tempo di lease rimanente nel record client di input

### <a name="return-values"></a>Valori restituiti

- Record client di **NX_SUCCESS** (0x0) ripristinato

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) nessuna interfaccia che esegue DHCP

- **NX_PTR_ERROR** (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_restore_record(client_ptr, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_interace_client_restore_record"></a>nx_dhcp_interace_client_restore_record

Ripristina il client DHCP da un record salvato in precedenza nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_interface_client_restore_record(NX_DHCP *dhcp_ptr, 
                                              NX_DHCP_CLIENT_RECORD       
                                              *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione di ripristinare il client DHCP sull'interfaccia specificata utilizzando il record client DHCP a cui punta record_ptr. L'input time_elapsed viene applicato al tempo rimanente per il lease del client DHCP.

A tale scopo, è necessario che l'applicazione client DHCP abbia creato un record del client DHCP prima dell'accensione e abbia salvato tale record nella memoria non volatile.

Se è abilitata più di un'interfaccia per il client DHCP, questo servizio viene applicato alla prima interfaccia valida presente nell'istanza del client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

- **record_ptr** Puntatore al record client DHCP

- **time_elapsed** Tempo di sottrazione dal tempo di lease rimanente nel record client di input

### <a name="return-values"></a>Valori restituiti

- Record client di **NX_SUCCESS** (0x0) ripristinato

- Client di **NX_DHCP_NOT_BOUND** (0x94) non associato all'indirizzo IP

- Indice di interfaccia **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0X9A) non valido

- NX_PTR_ERROR (0x16) puntatore DHCP non valido.

- L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state on the primary interface. */
status=  nx_dhcp_interface_client_restore_record(client_ptr, 0, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_-client_update_time_remaining"></a>nx_dhcp_ client_update_time_remaining

Aggiornare il tempo rimanente per il lease del client DHCP

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_client_update_time_remaining(NX_DHCP *dhcp_ptr
                                           ULONG time_elapsed);
```
### <a name="description"></a>Descrizione

Questo servizio aggiorna il tempo rimanente per il lease dell'indirizzo IP del client DHCP con l'input time_elapsed sulla prima interfaccia abilitata per DHCP trovato nell'istanza del client DHCP. L'applicazione deve sospendere il thread del client DHCP prima di utilizzare il servizio utilizzando *nx_dhcp_suspend*. Dopo la chiamata a questo servizio, l'applicazione può riprendere il thread del client DHCP chiamando *nx_dhcp_resume*.

Questa operazione è destinata alle applicazioni client DHCP che devono sospendere il thread del client DHCP per un determinato periodo di tempo, quindi aggiornare il tempo di lease degli indirizzi IP rimanente.

> [!NOTE]
> Questo servizio non deve essere utilizzato con *nx_dhcp_client_get_record* e *nx_dhcp_client_restore_record* descritto in precedenza). Questi servizi sono descritti in precedenza in questa sezione.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

- **time_elapsed** Tempo per la sottrazione dal tempo rimanente per il lease dell'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- Lease IP client **NX_SUCCESS** (0x0) aggiornato

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) non sono abilitate interfacce per DHCP

- **NX_PTR_ERROR** (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease. */
status=  nx_dhcp_client_update_time_remaining(client_ptr, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```


## <a name="nx_dhcp_interface_client_update_time_remaining"></a>nx_dhcp_interface_client_update_time_remaining

Aggiornare il tempo rimanente per il lease del client DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_interface_client_update_time_remaining(NX_DHCP *dhcp_ptr,
                                                     UINT interface_index,
                                                     ULONG time_elapsed);
```
### <a name="description"></a>Descrizione

Questo servizio aggiorna l'ora rimanente del lease di indirizzi IP del client DHCP con l'input time_elapsed sull'interfaccia specificata se tale interfaccia è abilitata per DHCP. L'applicazione deve sospendere il thread del client DHCP prima di utilizzare il servizio utilizzando *nx_dhcp_suspend*. Dopo la chiamata a questo servizio, l'applicazione può riprendere il thread del client DHCP chiamando *nx_dhcp_resume*. Nota sospendere e riprendere il thread del client DHCP si applica a tutte le interfacce abilitate per DHCP.

Questa operazione è destinata alle applicazioni client DHCP che devono sospendere il thread del client DHCP per un determinato periodo di tempo, quindi aggiornare il tempo di lease degli indirizzi IP rimanente.

> [!NOTE] 
> Questo servizio non deve essere utilizzato con *nx_dhcp_client_get_record* e *nx_dhcp_client_restore_record* descritto in precedenza). Questi servizi sono descritti in precedenza in questa sezione.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

- **interface_index** Indice dell'interfaccia per cui applicare il tempo trascorso

- **time_elapsed** Tempo per la sottrazione dal tempo rimanente per il lease dell'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- Lease IP client **NX_SUCCESS** (0x0) aggiornato

- Indice di interfaccia **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0X9A) non valido

- NX_PTR_ERROR (0x16) puntatore DHCP non valido.

- L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease on interface 1. */
status=  nx_dhcp_interface_client_update_time_remaining(client_ptr, 1, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```


## <a name="nx_dhcp_suspend"></a>nx_dhcp_suspend

Sospendere il thread del client DHCP

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_suspend(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio sospende il thread del client DHCP corrente. Si noti che, a differenza di *nx_dhcp_stop*, non viene apportata alcuna modifica allo stato del client DHCP quando viene chiamato questo servizio.

Questo servizio sospende DHCP in esecuzione su tutte le interfacce abilitate per DHCP.

Per aggiornare lo stato del client DHCP con il tempo trascorso mentre il client DHCP è sospeso, vedere la *nx_dhcp_client_update_time_remaining* descritta in precedenza. Per riprendere un thread client DHCP sospeso, l'applicazione deve chiamare *nx_dhcp_resume*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

### <a name="return-values"></a>Valori restituiti

- Thread client di **NX_SUCCESS** (0x0) sospeso

- **NX_PTR_ERROR** (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Pause the DHCP client thread. */
status=  nx_dhcp_suspend(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is paused. */
```


## <a name="nx_dhcp_resume"></a>nx_dhcp_resume

Riprendere un thread client DHCP sospeso

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcp_resume(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio riprende un thread client DHCP sospeso. Si noti che non viene apportata alcuna modifica allo stato del client DHCP effettivo dopo la ripresa del thread del client. Per aggiornare il tempo rimanente per il lease dell'indirizzo IP del client DHCP con il tempo trascorso prima di chiamare *nx_dhcp_resume*, vedere la *nx_dhcp_client_update_time_remaining* descritta in precedenza.

Questo servizio riprende DHCP in esecuzione su tutte le interfacce abilitate per DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al client DHCP

### <a name="return-values"></a>Valori restituiti

- Il thread client di **NX_SUCCESS** (0x0) viene ripreso

- NX_PTR_ERROR (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Resume the DHCP client thread. */
status=  nx_dhcp_resume(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is resumed. */
```