---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo SNMP
description: L'implementazione SNMP di NetX Duo è quella di un agente SNMP. Un agente è responsabile della risposta ai comandi del gestore SNMP e dell'invio di trap basati su eventi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5760e35fdbe8d7b27e2ccc82abac37b1f6fb5118
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821686"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-snmp"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo SNMP

Il Simple Network Management Protocol (SNMP) è un protocollo progettato per gestire i dispositivi su Internet. SNMP è un protocollo che utilizza i servizi UDP (User Datagram Protocol) senza connessione per eseguire la relativa funzione di gestione. L'implementazione SNMP di Azure RTO NetX Duo è quella di un agente SNMP. Un agente è responsabile della risposta ai comandi del gestore SNMP e dell'invio di trap basati su eventi. 

NetX Duo SNMP supporta la comunicazione sia IPv4 che IPv6 con i gestori SNMP. Le applicazioni SNMP NetX devono essere compilate ed eseguite in NetX Duo SNMP. Tuttavia, lo sviluppatore è incoraggiato a trasferire le applicazioni SNMP esistenti usando i servizi "Duo" equivalenti. Quando si inviano messaggi trap SNMP, ad esempio, i seguenti servizi "Duo" devono sostituire il relativo equivalente NetX:

*nxd_snmp_object_trap_send*

*nxd_snmp_object_trapv2_send*

*nxd_snmp_object_trapv3_send*

Per ulteriori informazioni, vedere la **Descrizione dei servizi SNMP Agent** in altre parti di questo manuale dell'utente.

## <a name="netx-duo-snmp-agent-requirements"></a>Requisiti dell'agente SNMP NetX Duo

Per il pacchetto SNMP NetX Duo è necessario che sia già stata creata un'istanza IP. Inoltre, è necessario abilitare UDP nella stessa istanza di IP.

L'agente SNMP NetX Duo presenta diversi requisiti aggiuntivi. Per prima cosa, è necessario l'accesso alla porta 161 per la gestione di tutte le richieste di gestione SNMP. Richiede inoltre l'accesso alla porta 162 per l'invio di messaggi trap al responsabile.

Per usare l'agente SNMP NetX Duo con su IPv6 e per ottenere gli oggetti IPv6, è necessario abilitare IPv6 in NetX Duo. Per informazioni dettagliate sull'abilitazione dell'istanza IP per i servizi IPv6, vedere la ***Guida dell'utente di NETX Duo*** .

## <a name="netx-duo-snmp-constraints"></a>Vincoli SNMP NetX Duo

Il protocollo SNMP NetX Duo implementa SNMP versione 1, 2 e 3. L'implementazione di SNMPv3 supporta l'autenticazione MD5 e SHA e la crittografia DES. Questa versione dell'agente SNMP NetX Duo presenta i vincoli seguenti:

1. Un agente SNMP per ogni istanza IP di NetX
2. Nessun supporto per RMON
3. Il protocollo SNMP v3 informa che i messaggi non sono supportati
4. I tipi di dati OPAQUE e NSAP non sono supportati
5. Gli indirizzi IPv6 sono definiti come stringhe ottetto e il controllo del formato viene lasciato all'applicazione.

## <a name="snmp-object-names"></a>Nomi degli oggetti SNMP

Il protocollo SNMP è progettato per gestire i dispositivi su Internet. A tale scopo, ogni dispositivo gestito SNMP dispone di un set di oggetti definiti dalla struttura delle informazioni di gestione (SMI) in base a quanto definito da RFC 1155. La struttura è un tipo di struttura ad albero gerarchico simile al seguente:

![Diagramma della struttura delle informazioni di gestione.](media/image3.png)

Ogni nodo dell'albero è un oggetto. L'oggetto "DOD" nell'albero è identificato dalla notazione 1.3.6, mentre l'oggetto "Internet" nella struttura ad albero è identificato dalla notazione 1.3.6.1. Tutti i nomi degli oggetti SNMP iniziano con la notazione 1.3.6.

Un gestore SNMP utilizza questa notazione dell'oggetto per specificare l'oggetto nel dispositivo che si desidera ottenere o impostare. L'agente SNMP NetX Duo interpreta tali richieste di gestione e fornisce meccanismi che consentono all'applicazione di eseguire l'operazione richiesta.

## <a name="snmp-manager-requests"></a>Richieste di gestione SNMP

