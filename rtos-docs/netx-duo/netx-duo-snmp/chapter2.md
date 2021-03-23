---
title: Capitolo 2-installazione e uso dell'agente SNMP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente NetX Duo SNMP Agent.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f011b73217c7f413dd19c555e9c2d40dace305ee
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821668"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-duo-snmp-agent"></a>Capitolo 2-installazione e uso dell'agente SNMP di Azure RTO NetX Duo

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente dell'agente SNMP di Azure RTO NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

L'agente SNMP per NetX Duo è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include quattro file di origine, un file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_snmp. h** File di intestazione per SNMP per NetX Duo
- **demo_snmp_helper. h** File di intestazione per i dati MIB SNMP
- **nxd_snmp. c** File di origine C per l'agente SNMP per NetX Duo
- **nx_md5. c** Algoritmi digest MD5
- **nx_sha. c** Algoritmi del digest SHA
- **nx_des. c** Algoritmi di crittografia DES
- **nxd_snmp.pdf** Guida dell'utente per l'agente SNMP per NetX Duo
- **demo_netxduo_snmp. c** Semplice dimostrazione SNMP
- **demo_netxduo_mib2. c** Dimostrazione MIB2 semplice (MIB con elementi Address IPv6)
- **demo_snmp_helper. h** File di intestazione che definisce gli elementi MIB

## <a name="netx-duo-snmp-agent-installation"></a>Installazione dell'agente SNMP NetX Duo

Per usare NetX Duo SNMP, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_snmp. h*, *nxd_snmp. c*, *nx_md5. c, nx_sha. c* e nx_ *des. c* devono essere copiati in questa directory.

## <a name="using-the-netx-duo-snmp-agent"></a>Uso dell'agente SNMP NetX Duo

Nell'applicazione devono essere presenti *nxd_snmp. c*, *nx_md5. c, nx_sha. c* e *nx_des. c* nel progetto di compilazione. Il codice dell'applicazione deve includere anche *nxd_snmp. h* dopo aver incluso *nx_api. h per* poter richiamare i servizi SNMP. Questi file devono essere compilati nello stesso modo in cui gli altri file dell'applicazione e il relativo form oggetto devono essere collegati alla libreria NetX Duo. Questo è tutto ciò che è necessario per usare NetX Duo SNMP.

> [!NOTE]
> *Se nel processo di compilazione viene specificato **NX_SNMP_NO_SECURITY** , i file nx_md5. c, nx_sha. c e nx_des. c non sono necessari.*

> [!NOTE]
> Poiché NetX Duo SNMP usa i servizi UDP, è necessario abilitare UDP con la chiamata *nx_udp_enable* prima di usare SNMP.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come usare NetX Duo SNMP Agent è descritto nella figura 1,0 riportata di seguito. In questo esempio il file di inclusione SNMP *nxd_snmp. h* viene introdotto nella riga 6. Il file di intestazione che definisce gli elementi del database MIB, *demo_snmp_helper. h,* viene introdotto nella riga 8. Il MIB viene definito a partire dalla riga 32. Successivamente, l'agente SNMP viene creato in "*tx_application_define*" alla riga 129. Si noti che il blocco di controllo dell'agente SNMP "*my_agent*" è stato definito come variabile globale alla riga 18 in precedenza. Se IPv6 è abilitato, gli indirizzi IPv6 vengono registrati con l'istanza IP nelle righe 166-223. L'agente SNMP viene avviato alla riga 229. Le definizioni di callback di oggetti SNMP per SNMP Manager GET, GetNext e SET richieste, nonché le richieste di aggiornamento di nome utente e MIB, vengono elaborate a partire dalla riga 250. Per questo esempio, non viene eseguita alcuna autenticazione.

> [!NOTE]
> *La tabella MIB2 illustrata di seguito è semplicemente un esempio. L'applicazione può usare un MIB diverso e includerla in file distinti, nonché definire GET, GetNext o impostare l'elaborazione in base ai requisiti dell'applicazione.*

