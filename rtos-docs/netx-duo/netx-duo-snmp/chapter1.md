---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo SNMP
description: L'implementazione SNMP di NetX Duo è quella di un agente SNMP. Un agente è responsabile della risposta ai comandi di SNMP Manager e dell'invio di trap guidati da eventi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6bf18efacc5ff7773e038a5140fc886e978ebd1ca59cc9b861139b3ce2d9ada6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797866"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-snmp"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo SNMP

Il Simple Network Management Protocol (SNMP) è un protocollo progettato per la gestione dei dispositivi su Internet. SNMP è un protocollo che utilizza i servizi UDP (User Datagram Protocol) senza connessione per eseguire la funzione di gestione. L Azure RTOS'implementazione SNMP di NetX Duo è quella di un agente SNMP. Un agente è responsabile della risposta ai comandi di SNMP Manager e dell'invio di trap guidati da eventi. 

NetX Duo SNMP supporta sia le comunicazioni IPv4 che IPv6 con i gestori SNMP. Le applicazioni SNMP NetX devono essere compilate ed eseguite in NetX Duo SNMP. Tuttavia, lo sviluppatore è invitato a convertire le applicazioni SNMP esistenti all'uso dei servizi "duo" equivalenti. Ad esempio, quando si inviano messaggi trap SNMP, i servizi "duo" seguenti devono sostituire l'equivalente NetX:

*nxd_snmp_object_trap_send*

*nxd_snmp_object_trapv2_send*

*nxd_snmp_object_trapv3_send*

Per altre informazioni, vedere **Descrizione dei servizi agente SNMP** in altre parti di questo Manuale dell'utente.

## <a name="netx-duo-snmp-agent-requirements"></a>Requisiti dell'agente SNMP di NetX Duo

Il pacchetto SNMP di NetX Duo richiede che sia già stata creata un'istanza IP. Inoltre, UDP deve essere abilitato nella stessa istanza IP.

NetX Duo SNMP Agent ha diversi requisiti aggiuntivi. Prima di tutto, richiede l'accesso alla porta 161 per la gestione di tutte le richieste di gestione SNMP. Richiede anche l'accesso alla porta 162 per l'invio di messaggi trap al manager.

Per usare NetX Duo SNMP Agent con su IPv6 e per ottenere oggetti IPv6, IPv6 deve essere abilitato in NetX Duo. Per informazioni ***dettagliate sull'abilitazione*** dell'istanza IP per i servizi IPv6, vedere la Guida dell'utente di NetX Duo.

## <a name="netx-duo-snmp-constraints"></a>Vincoli SNMP di NetX Duo

Il protocollo SNMP di NetX Duo implementa SNMP versione 1, 2 e 3. L'implementazione SNMPv3 supporta l'autenticazione MD5 e SHA e la crittografia DES. Questa versione di NetX Duo SNMP Agent presenta i vincoli seguenti:

1. Un agente SNMP per ogni istanza IP NetX
2. Nessun supporto per RMON
3. I messaggi SNMP v3 Inform non sono supportati
4. I tipi di dati OPAQUE e NSAP non sono supportati
5. Gli indirizzi IPv6 sono definiti come stringhe di ottetti e il controllo del formato viene lasciato all'applicazione.

## <a name="snmp-object-names"></a>Nomi degli oggetti SNMP

Il protocollo SNMP è progettato per gestire i dispositivi su Internet. A tale scopo, ogni dispositivo gestito SNMP ha un set di oggetti definiti dalla struttura delle informazioni di gestione (SMI) come definito da RFC 1155. La struttura è un tipo di albero gerarchico di struttura simile al seguente:

![Diagramma della struttura delle informazioni di gestione.](media/image3.png)

Ogni nodo nell'albero è un oggetto . L'oggetto "dod" nell'albero è identificato dalla notazione 1.3.6, mentre l'oggetto "internet" nell'albero è identificato dalla notazione 1.3.6.1. Tutti i nomi di oggetto SNMP iniziano con la notazione 1.3.6.

