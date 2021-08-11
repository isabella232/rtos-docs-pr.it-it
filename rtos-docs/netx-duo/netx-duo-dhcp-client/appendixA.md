---
title: 'Appendice A: Descrizione della funzionalità Stato di ripristino per Azure RTOS client DHCP NetX Duo'
description: Questo capitolo contiene una descrizione della funzionalità Stato ripristino per i Azure RTOS client DHCP NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5b6d01930abdf7dd9d91ebe2e60eaac69ac73d2663a10263f07380e5c2895551
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788457"
---
# <a name="appendix-a--description-of-the-restore-state-feature-for-azure-rtos-netx-duo-dhcp-client-services"></a>Appendice A: Descrizione della funzionalità Ripristina stato per Azure RTOS client DHCP NetX Duo

L'opzione di configurazione Client DHDP netX Duo, NX_DHCP_CLIENT_RESTORE_STATE, consente a un sistema di ripristinare un record client DHCP creato in precedenza in uno stato associato tra un riavvio del sistema e l'altro.

Quando questa opzione è abilitata, l'applicazione può sospendere e riprendere il thread client DHCP. È anche disponibile un servizio per aggiornare il client DHCP con il tempo trascorso tra la sospensione e la ripresa del thread.

## <a name="restoring-the-dhcp-client-between-reboots"></a>Ripristino del client DHCP tra un riavvio e l'altro

Prima di ripristinare un client DHCP dopo il riavvio, a un client DHCP creato in precedenza che deve raggiungere lo stato Associato e a cui viene assegnato un indirizzo IP dal server DHCP. Prima che venga arrestato, l'applicazione DHCP deve quindi salvare il record client DHCP corrente nella memoria non volatile. Deve anche essere presente un 'time keeper' indipendente altrove nel sistema per tenere traccia del tempo trascorso durante questo stato di alimentazione. All'accensione, l'applicazione crea una nuova istanza del client DHCP e quindi la aggiorna con il record client DHCP creato in precedenza. Il tempo trascorso viene ottenuto dal "time keeper" e quindi applicato al tempo rimanente nel lease del client DHCP. Si noti che ciò potrebbe causare la modifica degli stati del client DHCP, ad esempio da BOUND a RENEWING. A questo punto, l'applicazione può riprendere il client DHCP.

Se il tempo trascorso durante l'accensione imposta lo stato del client DHCP in uno stato RENEW o REBIND, il client DHCP avvierà automaticamente i messaggi DHCP che richiedono di rinnovare o riassociare il lease dell'indirizzo IP. Se l'indirizzo IP è scaduto, il client DHCP cancella automaticamente l'indirizzo IP nell'istanza IP e avvia il processo DHCP dallo stato INIT, richiedendo un nuovo indirizzo IP.

In questo modo il client DHCP può operare tra un riavvio e l'altro come ininterrottamente.

Di seguito è riportata un'illustrazione di questa funzionalità. Si presuppone che il client DHCP sia in esecuzione solo nell'interfaccia primaria.

```c
/* On the power up, create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) for the DHCP Client/application
   in tx_application_define().  */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCP_CLIENT_RECORD client_nv_record;


if (/* The application checks if there is a previously saved DHCP Client record. */)
{
    /* No previously saved Client record. Start the DHCP Client in the INIT state.  */
    status =  nx_dhcp_start(&dhcp_0);

    if (status !=NX_SUCCESS)
        return;

    do
    {
        /* Wait for DHCP to assign the IP address.  */
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
        restore it to the current DHCP Client instance.  */

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

Per sospendere un thread client DHCP senza  accensione, l'applicazione chiama nx_dhcp_suspend su un client DHCP che ha raggiunto lo stato BOUND e che ha un indirizzo IP valido. Quando è pronto per riprendere il client DHCP, chiama prima *nx_dhcp_client_update_time_remaining* per aggiornare il tempo rimanente nel lease dell'indirizzo DHCP (ottenendo il tempo trascorso da un controllo del tempo indipendente). Chiama quindi il *nx_dhcp_resume* per riprendere il thread client DHCP.

Se il tempo trascorso imposta lo stato del client DHCP in uno stato RENEW o REBIND, il client DHCP avvierà automaticamente i messaggi DHCP che richiedono di rinnovare o riassociare il lease dell'indirizzo IP. Se l'indirizzo IP è scaduto, il client DHCP cancella automaticamente l'indirizzo IP e avvia il processo DHCP dallo stato INIT, richiedendo un nuovo indirizzo IP.

Di seguito è illustrata l'uso di questa funzionalità.

```c
/* Create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) typically in tx_application_define().  */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

  /* Start the DHCP Client.  */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  while(1)
  {
   /* Wait for DHCP to obtain an IP address.  */
  }

  /* Do tasks with the IP address e.g. send pings to another host on the network...  */
  status =  nx_icmp_ping(…);

  if (status !=NX_SUCCESS)
          printf("Failed %d byte Ping!\n", length);

  /* At some later time, suspend the DHCP Client e.g. the device is going to low 
   power mode (sleep) so we do not want any threads to wake it up. */

  nx_dhcp_suspend(&dhcp_0);  

  /* During this suspended state, an independent timer is keeping track of the elapsed      
     time. */


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