```c
/* This is a small demo of the NetX SNMP Agent on the high-performance NetX TCP/IP  
   stack. This demo relies on ThreadX and NetX to show simple SNMP the SNMP
   GET/GETNEXT/SET requests on MIB-2 objects.  */

#include  "tx_api.h"
#include  "nx_api.h"
#include  "nxd_snmp.h"
#include  "demo_snmp_helper.h"

#define     DEMO_STACK_SIZE         4096
#define     AGENT_PRIMARY_ADDRESS   IP_ADDRESS(192, 2, 2, 66)

/* Define the ThreadX and NetX object control blocks...  */

TX_THREAD               thread_0;
NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;
NX_SNMP_AGENT           my_agent;


/* Indicate if using IPv6 to communicate with SNMP servers. Note that
   IPv6 must be enabled in the NetX Duo library first. Further, IPv6
   and ICMPv6 services are enabled before starting the SNMP agent. */
#define USE_IPV6


/* Define authentication and privacy keys.  */

#ifdef AUTHENTICATION_REQUIRED
NX_SNMP_SECURITY_KEY    my_authentication_key;
#endif

#ifdef PRIVACY_REQUIRED
NX_SNMP_SECURITY_KEY    my_privacy_key;
#endif

/* Define an error counter variable. */
UINT error_counter = 0;

/* This binds a secondary interfaces to the primary IP network interface 
   if SNMP is required for required for that interface. */
/* #define  MULTI_HOMED_DEVICE */

/* Define function prototypes.  A generic ram driver is used in this demo.  However
   to properly run an SNMP agent demo, a real driver should be substituted. */

VOID    thread_agent_entry(ULONG thread_input);
VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);
UINT    mib2_get_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data);
UINT    mib2_getnext_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data);
UINT    mib2_set_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data);
UINT    mib2_username_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *username);
VOID    mib2_variable_update(NX_IP *ip_ptr, NX_SNMP_AGENT *agent_ptr);


UCHAR context_engine_id[] = {0x80, 0x00, 0x0d, 0xfe, 0x03, 0x00, 0x11, 0x23, 0x23, 
                             0x44, 0x55};
UINT  context_engine_size = 11;
UCHAR context_name[] = {0x69, 0x6e, 0x69, 0x74, 0x69, 0x61, 0x6c};
UINT  context_name_size = 7;

/* Define main entry point.  */

int main()
{

   /* Enter the ThreadX kernel.  */
   tx_kernel_enter();
}


/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

UCHAR   *pointer;
UINT    status;


   /* Setup the working pointer.  */
   pointer =  (UCHAR *) first_unused_memory;

   status = tx_thread_create(&thread_0, "agent thread", thread_agent_entry, 0,  
            pointer, DEMO_STACK_SIZE, 
            4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
   if (status != NX_SUCCESS)
   {
      return;
   }

   pointer =  pointer + DEMO_STACK_SIZE;


   /* Initialize the NetX system.  */
   nx_system_initialize();

   /* Create packet pool.  */
   status = nx_packet_pool_create(&pool_0, "NetX Packet Pool 0", 2048, 
                                   pointer, 20000);

   if (status != NX_SUCCESS)
   {
      return;
   }
  
   pointer = pointer + 20000;
  
   /* Create an IP instance.  */
   status = nx_ip_create(&ip_0, "SNMP Agent IP Instance", AGENT_PRIMARY_ADDRESS, 
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 4096, 1);

   if (status != NX_SUCCESS)
   {
      return;
   }
  
   pointer =  pointer + 4096;
  
   /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
   nx_arp_enable(&ip_0, (void *) pointer, 1024);
   pointer = pointer + 1024;

   /* Enable UPD processing for IP instance.  */
   nx_udp_enable(&ip_0);
  
   /* Enable ICMP for ping.  */
   nx_icmp_enable(&ip_0);
  
   /* Create an SNMP agent instance.  */
   status = nx_snmp_agent_create(&my_agent, "SNMP Agent", &ip_0, pointer, 4096, 
                                 &pool_0, 
                                 mib2_username_processing, mib2_get_processing, 
                                 mib2_getnext_processing, 
                                 mib2_set_processing);


  
   if (status != NX_SUCCESS)
   {
      return;
   }
  
   pointer =  pointer + 4096;
  
   status = nx_snmp_agent_context_engine_set(&my_agent, context_engine_id, 
                                             context_engine_size);
  
   if (status != NX_SUCCESS)
   {
      error_counter++;
   }
  
   return;
}
  
VOID thread_agent_entry(ULONG thread_input)
{
  
#ifdef USE_IPV6
UINT        iface_index, address_index;
UINT        status;
NXD_ADDRESS agent_ipv6_address;
#endif
  
  
      /* Allow NetX time to get initialized. */
      tx_thread_sleep(100);
  
      /* If using IPv6, enable IPv6 and ICMPv6 services and get IPv6 addresses 
         registered with NetX Dou. */
  
#ifdef USE_IPV6
  
      /* Enable IPv6 on the IP instance. */
      status = nxd_ipv6_enable(&ip_0);
   
      /* Check for enable errors.  */
      if (status)
      {
  
         error_counter++;
         return;
      }
      /* Enable ICMPv6 on the IP instance. */
      status = nxd_icmp_enable(&ip_0);
  
      /* Check for enable errors.  */
      if (status)
      {
  
         error_counter++;
         return;
      }
  
      agent_ipv6_address.nxd_ip_address.v6[3] = 0x101;
      agent_ipv6_address.nxd_ip_address.v6[2] = 0x0;
      agent_ipv6_address.nxd_ip_address.v6[1] = 0x0000f101;
      agent_ipv6_address.nxd_ip_address.v6[0] = 0x20010db8;
      agent_ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
  
      /* Set the primary interface for our DNS IPv6 addresses. */
      iface_index = 0;
  
      /* This assumes we are using the primary network interface (index 0). */
      status = nxd_ipv6_address_set(&ip_0, iface_index, NX_NULL, 10, &address_index);
  
      /* Check for link local address set error.  */
      if (status) 
      {
  
         error_counter++;
         return;
      }
  
      /* Set the host global IP address. We are assuming a 64 
         bit prefix here but this can be any value (< 128). */
      status = nxd_ipv6_address_set(&ip_0, iface_index, &agent_ipv6_address, 64, 
                                    &address_index);
  
      /* Check for global address set error.  */
      if (status) 
      {
  
         error_counter++;
         return;
      }

      /* Wait while NetX Duo validates the link local and global address. */
      tx_thread_sleep(500);
#endif
  
#ifdef AUTHENTICATION_REQUIRED

      /* Create an authentication key.  */
      nx_snmp_agent_md5_key_create(&my_agent, "authpassword", &my_authentication_key);
  
      /* Use the authentication key.  */
      nx_snmp_agent_authenticate_key_use(&my_agent, &my_authentication_key);
#endif
  
#ifdef PRIVACY_REQUIRED
  
      /* Create a privacy key.  */
      nx_snmp_agent_md5_key_create(&my_agent, "privpassword", &my_privacy_key);
  
      /* Use the privacy key.  */
      nx_snmp_agent_privacy_key_use(&my_agent, &my_privacy_key);
#endif
  
      /* Start the SNMP instance.  */
      nx_snmp_agent_start(&my_agent);
  
}
  
/* Define the application's GET processing routine.  */
  
UINT    mib2_get_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data)
{
  
UINT    i;
UINT    status;
  
  
      printf("SNMP Manager GET Request For:  %s", object_requested);
  
      /* Loop through the sample MIB to see if we have information for the supplied 
         variable.  */
      i =  0;
      status =  NX_SNMP_ERROR;
      while (mib2_mib[i].object_name)
      {
  
         /* See if we have found the matching entry.  */
         status =  nx_snmp_object_compare(object_requested, mib2_mib[i].object_name);
  
         /* Was it found?  */
         if (status == NX_SUCCESS)
         {
  
            /* Yes it was found.  */
            break;
         }
  
         /* Move to the next index.  */
         i++;
      }
  
      /* Determine if a not found condition is present.  */
      if (status != NX_SUCCESS)
      {
  
         printf(" NO SUCH NAME!\n");
  
         /* The object was not found - return an error.  */
         return(NX_SNMP_ERROR_NOSUCHNAME);
      }
  
      /* Determine if the entry has a get function.  */
      if (mib2_mib[i].object_get_callback)
      {
  
         /* Yes, call the get function.  */
         status =  (mib2_mib[i].object_get_callback)(mib2_mib[i].object_value_ptr, 
                                                     object_data);
      }
      else
      {
  
         printf(" NO GET FUNCTION!");
  
         /* No get function, return no access.  */
         status =  NX_SNMP_ERROR_NOACCESS;
      }
  
      printf("\n");

      /* Return the status.  */
      return(status);
}
  
  
/* Define the application's GETNEXT processing routine.  */
  
UINT    mib2_getnext_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                                NX_SNMP_OBJECT_DATA *object_data)
{
  
UINT    i;
UINT    status;
  
  
   printf("SNMP Manager GETNEXT Request For:  %s", object_requested);
  
   /* Loop through the sample MIB to see if we have information for the supplied 
      variable.  */
      i =  0;
      status =  NX_SNMP_ERROR;
      while (mib2_mib[i].object_name)
      {
  
         /* See if we have found the next entry.  */
         status =  nx_snmp_object_compare(object_requested, mib2_mib[i].object_name);
  
         /* Is the next entry the mib greater?  */
         if (status == NX_SNMP_NEXT_ENTRY)
         {
  
            /* Yes it was found.  */
            break;
         }
  
         /* Move to the next index.  */
         i++;
      }
  
      /* Determine if a not found condition is present.  */
      if (status != NX_SNMP_NEXT_ENTRY)
      {
  
         printf(" NO SUCH NAME!\n");
  
         /* The object was not found - return an error.  */
         return(NX_SNMP_ERROR_NOSUCHNAME);
      }
  
  
      /* Copy the new name into the object.  */
      nx_snmp_object_copy(mib2_mib[i].object_name, object_requested);
  
      printf(" Next Name is: %s", object_requested);
  
      /* Determine if the entry has a get function.  */
      if (mib2_mib[i].object_get_callback)
      {
  
         /* Yes, call the get function.  */
         status =  (mib2_mib[i].object_get_callback)(mib2_mib[i].object_value_ptr, 
                                                     object_data);
  
         /* Determine if the object data indicates an end-of-mib condition.  */
         if (object_data -> nx_snmp_object_data_type == NX_SNMP_END_OF_MIB_VIEW)
         {
  
            /* Copy the name supplied in the mib table.  */
            nx_snmp_object_copy(mib2_mib[i].object_value_ptr, object_requested);
         }
      }
      else
      {
  
         printf(" NO GET FUNCTION!");
  
         /* No get function, return no access.  */
         status =  NX_SNMP_ERROR_NOACCESS;
      }
  
      printf("\n");

      /* Return the status.  */
      return(status);
}
  
  
/* Define the application's SET processing routine.  */
  
UINT    mib2_set_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data)
{
  
UINT    i;
UINT    status;
  
  
   printf("SNMP Manager SET Request For:  %s", object_requested);
  
   /* Loop through the sample MIB to see if we have information for the supplied variable.  */
      i =  0;
      status =  NX_SNMP_ERROR;
      while (mib2_mib[i].object_name)
      {
  
         /* See if we have found the matching entry.  */
         status =  nx_snmp_object_compare(object_requested, mib2_mib[i].object_name);
  
         /* Was it found?  */
         if (status == NX_SUCCESS)
         {
  
            /* Yes it was found.  */
            break;
         }
  
         /* Move to the next index.  */
         i++;
      }
  
      /* Determine if a not found condition is present.  */
      if (status != NX_SUCCESS)
      {
  
         printf(" NO SUCH NAME!\n");
  
         /* The object was not found - return an error.  */
         return(NX_SNMP_ERROR_NOSUCHNAME);
      }
  
  
      /* Determine if the entry has a set function.  */
      if (mib2_mib[i].object_set_callback)
      {
  
         /* Yes, call the set function.  */
         status =  (mib2_mib[i].object_set_callback)(mib2_mib[i].object_value_ptr, 
                                                     object_data);
      }
      else
      {
  
         printf(" NO SET FUNCTION!");
  
         /* No get function, return no access.  */
         status =  NX_SNMP_ERROR_NOACCESS;
      }
  
      printf("\n");

      /* Return the status.  */
      return(status);
}
  
  
/* Define the application's authentication routine.  */
  
UINT  mib2_username_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *username)
{
  
      printf("Username is:  %s\n", username);
  
      /* Update MIB-2 objects. In this example, it is only the SNMP objects.  */
      mib2_variable_update(&ip_0, &my_agent);
  
      /* No authentication is done, just return success!  */
      return(NX_SUCCESS);
}
  
  
/* Define the application's update routine.  */ 
  
VOID  mib2_variable_update(NX_IP *ip_ptr, NX_SNMP_AGENT *agent_ptr)
{
  
      /* Update the snmp parameters.  */
      snmpInPkts =                agent_ptr -> nx_snmp_agent_packets_received;
      snmpOutPkts =               agent_ptr -> nx_snmp_agent_packets_sent;
      snmpInBadVersions =         agent_ptr -> nx_snmp_agent_invalid_version;
      snmpInBadCommunityNames =   agent_ptr -> nx_snmp_agent_authentication_errors;
      snmpInBadCommunityUsers =   agent_ptr -> nx_snmp_agent_username_errors; 
      snmpInASNParseErrs =        agent_ptr -> nx_snmp_agent_internal_errors;
      snmpInTotalReqVars =        agent_ptr -> nx_snmp_agent_total_get_variables;
      snmpInTotalSetVars =        agent_ptr -> nx_snmp_agent_total_set_variables;
      snmpInGetRequests =         agent_ptr -> nx_snmp_agent_get_requests;
      snmpInGetNexts =            agent_ptr -> nx_snmp_agent_getnext_requests;
      snmpInSetRequests =         agent_ptr -> nx_snmp_agent_set_requests;
      snmpOutTooBigs =            agent_ptr -> nx_snmp_agent_too_big_errors;
      snmpOutNoSuchNames =        agent_ptr -> nx_snmp_agent_no_such_name_errors;
      snmpOutBadValues =          agent_ptr -> nx_snmp_agent_bad_value_errors;
      snmpOutGenErrs =            agent_ptr -> nx_snmp_agent_general_errors;
      snmpOutTraps =              agent_ptr -> nx_snmp_agent_traps_sent;
}   
```
Figura 1,0 esempio di uso dell'agente SNMP con NetX Duo

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la creazione di SNMP per NetX Duo. Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:  
  