SNMP Manager usa questa notazione dell'oggetto per specificare l'oggetto nel dispositivo che vuole ottenere o impostare. L'agente SNMP di NetX Duo interpreta tali richieste di gestione e fornisce meccanismi per l'applicazione per eseguire l'operazione richiesta.

## <a name="snmp-manager-requests"></a>Richieste di SNMP Manager

SNMP ha un meccanismo semplice per la gestione dei dispositivi. È disponibile un set di comandi SNMP standard emessi da SNMP Manager al dispositivo SNMP *sulla porta 161.* Di seguito sono illustrati alcuni dei comandi di base di SNMP Manager:

| Comando SNMP | Significato                                                        |
|--------------|----------------------------------------------------------------|
| GET          | *Ottiene l'oggetto specificato*                                       |
| Getnext      | *Ottiene l'oggetto logico successivo dopo l'ID oggetto specificato*      |
| GETBULK      | *Ottiene più oggetti logici dopo l'ID oggetto specificato* |
| SET          | *Impostare l'oggetto specificato*                                       |

Questi comandi sono codificati nel formato ASN.1 (Abstract Syntax Notation One) e risiedono nel payload del pacchetto UDP inviato da Gestione SNMP. NetX Duo SNMP Agent elabora la richiesta e quindi chiama la routine di gestione corrispondente specificata nella nx_snmp_agent_create ***chiamata.***

## <a name="netx-duo-snmp-agent-traps"></a>Trap dell'agente SNMP di NetX Duo

L'agente SNMP di NetX Duo offre la possibilità di avvisare anche un gestore SNMP di eventi in modo asincrono. Questa operazione viene eseguita tramite un comando trap SNMP. Esiste un'API univoca per ogni versione di SNMP per l'invio di trap a SNMP Manager. Per impostazione predefinita, le trap vengono inviate a SNMP Manager sulla porta 162.

NetX Duo SNMP Agent fornisce chiavi di sicurezza separate per i messaggi trap SNMPv3. A tale scopo, l'applicazione SNMP deve creare un set separato di chiavi da quelle applicate alle risposte alle richieste manager. La sicurezza trap consente all'agente SNMP di usare le stesse password o password diverse per l'autenticazione e la privacy. Per altre informazioni sulla creazione di chiavi di sicurezza, vedere Autenticazione e crittografia **SNMP di NetX Duo** nella sezione successiva.

Nella parte superiore di *nxd_snmp.h* viene enumerato un elenco di variabili trap SNMP standard:

| Variabili                                 | Valore  |
|-------------------------------------------|---|
| #define NX_SNMP_TRAP_COLDSTART            | 0 |
| #define NX_SNMP_TRAP_WARMSTART            | 1 |
| #define NX_SNMP_TRAP_LINKDOWN             | 2 |
| #define NX_SNMP_TRAP_LINKUP               | 3 |
| #define NX_SNMP_TRAP_AUTHENTICATE_FAILURE | 4 |
| #define NX_SNMP_TRAP_EGPNEIGHBORLOSS      | 5 |
| #define NX_SNMP_TRAP_ENTERPRISESPECIFIC   | 6 |

Per includere queste variabili nel messaggio trap, l'argomento di input trap_type in *nx_snmp_agent_trapv2_send* (SNMPv2) o *nx_snmp_agent_trapv3_send* (SNMPv3) viene impostato sul valore enumerato di queste variabili. Di seguito è riportato un esempio in cui SNMPv2 invia una notifica a SNMP Manager di un evento di avvio a freddo:

```c
UINT trap_type = NX_SNMP_TRAP_COLDSTART;

status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                  (UCHAR *)"public", trap_type,
                                  tx_time_get(), NX_NULL);

```

Per includere variabili proprietarie nel messaggio trap, l'argomento trap_type di input è impostato su NX_SNMP_TRAP_CUSTOM e l'argomento di input dell'elenco trap contiene i dati proprietari. Si noti che il messaggio trap conterrà come tempo di esecuzione del sistema (1.3.6.1.6.3.1.1.4.1.0). Di seguito è riportato un esempio per SNMPv2:

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