SNMP dispone di un meccanismo semplice per la gestione dei dispositivi. È disponibile un set di comandi SNMP standard rilasciati da gestione SNMP al dispositivo SNMP sulla *porta 161*. Di seguito sono riportati alcuni dei comandi di base di SNMP Manager:

| Comando SNMP | Significato                                                        |
|--------------|----------------------------------------------------------------|
| GET          | *Ottenere l'oggetto specificato*                                       |
| GETNEXT      | *Ottiene l'oggetto logico successivo dopo l'ID oggetto specificato*      |
| GETBULK      | *Ottenere più oggetti logici dopo l'ID oggetto specificato* |
| SET          | *Imposta l'oggetto specificato*                                       |

Questi comandi sono codificati in formato ASN. 1 (Abstract Syntax Notation One) e si trovano nel payload del pacchetto UDP inviato da gestione SNMP. L'agente SNMP NetX Duo elabora la richiesta e quindi chiama la corrispondente routine di gestione specificata nella chiamata ***nx_snmp_agent_create*** .

## <a name="netx-duo-snmp-agent-traps"></a>Trap agente SNMP NetX Duo

L'agente SNMP NetX Duo consente inoltre di avvisare un gestore SNMP di eventi in modo asincrono. Questa operazione viene eseguita tramite un comando trap SNMP. È disponibile un'API univoca per ogni versione di SNMP per l'invio di trap a un gestore SNMP. Per impostazione predefinita, i trap vengono inviati al gestore SNMP sulla porta 162.

L'agente SNMP NetX Duo fornisce chiavi di sicurezza separate per i messaggi trap SNMPv3. A tale scopo, l'applicazione SNMP deve creare un set separato di chiavi da quelle applicate alle risposte alle richieste di gestione. Trap Security consente all'agente SNMP di usare le stesse password o password diverse per l'autenticazione e la privacy. Per ulteriori informazioni sulla creazione di chiavi di sicurezza, vedere **autenticazione e crittografia SNMP di NETX Duo** nella sezione successiva.

Un elenco di variabili trap SNMP standard è enumerato nella parte superiore di *nxd_snmp. h:*

| Variabili                                 | Valore  |
|-------------------------------------------|---|
| #define NX_SNMP_TRAP_COLDSTART            | 0 |
| #define NX_SNMP_TRAP_WARMSTART            | 1 |
| #define NX_SNMP_TRAP_LINKDOWN             | 2 |
| #define NX_SNMP_TRAP_LINKUP               | 3 |
| #define NX_SNMP_TRAP_AUTHENTICATE_FAILURE | 4 |
| #define NX_SNMP_TRAP_EGPNEIGHBORLOSS      | 5 |
| #define NX_SNMP_TRAP_ENTERPRISESPECIFIC   | 6 |

Per includere queste variabili nel messaggio trap, l'argomento di input trap_type in *nx_snmp_agent_trapv2_send* (SNMPv2) o *nx_snmp_agent_trapv3_send* (SNMPv3) viene impostato sul valore enumerato di queste variabili. Di seguito è riportato un esempio per SNMPv2 per notificare al gestore SNMP un evento di avvio a freddo:

```c
UINT trap_type = NX_SNMP_TRAP_COLDSTART;

status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                  (UCHAR *)"public", trap_type,
                                  tx_time_get(), NX_NULL);

```

Per includere variabili proprietarie nel messaggio trap, l'argomento di input trap_type è impostato su NX_SNMP_TRAP_CUSTOM e l'argomento di input trap List contiene i dati proprietari. Si noti che il messaggio trap conterrà come ora di sistema (1.3.6.1.6.3.1.1.4.1.0). Di seguito viene illustrato un esempio per SNMPv2:

```c
NX_SNMP_TRAP_OBJECT trap_list[3];
NX_SNMP_OBJECT_DATA trap_data0;

    /* Load the data into the OBJECT. */
    nx_snmp_object_id_get((void*)"1.3.6.1.4.1.7428.1.3.2.0", &trap_data0);

    /* Update the Trap Object with the object and OID. */
    trap_list[0].nx_snmp_object_string_ptr = (UCHAR *)"1.3.6.1.6.3.1.1.4.0";
    trap_list[0].nx_snmp_object_data  = &trap_data0;

    /* Null terminate the trap list. */
    trap_list[1].nx_snmp_object_string_ptr = NX_NULL;

    status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                      (UCHAR *)"trapduo",
                                      NX_SNMP_TRAP_CUSTOM,
                                      tx_time_get(), trap_list);
```