```c
ULONG nx_dhcp_ client_get_record(NX_DHCP *dhcp_ptr, NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio salva il client DHCP in esecuzione nella prima interfaccia abilitata per DHCP trovata nell'istanza del client DHCP nel record a cui punta record_ptr. Ciò consente all'applicazione client DHCP di ripristinare lo stato del client DHCP dopo, ad esempio, un'interruzione e un riavvio.

Per salvare un record client DHCP in un'interfaccia specifica se sono abilitate più interfacce per DHCP, usare il nx_dhcp_interface_client_get_record *dhcp.*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP
- **record_ptr:** puntatore al record client DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS (0x0):** record client creato
- **NX_DHCP_NOT_BOUND**: (0x94) Client non in stati associati
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) Nessuna interfaccia abilitata per DHCP
- NX_PTR_ERROR: (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_DHCP_CLIENT_RECORD dhcp_record;

/* Obtain a record of the current client state. */
status=  nx_dhcp_client_get_record(dhcp_ptr, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_interface_client_get_record"></a>nx_dhcp_interface_client_get_record

Creare un record dello stato corrente del client DHCP nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_interface_client_get_record(NX_DHCP *dhcp_ptr, UINT interface_index,
                                          NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio salva il client DHCP in esecuzione sull'interfaccia specificata nel record a cui punta record_ptr. Ciò consente all'applicazione client DHCP di ripristinare lo stato del client DHCP dopo, ad esempio, un'interruzione e un riavvio.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP
- **interface_index**: indice in base al quale ottenere il record
- **record_ptr:** puntatore al record client DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS (0x0):** record client creato
- **NX_DHCP_NOT_BOUND**: (0x94) **Client non in stato Associato**
- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR:**(0x9A) Indice di interfaccia non valido
- NX_PTR_ERROR: (0x16) Puntatore DHCP non valido.
- NX_INVALID_INTERFACE: (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_DHCP_CLIENT_RECORD dhcp_record;
/* Obtain a record of the current client state on interface 1. */
status=  nx_dhcp_interface_client_get_record(dhcp_ptr, 1, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_-client_restore_record"></a>nx_dhcp_ client_restore_record

Ripristinare il client DHCP da un record salvato in precedenza

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_client_restore_record(NX_DHCP *dhcp_ptr, 
                                    NX_DHCP_CLIENT_RECORD *record_ptr, 
                                    ULONG time_elapsed);

```

### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione di ripristinare il client DHCP da una sessione precedente usando il record client DHCP a cui punta record_ptr. L time_elapsed input viene applicato al tempo rimanente nel lease del client DHCP.

Questa operazione richiede che l'applicazione client DHCP ha creato un record del client DHCP prima dell'accensione e ha salvato il record in memoria non volatile.