Esistono due tipi di autenticazione, ad esempio *basic e* *digest.* L'autenticazione di base equivale a una semplice autenticazione del *nome utente* in testo normale disponibile in molti protocolli. Nell'autenticazione di base SNMP, l'utente verifica semplicemente che il nome utente fornito sia valido per l'esecuzione di operazioni SNMP. L'autenticazione di base è l'unica opzione per SNMP versioni 1 e 2.

Lo svantaggio principale dell'autenticazione di base è che il nome utente viene trasmesso in testo normale. L'autenticazione del digest SNMPv3 risolve questo problema non trasmettendo mai il nome utente in testo normale. Viene invece usato un algoritmo per derivare un 'digest' a 96 bit dal nome utente, dal motore di contesto e da altre informazioni. NetX Duo SNMP Agent supporta gli algoritmi digest MD5 e SHA.

Per abilitare l'autenticazione, l'agente SNMP deve impostare l'ID del motore di contesto usando *nx_snmp_agent_context_engine_set* servizio. L'ID del motore di contesto viene usato nella creazione della chiave di autenticazione.

La crittografia dei dati SNMPv3 è disponibile usando l'algoritmo DES. La crittografia richiede che l'autenticazione sia abilitata (non è possibile crittografare i dati senza impostare i parametri di autenticazione).

Per creare chiavi di autenticazione e privacy, viene usata l'API seguente:

```c
UINT  _nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)

UINT  _nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)
```

Successivamente, l'agente SNMP deve essere configurato per l'uso di queste chiavi. Per registrare una chiave con l'agente SNMP, viene usata l'API seguente:

```c
UINT  _nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr,
                                          NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr,
                                    NX_SNMP_SECURITY_KEY *key)
```

È possibile creare chiavi separate per i messaggi trap. Per applicare le chiavi per i messaggi trap sono disponibili le API seguenti:

```c
UINT  _nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)
```

Per disabilitare l'autenticazione o la crittografia per i messaggi di risposta e l'invio di trap, usare questi servizi con l'input del puntatore della chiave impostato su NULL.

## <a name="netx-duo-snmp-community-strings"></a>Stringhe Community SNMP di NetX Duo

NetX Duo SNMP Agent supporta le stringhe della community pubblica e privata. La stringa pubblica viene impostata con il *nx_snmp_agent _public_string_set* servizio. La stringa privata dell'agente SNMP di NetX Duo viene impostata usando il *nx_snmp_agent_private_string_set* servizio.

## <a name="netx-duo-snmp-username-callback"></a>Callback del nome utente SNMP di NetX Duo

Il pacchetto NetX Duo SNMP Agent consente all'applicazione di specificare (tramite la chiamata ***nx_snmp_agent_create)*** un callback del nome utente chiamato all'inizio della gestione di ogni richiesta client SNMP.

La routine di callback fornisce all'agente SNMP di NetX Duo il nome utente. Se il nome utente fornito è valido o se non è necessario alcun controllo del nome utente per rispondere alla richiesta, il callback del nome utente deve restituire il valore **di NX_SUCCESS**. In caso contrario, la routine **deve** restituire NX_SNMP_ERROR per indicare che il nome utente specificato non è valido.

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

Per le sessioni SNMPv1 e SNMPv2/v2C, l'applicazione dovrà esaminare la stringa della community in una richiesta SNMP in ingresso per determinare se la richiesta SNMP ha una stringa di community valida. A tale scopo, l'applicazione SNMP può eseguire diversi servizi.

L'applicazione SNMP può richiedere se la richiesta corrente di SNMP Manager è un tipo GET (ad esempio GET, GETNEXT o GETBULK) o SET di richiesta che usa questo servizio:

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

Se la richiesta è di tipo GET, l'applicazione dovrà confrontare la stringa della community di input con la stringa pubblica dell'agente SNMP:

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr,
                                      UCHAR *username,
                                      UINT *is_public);
```

Analogamente, se la richiesta è di tipo SET, l'applicazione dovrà confrontare la stringa della community di input con la stringa privata dell'agente SNMP:

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr,
                                       UCHAR *username,
                                       UINT *is_private);
```

