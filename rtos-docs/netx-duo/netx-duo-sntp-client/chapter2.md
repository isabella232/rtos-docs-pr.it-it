---
title: Capitolo 2 - Installazione e uso di Azure RTOS client NetX Duo SNTP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del client NetX Duo SNTP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2058875c08d64e2c16f67b48323814ec77ec96882eec26aaf2c9454459511db3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799048"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-sntp-client"></a>Capitolo 2 - Installazione e uso di Azure RTOS client NetX Duo SNTP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del Azure RTOS NetX Duo SNTP.

## <a name="product-distribution"></a>Distribuzione del prodotto

SNTP per NetX Duo è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_sntp_client.c** File di origine C del client SNTP  
- **nxd_sntp_client.h** File di intestazione del client SNTP  
- **demo_netxduo_sntp_client.c** Applicazione client SNTP dimostrativa  
- **nxd_sntp_client.pdf** Manuale dell'utente del client NetX Duo SNTP  

## <a name="netx-duo-sntp-client-installation"></a>Installazione del client NetX Duo SNTP

Per usare SNTP per NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*\threadx\arm7\green*", i file del client SNTP di NetX Duo *nxd_sntp_client.c* e *nxd_sntp_client.h* (*nx_sntp_client.c* e *nx_sntp_client.h* in NetX) devono essere copiati in questa directory.

## <a name="using-netx-duo-sntp-client"></a>Uso del client NetX Duo SNTP

L'uso del client NetX Duo SNTP è semplice. Fondamentalmente, il codice dell'applicazione deve includere *nxd_sntp_client.h* dopo aver incluso *rispettivamente tx_api.h, fx_api.h* e *nx_api.h,* per poter usare rispettivamente ThreadX e NetX Duo. Dopo *nxd_sntp_client.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione SNTP specificate più avanti in questa guida. L'applicazione deve anche *includere nxd_sntp_client.c* nel processo di compilazione. Questi file devono essere compilati nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato ai file dell'applicazione. Questo è tutto ciò che è necessario per usare il client NetX Duo SNTP.

> [!NOTE]
> Poiché il client NetX Duo SNTP usa i servizi UDP di NetX Duo, UDP deve essere abilitato con la chiamata *nx_udp_enable* prima di usare i servizi SNTP.

## <a name="small-example-system"></a>Small Example System

Di seguito è riportato un esempio di come usare NetX Duo SNTP. Si noti che non **è garantito** che questo esempio funzioni come nel sistema. Potrebbe essere necessario apportare modifiche per il sistema e l'hardware specifici. Ad esempio, sarà necessario sostituire il driver ram NetX con la funzione effettiva del driver. Questo esempio è destinato esclusivamente a scopo dimostrativo.

In questo esempio è incluso il file di intestazione *SNTP nxd_sntp_client.h.* Il client SNTP viene creato in "*tx_application_define*". Si noti che le funzioni di gestione della morte e del secondo intercalare sono facoltative quando si crea il client SNTP.

Questa demo può essere usata con IPv6 o IPv4. Per eseguire il client SNTP su IPv6, definire USE_IPV6. IPv6 deve essere abilitato anche in NetX Duo. L'host del client SNTP è configurato per la convalida degli indirizzi IPv6 e per i servizi ICMPv6 e IPv6 in NetX Duo. Per altri dettagli sul supporto IPv6 in NetX Duo, vedere il Manuale dell'utente di NetX Duo.

Il client SNTP deve quindi essere inizializzato per la modalità unicast o broadcast.

Il client SNTP scrive inizialmente gli aggiornamenti dell'ora del server nella propria struttura di dati interna. Non corrisponde all'ora locale del dispositivo. L'ora locale del dispositivo può essere impostata come ora di base nel client SNTP prima di avviare il thread del client SNTP. Ciò è utile se il client SNTP è configurato (NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP impostato su NX_FALSE) per confrontare il primo aggiornamento del server con il NX_SNTP_CLIENT_MAX_ADJUSTMENT (valore predefinito di 180 millisecondi). In caso contrario, il client SNTP imposta direttamente l'ora locale iniziale quando ottiene il primo aggiornamento dal server.

Un tempo di base viene applicato al client SNTP usando *il nx_sntp_client_set_local_time* servizio.