Se per il client DHCP sono abilitate più interfacce, questo servizio viene applicato alla prima interfaccia valida trovata nell'istanza del client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP
- **record_ptr:** puntatore al record client DHCP 
- **time_elapsed:** tempo da sottrarre dal tempo di lease rimanente nel record del client di input

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x0) Record client ripristinato
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) Nessuna interfaccia che esegue DHCP
- NX_PTR_ERROR: (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 

/* Obtain a record of the current client state. */
status=  nx_dhcp_client_restore_record(client_ptr, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_interace_client_restore_record"></a>nx_dhcp_interace_client_restore_record

Ripristinare il client DHCP da un record salvato in precedenza nell'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_interface_client_restore_record(NX_DHCP *dhcp_ptr, 
                                              NX_DHCP_CLIENT_RECORD *record_ptr, 
                                              ULONG time_elapsed);
```

### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione di ripristinare il proprio client DHCP sull'interfaccia specificata usando il record client DHCP a cui punta record_ptr. L time_elapsed input viene applicato al tempo rimanente nel lease del client DHCP.

Questa operazione richiede che l'applicazione client DHCP ha creato un record del client DHCP prima dell'accensione e ha salvato il record in memoria non volatile.

Se per il client DHCP sono abilitate più interfacce, questo servizio viene applicato alla prima interfaccia valida trovata nell'istanza del client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP
- **record_ptr:** puntatore al record client DHCP 
- **time_elapsed:** tempo da sottrarre dal tempo di lease rimanente nel record del client di input

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x0) Record client ripristinato
- **NX_DHCP_NOT_BOUND**: (0x94) Client non associato all'indirizzo IP
- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR:**(0x9A) Indice di interfaccia non valido
- NX_PTR_ERROR: (0x16) Puntatore DHCP non valido.
- NX_INVALID_INTERFACE: (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state on the primary interface. */
status=  nx_dhcp_interface_client_restore_record(client_ptr, 0, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_-client_update_time_remaining"></a>nx_dhcp_ client_update_time_remaining

Aggiornare il tempo rimanente per il lease del client DHCP

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_client_update_time_remaining(NX_DHCP *dhcp_ptr, ULONG time_elapsed);
```

### <a name="description"></a>Descrizione

Questo servizio aggiorna il tempo rimanente nel lease dell'indirizzo IP del client DHCP con l'input time_elapsed nella prima interfaccia abilitata per DHCP trovato nell'istanza del client DHCP. L'applicazione deve sospendere il thread client DHCP prima di utilizzare questo servizio *usando nx_dhcp_suspend*. Dopo aver chiamato questo servizio, l'applicazione può riprendere il thread del client DHCP *chiamando nx_dhcp_resume*.

È destinato alle applicazioni client DHCP che devono sospendere il thread client DHCP per un periodo di tempo e quindi aggiornare il tempo di lease dell'indirizzo IP rimanente.

Nota: questo servizio non deve essere usato con le nx_dhcp_client_get_record *e* *nx_dhcp_client_restore_record* descritte in precedenza). Questi servizi sono descritti in precedenza in questa sezione.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP 
- **time_elapsed:** tempo per sottrarre dal tempo rimanente nel lease dell'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x0) Lease IP client aggiornato
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) Nessuna interfaccia abilitata per DHCP
- NX_PTR_ERROR: (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease. */
status=  nx_dhcp_client_update_time_remaining(client_ptr, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```

## <a name="nx_dhcp_interface_client_update_time_remaining"></a>nx_dhcp_interface_client_update_time_remaining

Aggiornare il tempo rimanente sul lease del client DHCP sull'interfaccia specificata

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_interface_client_update_time_remaining(NX_DHCP *dhcp_ptr,
                                                     UINT interface_index,
                                                     ULONG time_elapsed);
```

### <a name="description"></a>Descrizione

Questo servizio aggiorna il tempo rimanente nel lease dell'indirizzo IP del client DHCP con l'input time_elapsed nell'interfaccia specificata se tale interfaccia è abilitata per DHCP. L'applicazione deve sospendere il thread client DHCP prima di utilizzare questo servizio *usando nx_dhcp_suspend*. Dopo aver chiamato questo servizio, l'applicazione può riprendere il thread del client DHCP *chiamando nx_dhcp_resume*. Si noti che la sospensione e la ripresa del thread del client DHCP si applicano a tutte le interfacce abilitate per DHCP.

È destinato alle applicazioni client DHCP che devono sospendere il thread client DHCP per un periodo di tempo e quindi aggiornare il tempo di lease dell'indirizzo IP rimanente.

Nota: questo servizio non deve essere usato con le nx_dhcp_client_get_record *e* *nx_dhcp_client_restore_record* descritte in precedenza). Questi servizi sono descritti in precedenza in questa sezione.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP
- **interface_index:** indice all'interfaccia a cui applicare il tempo trascorso
- **time_elapsed:** tempo per sottrarre dal tempo rimanente nel lease dell'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x0) Lease IP client aggiornato
- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR:**(0x9A) Indice di interfaccia non valido
- NX_PTR_ERROR: (0x16) Puntatore DHCP non valido.
- NX_INVALID_INTERFACE: (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
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

```c
ULONG nx_dhcp_suspend(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio sospende il thread client DHCP corrente. Si noti che *a nx_dhcp_stop*, non vi è alcuna modifica allo stato del client DHCP quando viene chiamato questo servizio.

Questo servizio sospende DHCP in esecuzione in tutte le interfacce abilitate per DHCP.

Per aggiornare lo stato del client DHCP con il tempo trascorso mentre il client DHCP è sospeso, vedere il nx_dhcp_client_update_time_remaining *descritto* in precedenza. Per riprendere un thread del client DHCP sospeso, l'applicazione deve chiamare *nx_dhcp_resume*.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** thread client (0x0) sospeso
- NX_PTR_ERROR: (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Pause the DHCP client thread. */
status=  nx_dhcp_suspend(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is paused. */
```

## <a name="nx_dhcp_resume"></a>nx_dhcp_resume

Riprendere un thread del client DHCP sospeso

### <a name="prototype"></a>Prototipo

```c
ULONG nx_dhcp_resume(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio riprende un thread del client DHCP sospeso. Si noti che non viene apportata alcuna modifica allo stato effettivo del client DHCP dopo la ripresa del thread client. Per aggiornare il tempo rimanente nel lease dell'indirizzo IP del client DHCP con il tempo trascorso prima di chiamare nx_dhcp_resume *,* vedere il nx_dhcp_client_update_time_remaining *descritto* in precedenza.

Questo servizio riprende l'esecuzione di DHCP in tutte le interfacce abilitate per DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** Puntatore al client DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x0) Thread client ripreso
- NX_PTR_ERROR: (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Resume the DHCP client thread. */
status=  nx_dhcp_resume(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is resumed. */
```