I is_public e is_private valori restituiti indicano rispettivamente se la stringa della community di input è una stringa di community pubblica o privata valida.

Il valore restituito della routine di callback del nome utente indica se il nome utente è valido. Il valore **NX_SUCCESS** viene restituito se il nome utente è valido o NX_SNMP_ERROR **se** il nome utente non è valido.

## <a name="netx-duo-snmp-agent-get-callback"></a>Callback GET dell'agente SNMP di NetX Duo

L'applicazione deve impostare una routine di callback per la gestione delle richieste di oggetti GET da Gestione SNMP. Il callback recupera il valore dell'oggetto specificato nella richiesta.

La routine di callback della richiesta GET dell'applicazione è definita di seguito:

```c
UINT nx_snmp_agent_get_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

I parametri di input sono definiti come segue:

| Parametro        | Significato |
|------------------|----------------------------------|
| *agent_ptr*        | Puntatore alla chiamata dell'agente SNMP |
| object_requested | Stringa ASCII che rappresenta l'ID oggetto per cui si trova l'operazione GET. |
| object_data      | Struttura dei dati per contenere il valore recuperato dal callback. Questa impostazione può essere impostata con una serie di API SNMP di NetX Duo descritte di seguito. |

> [!NOTE]
> *Per le stringhe di ottetti, all'oggetto deve essere assegnata la lunghezza in modo che la funzione interna conosca la lunghezza perché il callback stesso non ha un argomento length:*

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

Poiché il tipo di dati non è noto al callback GET, non è necessario controllare il tipo di dati. La lunghezza non avrà alcun effetto sui tipi numerici o sulle stringhe delimitate da Null.

Chiamare quindi la funzione interna:

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

Se la funzione di callback non riesce a trovare l'oggetto richiesto, **NX_SNMP_ERROR_NOSUCHNAME** restituito il codice di errore. Se viene rilevato un altro errore, NX_SNMP_ERROR **deve** essere restituito.

## <a name="netx-duo-snmp-agent-getnext-callback"></a>Callback GETNEXT dell'agente SNMP di NetX Duo

L'applicazione deve anche impostare la routine di callback per le richieste di oggetti GETNEXT da Gestione SNMP. Il callback GETNEXT recupera il valore dell'oggetto successivo specificato dalla richiesta.

La routine di callback della richiesta GETNEXT dell'applicazione è definita di seguito:

```c
UINT nx_snmp_agent_getnext_process(NX_SNMP_AGENT *agent_ptr,
                                   UCHAR *object_requested,
                                   NX_SNMP_OBJECT_DATA *object_data);
```

I parametri di input sono definiti come segue:

| Parametro        | Significato |
|------------------|-------------------------------------------|
| *agent_ptr*        | Puntatore alla chiamata dell'agente SNMP |
| object_requested | Stringa ASCII che rappresenta l'ID oggetto per cui si trova l'operazione GETNEXT. |
| object_data      | Struttura dei dati per contenere il valore recuperato dal callback. Questa impostazione può essere impostata con una serie di API SNMP di NetX Duo descritte di seguito. |

Come per i callback GET, agli oggetti con dati stringa ottetti deve essere assegnata la lunghezza in modo che la funzione interna sappia per quanto tempo è lunga perché il callback stesso non ha un argomento length:

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

Poiché il tipo di dati non è noto al callback GET, non è necessario controllare il tipo di dati. La lunghezza non avrà alcun effetto sui tipi numerici o sulle stringhe delimitate da Null.

Chiamare quindi la funzione interna:

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

Se la funzione di callback non riesce a trovare l'oggetto richiesto, **NX_SNMP_ERROR_NOSUCHNAME** restituito il codice di errore. Se viene rilevato un altro errore, NX_SNMP_ERROR **deve** essere restituito.

## <a name="netx-duo-snmp-agent-set-callback"></a>Callback SET dell'agente SNMP di NetX Duo

L'applicazione deve impostare la routine di callback per la gestione delle richieste di oggetti SET da Gestione SNMP. Il callback SET imposta il valore dell'oggetto specificato dalla richiesta.

La routine di callback della richiesta SET dell'applicazione è definita di seguito:

```c
UINT nx_snmp_agent_set_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

