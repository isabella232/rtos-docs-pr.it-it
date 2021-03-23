---
title: Appendice A-Descrizione della funzionalità di ripristino dello stato per il client DHCPv6 RTO NetX duo di Azure
description: L'NX_DHCPV6_CLIENT_RESTORE_STATE opzione di configurazione client Azure RTO NetX Duo DHDPv6 consente a un sistema di ripristinare un client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3e642af158202bb3b2a4e2a37397b47d707b566e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822004"
---
# <a name="appendix-a---description-of-the-restore-state-feature-for-azure-rtos-netx-duo-dhcpv6-client"></a>Appendice A-Descrizione della funzionalità di ripristino dello stato per il client DHCPv6 RTO NetX duo di Azure

L'NX_DHCPV6_CLIENT_RESTORE_STATE opzione di configurazione client Azure RTO NetX Duo DHDPv6 consente a un sistema di ripristinare un client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.

Questa opzione consente anche a un'applicazione di sospendere il thread del client DHCPv6 e di riprenderlo, aggiornato con il tempo trascorso tra la sospensione e la ripresa del thread senza spegnimento.

## <a name="restoring-the-dhcpv6-client-between-reboots"></a>Ripristino del client DHCPv6 tra i riavvii

Per ripristinare un client DHCPv6 tra i riavvii, l'applicazione DHCPv6 crea un'istanza del client DHCPv6, quindi ottiene un lease di indirizzi IP utilizzando il protocollo DHCPv6 normale e chiamando *nx_dhcpv6_start*. L'applicazione DHCPv6 attende quindi il completamento del protocollo. Se tutto va bene, il dispositivo raggiunge lo stato associato con un indirizzo IP valido assegnato dal server DHCPv6. Prima che venga disattivato, l'applicazione client DHCPv6 Salva l'istanza corrente del client DHCPv6 in un record client DHCPv6 che viene quindi archiviato nella memoria non volatile. Un "Time Keeper" indipendente in un'altra parte del sistema tiene traccia del tempo trascorso durante questo stato spento. Durante l'accensione, l'applicazione crea una nuova istanza del client DHCPv6 e la aggiorna con il record client DHCPv6 creato in precedenza. Il tempo trascorso viene ottenuto dal "Time Keeper" e quindi applicato al tempo rimanente nel lease Clientv6 DHCP. A questo punto, l'applicazione può riprendere il client DHCPv6.

Se il tempo trascorso durante il spegnimento imposta lo stato del client DHCPv6 in stato di rinnovo o riassociazione, il client DHCPv6 avvierà automaticamente i messaggi DHCPv6 che richiedono di rinnovare o riassociare il lease dell'indirizzo IP. Se l'indirizzo IP è scaduto, il client DHCPv6 cancellerà automaticamente l'indirizzo IP nell'istanza IP e avvierà il processo DHCPv6 dallo stato INIT, richiedendo un nuovo indirizzo IP.

In questo modo il client DHCPv6 può operare tra i riavvii come se non fosse interrotto.

Di seguito è riportata un'illustrazione di questa funzionalità.

```C
/* On the power up, create an IP instance, DHCPv6 Client, enable ICMPv6 and UDP
   and other resources (not shown) for the DHCPv6 Client/application
   in tx_application_define(). */
 
/* Define the DHCPv6 Client application thread. */     
void    thread_dhcpv6_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCPV6_CLIENT_RECORD client_my_record;


    /* No previously saved Client record. Start the DHCPv6 Client in the INIT state. */
    status =  nx_dhcpv6_start(&dhcp_0);

    if (status !=NX_SUCCESS)
        return;

    while(1)    
    {
    
        /* Wait for DHCPv6 Client to get the IP address. */
    }

    /* At some point decide we power down the system. */

    /* Save the Client state data which we will subsequently need to restore the DHCPv6    
       Client. */
    status = nx_dhcpv6_client_get_record(&dhcp_0, &client_my_record);               

    /* Copy this memory to non-volatile memory (not shown). */

    /* Delete the IP and DHCPv6 Client instances before powering down. */
    nx_dhcpv6_client_delete(&dhcp_0);

    nx_ip_delete(&ip_0);

    /* Ready to power down, having released other resources as necessary. */

    /* The application has determined there is a previously saved record. We will 
       restore it to the current DHCPv6 Client instance. */

/* Create the IP and DHCPv6 Client instances, enable ICMPv6 and UDP after powering up. */

/* Calculate the time elapsed during power down */

    /* Get the previous Client state data from non-volatile memory. */

    /* Apply the record to the current Client instance. This will also 
       update the IP instance with IP address, mask etc. */
    status = nx_dhcpv6_client_restore_record(&dhcp_0, &client_my_record, time_elapsed);   

     if (status != NX_SUCCESS)
          return;

     /* We are ready to resume the DHCPv6 Client thread and use the assigned IP address. */
     status = nx_dhcpv6_resume(&dhcp_0);

     if (status != NX_SUCCESS)
          return;

}
```

## <a name="nx_dhcpv6_client_get_record"></a>nx_dhcpv6_client_get_record

Creare un record dello stato corrente del client DHCPv6

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcpv6_client_get_record(NX_DHCPV6 *dhcpv6_ptr, 
                                  NX_DHCPV6_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio salva il client DHCPv6 nel record a cui fa riferimento record_ptr. Ciò consente all'applicazione client DHCPv6 di ripristinare lo stato del client DHCPv6 dopo, ad esempio, un spegnimento e un riavvio.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore al client DHCPv6

- **record_ptr** Puntatore al record client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS (0x0)** Record client valido creato

- Il client **NX_DHCPV6_NOT_BOUND** (0xE94) non è in stato associato e pertanto non è stato assegnato un indirizzo IP valido

- **NX_PTR_ERROR** (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;


/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_get_record(&dhcpv6_ptr, &dhcpv6_record);

/* If status is NX_SUCCESS dhcpv6_record contains the current DHCPv6 client record. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_resume
- nx_dhcpv6_suspend
- nx_dhcpv6_client_restore_record

## <a name="nx_dhcpv6_client_restore_record"></a>nx_dhcpv6_client_restore_record

Ripristinare lo stato del client DHCPv6 dal record salvato

### <a name="prototype"></a>Prototipo

```C
ULONG nx_dhcpv6_client_restore_record(NX_DHCPV6 *dhcpv6_ptr, 
                                      NX_DHCPV6_CLIENT_RECORD       
                                      *record_ptr, ULONG time_elapsed);
```

### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione DHCPv6 di ricreare lo stato client DHCPv6 da una sessione precedente aggiornando il client DHCPv6 con il record client DHCPv6 a cui punta record_ptr e aggiorna il tempo rimanente per il lease del client DHCPv6 con l'input di time_elapsed. Ciò consente all'applicazione client DHCPv6 di ricreare il client DHCPv6, ad esempio dopo l'accensione. A tale scopo, è necessario che l'applicazione client DHCPv6 abbia creato un record del client DHCPv6 prima dell'accensione e abbia salvato tale record nella memoria non volatile.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore al client DHCPv6

- **record_ptr** Puntatore al record client DHCPv6

- **time_elapsed** Tempo di sottrazione dal tempo di lease rimanente nel record client di input

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS (0x0)** Record client ripristinato

- NX_PTR_ERROR (0x16) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 

/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_restore_record(&dhcpv6_ptr, &dhcpv6_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCPv6 Client pointed to by dhcpv6_ptr contains the current client record updated for time elapsed during power down. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_client_get_record