## <a name="netx-duo-snmp-authentication-and-encryption"></a>Autenticazione e crittografia SNMP di NetX Duo

Esistono due tipi di autenticazione, ovvero *Basic* e *digest*. L'autenticazione di base equivale a una semplice autenticazione del *nome utente* in testo normale trovata in molti protocolli. Nell'autenticazione SNMP di base l'utente verifica semplicemente che il nome utente fornito sia valido per l'esecuzione di operazioni SNMP. L'autenticazione di base è l'unica opzione per SNMP versioni 1 e 2.

Lo svantaggio principale dell'autenticazione di base è che il nome utente viene trasmesso in testo normale. L'autenticazione del digest SNMPv3 risolve questo problema senza trasmettere mai il nome utente in testo normale. Viene invece usato un algoritmo per derivare un'digest ' a 96 bit dal nome utente, dal motore di contesto e da altre informazioni. L'agente SNMP NetX Duo supporta sia gli algoritmi MD5 che quelli del digest SHA.

Per abilitare l'autenticazione, l'agente SNMP deve impostare l'ID del motore di contesto utilizzando il servizio *nx_snmp_agent_context_engine_set* . L'ID del motore di contesto viene usato nella creazione della chiave di autenticazione.

La crittografia dei dati di SNMPv3 è disponibile tramite l'algoritmo DES. Per la crittografia è necessaria l'abilitazione dell'autenticazione (non è possibile crittografare i dati senza impostare i parametri di autenticazione).

Per creare le chiavi di autenticazione e privacy, vengono usate le API seguenti:

```c
UINT  _nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)

UINT  _nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)
```

Successivamente, è necessario configurare l'agente SNMP per l'utilizzo di queste chiavi. Per registrare una chiave con l'agente SNMP, vengono usate le API seguenti:

```c
UINT  _nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr,
                                          NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr,
                                    NX_SNMP_SECURITY_KEY *key)
```

È possibile creare chiavi separate per i messaggi trap. Per applicare le chiavi per i messaggi trap, sono disponibili le API seguenti:

```c
UINT  _nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)
```

Per disabilitare l'autenticazione o la crittografia per i messaggi di risposta e i trap di invio, usare questi servizi con l'input del puntatore alla chiave impostato su NULL.

## <a name="netx-duo-snmp-community-strings"></a>Stringhe della community SNMP di NetX Duo

L'agente SNMP NetX Duo supporta sia le stringhe di community pubbliche che private. La stringa pubblica viene impostata con il servizio *nx_snmp_agent _public_string_set* . La stringa privata dell'agente SNMP NetX Duo viene impostata tramite il servizio *nx_snmp_agent_private_string_set* .

## <a name="netx-duo-snmp-username-callback"></a>Callback nome utente SNMP NetX Duo

Il pacchetto dell'agente SNMP NetX Duo consente all'applicazione di specificare (tramite la chiamata ***nx_snmp_agent_create*** ) un callback del nome utente che viene chiamato all'inizio della gestione di ogni richiesta del client SNMP.

La routine di callback fornisce l'agente SNMP NetX Duo con il nome utente. Se il nome utente specificato è valido o se non è necessario un controllo nome utente per la risposta alla richiesta, il callback del nome utente deve restituire il valore di **NX_SUCCESS**. In caso contrario, la routine deve restituire **NX_SNMP_ERROR** per indicare che il nome utente specificato non è valido.

Il formato della routine di callback del nome utente dell'applicazione è definito di seguito:

```c
UINT nx_snmp_agent_username_process(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *username);
```

I parametri di input sono definiti come segue:

| Parametro | Significato                                              |
|-----------|------------------------------------------------------|
| *agent_ptr* | Puntatore alla chiamata dell'agente SNMP                        |
| username  | Destinazione per il puntatore al nome utente richiesto |

Per le sessioni SNMPv1 e SNMPv2/v2C, l'applicazione vuole esaminare la stringa della community in una richiesta SNMP in ingresso per determinare se la richiesta SNMP ha una stringa community valida. Sono disponibili diversi servizi per l'applicazione SNMP.

L'applicazione SNMP può verificare se la richiesta corrente di gestione SNMP è GET, ad esempio GET, GetNext o GetBulk, oppure impostare il tipo di richiesta utilizzando questo servizio:

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

