---
title: Capitolo 2 - Installazione e uso di Azure RTOS client PTP NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client NetX Duo PTP.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ee2e4184ce041679b5ae5368d91c436cf8a0bc2ac6f59deba67d996b318151bd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798028"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-ptp-client"></a>Capitolo 2 - Installazione e uso di Azure RTOS client PTP NetX Duo

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client NetX Duo PTP.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS NetX Duo può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo https://github.com/azure-rtos/netxduo/tree/master/addons/ptp .

***nxd_ptp_client.h*** File di intestazione per il client PTP per NetX Duo ***nxd_ptp_client.c*** File di origine C per il client PTP per netX Duo ***demo_netx_duo_ptp_client.c*** Dimostrazione client PTP NetX Duo


## <a name="using-ptp-client"></a>Uso del client PTP
L'uso del client PTP per NetX Duo è semplice. Fondamentalmente, il codice dell'applicazione deve includere ***nxd_ptp_client.h** _ dopo aver incluso _*_rispettivamente tx_api.h_*_ e _*_nx_api.h_*_, per poter usare rispettivamente ThreadX e NetX Duo. Dopo aver incluso il file di intestazione del client PTP, il codice dell'applicazione è in grado di effettuare le chiamate di funzione client PTP specificate più avanti in questa guida. L'applicazione deve includere anche _ *_nxd_ptp_client.c_** nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo modulo oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare il client NetX Duo PTP.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni
Un esempio di come usare i servizi client NetX Duo PTP è descritto nella figura 1 che viene visualizzata di seguito.
```C
/*
   This is a small demo of the NetX Duo PTP client on the high-performance NetX Duo TCP/IP stack.
   This demo relies on ThreadX, NetX Duo and NetX Duo PTP client API to execute the Precision Time
   Protocol.

 */

#include <stdio.h>
#include "nx_api.h"
#include "nxd_ptp_client.h"

#ifndef SAMPLE_DHCP_DISABLE
#include "nxd_dhcp_client.h"
#endif /* SAMPLE_DHCP_DISABLE */

#define PTP_THREAD_PRIORITY 2

/* Define the ThreadX and NetX object control blocks...  */
static TX_THREAD        thread_0;
static NX_PACKET_POOL   pool_0;
static NX_IP            ip_0;
#ifndef SAMPLE_DHCP_DISABLE
static NX_DHCP          dhcp_client;
#endif /* SAMPLE_DHCP_DISABLE */
static NX_PTP_CLIENT    ptp_client;

/* Define the IP thread's stack area.  */
static ULONG            ip_thread_stack[2048 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
static ULONG            packet_pool_area[((1536 + sizeof(NX_PACKET)) * 32) / sizeof(ULONG)];

/* Define the ARP cache area.  */
static ULONG            arp_space_area[512 / sizeof(ULONG)];

/* Define the main thread.  */
static ULONG            thread_0_stack[2048 / sizeof(ULONG)];
static ULONG            ptp_stack[2048 / sizeof(ULONG)];

/* Define an error counter.  */
static ULONG            error_counter;

/* Define ptp utc offset.  */
static SHORT            ptp_utc_offset = 0;

#ifndef SAMPLE_DHCP_DISABLE
#define IPV4_ADDRESS            IP_ADDRESS(0, 0, 0, 0)
#define IPV4_NETWORK_MASK       IP_ADDRESS(0, 0, 0, 0)
#else
#define IPV4_ADDRESS            IP_ADDRESS(10, 1, 0, 212)
#define IPV4_NETWORK_MASK       IP_ADDRESS(255, 255, 0, 0)
#define IPV4_GATEWAY_ADDR       IP_ADDRESS(10, 1, 0, 1)
#define DNS_SERVER_ADDRESS      IP_ADDRESS(10, 1, 0, 1)
#endif /* SAMPLE_DHCP_DISABLE */

/* Define the main thread entry point. */
static VOID thread_0_entry(ULONG thread_input);

/* PTP handler.  */
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data);

#ifndef SAMPLE_DHCP_DISABLE
static void dhcp_wait();
#endif /* SAMPLE_DHCP_DISABLE */

/***** Substitute your ethernet driver entry function here *********/
#ifndef NETWORK_DRIVER
#define NETWORK_DRIVER _nx_ram_network_driver
#endif
extern VOID NETWORK_DRIVER(NX_IP_DRIVER *driver_req_ptr);

#ifndef CLOCK_CALLBACK
#define CLOCK_CALLBACK nx_ptp_client_soft_clock_callback
#endif
extern UINT CLOCK_CALLBACK(NX_PTP_CLIENT *client_ptr, UINT operation,
                           NX_PTP_TIME *time_ptr, NX_PACKET *packet_ptr,
                           VOID *callback_data);

#ifdef HARDWARE_SETUP
extern VOID HARDWARE_SETUP();
#endif

int main()
{
#ifdef HARDWARE_SETUP
    HARDWARE_SETUP();
#endif

    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
    return 0;
}


/* Define what the initial system looks like.  */

void    tx_application_define(void *first_unused_memory)
{

UINT  status;


    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create a packet pool.  */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1536,  (ULONG*)(((int)packet_pool_area + 15) & ~15) , sizeof(packet_pool_area));

    /* Check for pool creation error.  */
    if (status)
        error_counter++;

    /* Create an IP instance.  */
    status = nx_ip_create(&ip_0,
                          "NetX IP Instance 0",
                          IPV4_ADDRESS,
                          IPV4_NETWORK_MASK,
                          &pool_0,
                          NETWORK_DRIVER,
                          (UCHAR*)ip_thread_stack,
                          sizeof(ip_thread_stack),
                          1);

    /* Check for IP create errors.  */
    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

    /* Check for ARP enable errors.  */
    if (status)
        error_counter++;

    /* Enable TCP traffic.  */
    status =  nx_tcp_enable(&ip_0);

    /* Check for TCP enable errors.  */
    if (status)
        error_counter++;

    /* Enable UDP traffic.  */
    status =  nx_udp_enable(&ip_0);

    /* Check for UDP enable errors.  */
    if (status)
        error_counter++;

    /* Enable ICMP.  */
    status =  nx_icmp_enable(&ip_0);

    /* Check for errors.  */
    if (status)
        error_counter++;

    /* Create the main thread.  */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                     thread_0_stack, sizeof(thread_0_stack),
                     4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
}


/* Define the test threads.  */
void    thread_0_entry(ULONG thread_input)
{

NX_PTP_TIME tm;
NX_PTP_DATE_TIME date;

#ifndef SAMPLE_DHCP_DISABLE
    dhcp_wait();
#endif /* SAMPLE_DHCP_DISABLE */

    /* Create the PTP client instance */
    nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                         PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                         CLOCK_CALLBACK, NX_NULL);

    /* start the PTP client */
    nx_ptp_client_start(&ptp_client, NX_NULL, 0, 0, 0, ptp_event_callback, NX_NULL);

    while(1)
    {

        /* read the PTP clock */
        nx_ptp_client_time_get(&ptp_client, &tm);

        /* convert PTP time to UTC date and time */
        nx_ptp_client_utility_convert_time_to_date(&tm, -ptp_utc_offset, &date);

        /* display the current time */
        printf("%2u/%02u/%u %02u:%02u:%02u.%09lu\r\n", date.day, date.month, date.year, date.hour, date.minute, date.second, date.nanosecond);

        tx_thread_sleep(NX_IP_PERIODIC_RATE);
    }
}

static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
    NX_PARAMETER_NOT_USED(callback_data);

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_MASTER:
        {
            printf("new MASTER clock!\r\n");
            break;
        }

        case NX_PTP_CLIENT_EVENT_SYNC:
        {
            nx_ptp_client_sync_info_get((NX_PTP_CLIENT_SYNC *)event_data, NX_NULL, &ptp_utc_offset);
            printf("SYNC event: utc offset=%d\r\n", ptp_utc_offset);
            break;
        }

        case NX_PTP_CLIENT_EVENT_TIMEOUT:
        {
            printf("Master clock TIMEOUT!\r\n");
            break;
        }
        default:
        {
            break;
        }
    }

    return 0;
}

/* DHCP */
#ifndef SAMPLE_DHCP_DISABLE
void dhcp_wait(void)
{

ULONG   actual_status;
ULONG   ip_address;
ULONG   network_mask;
ULONG   gw_address;

    printf("DHCP In Progress...\r\n");

    /* Create the DHCP instance.  */
    nx_dhcp_create(&dhcp_client, &ip_0, "dhcp_client");

    /* Start the DHCP Client.  */
    nx_dhcp_start(&dhcp_client);

    /* Wait util address is solved. */
    nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED, &actual_status, NX_WAIT_FOREVER);

    /* Get IP address. */
    nx_ip_address_get(&ip_0, &ip_address, &network_mask);
    nx_ip_gateway_address_get(&ip_0, &gw_address);

    /* Output IP address. */
    printf("IP address: %d.%d.%d.%d\r\nMask: %d.%d.%d.%d\r\nGateway: %d.%d.%d.%d\r\n",
           (INT)(ip_address >> 24),
           (INT)(ip_address >> 16 & 0xFF),
           (INT)(ip_address >> 8 & 0xFF),
           (INT)(ip_address & 0xFF),
           (INT)(network_mask >> 24),
           (INT)(network_mask >> 16 & 0xFF),
           (INT)(network_mask >> 8 & 0xFF),
           (INT)(network_mask & 0xFF),
           (INT)(gw_address >> 24),
           (INT)(gw_address >> 16 & 0xFF),
           (INT)(gw_address >> 8 & 0xFF),
           (INT)(gw_address & 0xFF));
}
#endif /* SAMPLE_DHCP_DISABLE  */
```