| Definire                     | Significato                                                                                                                                                                                                                                                                        |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **NX_SNMP_AGENT_PRIORITY**     | Priorità del thread dell'agente SNMP. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.                                                                                                                                                                         |
| **NX_SNMP_TYPE_OF_SERVICE**    | Tipo di servizio richiesto per le risposte UDP SNMP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP. Questa definizione può essere impostata dall'applicazione prima di includere *nxd_snmp. h.*                                                       |
| **NX_SNMP_FRAGMENT_OPTION**    | Consenti frammenti per richieste UDP SNMP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione UDP SNMP. Questa definizione può essere impostata dall'applicazione prima di includere *nxd_snmp. h.*                                                                                 |
| **NX_SNMP_TIME_TO_LIVE**       | Specifica la durata (TTL) prima della scadenza. Il valore predefinito è impostato su 0x80, ma può essere ridefinito prima dell'inclusione di *nxd_snmp. h.*                                                                                                                                         |
| **NX_SNMP_AGENT_TIMEOUT**      | Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono. Il valore predefinito è impostato su 100, ma può essere ridefinito prima dell'inclusione di *nxd_snmp. h.*                                                                                                         |
| **NX_SNMP_MAX_OCTET_STRING**   | Specifica il numero massimo di byte consentiti in una stringa di ottetto nell'agente SNMP. Il valore predefinito è impostato su 255, ma può essere ridefinito prima dell'inclusione di *nxd_snmp. h.*                                                                                                    |
| **NX_SNMP_MAX_CONTEXT_STRING** | Specifica il numero massimo di byte per una stringa del motore di contesto nell'agente SNMP. Il valore predefinito è impostato su 32, ma può essere ridefinito prima dell'inclusione di *nxd_snmp. h.*                                                                                                    |
| **NX_SNMP_MAX_USER_NAME**      | Specifica il numero massimo di byte in un nome utente (incluse le stringhe della community). Il valore predefinito è impostato su 64, ma può essere ridefinito prima dell'inclusione di *nxd_snmp. h.*                                                                                                      |
| **NX_SNMP_MAX_SECURITY_KEY**   | Specifica il numero di byte consentiti in una stringa di chiave di sicurezza. Il valore predefinito è impostato su 64, ma può essere ridefinito prima di nclusion di *nxd_snmp. h.*                                                                                                                          |
| **NX_SNMP_PACKET_SIZE**        | Specifica la dimensione minima dei pacchetti nel pool specificato durante la creazione dell'agente SNMP. Le dimensioni minime sono necessarie per garantire che il payload SNMP completo possa essere contenuto in un unico pacchetto. Il valore predefinito è impostato su 560, ma può essere ridefinito prima dell'inclusione di *nxd_snmp. h.* |
| **NX_SNMP_AGENT_PORT**         | Specifica la porta UDP per il campo richieste di gestione SNMP. La porta predefinita è la porta UDP 161, ma può essere ridefinita prima dell'inclusione di *nxd_snmp. h.*                                                                                                                             |
| **NX_SNMP_MANAGER_TRAP_PORT**  | Specifica la porta UDP a cui inviare richieste trap agente SNMP. La porta predefinita è la porta UDP 162, ma può essere ridefinita prima dell'inclusione di *nxd_snmp. h.*                                                                                                                           |
| **NX_SNMP_MAX_TRAP_NAME**      | Specifica la dimensione della matrice in cui inserire il nome utente inviato con messaggi trap. Il valore predefinito è 64.                                                                                                                                                                         |
| **NX_SNMP_MAX_TRAP_KEY**       | Specifica le dimensioni delle chiavi di autenticazione e di privacy per i messaggi trap. Il valore predefinito è 64.                                                                                                                                                                          |
| **NX_SNMP_TIME_INTERVAL**      | Questo determina l'intervallo di sospensione nei cicli del timer effettuati dall'attività thread SNMP tra l'elaborazione dei pacchetti SNMP ricevuti. Il valore predefinito è 100. Durante questo intervallo di sospensione, l'applicazione host ha accesso ai servizi API SNMP.                                           |
| **NX_SNMP_DISABLE_V1**         | Definito, in questo modo viene rimossa l'elaborazione di SNMP versione 1 in *nxd_snmp. c.* Per impostazione predefinita, questo valore non è definito.                                                                                                                                                                         |
| **NX_SNMP_DISABLE_V2**         | Questa operazione consente di rimuovere tutte le elaborazioni di SNMP versione 2 in *nxd_snmp. c.* Per impostazione predefinita, questo valore non è definito.                                                                                                                                                                         |
| **NX_SNMP_DISABLE_V3**         | Questa operazione consente di rimuovere tutte le elaborazioni di SNMPv3 in *nxd_snmp. c.* Per impostazione predefinita, questo valore non è definito.                                                                                                                                                                                 |