Se la richiesta è un tipo GET, l'applicazione dovrà confrontare la stringa della community di input con la stringa pubblica dell'agente SNMP:

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr,
                                      UCHAR *username,
                                      UINT *is_public);
```

Analogamente, se la richiesta è un tipo SET, l'applicazione dovrà confrontare la stringa della community di input con la stringa privata dell'agente SNMP:

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr,
                                       UCHAR *username,
                                       UINT *is_private);
```

I valori restituiti is_public e is_private indicano rispettivamente se la stringa della community di input è una stringa community pubblica o privata valida.

Il valore restituito dalla routine di callback username indica se il nome utente è valido. Il valore **NX_SUCCESS** viene restituito se il nome utente è valido oppure **NX_SNMP_ERROR** se il nome utente non è valido.

## <a name="netx-duo-snmp-agent-get-callback"></a>Callback di GET dell'agente SNMP NetX Duo

L'applicazione deve impostare una routine di callback per la gestione delle richieste di oggetti GET da gestione SNMP. Il callback recupera il valore dell'oggetto specificato nella richiesta.

La routine di callback di richiesta GET dell'applicazione è definita di seguito:

```c
UINT nx_snmp_agent_get_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

I parametri di input sono definiti come segue:

| Parametro        | Significato |
|------------------|----------------------------------|
| *agent_ptr*        | Puntatore alla chiamata dell'agente SNMP |
| object_requested | Stringa ASCII che rappresenta l'ID oggetto a cui è destinata l'operazione GET. |
| object_data      | Struttura dei dati per conservare il valore recuperato dal callback. Questa impostazione può essere configurata con una serie di API SNMP NetX Duo descritta di seguito. |

> [!NOTE]
> *Per le stringhe di ottetti, all'oggetto deve essere assegnata la lunghezza in modo che la funzione interna sappia quanto tempo la lunghezza è perché il callback stesso non ha un argomento length:*

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

Poiché il tipo di dati non è noto al callback GET, non è necessario controllare il tipo di dati. La lunghezza non avrà alcun effetto sui tipi numerici o sulle stringhe delimitate da valori null.

Chiamare quindi la funzione interna:

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

Se la funzione di callback non riesce a trovare l'oggetto richiesto, viene restituito il codice di errore **NX_SNMP_ERROR_NOSUCHNAME** . Se viene rilevato un altro errore, è necessario che venga restituito il **NX_SNMP_ERROR** .

## <a name="netx-duo-snmp-agent-getnext-callback"></a>Callback GetNext Agent NetX Duo SNMP

L'applicazione deve inoltre impostare la routine di callback per le richieste di oggetti GetNext da gestione SNMP. Il callback GetNext Recupera il valore dell'oggetto successivo specificato dalla richiesta.

La routine di callback di richiesta GetNext dell'applicazione è definita di seguito:

```c
UINT nx_snmp_agent_getnext_process(NX_SNMP_AGENT *agent_ptr,
                                   UCHAR *object_requested,
                                   NX_SNMP_OBJECT_DATA *object_data);
```

I parametri di input sono definiti come segue:

| Parametro        | Significato |
|------------------|-------------------------------------------|
| *agent_ptr*        | Puntatore alla chiamata dell'agente SNMP |
| object_requested | Stringa ASCII che rappresenta l'ID oggetto a cui è destinata l'operazione GetNext. |
| object_data      | Struttura dei dati per conservare il valore recuperato dal callback. Questa impostazione può essere configurata con una serie di API SNMP NetX Duo descritta di seguito. |

Analogamente a quanto avviene per i callback GET, è necessario assegnare a oggetti con dati stringa ottetto la lunghezza, in modo che la funzione interna sappia quanto tempo la lunghezza è perché il callback stesso non ha un argomento length:

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

Poiché il tipo di dati non è noto al callback GET, non è necessario controllare il tipo di dati. La lunghezza non avrà alcun effetto sui tipi numerici o sulle stringhe delimitate da valori null.

Chiamare quindi la funzione interna:

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

Se la funzione di callback non riesce a trovare l'oggetto richiesto, viene restituito il codice di errore **NX_SNMP_ERROR_NOSUCHNAME** . Se viene rilevato un altro errore, è necessario che venga restituito il **NX_SNMP_ERROR** .

## <a name="netx-duo-snmp-agent-set-callback"></a>Callback SET agenti SNMP NetX Duo

L'applicazione deve impostare la routine di callback per la gestione delle richieste di oggetti SET da gestione SNMP. Il callback SET imposta il valore dell'oggetto specificato dalla richiesta.

La routine di callback della richiesta del SET di applicazioni è definita di seguito:

```c
UINT nx_snmp_agent_set_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