## <a name="configuration-options"></a>Opzioni di configurazione
Con il client NetX Duo PTP sono disponibili diverse opzioni di configurazione. Di seguito è riportato un elenco di tutte le opzioni descritte in dettaglio:
* **NX_PTP_CLIENT_THREAD_TIME_SLICE** Definisce l'intervallo di tempo del thread client PTP. Il valore predefinito non è un intervallo di tempo.
* **NX_PTP_CLIENT_TIMER_TICKS_PER_SECOND** Definisce la frequenza del timer interno del client PTP. Il valore predefinito è 10, che indica un timer di 100 ms.
* **NX_PTP_CLIENT_ANNOUNCE_RECEIPT_TIMEOUT** Definisce il numero massimo di pacchetti Announce mancanti prima del timeout. Il valore predefinito è 3.
* **NX_PTP_CLIENT_LOG_ANNOUNCE_INTERVAL** Definisce l'intervallo di tempo tra il pacchetto Announce successivo, espresso come log 2. Questo valore deve essere uniforme in tutto un dominio. Il valore predefinito è 1, ovvero 2s.
* **NX_PTP_CLIENT_DELAY_REQ_INTERVAL** Definisce l'intervallo per l'invio di pacchetti di richiesta delay. Il valore predefinito è 2 secondi.
* **NX_PTP_CLIENT_MAX_QUEUE_DEPTH** Definisce la profondità massima della coda per il socket client. Il valore predefinito è 5.