I parametri di input sono definiti come segue:

| Parametro        | Significato |
|------------------|-------- |
| *agent_ptr*      | Puntatore alla chiamata dell'agente SNMP |
| object_requested | Stringa ASCII che rappresenta l'ID oggetto per cui si trova l'operazione SET. |
| object_data      | Struttura dei dati che contiene il nuovo valore per l'oggetto specificato. L'operazione effettiva può essere eseguita usando l'API SNMP di NetX Duo descritta di seguito. |

Si noti che per le stringhe di ottetti, il callback SET deve aggiornare la tabella MIB con la lunghezza dei dati poiché l'agente SNMP ha analizzato i dati e conosce il tipo e la lunghezza:

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

Se la funzione di callback non riesce a trovare l'oggetto richiesto, **NX_SNMP_ERROR_NOSUCHNAME** restituito il codice di errore.

Se l'host SNMP NetX Duo ha creato stringhe di community private e il mittente SNMP della richiesta SET non ha la stringa privata corrispondente, potrebbe restituire un NX_SNMP_ERROR_NOACCESS **errore.** Se viene rilevato un altro errore, NX_SNMP_ERROR **deve** essere restituito.

> [!NOTE]
> *Anche se NetX Duo SNMP Agent fornisce un database MIB SNMP con la distribuzione, è principalmente a scopo di test e sviluppo. Lo sviluppatore richiederà probabilmente un database MIB proprietario per un'applicazione SNMP professionale.*

## <a name="changing-snmp-version-at-run-time"></a>Modifica della versione SNMP in fase di esecuzione

L'host dell'agente SNMP può modificare la versione SNMP per ognuna delle tre versioni in fase di esecuzione usando il *nx_snmp_agent_set_version* locale. L'agente SNMP è abilitato per impostazione predefinita per tutte e tre le versioni quando l'agente SNMP viene creato in *nx_snmp_agent_create*. Tuttavia, l'applicazione può limitarsi a un subset di tutte le versioni.

> [!NOTE]
> *Se le opzioni di NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 e/o NX_SNMP_DISABLE_V3 sono definite, questa funzione non avrà alcun effetto abilitando le versioni effettive.*

L'agente SNMP può recuperare la versione SNMP dell'ultimo pacchetto SNMP ricevuto usando il *nx_snmp_agent_get_current_version* servizio.

## <a name="snmpv3-discovery"></a>Individuazione SNMPv3

L'agente SNMP, se abilitato per SNMPv3, risponderà alle richieste di individuazione da Gestione SNMP. Tale richiesta contiene i dati dei parametri di sicurezza con valori Null per ID motore autorevole, nome utente, numero di avvio e ora di avvio. I parametri di autenticazione non vengono applicati al messaggio DISCOVERY. L'elenco di binding delle variabili nella richiesta è vuoto (contiene zero elementi). L'agente SNMP risponde con un tempo di avvio e un conteggio pari a zero e l'elenco di binding delle variabili contenente 1 elemento, *usmStatsUnknownEngineIDs*, ovvero il numero di richieste ricevute con un ID motore sconosciuto (Null). Alla successiva richiesta GETNEXT da Browser/Manager, i dati di avvio e i parametri di sicurezza vengono compilati solo se la sicurezza è abilitata. In tal caso, invierà anche un aggiornamento dei dati NotInTime nella PDU. I parametri di sicurezza, ad esempio l'autenticazione, dimostrano l'identità dell'agente al manager.

Informazioni più dettagliate sull'autenticazione SNMPv3 sono disponibili in RFC 3414 "User-based Security Model (USM) for version 3 of the Simple Network Management Protocol (SNMPv3)".

## <a name="netx-duo-snmp-rfcs"></a>RFC SNMP di NetX Duo

NetX Duo SNMP è conforme a RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 e RFC 3414 correlate.