I parametri di input sono definiti come segue:

| Parametro        | Significato |
|------------------|-------- |
| *agent_ptr*      | Puntatore alla chiamata dell'agente SNMP |
| object_requested | Stringa ASCII che rappresenta l'ID oggetto a cui è destinata l'operazione di impostazione. |
| object_data      | Struttura di dati che contiene il nuovo valore per l'oggetto specificato. L'operazione effettiva può essere eseguita usando l'API SNMP NetX Duo descritta di seguito. |

Si noti che per le stringhe ottetto, il callback SET deve aggiornare la tabella MIB con la lunghezza dei dati, perché l'agente SNMP ha analizzato i dati e conosce il tipo e la lunghezza:

```c
if (object_data -> nx_snmp_object_data_type ==
                           NX_SNMP_ANS1_OCTET_STRING)
{
    mib2_mib[i].length =
        object_data -> nx_snmp_object_octet_string_size;
}

object_data -> nx_snmp_object_octet_string_size =
                                 mib2_mib[i].length;
```

Se la funzione di callback non riesce a trovare l'oggetto richiesto, viene restituito il codice di errore **NX_SNMP_ERROR_NOSUCHNAME** .

Se l'host SNMP NetX duo ha creato stringhe di community private e il mittente SNMP della richiesta SET non ha la stringa privata corrispondente, può restituire un errore **NX_SNMP_ERROR_NOACCESS** . Se viene rilevato un altro errore, è necessario che venga restituito il **NX_SNMP_ERROR** .

> [!NOTE]
> *Sebbene l'agente SNMP di NetX Duo fornisca un database MIB SNMP con la distribuzione, è principalmente a scopo di test e sviluppo. È probabile che lo sviluppatore richieda un database MIB proprietario per un'applicazione SNMP professionale.*

## <a name="changing-snmp-version-at-run-time"></a>Modifica della versione di SNMP in fase di esecuzione

L'host agente SNMP può modificare la versione SNMP per ognuna delle tre versioni in fase di esecuzione utilizzando il servizio *nx_snmp_agent_set_version* . Per impostazione predefinita, l'agente SNMP è abilitato per tutte e tre le versioni quando viene creato l'agente SNMP in *nx_snmp_agent_create*. Tuttavia, l'applicazione può limitarla a un subset di tutte le versioni.

> [!NOTE]
> *Se le opzioni di configurazione NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 e/o NX_SNMP_DISABLE_V3 sono definite, questa funzione non avrà alcun effetto sull'abilitazione delle versioni effettive.*

L'agente SNMP può recuperare la versione SNMP del pacchetto SNMP più recente ricevuto tramite il servizio *nx_snmp_agent_get_current_version* .

## <a name="snmpv3-discovery"></a>Individuazione SNMPv3

L'agente SNMP, se abilitato per SNMPv3, risponderà alle richieste di individuazione da gestione SNMP. Tale richiesta contiene i dati dei parametri di sicurezza con valori null per l'ID del motore autorevole, il nome utente, il numero di avvio e l'ora di avvio. I parametri di autenticazione non vengono applicati al messaggio di individuazione. L'elenco di associazioni variabili nella richiesta è vuoto (contiene zero elementi). L'agente SNMP risponde con un'ora di avvio e un conteggio pari a zero e l'elenco di associazioni di variabili contenente 1 elemento, *usmStatsUnknownEngineIDs*, che corrisponde al numero di richieste ricevute con un ID di motore sconosciuto (null). Alla successiva richiesta GetNext dal browser o dal gestore, i dati di avvio e i parametri di sicurezza vengono compilati solo se è abilitata la sicurezza. In tal caso, verrà inviato anche un aggiornamento dei dati di NotInTime in PDU. I parametri di sicurezza, ad esempio l'autenticazione, dimostrano l'identità dell'agente al responsabile.

Informazioni più dettagliate sull'autenticazione SNMPv3 sono disponibili in RFC 3414 "user-based Security Model (USM) per la versione 3 del Simple Network Management Protocol (SNMPv3)".

## <a name="netx-duo-snmp-rfcs"></a>RFC SNMP NetX Duo

NetX Duo SNMP è conforme a RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 e RFC correlate.