Il client SNTP viene avviato rispettivamente per la modalità unicast e broadcast. Per un determinato intervallo (leggermente inferiore all'intervallo di polling unicast), l'applicazione aggiorna l'ora locale del client SNTP, usando *il nx_sntp_client_set_local_time*, dall'"orologio in tempo reale" simulato semplicemente incrementando i secondi e i millisecondi dell'ora corrente. Dopo ogni intervallo, l'applicazione verifica periodicamente la disponibilità di aggiornamenti dal server SNTP. Il *nx_sntp_client_receiving _updates* verifica che il client SNTP riceva attualmente aggiornamenti validi. In tal caso, recupererà l'ora dell'aggiornamento più recente *usando il nx_sntp_client_get_local_time_extended* servizio.

Il client SNTP può essere arrestato in qualsiasi momento usando il servizio *nx_sntp_client_stop se,* ad esempio, rileva che il client SNTP non riceve più aggiornamenti validi. Per riavviare il client, l'applicazione deve chiamare il servizio di inizializzazione unicast o broadcast e quindi chiamare i servizi di esecuzione unicast o broadcast. Mentre l'attività del thread del client SNTP viene arrestata, il client SNTP può cambiare server e modalità SNTP (unicast o broadcast), se necessario, ad esempio il server SNTP precedente sembra essere in stato insoddiente.

```c
/* 
   This is a small demo of the NetX SNTP Client on the high-performance NetX
   TCP/IP stack. This demo relies on Thread, NetX and NetX SNTP Client API to
   execute the Simple Network Time Protocol in unicast and broadcast modes.  
 */

#include <stdio.h>
#include "nx_api.h"
#include "nx_ip.h"
#include "nxd_sntp_client.h"
                
/* Define SNTP packet size. */
#define NX_SNTP_CLIENT_PACKET_SIZE      (NX_UDP_PACKET + 100)

/* Define SNTP packet pool size. */
#define NX_SNTP_CLIENT_PACKET_POOL_SIZE      (4 * (NX_SNTP_CLIENT_PACKET_SIZE + 
                                                            sizeof(NX_PACKET)))

/* Define how often the demo checks for SNTP updates. */
#define DEMO_PERIODIC_CHECK_INTERVAL      (1 * NX_IP_PERIODIC_RATE) 

/* Define how often we check on SNTP server status. 
   We expect updates from the SNTP server about every hour using 
   the SNTP Client defaults. For testing
   make this (much) shorter. */
#define CHECK_SNTP_UPDATES_TIMEOUT       (180 * NX_IP_PERIODIC_RATE) 

/* Set up generic network driver for demo program. */
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Application defined services of the NetX SNTP Client. */

UINT leap_second_handler(NX_SNTP_CLIENT *client_ptr, 
                                UINT leap_indicator);
UINT kiss_of_death_handler(NX_SNTP_CLIENT *client_ptr, 
                                        UINT KOD_code);
VOID time_update_callback(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                       NX_SNTP_TIME *local_time);


/* Set up client thread and network resources. */

NX_PACKET_POOL      client_packet_pool;
NX_IP               client_ip;
TX_THREAD           demo_client_thread;
NX_SNTP_CLIENT      demo_sntp_client;
TX_EVENT_FLAGS_GROUP sntp_flags;

#define DEMO_SNTP_UPDATE_EVENT  1

/* Configure the SNTP Client to use IPv6. If not enabled, the 
   Client will use IPv4.  Note: IPv6 must be enabled in NetX Duo
   for the Client to communicate over IPv6.    */
#ifdef FEATURE_NX_IPV6
/* #define USE_IPV6 */
#endif /* FEATURE_NX_IPV6 */


/* Configure the SNTP Client to use unicast SNTP. */
#define USE_UNICAST


#define CLIENT_IP_ADDRESS       IP_ADDRESS(192,2,2,66)
#define SERVER_IP_ADDRESS       IP_ADDRESS(192,2,2,92)
#define SERVER_IP_ADDRESS_2     SERVER_IP_ADDRESS

/* Set up the SNTP network and address index; */
UINT     iface_index =0;
UINT     prefix = 64;   
UINT     address_index;

/* Set up client thread entry point. */
void    demo_client_thread_entry(ULONG info);

/* Define main entry point.  */
int main()
{
    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
    return 0;
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

UINT     status;
UCHAR    *free_memory_pointer;


    free_memory_pointer = (UCHAR *)first_unused_memory;

    /* Create client packet pool. */
    status =  nx_packet_pool_create(&client_packet_pool, 
                                "SNTP Client Packet Pool",
                                NX_SNTP_CLIENT_PACKET_SIZE, 
                                free_memory_pointer, 
                                NX_SNTP_CLIENT_PACKET_POOL_SIZE);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        return;
    }

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + NX_SNTP_CLIENT_PACKET_POOL_SIZE;

    /* Create Client IP instances */
    status = nx_ip_create(&client_ip, "SNTP IP Instance", 
                                        CLIENT_IP_ADDRESS, 
                                        0xFFFFFF00UL, 
                                        &client_packet_pool, 
                                       _nx_ram_network_driver, 
                                       free_memory_pointer, 2048, 1);
    
    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }

    free_memory_pointer =  free_memory_pointer + 2048;

#ifndef NX_DISABLE_IPV4
    /* Enable ARP and supply ARP cache memory. */
    status =  nx_arp_enable(&client_ip, (void **) free_memory_pointer, 2048);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }
#endif /* NX_DISABLE_IPV4  */

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;
    
    /* Enable UDP for client. */
    status =  nx_udp_enable(&client_ip);
    
    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }

#ifndef NX_DISABLE_IPV4
    status = nx_icmp_enable(&client_ip);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }
#endif /* NX_DISABLE_IPV4  */

    /* Create the client thread */
    status = tx_thread_create(&demo_client_thread, "SNTP Client Thread", 
                                                demo_client_thread_entry, 
                                              (ULONG)(&demo_sntp_client), 
                                                free_memory_pointer, 2048, 
                                                  4, 4, TX_NO_TIME_SLICE, 
                                                        TX_DONT_START);

    /* Check for errors */
    if (status != TX_SUCCESS)
    {

        return;
    }

    /* Create the event flags. */
    status = tx_event_flags_create(&sntp_flags, "SNTP event flags");

    /* Check for errors */
    if (status != TX_SUCCESS)
    {

        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* set the SNTP network interface to the primary interface. */
    iface_index = 0;

    /* Create the SNTP Client to run in broadcast mode.. */
status =  nx_sntp_client_create(&demo_sntp_client, &client_ip,
                           iface_index, &client_packet_pool,  
                               leap_second_handler, 
                               kiss_of_death_handler, 
                               NULL /* no random_number_generator callback */);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        /* Bail out!*/
        return;
    }

    tx_thread_resume(&demo_client_thread);

    return;
}

/* Define size of buffer to display client's local time. */
#define BUFSIZE 50

/* Define the client thread.  */
void    demo_client_thread_entry(ULONG info)
{

UINT   status;
UINT   spin;
UINT   server_status;
ULONG  base_seconds;
ULONG  base_fraction;
ULONG  seconds, milliseconds, microseconds, fraction;
UINT   wait = 0;
UINT   error_counter = 0;
ULONG  events = 0;
#ifdef USE_IPV6
NXD_ADDRESS sntp_server_address;
NXD_ADDRESS client_ip_address;
#endif

    NX_PARAMETER_NOT_USED(info);

    /* Give other threads (IP instance) initialize first. */
    tx_thread_sleep(NX_IP_PERIODIC_RATE); 

#ifdef USE_IPV6
    /* Set up IPv6 services. */
    status = nxd_ipv6_enable(&client_ip);

    status += nxd_icmp_enable(&client_ip);

    if (status  != NX_SUCCESS)
        return;

    client_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    client_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    client_ip_address.nxd_ip_address.v6[2] = 0x0;
    client_ip_address.nxd_ip_address.v6[3] = 0x101;
    client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

    /* Set the IPv6 server address. */
    sntp_server_address.nxd_ip_address.v6[0] = 0x20010db8;  
    sntp_server_address.nxd_ip_address.v6[1] = 0x0000f101;
    sntp_server_address.nxd_ip_address.v6[2] = 0x0;
    sntp_server_address.nxd_ip_address.v6[3] = 0x00000106;
    sntp_server_address.nxd_ip_version = NX_IP_VERSION_V6;

    /* Establish the link local address for the host. The RAM driver creates
       a virtual MAC address. */
    status = nxd_ipv6_address_set(&client_ip, iface_index, NX_NULL, 10, NULL);

    /* Check for link local address set error.  */
    if (status != NX_SUCCESS) 
    {
        return;
    }

     /* Set the host global IP address. We are assuming a 64 
       bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&client_ip, iface_index, 
                                        &client_ip_address, 
                                    prefix, &address_index);

    /* Check for global address set error.  */
    if (status != NX_SUCCESS) 
    {
        return;
    }

    /* Wait while NetX Duo validates the global and link local addresses. */
    tx_thread_sleep(5 * NX_IP_PERIODIC_RATE);

#endif

    /* Setup time update callback function. */
    nx_sntp_client_set_time_update_notify(&demo_sntp_client, 
                                        time_update_callback);

    /* Set up client time updates depending on mode. */
#ifdef USE_UNICAST

    /* Initialize the Client for unicast mode to 
       poll the SNTP server once an hour. */
#ifdef USE_IPV6
/* Use the duo service to set up the Client and set the IPv6 SNTP server.
   Note: this can take either an IPv4 or IPv6 address. */
    status = nxd_sntp_client_initialize_unicast(&demo_sntp_client, 
                                            &sntp_server_address);
#else
    /* Use the IPv4 service to set up the Client and set the IPv4 SNTP server. */
    status = nx_sntp_client_initialize_unicast(&demo_sntp_client, 
                                                SERVER_IP_ADDRESS);
#endif  /* USE_IPV6 */


#else   /* Broadcast mode */

/* Initialize the Client for broadcast mode, no roundtrip calculation
   required and a broadcast SNTP service. */
#ifdef USE_IPV6
    /* Use the duo service to initialize the Client 
       and set IPv6 SNTP all hosts multicast address. 
       (Note: This can take either an IPv4 or IPv6 address.)*/
    status = nxd_sntp_client_initialize_broadcast(&demo_sntp_client, 
                                                &sntp_server_address, 
                                                            NX_NULL);
#else

    /* Use the IPv4 service to initialize the Client and set 
       IPv4 SNTP broadcast address. */
    status = nx_sntp_client_initialize_broadcast(&demo_sntp_client,  
                                                NX_NULL, 
                                                SERVER_IP_ADDRESS);
#endif  /* USE_IPV6 */
#endif  /* USE_UNICAST */

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Set the base time which is approximately the number of seconds since
       the turn of the last century. If this is not available in SNTP format,
       the nx_sntp_client_utility_add_msecs_to_ntp_time service can convert
       milliseconds to fraction.  For how to compute NTP seconds from real
   time, read the NetX SNTP User Guide. Otherwise set the base time to 
   zero and set NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP to NX_TRUE for
       the SNTP CLient to accept the first time update without applying a
       minimum or maximum adjustment parameters
      (NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT and
       NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT). */

    base_seconds =  0xd2c96b90;  /* Jan 24, 2012 UTC */
    base_fraction = 0xa132db1e;

    /* Apply to the SNTP Client local time.  */
status = nx_sntp_client_set_local_time(&demo_sntp_client, base_seconds,
                                base_fraction);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Run whichever service the client is configured for. */
#ifdef USE_UNICAST
    status = nx_sntp_client_run_unicast(&demo_sntp_client);
#else
    status = nx_sntp_client_run_broadcast(&demo_sntp_client);
#endif  /* USE_UNICAST */

    if (status != NX_SUCCESS)
    {
        return;
    }

    spin = NX_TRUE;

    /* Now check periodically for time changes. */
    while(spin)
    {
        /* Wait for a server update event. */
        tx_event_flags_get(&sntp_flags, DEMO_SNTP_UPDATE_EVENT, 
                                          TX_OR_CLEAR, &events, 
                                 DEMO_PERIODIC_CHECK_INTERVAL);

        if (events == DEMO_SNTP_UPDATE_EVENT)
        {

            /* Check for valid SNTP server status. */
            status = nx_sntp_client_receiving_updates(&demo_sntp_client,
                                               &server_status);

            if ((status != NX_SUCCESS) || (server_status == NX_FALSE))
            {

                /* We do not have a valid update. Skip processing any time
                   data. If this happens repeatedly, consider stopping the
                   SNTP Client thread, picking another SNTP server and
                   resuming the SNTP Client thread task (more details about
                   that in the comments at the end of this function).
                 
                   If SNTP Client configurable parameters are too restrictive,
                   such as Max Adjustment, that may also cause valid server
                   updates to be rejected. Configurable parameters, however,
                   cannot be changed at run time.
                 */
                 
                continue;
            }

            /* We have a valid update.  Get the SNTP Client time.  */
            status = nx_sntp_client_get_local_time_extended(&demo_sntp_client, 
                                                    &seconds, &fraction,  
                                                    NX_NULL, 0); 

            /* Convert fraction to microseconds. */
            nx_sntp_client_utility_fraction_to_usecs(fraction, &microseconds);

            milliseconds = ((microseconds + 500) / 1000);

            if (status != NX_SUCCESS)
            {
                printf("Internal error with getting local time 0x%x\n", 
                       status);
                error_counter++;
            }
            else
            {
                printf("\nSNTP updated\n");
                printf("Time: %lu.%03lu sec.\r\n", seconds, milliseconds);
            }

            /* Clear all events in our event flag. */
            events = 0;
        }
        else
        {

            /* No SNTP update event.             
               In the meantime, if we have an RTC we might want to check
               its notion of time. In this demo, we simulate the passage of 
               time on our 'RTC' really just the CPU counter, assuming that 
               seconds and milliseconds have previously been set to a base 
              (starting) time (as was the SNTP Client before running it) 
             */

            seconds += 1;
            milliseconds += 1;

            /* Update our timer. */
            wait += DEMO_PERIODIC_CHECK_INTERVAL;

            /* Check if it is time to display the local 'RTC' time. */
            if (wait >= CHECK_SNTP_UPDATES_TIMEOUT)
            {
                /* It is. Reset the timeout and print local time. */
                wait = 0;

                printf("Time: %lu.%03lu sec.\r\n", seconds, milliseconds);
            }           
        }
    }

/* We can stop the SNTP service if for example we think the SNTP server 
   has stopped sending updates.
     
       To restart the SNTP Client, simply call the
       nx_sntp_client_initialize_unicast or
       nx_sntp_client_initialize_broadcast using another SNTP server IP
       address as input, and resume the SNTP Client by calling
       nx_sntp_client_run_unicast or
       nx_sntp_client_run_braodcast. */
    status = nx_sntp_client_stop(&demo_sntp_client);

    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    /* When done with the SNTP Client, we delete it */
    status = nx_sntp_client_delete(&demo_sntp_client);

    return;
}


/* This application defined handler for handling an 
   impending leap second is not required by 
   the SNTP Client. The default handler below only logs the
   event for every time stamp received with the 
   leap indicator set.  */

UINT leap_second_handler(NX_SNTP_CLIENT *client_ptr, 
                                UINT leap_indicator)
{
    NX_PARAMETER_NOT_USED(client_ptr);
    NX_PARAMETER_NOT_USED(leap_indicator);

    /* Handle the leap second handler... */

    return NX_SUCCESS;
}

/* This application defined handler for handling 
   a Kiss of Death packet is not required by the SNTP Client. 
   A KOD handler should determine if the Client task should continue vs. 
   abort sending/receiving time data from its current time server, 
   and if aborting if it should remove
   the server from its active server list. 

   Note that the KOD list of codes is subject to change. The list
   below is current at the time of this software release. */

UINT kiss_of_death_handler(NX_SNTP_CLIENT *client_ptr, UINT KOD_code)
{

UINT    remove_server_from_list = NX_FALSE;
UINT    status = NX_SUCCESS;

    NX_PARAMETER_NOT_USED(client_ptr);

    /* Handle kiss of death by code group. */
    switch (KOD_code)
    {

        case NX_SNTP_KOD_RATE:
        case NX_SNTP_KOD_NOT_INIT:
        case NX_SNTP_KOD_STEP:

            /* Find another server while this one 
               is temporarily out of service.  */
            status =  NX_SNTP_KOD_SERVER_NOT_AVAILABLE;

        break;

        case NX_SNTP_KOD_AUTH_FAIL:
        case NX_SNTP_KOD_NO_KEY:
        case NX_SNTP_KOD_CRYP_FAIL:

            /* These indicate the server will not 
               service client with time updates
               without successful authentication. */


            remove_server_from_list =  NX_TRUE;

        break;


        default:

            /* All other codes. Remove server 
               before resuming time updates. */

            remove_server_from_list =  NX_TRUE;
        break;
    }

    /* Removing the server from the active server list? */
    if (remove_server_from_list)
    {

        /* Let the caller know it has to bail on 
           this server before resuming service. */
        status = NX_SNTP_KOD_REMOVE_SERVER;
    }

    return status;
}


/* This application defined handler for notifying SNTP time update event.  */

VOID time_update_callback(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                       NX_SNTP_TIME *local_time)
{
    tx_event_flags_set(&sntp_flags, DEMO_SNTP_UPDATE_EVENT, TX_OR);
}

```

Figura 1 Esempio di uso del client SNTP con NetX Duo

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la definizione del client NetX Duo SNTP. L'elenco seguente descrive ogni elemento in dettaglio:  
  

**NX_SNTP_CLIENT_THREAD_STACK_SIZE**  
Questa opzione imposta le dimensioni dello stack di thread del client. La dimensione predefinita del client NetX Duo SNTP è 2048.

**NX_SNTP_CLIENT_THREAD_TIME_SLICE**  
Questa opzione imposta l'intervallo di tempo dell'utilità di pianificazione per l'esecuzione del thread client. Le dimensioni predefinite del client NetX Duo SNTP sono TX_NO_TIME_SLICE.

**NX_SNTP_CLIENT_ THREAD_PRIORITY**  
Questa opzione imposta la priorità del thread client. Il valore predefinito di NetX Duo SNTP Client è 2.

**NX_SNTP_CLIENT_PREEMPTION_THRESHOLD**  
Questa opzione imposta il livello di priorità al quale il thread client consente la precedenza. Il valore predefinito di NetX Duo SNTP Client è impostato su `NX_SNTP_CLIENT_ THREAD_PRIORITY` .

**NX_SNTP_CLIENT_UDP_SOCKET_NAME**  
Questa opzione imposta il nome del socket UDP. Il nome predefinito del socket UDP del client NetX Duo SNTP è "SNTP Client socket".

**NX_SNTP_CLIENT_UDP_PORT**  
In questo modo viene impostata la porta a cui è associato il socket client. La porta predefinita del client NetX Duo SNTP è 123.

**NX_SNTP_SERVER_UDP_PORT**  
Si tratta della porta su cui il client invia i messaggi SNTP al server SNTP. La porta predefinita del server NetX SNTP è 123.

**NX_SNTP_CLIENT_TIME_TO_LIVE**  
Specifica il numero di router che un pacchetto client può passare prima di essere eliminato. Il client NetX Duo SNTP predefinito è impostato su 0x80 *.*

**NX_SNTP_CLIENT_MAX_QUEUE_DEPTH**  
Numero massimo di pacchetti UDP (datagrammi) che possono essere accodati nel socket del client SNTP di NetX Duo. I pacchetti aggiuntivi ricevuti significano che vengono rilasciati i pacchetti meno recenti. Il client NetX Duo SNTP predefinito è impostato su 5.

**NX_SNTP_CLIENT_PACKET_TIMEOUT**  
Timeout per l'allocazione di pacchetti NetX Duo. Il timeout predefinito del pacchetto del client NetX Duo SNTP è di 1 secondo.

**NX_SNTP_CLIENT_NTP_VERSION**  
Versione SNTP usata dal client L'API client SNTP di NetX Duo è basata sulla versione 4. Il valore predefinito è 3.

**NX_SNTP_CLIENT_MIN_NTP_VERSION**  
Versione SNTP meno recente che il client sarà in grado di usare. L'impostazione predefinita del client SNTP di NetX Duo è la versione 3.

**NX_SNTP_CLIENT_MIN_SERVER_STRATUM**  
Livello più basso (livello massimo di strato numerico) dello strato del server SNTP accettato dal client. Il valore predefinito di NetX Duo SNTP Client è 2.

**NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT**  
Regolazione dell'ora minima in millisecondi che il client farà all'ora dell'orologio locale. Le rettifiche di tempo al di sotto di questo valore verranno ignorate. Il valore predefinito di NetX Duo SNTP Client è 10.

**NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT**  
Regolazione dell'ora massima in millisecondi che il client farà all'ora dell'orologio locale. Per le rettifiche di tempo superiori a questo valore, la regolazione dell'orologio locale è limitata alla regolazione massima dell'ora. Il valore predefinito del client NetX Duo SNTP è 180000 (3 minuti).

**NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP**  
Ciò consente di rinunciare alla regolazione del tempo massima quando il client riceve il primo aggiornamento dal server di tempo. Successivamente, viene applicata la regolazione temporale massima. L'intenzione è di sincronizzare il client con l'orologio del server il prima possibile. Il client NetX Duo SNTP predefinito è NX_TRUE.

**NX_SNTP_CLIENT_MAX_TIME_LAPSE**  
Tempo massimo consentito (secondi) trascorso senza un aggiornamento di tempo valido ricevuto dal client SNTP. Il client SNTP continuerà a essere in esecuzione, ma lo stato del server SNTP è impostato su NX_FALSE. Il valore predefinito è 7200.


**NX_SNTP_UPDATE_TIMEOUT_INTERVAL**  
Intervallo (secondi) in cui il timer del client SNTP aggiorna il tempo del client SNTP rimanente dall'ultimo aggiornamento valido ricevuto e il client unicast aggiorna il tempo rimanente dell'intervallo di polling prima di inviare la richiesta di aggiornamento SNTP successiva. Il valore predefinito è 1.

**NX_SNTP_CLIENT_UNICAST_POLL_INTERVAL**  
Intervallo di polling iniziale (secondi) in cui il client invia una richiesta unicast al server SNTP. Il valore predefinito del client SNTP di NetX Duo è 3600.

**NX_SNTP_CLIENT_EXP_BACKOFF_RATE**  
Fattore in base al quale viene aumentato l'intervallo di polling unicast del client corrente. Quando il client non riceve un aggiornamento dell'ora del server o riceve indicazioni dal server che non è temporaneamente disponibile (ad esempio non è ancora sincronizzato) per il servizio di aggiornamento temporale, l'intervallo di polling corrente aumenta di questa frequenza fino a non superare NX_SNTP_CLIENT_MAX_TIME_LAPSE. Il valore predefinito è 2.

**NX_SNTP_CLIENT_RTT_REQUIRED**  
Questa opzione, se abilitata, richiede che il client SNTP calcoli round trip'ora dei messaggi SNTP quando si applicano gli aggiornamenti del server all'orologio locale. Il valore predefinito è NX_FALSE (disabilitato).

**NX_SNTP_CLIENT_MAX_ROOT_DISPERSION**  
La dispersione massima dell'orologio del server (microsecondi), ovvero una misura della precisione dell'orologio del server, verrà accettata dal client. Per disabilitare questo requisito, impostare la dispersione radice massima su 0x0. Il valore predefinito di NetX Duo SNTP Client è 50000.

**NX_SNTP_CLIENT_INVALID_UPDATE_LIMIT**  
Limite al numero di aggiornamenti non validi consecutivi ricevuti dal server client in modalità broadcast o unicast. Quando viene raggiunto questo limite, il client imposta lo stato corrente del server SNTP su non valido (NX_FALSE), anche se continuerà a provare a ricevere aggiornamenti dal server. Il valore predefinito del client SNTP di NetX Duo è 3.

**NX_SNTP_CLIENT_RANDOMIZE_ON_STARTUP**  
Ciò determina se il client SNTP in modalità unicast deve inviare la prima richiesta SNTP con il server SNTP corrente dopo un intervallo di attesa casuale. Viene usato nei casi in cui un numero significativo di client SNTP viene avviato contemporaneamente per limitare la congestione del traffico nel server SNTP. Il valore predefinito è NX_FALSE.

**NX_SNTP_CLIENT_SLEEP_INTERVAL**  
Intervallo di tempo durante il quale l'attività del client SNTP viene sospensione. In questo modo le chiamate API dell'applicazione possono essere eseguite dal client SNTP. Il valore predefinito è 1 tick timer.

**NX_SNTP_CURRENT_YEAR**  
Per visualizzare la data nel formato anno/mese/data, impostare questo valore su uguale o minore dell'anno corrente (non deve essere lo stesso anno dell'ora NTP in fase di valutazione). Il valore predefinito è 2015.

**NTP_SECONDS_AT_01011999**  
Questo è il numero di secondi nel primo ntp epoch sull'orologio NTP master. È definito come 0xBA368E80. Per disabilitare la visualizzazione dei secondi NTP in data e ora, impostare su zero.
