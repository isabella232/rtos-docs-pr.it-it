---
title: Capitolo 4-Descrizione dei servizi sicuri di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi protetti NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89761ec3438b1b16c1a603764bf7d4e1eac1b4ea
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822853"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a>Capitolo 4-Descrizione dei servizi sicuri di Azure RTO NetX

Questo capitolo contiene una descrizione di tutti i servizi protetti di Azure RTO NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni API seguenti i valori in **grassetto** non sono interessati dalla macro **NX_SECURE_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- [nx_secure_crypto_table_self_test](#nx_secure_crypto_table_self_test)
  - Eseguire self_test sui metodi di crittografia
- [nx_secure_module_hash_compute](#nx_secure_module_hash_compute)
  - Calcola il valore hash utilizzando user_supplied funzione hash
- [nx_secure_tls_active_certificate_set](#nx_secure_tls_active_certificate_set)
  - Impostare il certificato di identità attivo per una sessione TLS protetta NetX
- [nx_secure_tls_client_psk_set](#nx_secure_tls_client_psk_set)
  - Impostare una chiave di Pre_Shared per una sessione client TLS sicura NetX
- [nx_secure_tls_initialize](#nx_secure_tls_initialize)
  - Inizializza il modulo TLS sicuro NetX]
- [nx_secure_tls_local_certificate_add](#nx_secure_tls_local_certificate_add)
  - Aggiungere un certificato locale a una sessione TLS protetta NetX
- [nx_secure_tls_local_certificate_find](#nx_secure_tls_local_certificate_find)
  - Trovare un certificato locale in una sessione TLS sicura NetX per nome comune
- [nx_secure_tls_local_certificate_remove](#nx_secure_tls_local_certificate_remove)
  - Rimuovere il certificato locale dalla sessione TLS protetta NetX
- [nx_secure_tls_metadata_size_calculate](#nx_secure_tls_metadata_size_calculate)
  - Calcolo delle dimensioni dei metadati crittografici per una sessione TLS sicura NetX
- [nx_secure_tls_packet_allocate](#nx_secure_tls_packet_allocate)
  - Allocare un pacchetto per una sessione TLS sicura NetX
- [nx_secure_tls_psk_add](#nx_secure_tls_psk_add)
  - Aggiungere una chiave di Pre_Shared a una sessione TLS sicura NetX
- [nx_secure_tls_remote_certificate_allocate](#nx_secure_tls_remote_certificate_allocate)
  - Alloca spazio per il certificato fornito da un host TLS remoto
- [nx_secure_tls_remote_certificate_buffer_allocate](#nx_secure_tls_remote_certificate_buffer_allocate)
  - Alloca spazio per tutti i certificati forniti da un host TLS remoto
- [nx_secure_tls_remote_certificate_free_all](#nx_secure_tls_remote_certificate_free_all)
  - Spazio disponibile allocato per i certificati in ingresso
- [nx_secure_tls_server_certificate_add](#nx_secure_tls_server_certificate_add)
  - Aggiungere un certificato in modo specifico per i server TLS usando un identificatore numerico
- [nx_secure_tls_server_certificate_find](#nx_secure_tls_server_certificate_find)
  - Trovare un certificato usando un identificatore numerico
- [nx_secure_tls_server_certificate_remove](#nx_secure_tls_server_certificate_remove)
  - Rimuovere un certificato del server locale usando un identificatore numerico
- [nx_secure_tls_session_certificate_callback_set](#nx_secure_tls_session_certificate_callback_set)
  - Configurare un callback per TLS da usare per la convalida aggiuntiva dei certificati
- [nx_secure_tls_session_client_callback_set](#nx_secure_tls_session_client_callback_set)
  - Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS
- [nx_secure_tls_session_x509_client_verify_configure](#nx_secure_tls_session_x509_client_verify_configure)
  - Abilitare la verifica del client X. 509 e allocare spazio per i certificati client
- [nx_secure_tls_session_client_verify_disable](#nx_secure_tls_session_client_verify_disable)
  - Disabilitare l'autenticazione del certificato client per una sessione TLS sicura NetX
- [nx_secure_tls_session_client_verify_enable](#nx_secure_tls_session_client_verify_enable)
  - Abilitare l'autenticazione del certificato client per una sessione TLS sicura NetX
- [nx_secure_tls_session_create](#nx_secure_tls_session_create)
  - Creare una sessione TLS sicura NetX per le comunicazioni sicure
- [nx_secure_tls_session_delete](#nx_secure_tls_session_delete)
  - Eliminare una sessione TLS sicura NetX
- [nx_secure_tls_session_end](#nx_secure_tls_session_end)
  - Terminare una sessione TLS protetta NetX attiva
- [nx_secure_tls_session_packet_buffer_set](#nx_secure_tls_session_packet_buffer_set)
  - Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS sicura NetX
- [nx_secure_tls_session_protocol_version_override](#nx_secure_tls_session_protocol_version_override)
  - Eseguire l'override della versione del protocollo TLS predefinita per una sessione TLS protetta NetX
- [nx_secure_tls_session_receive](#nx_secure_tls_session_receive)
  - Ricevere dati da una sessione TLS protetta NetX
- [nx_secure_tls_session_renegotiate_callback_set](#nx_secure_tls_session_renegotiate_callback_set)
  - Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione
- [nx_secure_tls_session_renegotiate](#nx_secure_tls_session_renegotiate)
  - Avviare un handshake di rinegoziazione della sessione con l'host remoto
- [nx_secure_tls_session_reset](#nx_secure_tls_session_reset)
  - Cancellare e reimpostare una sessione TLS sicura NetX
- [nx_secure_tls_session_send](#nx_secure_tls_session_send)
  - Inviare dati tramite una sessione TLS sicura NetX
- [nx_secure_tls_session_server_callback_set](#nx_secure_tls_session_server_callback_set)
  - Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS
- [nx_secure_tls_session_sni_extension_parse](#nx_secure_tls_session_sni_extension_parse)
  - Analizzare un'estensione di Indicazione nome server (SNI) ricevuta da un client TLS
- [nx_secure_tls_session_sni_extension_set](#nx_secure_tls_session_sni_extension_set)
  - Impostare un nome DNS dell'estensione Indicazione nome server (SNI) da inviare a un server remoto
- [nx_secure_tls_session_start](#nx_secure_tls_session_start)
  - Avviare una sessione TLS sicura NetX
- [nx_secure_tls_session_time_function_set](#nx_secure_tls_session_time_function_set)
  - Assegnare una funzione timestamp a una sessione TLS protetta NetX
- [nx_secure_tls_trusted_certificate_add](#nx_secure_tls_trusted_certificate_add)
  - Aggiungere un certificato attendibile alla sessione TLS protetta NetX
- [nx_secure_tls_trusted_certificate_remove](#nx_secure_tls_trusted_certificate_remove)
  - Rimuovere il certificato attendibile dalla sessione TLS protetta NetX
- [nx_secure_x509_certificate_initialize](#nx_secure_x509_certificate_initialize)
  - Inizializzare il certificato X. 509 per NetX Secure TLS
- [nx_secure_x509_common_name_dns_check](#nx_secure_x509_common_name_dns_check)
  - Verificare il nome DNS rispetto al certificato X. 509
- [nx_secure_x509_crl_revocation_check](#nx_secure_x509_crl_revocation_check)
  - Controllare il certificato X. 509 in base a un elenco di revoche di certificati (CRL) specificato]
- [nx_secure_x509_dns_name_initialize](#nx_secure_x509_dns_name_initialize)
  - Inizializzare una struttura del nome DNS X. 509
- [nx_secure_x509_extended_key_usage_extension_parse](#nx_secure_x509_extended_key_usage_extension_parse)
  - Trovare e analizzare un'estensione per l'utilizzo delle chiavi estese X. 509 in un certificato X. 509
- [nx_secure_x509_extension_find](#nx_secure_x509_extension_find)
  - Trovare e restituire un'estensione X. 509 in un certificato X. 509
- [nx_secure_x509_key_usage_extension_parse](#nx_secure_x509_key_usage_extension_parse)
  - Trovare e analizzare un'estensione per l'utilizzo della chiave X. 509 in un certificato X. 509

## <a name="nx_secure_crypto_table_self_test"></a>nx_secure_crypto_table_self_test

Eseguire test autonomi sui metodi di crittografia

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a>Descrizione

Questo servizio esegue gli autotest del metodo Crypto per la convalida. Il test automatico è disponibile solo se la libreria protetta NetX è compilata con il simbolo NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK definito.

Per ogni metodo Crypto supportato, il test automatico fornisce dati di input predefiniti e verifica che l'output corrisponda al valore previsto predefinito.

NetX Secure Crypto self test supporta gli algoritmi e le dimensioni delle chiavi seguenti:

- DES: crittografia e decrittografia
- Triple DES (3DES): crittografia e decrittografia
- AES: 128-, 192-, dimensioni della chiave a 256 bit, crittografia e decrittografia, in modalità CBC e in modalità contatore.
- HMAC-MD5: autenticazione e calcolo hash
- HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2-512, autenticazione e calcolo hash
- MD5: autenticazione
- Funzione pseudo-random (PRF): PRF_HMAC_SHA1 e PRF_HMAC_SHA2-256
- RSA: 1024-, 2048-, operazione RSA di Power-Modul a 4096 bit
- SHA: SHA1 (96-and 160-bit), SHA2 (256bit, 384bit, 512bit) Authentication

Questa funzione include i vettori predefiniti per gli algoritmi di crittografia elencati in precedenza. Tuttavia, verifica solo quelli elencati nell' *cipher_table* passati a questa funzione. Ad esempio, per una sessione TLS usa solo la TLS_RSA_WITH_AES_128_CBC_SHA ciphersuite, questa funzione eseguirà il test automatico su RSA (1024-, 2048-, 4096-bit), AES-CBC (128 bit) e SHA1.

### <a name="parameters"></a>Parametri

- **crypto_table** Puntatore alla tabella Crypto utilizzata dalla sessione TLS. Si tratta dello stesso crypto_table passato nella chiamata **_nx_secure_tls_session_create ()_** .
- **metadati** di Puntatore allo spazio per l'area dei metadati di crittografia. .
- **metadata_size** Dimensioni del buffer dei metadati.

### <a name="return-values"></a>Valori restituiti

- **NX_SECURE_TLS_SUCCESS** (0x00) ha testato correttamente i metodi di crittografia forniti.
- Struttura del metodo Crypto **NX_PTR_ERROR** (0x07) non valida
- **NX_NOT_SUCCESSFUL** (0X43) Crypto self test ha esito negativo.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* crypto_tls_ciphers is the cipher table for the TLS session. */
/* metadata_buffer is the memory area used by the cipher functions. */

/* The following function verifies the supplied ciphersuties using the built-in
   self test. */

if (nx_secure_crypto_table_self_test(&crypto_tls_ciphers, metadata_buffer,
    sizeof(metadata_buffer)))
{
    printf("Crypto self test failed!\r\n");
    exit(0);
}
else
{
    printf("Crypto self test succeed!\r\n");
}

/* Now the ciphersuites are successfully test, it can be used in
   nx_secure_tls_session_create() */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_module_hash_compute"></a>nx_secure_module_hash_compute

Calcola il valore hash utilizzando la funzione hash fornita dall'utente

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a>Descrizione

Questa funzione calcola il valore hash del flusso di dati nell'area di memoria specificata, usando il metodo crittografico HMAC fornito e la stringa chiave. La funzione di calcolo hash del modulo è disponibile solo se la libreria protetta NetX viene compilata con il simbolo seguente definito: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK

### <a name="parameters"></a>Parametri

- **hmac_ptr** Puntatore al metodo crittografico HMAC utilizzato per il calcolo del valore hash.
- **start_address** Indirizzo iniziale del buffer di dati
- **end_address** Indirizzo finale del buffer di dati. Si noti che il calcolo hash non copre i dati in questo end_address.
- **chiave** di Stringa chiave utilizzata nel calcolo HMAC.
- **Key_Length** Dimensione della stringa di chiave, in byte
- **metadati** di Puntatore allo spazio utilizzato dall'algoritmo HMAC.
- **metadata_size** Dimensioni del buffer dei metadati.
- **output_buffer** Posizione di memoria in cui viene archiviato l'output hash.
- **output_buffer_size** Spazio disponibile del buffer di output, in byte
- **actual_size** Restituito dalla funzione che indica il numero effettivo di byte scritti nell'output_buffer.

### <a name="return-values"></a>Valori restituiti

- **0** ha calcolato correttamente il valore hash.
- **1** il calcolo hash non è riuscito.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Define the HMAC SHA256 method */
NX_CRYPTO_METHOD hmac_sha256 =
{
    NX_CRYPTO_AUTHENTICATION_HMAC_SHA2_256,    /* HMAC SHA256 algorithm  */
    0,                                         /* Key size, not used     */
    0,                                         /* IV size, not used      */
    NX_CRYPTO_HMAC_SHA256_ICV_FULL_LEN_IN_BITS,/* Transmitted ICV size   */
    NX_CRYPTO_SHA2_BLOCK_SIZE_IN_BYTES,        /* Block size in bytes    */
    sizeof(NX_CRYPTO_SHA256_HMAC),             /* Metadata size in bytes */
    _nx_crypto_method_hmac_sha256_init,        /* HMAC SHA256 init       */
    _nx_crypto_method_hmac_sha256_cleanup,     /* HMAC SHA256 cleanup    */
    _nx_crypto_method_hmac_sha256_operation    /* HMAC SHA256 operation  */
};

/* Define the hash key being used. */
const CHAR hash_key = “my hash key”;

/* Define starting address. */
UINT starting_address = 0x10000;

/* Define the ending address.
   Note that the hash computation covers the memory location
   before the ending address. */
UINT ending_address = 0x11000;

/* Declare the output buffer. */
#define OUTPUT_BUFFER_SIZE
UCHAR output_buffer[OUTPUT_BUFFER_SIZE];

UINT actual_size;

/* Declare 1K bytes of metadata buffer area. */
UCHAR metadata_buffer[1024];

/* Compute the hash value of the data between 0x10000 – 0x10FFF */
nx_secure_module_hash_compute(&hmac_sha256,
                              starting_address, ending_address,
                              hash_key, strlen(hash_key),
                              metadata_buffer, sizeof(metadata_buffer),
                              output_buffer, OUTPUT_BUFFER_SIZE, &actual_size);

/* If this function returns “0”, the hash value has been computed and is stored
   in output_buffer. */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_crypto_method_self_test

## <a name="nx_secure_tls_active_certificate_set"></a>nx_secure_tls_active_certificate_set

Impostare il certificato di identità attivo per una sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a>Descrizione

Questo servizio è destinato a essere chiamato dall'interno di un callback di sessione (vedere nx_secure_tls_session_client_callback_set e nx_secure_tls_session_server_callback_set). Quando viene chiamato con una struttura di NX_SECURE_X509_CERT inizializzata in precedenza, il certificato verrà usato al posto del certificato di identità predefinito. Nella maggior parte dei casi, il certificato deve essere stato aggiunto all'archivio locale (vedere nx_secure_tls_local_certificate_add) o l'handshake TLS potrebbe non riuscire.

Questo servizio è progettato per consentire a TLS di supportare più certificati di identità. Questa operazione è utile per un server TLS che fornisce servizi a più indirizzi di rete in modo che il server possa scegliere un certificato appropriato da fornire al client remoto a seconda del EntryPoint del client. Per un client TLS, questa routine può essere usata per modificare il certificato inviato a un server remoto in fase di esecuzione dopo che il server è stato identificato nell'handshake TLS (questo è più raro del caso d'uso del server TLS).

Nel caso in cui più certificati possano condividere lo stesso nome distinto X. 509, è necessario aggiungere i certificati utilizzando nx_secure_tls_server_certificate_add, che introduce un identificatore numerico separato dal certificato.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS passata al callback della sessione.
- **certificato** di Puntatore a un certificato X. 509 inizializzato da utilizzare per la sessione corrente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) assegnazione del certificato alla sessione completata.
- **NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore al certificato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define TLS_SNI_SERVER_NAME “www.example.com”
#define TLS_DEFAULT_SERVER_CERT_ID 2
#define TLS_EXAMPLE_CERT_ID 3


/* Callback for ClientHello extensions processing. */
static ULONG tls_server_callback(NX_SECURE_TLS_SESSION *tls_session,
                                 NX_SECURE_TLS_HELLO_EXTENSION *extensions,
                                 UINT num_extensions)
{
NX_SECURE_X509_DNS_NAME dns_name;
INT compare_value;
UINT status;
NX_SECURE_X509_CERT *cert_ptr;

    /* Grab a pointer to our default certificate in case the SNI extension is not
       available or the specified server name is unknown. */
    nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                     TLS_DEFAULT_SERVER_CERT_ID);


    /* Process Server Name Indication extension. */
    status = _nx_secure_tls_session_sni_extension_parse(tls_session, extensions,
                                                    num_extensions, &dns_name);

    /* If no extension found, that is OK. Use default certificate. */
    if(status == NX_SUCCESS)
    {
          /* SNI extension found, select an active certificate based on the server
             name. */

          /* Make sure our SNI name matches. */
          compare_value = memcmp(dns_name.nx_secure_x509_dns_name,
                                TLS_SNI_SERVER_NAME, strlen(TLS_SNI_SERVER_NAME));

          if(compare_value == 0 && dns_name.nx_secure_x509_dns_name_length !=
             strlen(TLS_SNI_SERVER_NAME))
          {
             /* Found a match, find the certificate we want to use. */
             _nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                                      TLS_EXAMPLE_CERT_ID);
          }
          else
          {
             /* No matching server name found. The application may choose to simply
                provide the default certificate (and probably resulting in an error
                in the remote client) or returning an error here to end the
                handshake. A user-defined non-zero error code will be sufficient –
                the error code will abort the TLS handshake and be returned to the
                caller that started the server. */
                return(0x500);
          }
      }
      else
      {
      }
      /* Set the certificate we want to use. */
      nx_secure_tls_active_certificate_set(tls_session, cert_ptr);

      /* Return success to continue TLS handshake. */
      return(NX_SUCCESS);
}

/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_TLS_SESSION server_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&server_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_tls_session_create: 0x%x\n", status);
    }

    /* Setup our packet reassembly buffer. See
       nx_secure_tls_session_packet_buffer_set for more information. */
    nx_secure_tls_session_packet_buffer_set(&server_tls_session,
                                      server_packet_buffer,
                                      sizeof(server_packet_buffer));


    /* Set callback for server TLS extension handling. */
    _nx_secure_tls_session_server_callback_set(&server_tls_session,
                                              tls_server_callback);

    /* Initialize our certificates – certificate data defined elsewhere. See
       section “Importing X.509 Certificates into NetX Secure” for more
       information. */
    nx_secure_x509_certificate_initialize(&default_certificate,
                                      default_cert_der,
                                      default _cert_der_len, NX_NULL, 0,
                                      default_cert_key_der,
                                      default_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &default_certificate,
                                         TLS_DEFAULT_SERVER_CERT_ID);

    /* Alternative identity certificate, needs to have a private key! */
    nx_secure_x509_certificate_initialize(&example_certificate,
                                      example_cert_der,
                                      example cert_der_len, NX_NULL, 0,
                                      example_cert_key_der,
                                      example_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &example_certificate,
                                         TLS_EXAMPLE_CERT_ID);

    /* Now we can start the TLS session as normal. */
       …
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_session_server_callback_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find
- nx_secure_tls_server_certificate_remove

## <a name="nx_secure_tls_client_psk_set"></a>nx_secure_tls_client_psk_set

Impostare una chiave precondivisa per una sessione client TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una chiave precondivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione TLS e imposta tale PSK da usare nelle connessioni client TLS successive. Il valore PSK viene usato al posto di un certificato digitale quando si Abilita e si usa PSK ciphersuites.

In questo caso, la PSK è associata a un server TLS remoto specifico con cui il client TLS desidera comunicare. Il set di PSK tramite questa API verrà fornito all'host del server TLS remoto durante il successivo handshake TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **pre_shared_key** Valore PSK effettivo.
- **psk_length** Lunghezza del valore PSK.
- **psk_identity** Stringa utilizzata per identificare il valore PSK.
- **identity_length** Lunghezza dell'identità PSK.
- **hint** Stringa utilizzata per indicare il gruppo di precondivise da scegliere in un server TLS.
- **hint_length** Lunghezza della stringa del suggerimento.

### <a name="return-values"></a>Valori restituiti

- L'aggiunta di PSK è stata completata **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0X125) non è in grado di aggiungere un'altra PSK.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_psk_add
- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_initialize"></a>nx_secure_tls_initialize

Inizializza il modulo TLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza il modulo TLS sicuro NetX. Deve essere chiamato prima che sia possibile accedere ad altri servizi NetX Secure.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

nessuno

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_tls_local_certificate_add"></a>nx_secure_tls_local_certificate_add

Aggiungere un certificato locale a una sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza della struttura NX_SECURE_X509_CERT inizializzata all'archivio locale di una sessione TLS. Questo certificato può essere usato dallo stack TLS per identificare il dispositivo durante l'handshake TLS (se è stato contrassegnato come certificato di identità durante l'inizializzazione della struttura del certificato usando nx_secure_x509_certificate_initialize) o come emittente come parte di una catena di certificati fornita all'host remoto durante l'handshake TLS.

Se sono necessari più certificati locali con lo stesso nome comune, i certificati possono essere aggiunti usando il servizio *nx_secure_tls_server_certificate_add* (vedere l'avviso riportato di seguito).

Per la modalità server TLS è **necessario** un certificato.

Un certificato è *facoltativo* per la modalità client TLS.

> [!IMPORTANT]
> *Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API Certificate Server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add gli indici in base al nome comune X. 509. I servizi certificati locali forniscono una comoda alternativa all'identificatore numerico per le applicazioni che usano solo un singolo certificato di identità: usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificate_ptr** Puntatore a un'istanza di certificato TLS inizializzata.

### <a name="return-values"></a>Valori restituiti

- Aggiunta del certificato **NX_SUCCESS** (0x00) completata.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) ha tentato di aggiungere un certificato non valido o duplicato.
- **NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore al certificato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_local_certificate_find

## <a name="nx_secure_tls_local_certificate_find"></a>nx_secure_tls_local_certificate_find

Trovare un certificato locale in una sessione TLS sicura NetX per nome comune

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a>Descrizione

Questo servizio trova un certificato nell'archivio certificati del dispositivo locale di una sessione TLS e restituisce un puntatore alla struttura NX_SECURE_X509_CERT nell'archivio. Il parametro common_name e la lunghezza (name_length) vengono usati per identificare il certificato nell'archivio corrispondente al campo del nome comune del soggetto X. 509 del certificato.

Se è presente più di un certificato con lo stesso nome comune, viene restituito solo il primo: usare *nx_secure_tls_server_certificate_find* .

> [!IMPORTANT]
> *Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API Certificate Server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add gli indici in base al nome comune X. 509. I servizi certificati locali forniscono una comoda alternativa all'identificatore numerico per le applicazioni che usano solo un singolo certificato di identità: usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificato** di Restituisce il puntatore al certificato corrispondente.
- **common_name** Stringa del nome comune da confrontare (nome DNS).
- **name_length** Lunghezza dei dati della stringa common_name.

### <a name="return-values"></a>Valori restituiti

- È stato trovato il certificato **NX_SUCCESS** (0x00) e il puntatore è stato restituito nel parametro "Certificate".
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) non è stato trovato alcun certificato con il nome comune fornito.
- **NX_PTR_ERROR** (0x07) una sessione TLS non valida, un puntatore al certificato o una stringa del nome comune.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_SECURE_X509_CERT *certificate_ptr;

/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */

status = nx_secure_tls_local_certificate_find(&tls_session, &certificate_ptr,
                                      “common name”, strlen(“common name”));

/* If status is NX_SUCCESS the variable “certificate_ptr” points to a certificate
   structure containing a certificate with the Common Name “common name”. */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_local_certificate_remove"></a>nx_secure_tls_local_certificate_remove

Rimuovere il certificato locale dalla sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un'istanza del certificato locale da una sessione TLS, con chiave nel campo del nome comune nel certificato.

> [!IMPORTANT]
> *Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API Certificate Server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add gli indici in base al nome comune X. 509. I servizi certificati locali forniscono una comoda alternativa all'identificatore numerico per le applicazioni che usano solo un singolo certificato di identità: usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **common_name** Valore del nome comune del certificato da rimuovere.
- **common_name_length** Lunghezza della stringa del nome comune.

### <a name="return-values"></a>Valori restituiti

- Aggiunta del certificato **NX_SUCCESS** (0x00) completata.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- Il certificato **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) non è stato trovato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_metadata_size_calculate"></a>nx_secure_tls_metadata_size_calculate

Calcolo delle dimensioni dei metadati crittografici per una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a>Descrizione

Questo servizio calcola e restituisce le dimensioni dei metadati di crittografia necessari per una determinata sessione TLS e una tabella di crittografia TLS (vedere la sezione "inizializzazione di TLS con i metodi di crittografia" per ulteriori informazioni sulla tabella di crittografia crittografica).

Questo servizio deve essere chiamato con la tabella di crittografia desiderata per calcolare le dimensioni del buffer dei metadati passato in nx_secure_tls_session_create.

### <a name="parameters"></a>Parametri

- **crypto_table** Puntatore a una tabella di crittografia TLS protetta NetX completa.
- **metadata_size** Output del calcolo delle dimensioni in byte.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il calcolo delle dimensioni dei metadati è riuscito.
- **NX_PTR_ERROR** (0x07) tabella di crittografia o puntatore alla dimensione restituito non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Return variable for metadata size. */
ULONG crypto_metadata_size;

/* Calculate metadata size.  */
status =  nx_secure_tls_metadata_size_calculate(&nx_crypto_tls_ciphers,
                                                &crypto_metadata_size);


/* If status is NX_SUCCESS then crypto_metadata_size contains the size of the
   metadata buffer for the table nx_crypto_tls_ciphers.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_module_hash_compute"></a>nx_secure_module_hash_compute

Calcola il valore hash delle routine della libreria protetta NetX

### <a name="prototype"></a>Prototipo

```C
VOID nx_secure_module_hash_compute(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza il modulo TLS sicuro NetX. Deve essere chiamato prima che sia possibile accedere ad altri servizi NetX Secure.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

nessuno

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_tls_packet_allocate"></a>nx_secure_tls_packet_allocate

Allocare un pacchetto per una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio alloca un NX_PACKET per la sessione TLS attiva specificata dalla NX_PACKET_POOL specificata. Questo servizio deve essere chiamato dall'applicazione per allocare i pacchetti di dati da inviare tramite una connessione TLS. È necessario inizializzare la sessione TLS prima di chiamare il servizio.

Il pacchetto allocato è stato inizializzato correttamente in modo che i dati di intestazione e piè di pagina TLS possano essere aggiunti dopo il popolamento dei dati del pacchetto. In caso contrario, il comportamento è identico a *nx_packet_allocate*.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **pool_ptr** Puntatore a un NX_PACKET_POOL da cui allocare il pacchetto.
- **packet_ptr** Puntatore di output al pacchetto appena allocato.
- **WAIT_OPTION** Opzione di sospensione per l'allocazione dei pacchetti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) allocare il pacchetto correttamente.
- L'allocazione del pacchetto sottostante **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è riuscita.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_psk_add"></a>nx_secure_tls_psk_add

Aggiungere una chiave precondivisa a una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una chiave precondivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione TLS. Il valore PSK viene usato al posto di un certificato digitale quando si Abilita e si usa PSK ciphersuites.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **pre_shared_key** Valore PSK effettivo.
- **psk_length** Lunghezza del valore PSK.
- **psk_identity** Stringa utilizzata per identificare il valore PSK.
- **identity_length** Lunghezza dell'identità PSK.
- **hint** Stringa utilizzata per indicare il gruppo di precondivise da scegliere in un server TLS.
- **hint_length** Lunghezza della stringa del suggerimento.

### <a name="return-values"></a>Valori restituiti

- L'aggiunta di PSK è stata completata **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0X125) non è in grado di aggiungere un'altra PSK.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_client_psk_set
- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_remote_certificate_allocate"></a>nx_secure_tls_remote_certificate_allocate

Alloca spazio per il certificato fornito da un host TLS remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza di struttura di NX_SECURE_X509_CERT non inizializzata a una sessione TLS allo scopo di allocare spazio per i certificati forniti da un host remoto durante una sessione TLS. I dati del certificato remoto vengono analizzati da NetX Secure TLS e tali informazioni vengono utilizzate per popolare l'istanza della struttura del certificato fornita a questa funzione. I certificati aggiunti in questo modo vengono inseriti in un elenco collegato.

Se si prevede che l'host remoto fornirà più certificati, è necessario chiamare ripetutamente questa funzione per allocare spazio per tutti i certificati. I certificati aggiuntivi vengono aggiunti alla fine dell'elenco collegato al certificato.

Se non si alloca un certificato remoto, la modalità client TLS avrà esito negativo durante l'handshake TLS a meno che non sia in uso una chiave precondivisa (PSK) ciphersuite.

Il parametro *raw_certificate_buffer* punta allo spazio allocato per archiviare il certificato remoto in ingresso. I certificati tipici con chiavi RSA di 2048 bit che usano SHA-256 per le firme sono compresi nell'intervallo da 1000-2000 byte. Il buffer deve essere sufficientemente grande da contenere almeno questa dimensione, ma a seconda dei certificati dell'host remoto può essere significativamente più piccolo o più grande. Si noti che se il buffer è troppo piccolo per conservare il certificato in ingresso, l'handshake TLS termina con un errore.

Per la modalità server TLS, è necessaria un'allocazione di certificati remota solo se è abilitata l'autenticazione del certificato client.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificate_ptr** Puntatore a un'istanza di un certificato X. 509 non inizializzato.
- **raw_certificate_buffer** Puntatore a un buffer per contenere il certificato non analizzato ricevuto dall'host remoto.
- **raw_buffer_size** Dimensioni del buffer del certificato non elaborato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) l'allocazione del certificato è riuscita.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0X12D) il buffer fornito è troppo piccolo.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) ha tentato di aggiungere un certificato non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize,
- nx_secure_tls_session_create

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a>nx_secure_tls_remote_certificate_buffer_allocate

Alloca spazio per tutti i certificati forniti da un host TLS remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio alloca spazio per elaborare le catene di certificati in ingresso dagli host server remoti per eseguire l'autenticazione e la verifica X. 509 in un'istanza client TLS. Per la modalità server TLS, l'allocazione di certificati remoti è necessaria solo se è abilitata l'autenticazione del certificato X. 509 del client: per le istanze del server TLS è necessario usare invece il *nx_secure_tls_session_x509_client_verify_configure* di servizio.

Se non si allocano certificati remoti, la modalità client TLS avrà esito negativo durante l'handshake TLS a meno che non sia in uso una chiave precondivisa (PSK) ciphersuite.

Il parametro *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati. Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale assegnata a ogni certificato. Il parametro *BUFFER_SIZE*  indica le dimensioni del buffer. È possibile trovare lo spazio necessario con la formula seguente:

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

I certificati tipici con chiavi RSA di 2048 bit che usano SHA-256 per le firme sono compresi nell'intervallo da 1000-2000 byte. Il buffer deve essere sufficientemente grande da contenere almeno tali dimensioni per ogni certificato, ma a seconda dei certificati dell'host remoto può essere significativamente più piccolo o più grande. Si noti che se il buffer è troppo piccolo per conservare il certificato in ingresso, l'handshake TLS termina con un errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certs_number** Numero di certificati da allocare dal buffer specificato.
- **certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.
- **BUFFER_SIZE** Dimensioni del buffer del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) l'allocazione del certificato è riuscita.
- **NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore del buffer non è valido.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0X12D) il buffer fornito è troppo piccolo.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) il buffer era troppo piccolo per conservare il numero desiderato di certificati.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE           (CERTIFICATE_NUMBER * \
                              (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_buffer_allocate(&tls_session,
                                                      CERTIFICATE_NUMBER,
                                                      certificate_buffer,
                                                      BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create

## <a name="nx_secure_tls_remote_certificate_free_all"></a>nx_secure_tls_remote_certificate_free_all

Spazio disponibile allocato per i certificati in ingresso

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per liberare tutti i buffer di certificato allocati a una determinata sessione TLS da nx_secure_tls_remote_certificate_allocated restituendo tali buffer allo spazio dei certificati libero della sessione. Questa operazione può essere necessaria se un'applicazione riutilizza un oggetto sessione TLS senza eliminarlo e ricrearlo con nx_secure_tls_session_delete e nx_secure_tls_session_create.

Si noti che lo spazio del certificato remoto viene recuperato automaticamente quando la sessione TLS viene reimpostata come avviene in nx_secure_tls_session_end, quindi la maggior parte delle applicazioni non deve chiamare questo servizio.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) operazione riuscita.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- Errore interno **NX_INVALID_PARAMETERS** (irreversibile 0x4D): probabilmente danneggiato nell'archivio certificati.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */

/* … TLS session setup, TCP connection, etc… */

/* End TLS session. */
nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

/* Free up certificate buffers for next connection. */
nx_secure_tls_remote_certificate_free_all(&tls_session);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_end

## <a name="nx_secure_tls_server_certificate_add"></a>nx_secure_tls_server_certificate_add

Aggiungere un certificato in modo specifico per i server TLS usando un identificatore numerico

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per aggiungere un certificato a un archivio locale della sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X. 509 (nome comune) all'interno del certificato. L'identificatore numerico è separato dal certificato e consente l'aggiunta di più certificati come certificati di identità a un server TLS, oltre a consentire l'aggiunta di più certificati con lo stesso nome comune allo stesso archivio locale della sessione TLS. Questo stesso servizio può essere usato per i certificati client, ma è raro che un client TLS disponga di più certificati di identità.

Il parametro cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione. Il valore effettivo non è rilevante (diverso da zero), ma deve essere univoco nell'archivio per la sessione TLS specificata. Il valore cert_id può essere usato per trovare e rimuovere i certificati dall'archivio locale usando rispettivamente nx_secure_tls_server_certificate_find e nx_secure_tls_server_certificate_remove.

> [!IMPORTANT]
> *Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L'API nx_secure_tls_server_certificate_add usa un identificatore numerico univoco per ogni certificato e l'indice locale di Servizi certificati in base al nome comune X. 509. I servizi certificati server consentono di esistere più certificati con dati condivisi (in particolare il nome comune) nello stesso archivio locale. questa operazione è utile per un server con più identità.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificato** di Puntatore a un'istanza di certificato X. 509 inizializzata in precedenza.
- **cert_id** Numero ID certificato positivo, diverso da zero, relativamente univoco.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) operazione riuscita.
- Il puntatore orcertificate della sessione TLS **NX_PTR_ERROR** (0x07) non è valido.
- **NX_SECURE_TLS_CERT_ID_INVALID** (0X138) l'ID certificato specificato presenta un valore non valido (probabilmente 0).
- **NX_SECURE_TLS_CERT_ID_DUPLICATE** (0X139) l'ID certificato specificato è già presente nell'archivio locale.
- **NX_INVALID_PARAMETERS (irreversibile 0x4D)** Errore interno: l'archivio certificati probabilmente è danneggiato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_find
- nx_secure_tls_server_certificate_remove

## <a name="nx_secure_tls_server_certificate_find"></a>nx_secure_tls_server_certificate_find

Trovare un certificato usando un identificatore numerico

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per trovare un certificato nell'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X. 509 (nome comune) all'interno del certificato.

Il parametro cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS utilizzando nx_secure_tls_server_certificate_add.

> [!IMPORTANT]
> *Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L'API nx_secure_tls_server_certificate_add usa un identificatore numerico univoco per ogni certificato e l'indice locale di Servizi certificati in base al nome comune X. 509. I servizi certificati server consentono di esistere più certificati con dati condivisi (in particolare il nome comune) nello stesso archivio locale. questa operazione è utile per un server con più identità.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificato** di Puntatore a un puntatore al certificato X. 509 per restituire un riferimento al certificato trovato.
- **cert_id** Valore ID certificato positivo diverso da zero.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) operazione riuscita.
- **NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore al certificato non è valido.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) l'ID certificato specificato non corrisponde a nessuno nell'archivio locale della sessione TLS specificata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_remove

##  <a name="nx_secure_tls_server_certificate_remove"></a>nx_secure_tls_server_certificate_remove

Rimuovere un certificato del server locale usando un identificatore numerico

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per rimuovere un certificato da un archivio locale della sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X. 509 (nome comune) all'interno del certificato.

Il parametro cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS utilizzando nx_secure_tls_server_certificate_add.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **cert_id** Valore ID certificato positivo diverso da zero.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) operazione riuscita.
- **NX_PTR_ERROR** sessione TLS non valida (0x07).
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) l'ID certificato specificato non corrisponde a nessuno nell'archivio locale della sessione TLS specificata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);
/* Use certificate in TLS session, etc… */

/* Remove certificate from TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_remove(&tls_session, 0x12);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find

## <a name="nx_secure_tls_session_alert_value_get"></a>nx_secure_tls_session_alert_value_get

Ottenere il livello e il valore di avviso TLS inviati dall'host remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per recuperare il livello e il valore di avviso TLS quando l'host remoto invia un avviso in risposta a un problema o a un errore.

I valori dei parametri alert_level e alert_value sono validi solo se questa funzione viene chiamata immediatamente dopo una chiamata API TLS che ha restituito lo stato NX_SECURE_TLS_ALERT_RECEIVED (0x114) che indica che è stato ricevuto un avviso dall'host remoto.

Si noti che se l'host locale TLS Invia un avviso, i codici di errore restituiti sono molto più descrittivi dell'errore effettivo rispetto all'avviso TLS stesso perché i valori di avviso TLS sono intenzionalmente lasciati ambigui per evitare determinati tipi di attacco (ad esempio, un attacco "riempimento Oracle" o simile).

Il livello di avviso accetta solo uno dei due valori seguenti: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) o NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2). In generale, viene fornito un livello di "avviso" solo per l'avviso CloseNotify (usato per indicare un esito positivo di una sessione TLS), anche se alcune situazioni di configurazione dell'estensione possono essere considerate avvisi. La maggior parte degli avvisi sarà "irreversibile", che indica un potenziale errore di sicurezza e con conseguente chiusura immediata della connessione TLS (handshake o Session).

I valori di avviso TLS sono definiti nelle RFC di TLS. di seguito è riportato l'elenco di RFC 5246 (TLSv 1.2) per riferimento:

| Nome avviso                     | Valore | Descrizione                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| close_notify                  | 0     | Nessun errore, indica la fine della sessione completata                                                                                                                   |
| unexpected_message            | 10    | Un messaggio imprevisto o non ordinato è stato ricevuto da TLS                                                                                                           |
| bad_record_mac               | 20    | Verifica decrittografia e/o MAC non riuscita                                                                                                                    |
| decryption_failed_RESERVED   | 21    | **Obsoleto** Decrittografia non riuscita (deprecata a causa di attacchi Oracle di riempimento)                                                                                      |
| record_overflow               | 22    | È stato ricevuto un record maggiore della dimensione massima del record TLS                                                                                        |
| decompression_failure         | 30    | Si è verificato un problema durante la compressione/decompressione di un record TLS                                                                                       |
| handshake_failure             | 40    | Si è verificato un errore di handshake non specificato che non è coperto da un avviso diverso                                                                            |
| no_certificate_RESERVED      | 41    | **Deprecato** in TLS (solo SSL)                                                                                                                                 |
| bad_certificate               | 42    | Un certificato ricevuto contiene una formattazione o una firma non valida                                                                                   |
| unsupported_certificate       | 43    | È stato ricevuto un certificato di tipo non valido (ad esempio, il certificato di sola firma usato per l'autenticazione del server TLS)                                    |
| certificate_revoked           | 44    | Lo stato del certificato (come fornito da un CRL o OCSP) è stato indicato come "revocato"                                                                       |
| certificate_expired           | 45    | Il certificato ricevuto non è compreso nell'intervallo di date valido, ovvero non è ancora valido o è scaduto.                                                                 |
| certificate_unknown           | 46    | Si è verificato un problema di certificato sconosciuto non coperto da altri avvisi                                                                          |
| illegal_parameter             | 47    | Una configurazione o un valore negoziato nell'handshake TLS non è valido o non è compreso nell'intervallo                                                                      |
| unknown_ca                    | 48    | Non è stato possibile tracciare il certificato di identità ricevuto tramite una catena di certificati a un certificato CA radice attendibile.                                              |
| access_denied                 | 49    | Indica che è stato ricevuto un certificato valido, ma il controllo di accesso dell'applicazione ha indicato che il certificato non è valido per le risorse richieste.            |
| decode_error                  | 50    | Alcuni campi o valori in un messaggio di intestazione o di handshake TLS non sono compresi nell'intervallo o non sono validi, causando un errore nella decodifica di un record TLS.                      |
| decrypt_error                 | 51    | Non è stato possibile verificare una firma o un hash del messaggio terminato durante l'handshake TLS.                                                                         |
| export_restriction_RESERVED  | 60    | DEPRECAto in TLSv 1.2                                                                                                                                        |
| protocol_version              | 70    | La versione del protocollo TLS negoziata durante l'handshake è riconosciuta ma non supportata (ad esempio, TLSv 1.0 è stato presentato ma non è abilitato).                       |
| insufficient_security         | 71    | Inviato ogni volta che l'handshake ha esito negativo a causa della mancanza di crittografie sicure (ad esempio, la dimensione della chiave è troppo piccola per i requisiti dell'applicazione)                                |
| internal_error                | 80    | Si è verificato un errore non TLS, ad esempio problemi di allocazione della memoria e problemi dell'applicazione, causando una sessione TLS interruppe.                                         |
| user_canceled                 | 90    | Restituito se la sessione TLS viene annullata da un utente o da un'applicazione prima del completamento dell'handshake (simile a CloseNotify).                                 |
| no_renegotiation              | 100   | Indiates che l'host remoto non è disposto a eseguire handshake di rinegoziazione TLS in risposta a una richiesta di rinegoziazione.                                 |
| unsupported_extension         | 110   | Inviato se un client TLS riceve un ServerHello contenente le estensioni non richieste in modo esplicito nel ClientHello iniziale (indicante che si è verificato un problema nel server). |

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **alert_level** Restituisce il livello dell'avviso ricevuto (avviso o irreversibile).
- **alert_value** Restituisce il valore dell'avviso ricevuto (vedere la tabella).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) operazione riuscita.
- **NX_PTR_ERROR** sessione TLS non valida (0x07).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Return values. */
UINT status, alert_level, alert_value;


/* Start a TLS session.  */
status =  nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Check for “alert received” error. */
if(status == NX_SECURE_TLS_ALERT_RECEIVED)
{

        /* Get the alert level and value. */
        status =  nx_secure_tls_session_alert_value_get(&tls_session,
                                             &alert_level, &alert_value);

        /* Print out the received alert level and value. */
        printf("Alert recieved. Value: %d, Level: %d\n", alert_value,
                alert_level);
}
else if(status != NX_SUCCESS)
{
    /* Additional error handling. */
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_start
- nx_secure_tls_session_send
- nx_secure_tls_session_receive

## <a name="nx_secure_tls_session_certificate_callback_set"></a>nx_secure_tls_session_certificate_callback_set

Configurare un callback per TLS da usare per la convalida aggiuntiva dei certificati

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un puntatore a funzione a una sessione TLS che verrà richiamata da TLS quando un certificato viene ricevuto da un host remoto, consentendo all'applicazione di eseguire controlli di convalida, ad esempio la convalida DNS, la revoca dei certificati e l'applicazione dei criteri dei certificati.

NetX Secure TLS eseguirà la convalida di base del percorso X. 509 sul certificato prima di richiamare il callback per garantire che il certificato possa essere tracciato a un certificato nell'archivio certificati trusted TLS, ma tutte le altre convalide verranno gestite da questo callback.

Il callback fornisce il puntatore della sessione TLS e un puntatore al certificato di identità dell'host remoto (foglia nella catena di certificati). Il callback deve restituire NX_SUCCESS se la convalida ha esito positivo; in caso contrario, deve restituire un codice di errore che indica l'errore di convalida. Qualsiasi valore diverso da NX_SUCCESS farà sì che l'handshake TLS venga interrotto immediatamente.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **func_ptr** Puntatore alla funzione di callback di convalida del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) allocazione riuscita del puntatore a funzione.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
    /* Certificate validation checking goes here. */
    return(NX_SUCCESS);
}

/* In TLS setup routine. */
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                            certificate_callback);

        /* If status is NX_SUCCESS the certificate callback was added.  */
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_crl_revocation_check

## <a name="nx_secure_tls_session_client_callback_set"></a>nx_secure_tls_session_client_callback_set

Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un puntatore a funzione a una sessione TLS che verrà richiamata da TLS quando un handshake del client TLS riceve un messaggio ServerHelloDone. La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ServerHello ricevuto che richiede l'input o il processo decisionale.

Il callback viene eseguito con il blocco di controllo della sessione TLS chiamante e una matrice di oggetti NX_SECURE_TLS_HELLO_EXTENSION. La matrice di oggetti estensione deve essere passata in una funzione helper che troverà e analizzerà un'estensione specifica. Attualmente non sono presenti estensioni specifiche supportate in NetX Secure che richiedono l'input del client TLS, ma il callback è disponibile per le finestre di progettazione delle applicazioni per gestire le estensioni personalizzate o nuove che potrebbero diventare disponibili. Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi Hello, vedere *nx_secure_tls_session_sni_extension_parse*.

Il callback del client può essere usato anche per selezionare il certificato di identità attivo usando *nx_secure_tls_active_certificate_set* per il client TLS nel caso in cui il server remoto abbia richiesto un certificato e abbia fornito informazioni per consentire al client TLS di selezionare un certificato specifico. Per ulteriori informazioni, vedere il riferimento per nx_secure_tls_active_certificate_set.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **func_ptr** Puntatore alla funzione di callback del client TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) allocazione riuscita del puntatore a funzione.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Callback routine used to process ServerHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the server). */

ULONG tls_client_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{

    /* Extension parsing would go here. */

    /* Set an active identity certificate – the certificate should have been added
       to the local store at application start with
       nx_secure_tls_local_certificate_add. */
    nx_secure_tls_active_certificate_set(session, &global_identity_certificate);

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
    /* Add callback to TLS session.  */
    status =  nx_secure_tls_session_client_callback_set(tls_session,
                                                        client_callback);

    /* If status is NX_SUCCESS the callback was added and will be invoked once
       a ServerHelloDone message is received. */

    return(status);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_server_callback_set
- nx_secure_tls_active_certificate_set

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a>nx_secure_tls_session_x509_client_verify_configure

Abilitare la verifica del client X. 509 e allocare spazio per i certificati client

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita l'autenticazione client X. 509 facoltativa per un'istanza del server TLS. Alloca inoltre lo spazio necessario per elaborare le catene di certificati in ingresso dall'host client remoto. I certificati forniti dal client remoto verranno verificati in base ai certificati attendibili dell'istanza del server TLS, assegnati con il nx_secure_tls_trusted_certificate_add del servizio *.*

Per la modalità client TLS, è necessaria l'allocazione di certificati remoti ed è invece necessario usare il *nx_secure_tls_remote_certificate_buffer_allocate* di servizio. L'abilitazione dell'autenticazione client X. 509 su un'istanza del client TLS non avrà alcun effetto.

Il parametro *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati. Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale assegnata a ogni certificato. Il parametro *BUFFER_SIZE* indica le dimensioni del buffer. È possibile trovare lo spazio necessario con la formula seguente:

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

I certificati tipici con chiavi RSA di 2048 bit che usano SHA-256 per le firme sono compresi nell'intervallo da 1000-2000 byte. Il buffer deve essere sufficientemente grande da contenere almeno tali dimensioni per ogni certificato, ma a seconda dei certificati dell'host remoto può essere significativamente più piccolo o più grande. Si noti che se il buffer è troppo piccolo per conservare il certificato in ingresso, l'handshake TLS termina con un errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certs_number** Numero di certificati da allocare dal buffer specificato.
- **certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.
- **BUFFER_SIZE** Dimensioni del buffer del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) l'allocazione del certificato è riuscita.
- **NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore del buffer non è valido.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0X12D) il buffer fornito è troppo piccolo.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) il buffer era troppo piccolo per conservare il numero desiderato di certificati.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE          (CERTIFICATE_NUMBER * \
                                (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Enable X.509 Client verification and allocate certificate space in our TLS
   Server session.  */
status =  nx_secure_tls_session_x509_client_verify_configure(&tls_session,
                                                    CERTIFICATE_NUMBER,
                                                    certificate_buffer,
                                                    BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_buffer_allocate

## <a name="nx_secure_tls_session_client_verify_disable"></a>nx_secure_tls_session_client_verify_disable

Disabilitare l'autenticazione del certificato client per una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Disabilita l'autenticazione del certificato client per una sessione TLS specifica. Per ulteriori informazioni, vedere nx_secure_tls_session_client_verify_enable.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.

### <a name="return-values"></a>Valori restituiti

- Modifica dello stato **NX_SUCCESS** (0x00) riuscita.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_client_verify_enable
- nx_secure_tls_session_start
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_client_verify_enable"></a>nx_secure_tls_session_client_verify_enable

Abilitare l'autenticazione del certificato client per una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita l'autenticazione del certificato client per una sessione TLS specifica. L'abilitazione dell'autenticazione del certificato client per un'istanza del server TLS farà sì che il server TLS richieda un certificato da qualsiasi client TLS remoto durante l'handshake TLS iniziale. Il certificato ricevuto dal client TLS remoto è accompagnato da un messaggio CertificateVerify, che il server TLS usa per verificare che il client sia proprietario del certificato (ha accesso alla chiave privata associata al certificato).

Se il certificato fornito può essere verificato e ritracciato a un certificato nell'archivio certificati attendibili del server TLS tramite una catena di certificati X. 509, il client TLS remoto viene autenticato e l'handshake continua. In caso di errori durante l'elaborazione del certificato o del messaggio CertificateVerify, l'handshake TLS termina con un errore.

> [!NOTE]
> *Il server TLS deve avere almeno un certificato nell'archivio attendibile aggiunto con nx_secure_tls_trusted_certificate_add o l'autenticazione avrà sempre esito negativo.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.

### <a name="return-values"></a>Valori restituiti

- Modifica dello stato **NX_SUCCESS** (0x00) riuscita.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_client_verify_enable
- nx_secure_tls_session_start
- nx_secure_tls_session_create
- nx_secure_tls_trusted_certificate_add

## <a name="nx_secure_tls_session_create"></a>nx_secure_tls_session_create

Creare una sessione TLS sicura NetX per le comunicazioni sicure

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza un'istanza della struttura NX_SECURE_TLS_SESSION da usare per stabilire comunicazioni TLS sicure su una connessione di rete.

Il metodo accetta un oggetto NX_SECURE_TLS_CRYPTO popolato con i metodi di crittografia disponibili da usare per TLS. Il *encryption_metadata_area* punta a un buffer allocato per l'uso da parte di TLS per i "metadati" usati dai metodi crittografici nella tabella NX_SECURE_TLS_CRYPTO per i calcoli. È possibile determinare le dimensioni della tabella utilizzando il servizio nx_secure_tls_metadata_size_calculate. Per altri dettagli, vedere la sezione "crittografia in NetX Secure TLS" nel capitolo 3.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **cipher_table** Puntatore ai metodi di crittografia TLS.
- **encryption_metadata_area** Puntatore allo spazio per i metadati di crittografia.
- **encryption_metadata_size** Dimensioni del buffer dei metadati.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) il buffer dei metadati è troppo piccolo per i metodi specificati.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0X106) un metodo di crittografia obbligatorio per la versione abilitata di TLS non è stato fornito nella tabella di crittografia.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Reference the platform-specific TLS cryptographic method table. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Declare a buffer for the cryptographic metadata. The size should be calculated
   using nx_secure_tls_metadata_size_calculate. */
UCHAR crypto_metadata[4500];

/* Initialize TLS session.  */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* If status is NX_SUCCESS the TLS Session was successfully initialized.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_metadata_size_calculate
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_end
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_delete
- Crittografia in NetX Secure TLS nel capitolo 3

## <a name="nx_secure_tls_session_delete"></a>nx_secure_tls_session_delete

Eliminare una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina una sessione TLS rappresentata da un'istanza della struttura NX_SECURE_TLS_SESSION e rilascia tutte le risorse di sistema di proprietà di tale istanza di sessione.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_end
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_end"></a>nx_secure_tls_session_end

Terminare una sessione TLS protetta NetX attiva

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio termina una sessione TLS rappresentata da un'istanza della struttura NX_SECURE_TLS_SESSION inviando il messaggio TLS CloseNotify all'host remoto. Il servizio attende quindi che l'host remoto risponda con il proprio messaggio CloseNotify.

Se l'host remoto non invia un messaggio CloseNotify, TLS considera un errore e una possibile violazione della sicurezza, quindi il controllo del valore restituito è importante per una connessione protetta. Il parametro **WAIT_OPTION** può essere utilizzato per controllare per quanto tempo il servizio deve attendere la risposta prima di restituire il controllo al thread chiamante.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **WAIT_OPTION** Indica per quanto tempo il servizio deve attendere la risposta dall'host remoto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) non ha ricevuto una risposta dall'host remoto prima del timeout.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è in grado di allocare un pacchetto per l'invio del messaggio CloseNotify.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) non è in grado di inviare il messaggio CloseNotify sul socket TCP.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_packet_buffer_set"></a>nx_secure_tls_session_packet_buffer_set

Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio associa un buffer di riassemblaggio del pacchetto a una sessione TLS. Per decrittografare e analizzare i record TLS in ingresso, è necessario assemblare i dati in ogni record dai pacchetti TCP sottostanti. I record TLS possono avere dimensioni fino a 16KB, anche se in genere sono molto più piccoli, quindi potrebbero non rientrare in un singolo pacchetto TCP.

Se si è certi che le dimensioni del messaggio in ingresso saranno inferiori al limite dei record TLS di 16KB, le dimensioni del buffer possono essere rese più piccole, ma per gestire i dati in ingresso sconosciuti il buffer deve essere reso il più grande possibile. Se un record in ingresso è più grande del buffer fornito, la sessione TLS termina con un errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **buffer_ptr** Puntatore al buffer usato da TLS per il riassemblaggio dei pacchetti.
- **BUFFER_SIZE** Dimensioni in byte del buffer fornito.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- Il puntatore della sessione TLS o il buffer di **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è valido.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_protocol_version_override"></a>nx_secure_tls_session_protocol_version_override

Eseguire l'override della versione del protocollo TLS predefinita per una sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a>Descrizione

Questo servizio esegue l'override della versione del protocollo TLS predefinita (più recente) utilizzata da una determinata sessione. Questo consente a NetX Secure TLS di usare una versione precedente di TLS per una sessione TLS specifica senza disabilitare le versioni più recenti di TLS in fase di compilazione. Questa operazione può essere utile nelle applicazioni che possono avere la necessità di comunicare con un host precedente che non supporta la versione più recente di TLS.

> [!IMPORTANT]
> *A partire dalla versione 5.11 SP3, NetX Secure TLS supporta RFC 7507 (vedere la nota di seguito) e qualsiasi override a una versione precedente con questa API determinerà l'invio di un SCSV di fallback in ClientHello. Se il server supporta una versione più recente di TLS e il SCSV di fallback è incluso in ClientHello, il server interromperà l'handshake TLS con un avviso "fallback non appropriato". SCSV viene inviato solo quando l'override della versione è una versione precedente di TLS rispetto a quella abilitata (ad esempio, se si sostituisce la versione a TLS 1,2, non verrà inviato alcun SCSV).*

I valori validi per il parametro protocol_version sono le macro seguenti: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 e NX_SECURE_TLS_VERSION_TLS_1_2.

Le macro NX_SECURE_TLS_DISABLE_TLS_1_1 e NX_SECURE_TLS_ENABLE_TLS_1_0 possono essere usate per controllare le versioni di TLS compilate nell'applicazione. La versione 1,2 di TLS è sempre abilitata.

Si noti che se l'host remoto non supporta la versione fornita, la connessione avrà esito negativo. solo la versione di sostituzione fornita verrà negoziata da NetX Secure TLS.

> [!IMPORTANT]
> RFC 7507: SCSV di fallback TLS. Questa RFC è stata introdotta per attenuare un problema di sicurezza che era originariamente causato da server che gestivano in modo errato la negoziazione del downgrade del protocollo e che invece rifiutavano messaggi ClientHello validi. Nel tentativo di mantenere la compatibilità con questi server obsoleti, alcune applicazioni client TLS hanno iniziato a ritentare gli handshake non riusciti con una versione precedente di TLS (ad esempio, TLS 1,2 non è riuscita, quindi provare TLS 1,1). Questa soluzione ha tuttavia introdotto un nuovo problema: un utente malintenzionato potrebbe forzare il downgrade di un client introducendo artificialmente un errore di rete o di pacchetto che causa la mancata connessione del server, anche quando il server supporta la versione più recente di TLS. Effettuando il downgrade a una versione precedente, l'autore dell'attacco potrebbe sfruttare i punti deboli in tale versione (SSLv3<sup>21</sup> in particolare è debole per l'attacco Poodle). Per evitare questa situazione, RFC 7507 introdued "fallback SCSV", uno pseudo-ciphersuite<sup>22</sup> inviato nel ClientHello che notifica a un server TLS quando un client TLS usa una versione di TLS che non è la versione più recente supportata. In questo modo, un server che supporta una versione più recente può rifiutare un ClientHello contenente il SCSV di fallback e impedire che il downgrade venga eseguito correttamente.

21. NetX Secure non implementa SSLv3 a causa dell'esistenza di debolezze gravi note, ad esempio POODLE.

22. Un ciphersuite, o SCSV (signaling Cipher Suite value), è un numero ciphersuite riservato usato per segnalare le implementazioni TLS abilitate sulle funzionalità non disponibili nelle versioni precedenti di TLS. I SCSV di fallback e i TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) sono esempi.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **protocol_version** Macro della versione TLS per la versione specifica di TLS da usare.

### <a name="return-values"></a>Valori restituiti

- Modifica dello stato **NX_SUCCESS** (0x00) riuscita.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) versione TLS nota ma non supportata.
- La versione del protocollo **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) non è valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_start
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_receive"></a>nx_secure_tls_session_receive

Ricevere dati da una sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve i dati dalla sessione TLS attiva specificata, gestendo la decrittografia dei dati prima di fornirli al chiamante nel parametro NX_PACKET. Se nella sessione specificata non viene accodato alcun dato, la chiamata viene sospesa in base all'opzione wait fornita.

> [!IMPORTANT]
> *Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **packet_ptr** Puntatore a un puntatore di pacchetto TLS allocato.
- **WAIT_OPTION** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_NO_PACKET** (0x01) non sono stati ricevuti dati.
- **NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio ricevuto non ha superato un controllo hash di autenticazione.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio ricevuto contiene una versione del protocollo sconosciuta nell'intestazione.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0X114) ha ricevuto un avviso TLS dall'host remoto.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a>nx_secure_tls_session_renegotiate_callback_set

Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un callback a una sessione TLS che verrà richiamata ogni volta che il primo messaggio di handshake di rinegoziazione della sessione viene ricevuto dall'host remoto.

La funzione di callback è concepita come una notifica all'applicazione a partire dall'inizio di un handshake di rinegoziazione. l'applicazione può scegliere di terminare la sessione TLS restituendo qualsiasi valore diverso da zero dal callback, in modo che TLS concluda la sessione TLS con un errore. Se l'applicazione desidera procedere con la rinegoziazione, il callback deve restituire NX_SUCCESS.

> [!NOTE]
> *A causa della semantica di rinegoziazione TLS, viene richiamato il callback per i client TLS sicuri NetX ogni volta che un HelloRequest viene ricevuto dal server remoto, ma non quando il client avvia la rinegoziazione. In NetX Secure TLS Servers, il callback verrà richiamato ogni volta che viene ricevuta una rinegoziazione ClientHello (qualsiasi ClientHello ricevuto nel contesto di una sessione TLS attiva). Ciò significa che il callback verrà richiamato se l'host remoto o l'applicazione locale ha avviato la rinegoziazione perché il server TLS invierà una HelloRequest a cui il client remoto risponderà.*

NetX Secure TLS implementa l'estensione Inidication di rinegoziazione sicura da RFC 5746 per assicurarsi che gli handshake di rinegoziazione non siano soggetti a attacchi man-in-the-Middle.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore all'istanza della sessione TLS.
- **func_ptr** Puntatore alla funzione di callback.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) assegnazione riuscita del callback.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido per la funzione di callback o la sessione TLS.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Simple callback notifying the user that a renegotiation is starting. */
ULONG tls_renegotiation_callback(NX_SECURE_TLS_SESSION *session)
{
    printf("Renegotiation initiated by remote host\n");

    return(NX_SUCCESS);
}

/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Set callback for renegotiation notification. */
status = nx_secure_tls_session_renegotiate_callback_set(&tls_session,
                                                tls_renegotiation_callback);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_start
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_renegotiate

## <a name="nx_secure_tls_session_renegotiate"></a>nx_secure_tls_session_renegotiate

Avviare un handshake di rinegoziazione della sessione con l'host remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un handshake di *rinegoziazione* della sessione con un host TLS remoto connesso. Una rinegoziazione è costituita da un secondo handshake TLS all'interno del contesto di una sessione TLS stabilita in precedenza. Ogni nuovo messaggio di handshake viene crittografato usando la sessione TLS finché non vengono generate nuove chiavi di sessione e vengono scambiati i messaggi ChangeCipherSpec, a quel punto le nuove chiavi vengono usate per crittografare tutti i messaggi.

Una rinegoziazione può essere avviata in qualsiasi momento dopo che è stata stabilita una sessione TLS. Se viene effettuato un tentativo di rinegoziazione durante un handshake TLS o prima che venga stabilita una sessione TLS, non verrà eseguita alcuna azione.

> [!NOTE]
> *Quando il servizio viene richiamato, viene eseguito un handshake TLS intero, quindi il tempo per il completamento e lo stato restituito variano a seconda delle impostazioni TLS correnti e dei parametri di sessione.*

NetX Secure TLS implementa l'estensione Inidication di rinegoziazione sicura da RFC 5746 per assicurarsi che gli handshake di rinegoziazione non siano soggetti a attacchi man-in-the-Middle.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore all'istanza della sessione TLS.
- **WAIT_OPTION** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione. Viene passato a tutti i servizi NetX in TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) rinegoziazioni riuscite.
- **NX_NO_PACKET** (0x01) non sono stati ricevuti dati.
- **NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio ricevuto non ha superato un controllo hash di autenticazione.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio ricevuto contiene una versione del protocollo sconosciuta nell'intestazione.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0X114) ha ricevuto un avviso TLS dall'host remoto.
- **NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0X134) la sessione TLS locale o remota è inattiva, rendendo impossibile la rinegoziazione.
- **NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0X13A) l'host remoto non ha fornito l'estensione SCSV o di rinegoziazione sicura e pertanto non è possibile eseguire la rinegoziazione.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.
- L'allocazione del pacchetto sottostante **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è riuscita.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Setup a client socket connection.  */
status = nx_tcp_client_socket_connect(&tcp_socket, server_ipv4_address,
REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

/* Start the TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Send some data in the first TLS session. (Check “status” for errors…)*/
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Hello there!\r\n", 14, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);

/* Now renegotiate the session. */
status  = nx_secure_tls_session_renegotiate(&tls_session, NX_WAIT_FOREVER);

/* If status == NX_SUCCESS, new TLS session keys have been generated. */

/* Send some data in the new TLS session. This will be encrypted using the new
   keys. */
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Another message…\r\n", 18, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_start
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_renegotiation_callback_set

## <a name="nx_secure_tls_session_reset"></a>nx_secure_tls_session_reset

Cancellare e reimpostare una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella una sessione TLS e Reimposta lo stato come se la sessione fosse stata appena creata in modo che un oggetto sessione TLS esistente possa essere riutilizzato per una nuova sessione.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) puntatore a sessione TLS non valido.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_send"></a>nx_secure_tls_session_send

Inviare dati tramite una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia i dati nel NX_PACKET fornito, usando la sessione TLS attiva specificata e gestendo la crittografia dei dati prima di inviarli all'host remoto. Se le ultime dimensioni della finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio sospende facoltativamente in base alle opzioni di attesa specificate.

> [!IMPORTANT]
> *A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **packet_ptr** Puntatore a un pacchetto TLS contenente i dati da inviare.
- **WAIT_OPTION** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del destinatario.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_NO_PACKET** (0x01) non sono stati ricevuti dati.
- **NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0X109) l'invio del socket TCP sottostante non è riuscito.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_packet_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_server_callback_set"></a>nx_secure_tls_session_server_callback_set

Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un puntatore a funzione a una sessione TLS che verrà richiamata da TLS quando un handshake del server TLS riceve un messaggio ClientHello. La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ClientHello ricevuto che richiede l'input o il processo decisionale.

Il callback viene eseguito con il blocco di controllo della sessione TLS chiamante e una matrice di oggetti NX_SECURE_TLS_HELLO_EXTENSION. La matrice di oggetti estensione deve essere passata in una funzione helper che troverà e analizzerà un'estensione specifica. Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi Hello, vedere *nx_secure_tls_session_sni_extension_parse*.

Il callback del server può essere usato anche per selezionare il certificato di identità attivo usando *nx_secure_tls_active_certificate_set* per il server TLS. Questo problema si verifica più spesso in risposta a un'estensione Indicazione nome server (SNI) che consente a un client TLS di indicare quale server si sta tentando di contattare. Per ulteriori informazioni, vedere i riferimenti per *nx_secure_tls_session_sni_extension_parse* e *nx_secure_tls_active_certificate_set* .

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **func_ptr** Puntatore alla funzione di callback del server TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) allocazione riuscita del puntatore a funzione.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Application-supplied function to map server DNS name to a specific certificate
   ID. The certificate ID is supplied by the application when the certificate is
   added with nx_secure_tls_server_certificate_add. */
UINT application_find_id_by_dns_name(NX_SECURE_X509_DNS_NAME *dns_name)
{
    if(strncmp(dns_name->nx_secure_x509_dns_name, “server_name”,
               dns_name->nx_secure_x509_dns_name_length) == 0)
    {
        /* DNS name matches one we know, return it’s ID. */
        return(0x12);
    }

    /* Unknown DNS name, return 0 to indicate no matching ID found. */
    return(0);
}

/* Callback routine used to process ClientHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the client). */
ULONG tls_server_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;
UINT cert_id;
NX_SECURE_X509_CERT *certificate;


    /* Find and parse a Server Name Indication (SNI) extension. */
    status = nx_secure_tls_session_sni_extension_parse(session, extensions,
                                                       num_extensions, &dns_name);

    if(status != NX_SUCCESS && status != NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
        /* Parsed an invalid extension, return the error. */
        return(status);
    }

    if(status == NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
            /* SNI extension not found, just return success to use the default
               certificate. */
            return(NX_SUCCESS);
    }

    /* Find the application-supplied numeric identifier for the specified DNS
       name provided by the remote client. */
    cert_id = application_find_id_by_dns_name(&dns_name);

    /* If cert_id is 0, just use the default identity certificate added with
       nx_secure_tls_local_certificate_add. */
    if(cert_id != 0)
    {
        /* Application found a matching name, find the certificate in our
           store. */
        status = nx_secure_tls_server_certificate_find(tls_session, &certificate,
                                                       cert_id);

        if(status != NX_SUCCESS)
        {
            /* Didn’t find a valid certificate with the supplied ID. Return an
               error so TLS can shut down the handshake. */
            return(NX_SECURE_TLS_CERTIFICATE_NOT_FOUND);
        }

        /* Set the active identity certificate – the certificate should have been
           added to the local store at application start with
           nx_secure_tls_local_certificate_add. */
        nx_secure_tls_active_certificate_set(session, certificate);
    }

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_server_callback_set(tls_session,
                                                            server_callback);

        /* If status is NX_SUCCESS the callback was added and will be invoked
           immediately after a ClientHello message is received. */

        return(status);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_active_certificate_set
- nx_secure_tls_session_sni_extension_parse
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find

## <a name="nx_secure_tls_session_sni_extension_parse"></a>nx_secure_tls_session_sni_extension_parse

Analizzare un'estensione di Indicazione nome server (SNI) ricevuta da un client TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a>Descrizione

Questo servizio è destinato a essere chiamato dall'interno di un callback di sessione del server TLS, aggiunto a una sessione TLS utilizzando nx_secure_tls_session_server_callback_set. Il callback viene richiamato dopo la ricezione di un messaggio ClientHello da un client TLS remoto e viene fornita una matrice di estensioni disponibili (e il numero di estensioni nella matrice). Tale matrice e la relativa lunghezza possono essere passate direttamente a questa routine per determinare se è presente un'estensione SNI. in caso contrario, viene restituito NX_SECURE_TLS_EXTENSION_NOT_FOUND che indica semplicemente che il client ha scelto di non proviceare l'estensione SNI (questo non è un errore).

Se viene rilevata l'estensione SNI, il nome DNS X. 509 fornito dal client TLS viene restituito nella struttura dns_name. Attualmente, l'estensione SNI fornisce solo una voce di nome DNS singola, che può essere usata dal server TLS per determinare quale certificato di identità inviare al client remoto. * *

La struttura NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo *nx_secure_x509_dns_name* e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*. La macro NX_SECURE_X509_DNS_NAME_MAX controlla la dimensione del buffer di nx_secure_x509_dns_name.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **estensioni** di Puntatore a una matrice di estensioni di TLS Hello (dal callback della sessione).
- **num_extensions** Numero di estensioni nella matrice (dal callback della sessione).
- **dns_name** Restituisce il nome DNS specificato nell'estensione SNI.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) l'analisi dell'estensione è riuscita.
- **NX_PTR_ERROR** (0x07) estensioni non valide per array o puntatore di sessione TLS.
- Impossibile trovare l'estensione SNI **NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136).
- Il formato dell'estensione SNI **NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_server_callback_set
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_server_callback_set
- nx_secure_tls_active_certificate_set

## <a name="nx_secure_tls_session_sni_extension_set"></a>nx_secure_tls_session_sni_extension_set

Impostare un nome DNS dell'estensione Indicazione nome server (SNI) da inviare a un server remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione client TLS di fornire un nome DNS del server preferito a un server TLS remoto usando l'estensione TLS Indicazione nome server (SNI). L'estensione SNI consente al server di selezionare il certificato di identità e i parametri appropriati in base alle preferenze del server indicate dal client. L'estensione SNI supporta attualmente solo un singolo nome DNS da inviare, quindi il parametro del nome singolare. Il parametro dns_name deve essere inizializzato con *nx_secure_x509_dns_name_initialize* e conterrà il server preferito del client. Per annullare il nome dell'estensione, è sufficiente chiamare questo servizio con un valore di parametro "dns_name" di NX_NULL.

La struttura NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo  *nx_secure_x509_dns_name* e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*. La macro NX_SECURE_X509_DNS_NAME_MAX controlla la dimensione del buffer di nx_secure_x509_dns_name.

> [!NOTE]
> *Questa routine deve essere chiamata prima che venga richiamato nx_secure_tls_session_start o ClientHello non conterrà l'estensione SNI.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **dns_name** Nome DNS fornito dall'applicazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) aggiunta del nome del server DNS completata.
- **NX_PTR_ERROR** (0x07) nome DNS o puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define TLS_SNI_SERVER_NAME “www.example.com”

NX_SECURE_X509_DNS_NAME dns_name;
NX_SECURE_TLS_SESSION client_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&client_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));


    /* Initialize the DNS server name we want to send in the SNI extension. */
    nx_secure_x509_dns_name_initialize(&dns_name, TLS_SNI_SERVER_NAME,
                                    strlen(TLS_SNI_SERVER_NAME));

    /* The SNI server name needs to be set prior to starting the TLS session. */
    nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);

   /* Start TLS session as normal. */
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_start
- nx_secure_x509_dns_name_initialize

## <a name="nx_secure_tls_session_start"></a>nx_secure_tls_session_start

Avviare una sessione TLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione TLS utilizzando il blocco di controllo della sessione TLS fornito e un socket TCP connesso. È necessario che la connessione TCP sia già stata completata in seguito a una chiamata riuscita a nx_tcp_client_socket_connect o nx_tcp_server_socket_accept.

Questo servizio determinerà il tipo di sessione TLS (client o server) dal socket TCP.

L'opzione wait definisce il comportamento del servizio mentre l'handshake TLS è in corso.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **tcp_socket_ptr** Puntatore a un socket TCP connesso.
- **WAIT_OPTION** Definisce il comportamento del servizio mentre è in corso l'handshake TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0X102) un tipo di messaggio TLS ricevuto non è corretto.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0X106) una crittografia fornita dall'host remoto non è supportata.
- L'elaborazione del messaggio **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) durante l'handshake TLS non è riuscita.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio in arrivo non ha superato un controllo Mac hash.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) non è stato possibile inviare un socket TCP sottostante.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0X10A) un messaggio in ingresso ha un campo di lunghezza non valido.
- **NX_SECURE_TLS_BAD_CIPHERSPEC** (0X10B) un messaggio ChangeCipherSpec in ingresso non è corretto.
- **NX_SECURE_TLS_INVALID_SERVER_CERT** (0X10C) un certificato TLS in ingresso è inutilizzabile per l'identificazione del server TLS remoto.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0X10D) la crittografia a chiave pubblica fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0X10E) l'host remoto non ha indicato ciphersuites supportati dallo stack TLS sicuro NETX.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio TLS ricevuto ha una versione di TLS sconosciuta nell'intestazione.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) un messaggio TLS ricevuto ha una versione di TLS nota ma non supportata nell'intestazione.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0X111) l'allocazione di pacchetti TLS interna non è riuscita.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0X112) l'host remoto ha fornito un certificato non valido.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0X114) l'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.
- **NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0X13B) una voce nella tabella ciphersuite include un puntatore a funzione null.
- **NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0X146) un ClientHello TLS remoto includeva il fallback SCSV andattempted un fallback della versione.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Initialize the TLS session structure. */
nx_secure_tls_session_create(&tls_session,
                              &nx_crypto_tls_ciphers,
                              crypto_metadata,
                              sizeof(crypto_metadata));

/* Setup the TLS packet reassembly buffer. */
status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                 sizeof(tls_packet_buffer));

/* Initialize a certificate for the TLS server. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data, 500,
NX_NULL, 0, private_key, 64);

/* If status is NX_SUCCESS, certificate is initialized. */

/* Add the certificate a local certificate to identify this TLS server. */
status = nx_secure_tls_add_local_certificate(&tls_session, &certificate);

/* If status is NX_SUCCESS, certificate was added successfully. */

/* Create and start a TCP socket as a server. */
/* NOTE: This assumes an IP instance called “ip_0” has already been created. */

/* Create a TCP server socket on the previously created IP instance, with normal
   delivery, IP fragmentation enabled, default time to live, a 8192-byte receive
   window, no urgent callback routine, and the "client_disconnect" routine to
   handle disconnection initiated from the other end of the connection.  */
status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Server Socket", NX_IP_NORMAL,
                               NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192, NX_NULL,
                               NX_NULL);

/* If status is NX_SUCCESS, the TCP socket was created successfully. */

/* Start up a TCP server socket by listening on port 443 with a listen queue of
   size 5. */
status =  nx_tcp_server_socket_listen(&ip_0, 443, &tcp_socket, 5, NX_NULL);

/* Application main loop. */
while(1)
{
        /* Accept incoming requests on the TCP socket. */
        status =  nx_tcp_server_socket_accept(&tcp_socket, NX_WAIT_FOREVER);

        /* At this point, the TCP socket should be established (but not the TLS
        session yet). */

        /* Start the TLS session on our active TCP socket. */
        status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                             NX_WAIT_FOREVER);

        /* At this point, if status is NX_SUCCESS, the TLS session has been
           established.  Application may now send/receive data through this
           channel. */

        /* Send and receive data using the TLS session. */
        /* Allocate TLS packets using nx_secure_tls_packet_allocate, write data with
           nx_packet_data_append, read data with nx_packet_data_extract_offset. */

        /* Send TLS data. */
        nx_secure_tls_session_send(&tls_session, &send_packet, NX_WAIT_FOREVER);

        nx_secure_tls_session_receive(&tls_session, &receive_packet_ptr,
        NX_WAIT_FOREVER);


        /* Once all application data is sent/received, end the TLS session. */
        status = nx_secure_tls_session_end(&tls_session);

        /* If status is NX_SUCCESS, the TLS session has been closed properly. */

        /* Now disconnect the TCP server socket from the client.  */
        nx_tcp_socket_disconnect(&tcp_socket, 200);

        /* Unaccept the TCP server socket.  Note that unaccept is called even if
           disconnect or accept fails.  */
        nx_tcp_server_socket_unaccept(&tcp_socket);

        /* Setup server socket for listening with this socket again.  */
        nx_tcp_server_socket_relisten(&ip_0, 443, &tcp_socket);
}

/* When the server application is shut down, clean up the TLS session. */
nx_secure_tls_session_delete(&tls_session);

/* Finally, clean up the TCP socket as well. */
nx_tcp_socket_delete(&tcp_socket);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_send
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_packet_allocate
- nx_secure_tls_session_end
- nx_secure_tls_session_create
- nx_tcp_socket_accept
- nx_tcp_socket_listen
- nx_tcp_socket_disconnect
- nx_tcp_socket_unaccept
- nx_tcp_socket_relisten
- nx_tcp_socket_delete
- nx_packet_allocate
- nx_packet_data_append
- nx_packet_data_extract_offset

## <a name="nx_secure_tls_session_time_function_set"></a>nx_secure_tls_session_time_function_set

Assegnare una funzione timestamp a una sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a>Descrizione

Questa funzione configura un puntatore a funzione che TLS richiamerà quando deve ottenere l'ora corrente, che viene utilizzata in vari messaggi di handshake TLS e per la verifica dei certificati.

Si prevede che la funzione restituisca il GMT corrente nel formato UNIX a 32 bit (secondi dalla mezzanotte del 1 ° gennaio 1970, UTC, ignorando i secondi intercalari), in base ai requisiti di ClientHello in TLS RFC 5246.

Se non viene assegnata alcuna funzione timestamp, verrà usato il valore 0 per il timestamp nell'handshake TLS e il controllo della scadenza del certificato non funzionerà.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza della sessione TLS.
- **time_func_ptr** Puntatore a una funzione che restituisce l'ora corrente (GMT) nel formato UNIX 32 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) puntatore a sessione TLS non valido.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* This function returns a 32-bit UNIX-style representation of the current GMT
   time. */
ULONG get_gmt_time(void)
{
ULONG time_value;

   /* Platform-specific time calculation goes here… */

   return(time_value);
}

/* Reset a TLS session.  */
status =  nx_secure_tls_timestamp_function_set(&tls_session, get_gmt_time);


/* If status is NX_SUCCESS the function was successfully added.*/
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_sendnx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_trusted_certificate_add"></a>nx_secure_tls_trusted_certificate_add

Aggiungere un certificato attendibile alla sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza di struttura NX_SECURE_X509_CERT inizializzata a una sessione TLS. Questo certificato viene usato dallo stack TLS per verificare i certificati forniti dall'host remoto durante l'handshake TLS.

Per la modalità client TLS sono necessari certificati attendibili.

I certificati attendibili sono necessari solo per la modalità server TLS se è abilitata l'autenticazione del certificato client.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificate_ptr** Puntatore a un'istanza di certificato TLS inizializzata.

### <a name="return-values"></a>Valori restituiti

- Aggiunta del certificato **NX_SUCCESS** (0x00) completata.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) ha tentato di aggiungere un certificato non valido.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Initialize certificate structure. */
status = nx_secure_x509_certificate_initialize(&certificate, certificate_data,
                                               certificate_buffer,
                                               sizeof(certificate_buffer), 500,
                                               private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_trusted_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_remove

## <a name="nx_secure_tls_trusted_certificate_remove"></a>nx_secure_tls_trusted_certificate_remove

Rimuovere il certificato attendibile dalla sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un certificato attendibile da una sessione TLS, con chiave nel campo nome comune nel certificato.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **common_name** Valore del nome comune del certificato da rimuovere.
- **common_name_length** Lunghezza della stringa del nome comune.

### <a name="return-values"></a>Valori restituiti

- Aggiunta del certificato **NX_SUCCESS** (0x00) completata.
- **NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.
- Il certificato **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) non è stato trovato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_add

## <a name="nx_secure_x509_certificate_initialize"></a>nx_secure_x509_certificate_initialize

Inizializzare il certificato X. 509 per NetX Secure TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_certificate_initialize(
                  NX_SECURE_X509_CERT *certificate_ptr,
                  const UCHAR *certificate_data,
                  USHORT certificate_data_length,
                  UCHAR *raw_data_buffer,
                  USHORT buffer_size,
                  const UCHAR *private_key_data,
                  USHORT private_key_data_length,
                  UINT private_key_type);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza una struttura di NX_SECURE_X509_CERT da un certificato digitale X. 509 con codifica binaria da usare in una sessione TLS.

I dati del certificato **devono** essere un certificato digitale X. 509 valido nel formato binario con codifica der. I dati possono essere determinati da qualsiasi origine (ad esempio file system, buffer costante compilato e così via), purché venga fornito un puntatore UCHAR a tali dati.

Il parametro *raw_data_buffer* e le relative dimensioni sono parametri facoltativi che specificano un buffer dedicato in cui i dati del certificato vengono copiati prima dell'analisi. Se raw_data_buffer viene passato come NX_NULL, la struttura NX_SECURE_X509_CERT punterà direttamente nella matrice di certificate_data (in questo caso buffer_size viene ignorato). Se raw_data_buffer viene passato come NX_NULL, ***non*** modificare i dati a cui punta il certificate_data puntatore o l'elaborazione del certificato probabilmente avrà esito negativo.

Il parametro della chiave privata è per i certificati di identità locali: la chiave privata viene usata dai server per decrittografare i dati delle chiavi in ingresso da un client (crittografato con la chiave pubblica del server) e dai client per verificarne l'identità a un server quando il server richiede un certificato client. Se si aggiunge una chiave privata con questa API, il certificato associato verrà automaticamente contrassegnato come certificato di identità per un'applicazione TLS. Quando si inizializzano i certificati per altri scopi (ad esempio, l'archivio attendibile), il *private_key_data* parametro deve essere passato come null, il *private_key_data_length* come 0 e il *private_key_type* deve essere passato come NX_SECURE_X509_KEY_TYPE_NONE.

Il parametro *private_key_type* indica la formattazione della chiave privata. Se ad esempio la chiave privata è una chiave privata RSA con codifica DER PKCS # 1, il private_key_type deve essere passato come NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, un tipo noto a NetX Secure che verrà analizzato immediatamente e salvato per un uso successivo.

Il private_key_type supporta anche i tipi di chiave definiti dall'utente<sup>23</sup> per le piattaforme e le applicazioni con formati chiave specifici o altre esigenze. Un motore di crittografia basato su hardware, ad esempio, può utilizzare un formato specifico non riconosciuto dal software NetX Secure, oppure una chiave privata può essere crittografata o rappresentata da un token crittografico come se si trattasse di un hardware di crittografia Trusted Platform Module (TPM) o PKCS # 11. Quando si usa un tipo di chiave definito dall'utente, i dati della chiave vengono passati Verbatim alla routine di crittografia appropriata. ad esempio, viene passata una chiave privata RSA, senza analisi o elaborazione, direttamente alla routine di crittografia RSA fornita a TLS nella tabella ciphersuite. Il tipo di chiave definito dall'utente viene inoltre passato alla routine di crittografia (nel caso di RSA, questo è il parametro "op").

L'intervallo di chiavi definite dall'utente copre la metà superiore di un Unsigned Integer a 32 bit, da 0x0001 0000-0xFFFF FFFF. I valori minori di 0x0001 0000 sono riservati per l'uso sicuro di NetX.

I tipi di chiave definiti dall'utente sono una funzionalità avanzata che richiede routine di crittografia personalizzate per gestire i dati della chiave privata non elaborata. Se questa funzionalità è necessaria, contattare il rappresentante della logica Express.

### <a name="parameters"></a>Parametri

- **certificate_ptr** Puntatore a un'istanza di un certificato X. 509 non inizializzato.
- **certificate_data** Puntatore ai dati binari X. 509 con codifica DER.
- **raw_data_buffer** Puntatore al buffer di dati del certificato dedicato facoltativo.
- **BUFFER_SIZE** Dimensioni del buffer di dati del certificato dedicato facoltativo.
- **certificate_data_length** Lunghezza in byte dei dati binari del certificato.
- **private_key_data** Puntatore ai dati facoltativi della chiave privata.
- **private_key_data_length** Lunghezza dei dati della chiave privata.
- **private_key_type** Identificatore del tipo di chiave.

### <a name="return-values"></a>Valori restituiti

- Aggiunta del certificato **NX_SUCCESS** (0x00) completata.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.
- I dati del certificato **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) non contengono un certificato X. 509 con codifica der.
- Il certificato **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) non dispone di una crittografia a chiave pubblica supportata da NETX Secure.
- Il certificato o la chiave privata **NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) non contiene una sequenza ASN. 1 valida.
- **NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0X18A) la chiave privata specificata non era una chiave RSA PKCS # 1 valida.
- **NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0X19D) il tipo di chiave privata fornito non è stato definito dall'utente e non corrisponde ad alcun tipo noto.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_local_certificate_add
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- Importazione di certificati X. 509 in NetX Secure nel capitolo 3.

## <a name="nx_secure_x509_common_name_dns_check"></a>nx_secure_x509_common_name_dns_check

Verificare il nome DNS rispetto al certificato X. 509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a>Descrizione

Questo servizio controlla il nome comune di un certificato rispetto a un nome di dominio principale (TLD) fornito dal chiamante ai fini della convalida DNS di un host remoto. Questa funzione di utilità è progettata per essere chiamata dall'interno di una routine di callback di convalida del certificato fornita dall'applicazione. Il nome TLD deve essere la parte superiore dell'URL usato per accedere all'host remoto (il "." -stringa separata prima della prima barra). Se il nome comune contiene un carattere jolly, ad esempio *. example.com, il carattere jolly corrisponderà a qualsiasi con lo stesso suffisso. Si noti che viene considerato solo il primo carattere jolly ("*") rilevato (lettura da destra a sinistra) per la corrispondenza con caratteri jolly, ad esempio ABC. *. example. com corrisponderà a *qualsiasi* nome che termina con ". example.com".

Se il nome comune non corrisponde alla stringa specificata, l'estensione "subjectAltName" viene analizzata (se presente nel certificato) e vengono confrontate anche le voci di DNSName. Se nessuna di queste voci corrisponde, viene restituito un errore.

È importante comprendere il formato del nome comune (e le voci subjectAltName) nei certificati previsti. Ad esempio, alcuni certificati possono utilizzare un indirizzo IP non elaborato o un carattere jolly. La stringa TLD DNS deve essere formattata in modo che corrisponda ai valori previsti nei certificati ricevuti.

### <a name="parameters"></a>Parametri

- **certificate_ptr** Puntatore a un'istanza del certificato X. 509.
- **dns_tld** Top-Level nome di dominio rispetto al quale eseguire il confronto.
- **dns_tld_length** Lunghezza della stringa TLD.

### <a name="return-values"></a>Valori restituiti

- Il confronto tra **NX_SUCCESS** (0x00) ha esito positivo con il nome comune o SubjectAltName.
- **NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0X195) non è stato trovato alcun nome corrispondente.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
UCHAR *tld = “www.example.com”;

    /* Check our DNS TLD against the certificate provided by the
       remote TLS host. */
    status = nx_secure_x509_common_name_dns_check(certificate, tld, strlen(tld));

        if(status != NX_SUCCESS)
        {
            /* TLD did not match any names in the certificate. */
            return(status);
        }

        /* DNS validation and any other checks were successful. */
        return(NX_SUCCESS);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_crl_revocation_check

## <a name="nx_secure_x509_crl_revocation_check"></a>nx_secure_x509_crl_revocation_check

Controllare il certificato X. 509 in base a un elenco di revoche di certificati (CRL) fornito

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a>Descrizione

Questo servizio accetta un elenco di revoche di certificati con codifica DER e cerca un certificato specifico in tale elenco. L'emittente del CRL viene convalidato in base a un archivio certificati fornito, l'emittente CRL viene convalidato in modo che corrisponda a quello per il certificato sottoposto a verifica e il numero di serie del certificato in questione viene usato per la ricerca nell'elenco dei certificati revocati. Se le autorità emittenti corrispondono, la firma si estrae e il certificato **non** è presente nell'elenco, la chiamata ha esito positivo. Tutti gli altri casi provocano la restituzione di un errore.

### <a name="parameters"></a>Parametri

- **crl_data** Puntatore a un CRL con codifica DER.
- **crl_length** Lunghezza in byte dei dati CRL.
- **Archivio** di Puntatore a un archivio certificati X. 509.
- **certificate_ptr** Puntatore a un'istanza del certificato X. 509.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la convalida ha esito positivo che il certificato non è stato revocato.
- Impossibile trovare il certificato dell'autorità emittente CRL **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119).
- Il certificato dell'autorità emittente del certificato **NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) non è stato trovato.
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0X182) il CRL ASN. 1 conteneva un campo di lunghezza non valido.
- **NX_SECURE_X509_UNEXPECTED_ASN1_TAG (0x189)** Il CRL contiene ASN. 1 non valido.
- **NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0X18C) la verifica della catena di certificati non è riuscita.
- **NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0X197) CRL e le autorità emittenti di certificati non corrispondono.
- **NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0X198) la firma CRL non è valida.
- **NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0X199) il certificato verificato è stato trovato nel CRL ed è quindi revocato.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* CRL obtained for the expected certificate issuer through some means (downloaded
   from server manually, obtained from CRL endpoint, etc…) */
const UCHAR *crl_data;
UINT crl_length = 300;

/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
NX_SECURE_X509_CERTIFICATE_STORE *store;

    /* Obtain a certificate store to check against. In the certificate callback,
       it usually makes the most sense to use the store associated with the TLS
       session. */
    store = &session -> nx_secure_tls_credentials.nx_secure_tls_certificate_store;

    /* Check our certificate against the CRL and TLS certificate store. */
    status = nx_secure_x509_crl_revocation_check(crl, crl_length, store,
                                                 certificate);

        if(status != NX_SUCCESS)
        {
            if(status == NX_SECURE_X509_CRL_CERTIFICATE_REVOKED)
            {
                /* Certificate was revoked. */
               return(status);
            }
            else
            {
               /* CRL was invalid or some other issue. In this case the certificate
                  may still be valid since the CRL itself was a problem. At this
                  point it is up to the application to decide whether to continue
                  with the TLS handshake. For this example, assume certificate is
                  valid (faulty CRL is a possible Denial-of-Service attack).*/
               status = NX_SUCCESS;
        }

    /* Other certificate checking can go here. */

    /* Return status of certificate checks. */
    return(status);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_common_name_dns_check

## <a name="nx_secure_x509_dns_name_initialize"></a>nx_secure_x509_dns_name_initialize

Inizializzare una struttura del nome DNS X. 509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza un nome DNS X. 509 da usare con determinati servizi API che richiedono un formato di nome specifico. Ad esempio, il servizio *nx_secure_tls_sni_extension_parse* prevede un oggetto NX_SECURE_X509_DNS_NAME in modo che corrisponda al nome fornito da un host remoto nell'estensione indicazione nome server durante l'handshake TLS. Un nome DNS è semplicemente una stringa charater con lunghezza, ovvero la lunghezza massima consentita di un nome DNS (e la dimensione del buffer interno in NX_SECURE_X509_DNS_NAME) è controllata dalla macro NX_SECURE_X509_DNS_NAME_MAX (valore predefinito 100 byte).

### <a name="parameters"></a>Parametri

- **dns_name** Struttura del nome DNS da inizializzare.
- **name_string** Dati della stringa del nome DNS.
- **lunghezza** Lunghezza della stringa del nome.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) inizializzazione riuscita.
- **NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) è stata superata la stringa del nome specificata NX_SECURE_X509_DNS_NAME_MAX.
- **NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_sni_extension_parse
- nx_secure_tls_session_sni_extension_set

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a>nx_secure_x509_extended_key_usage_extension_parse

Trovare e analizzare un'estensione per l'utilizzo delle chiavi estese X. 509 in un certificato X. 509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a>Descrizione

Questo servizio è destinato a essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)*. Eseguirà la ricerca di un OID di utilizzo chiave esteso specifico all'interno di un certificato X. 509 e restituirà se l'OID è presente. Il key_usage parametro è un mapping di tipo Integer di OID che viene utilizzato internamente da NetX Secure X. 509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.

Nella tabella seguente vengono forniti i OID rilevanti per l'estensione utilizzo chiavi avanzato. Una tipica implementazione del client TLS che desidera controllare l'utilizzo della chiave estesa in un certificato del server TLS ricevuto verificherebbe l'esistenza dell'OID NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH: se l'estensione è presente, ma tale OID non lo è, il certificato verrebbe considerato non valido per identifiying l'host come server TLS e il callback di verifica del certificato dovrebbe restituire un errore. Se non è presente l'estensione, è possibile che l'applicazione proceda o meno con l'handshake TLS.

Nel callback di verifica del certificato, il codice restituito dall'errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'utilizzo da parte dell'applicazione. Se si verifica un errore durante il controllo dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare la causa dell'errore.

| Identificatore sicuro NetX                                | Valore OID         | Descrizione                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH   | 1.3.6.1.5.5.7.3.1 | Il certificato può essere usato per identificare un server TLS |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH   | 1.3.6.1.5.5.7.3.2 | Il certificato può essere usato per identificare un client TLS |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING  | 1.3.6.1.5.5.7.3.3 | Il certificato può essere usato per firmare il codice             |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT | 1.3.6.1.5.5.7.3.4 | Il certificato può essere usato per firmare i messaggi di posta elettronica           |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING | 1.3.6.1.5.5.7.3.8 | Il certificato può essere usato per firmare i timestamp       |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING  | 1.3.6.1.5.5.7.3.9 | Il certificato può essere usato per firmare le risposte OCSP   |

OID e mapping per l'estensione utilizzo chiavi esteso X. 509

### <a name="parameters"></a>Parametri

- **certificato** di Puntatore al certificato da verificare.
- **KEY_USAGE** Mapping Integer OID dalla tabella precedente.

### <a name="return-values"></a>Valori restituiti

- È stato trovato l'OID di utilizzo della chiave specificato **NX_SUCCESS** (0x00).
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) è stato rilevato un tag a più byte ASN. 1 (certificato non supportato).
- È stato rilevato il campo ASN. 1 **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) invaild (certificato non valido).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) classe di tag ASN. 1 non valida rilevata (certificato non valido).
- È stata rilevata un'estensione di **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0X192) non valida. certificato non valido.
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Impossibile trovare l'estensione utilizzo chiavi avanzato nel certificato fornito.
- Puntatore al certificato **NX_PTR_ERROR** (0x07) non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT* certificate)
{
UINT status;

    /* Extended key usage - look for specific OIDs. */
    status = nx_secure_x509_extended_key_usage_extension_parse(certificate,
                        NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH);

    if(status != NX_SUCCESS)
    {
        if(NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND)
        {
            printf("Extended key usage extension not found or specified key usage OID not
                    provided in extension.\n");
            /* The certificate was valid but the specified OID was not found. The
               application can decide whether to continue or abort the TLS handshake. */
            return(NX_SECURE_X509_KEY_USAGE_ERROR);
        }
        else
        {
            /* The extension or certificate was invalid. */
            return(status);
        }
    }

    /* The specified OID was found, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extension_find

## <a name="nx_secure_x509_extension_find"></a>nx_secure_x509_extension_find

Trovare e restituire un'estensione X. 509 in un certificato X. 509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a>Descrizione

Questo servizio è destinato a essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)* ed è un servizio X. 509 avanzato.

La funzione eseguirà la ricerca di un'estensione specifica all'interno di un certificato X. 509 in base a un OID e restituirà se l'OID è presente, insieme a una struttura che contiene riferimenti ai dati di estensione non elaborati pertinenti. Il extension_id parametro è un mapping di tipo Integer di OID che viene utilizzato internamente da NetX Secure X. 509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.

Le funzioni di supporto fornite per estensioni specifiche (ad esempio *nx_secure_x509_key_usage_extension_parse*) chiamano nx_secure_x509_extension_find internamente per ottenere i dati dell'estensione.

Nella tabella seguente vengono forniti i OID rilevanti per le estensioni X. 509 note.

La struttura NX_SECURE_X509_EXTENSION contiene puntatori al certificato X. 509 che consentono alle funzioni di supporto, ad esempio *nx_secure_x509_key_usage_extension_parse* di decodificare rapidamente i dati ASN. 1 con codifica der di estensione non elaborata.

Per informazioni sulle estensioni specifiche, vedere RFC 5280 (specifica X. 509) o il riferimento per le funzioni di supporto appropriate, se disponibili.

La versione corrente di NetX Secure X. 509 ha un supporto limitato per le estensioni X. 509. In futuro verranno aggiunte altre funzioni helper.

> [!IMPORTANT]
> *Questo servizio è una funzionalità avanzata per gli utenti che hanno familiarità con le estensioni X. 509 e la codifica DER ASN. 1. Viene fornito per consentire a tali utenti di accedere alle estensioni per le quali NetX Secure X. 509 attualmente non fornisce funzioni di supporto. Per tali estensioni senza funzioni di supporto, sarà necessario analizzare il file ASN. 1 con codifica DER non elaborato.*

| Identificatore sicuro NetX                              | Valore OID | Descrizione                                                                    | Funzione helper? |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES  | 2.5.29.9  | Attributi di directory: attributi di informazioni di base sul soggetto del certificato  | No               |
| NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID       | 2.5.29.14 | Usato per identificare una chiave pubblica specifica                                         | No               |
| NX_SECURE_TLS_X509_TYPE_KEY_USAGE             | 2.5.29.15 | Fornisce informazioni sugli utilizzi validi per la chiave pubblica del certificato              | Sì              |
| NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME     | 2.5.29.17 | Fornisce nomi DNS alternativi per identificare il certificato                     | Sì<sup>24</sup>        |
| NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME      | 2.5.29.18 | Fornisce nomi DNS alternativi per identificare l'emittente del certificato            | No               |
| NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS     | 2.5.29.19 | Fornisce informazioni di base sui vincoli di utilizzo del certificato                        | No               |
| NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS      | 2.5.29.30 | Usato per vincolare i nomi dei certificati a domini specifici                        | No               |
| NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION      | 2.5.29.31 | Fornisce gli URI per la distribuzione CRL                                             | No               |
| NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES  | 2.5.29.32 | Elenco dei criteri di certificato per i sistemi PKI di grandi dimensioni                             | No               |
| NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS | 2.5.29.33 | Elenco dei criteri del certificato della CA                                                | No               |
| NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID     | 2.5.29.35 | Usato per identificare una chiave pubblica specifica associata a una firma del certificato | No               |
| NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS    | 2.5.29.36 | Vincoli dei criteri della CA                                                          | No               |
| NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE   | 2.5.29.37 | Informazioni aggiuntive sull'utilizzo della chiave basato su OID                                     | Sì              |
| NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL          | 2.5.29.46 | Fornisce informazioni per ottenere Delta CRL                                  | No               |
| NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY     | 2.5.29.54 | Campo certificato CA che indica che non è possibile usare AnyPolicy                  | No               |

OID e mapping per le estensioni X. 509

24. L'estensione SubjectAltName viene analizzata come parte del controllo del nome DNS nel servizio nx_secure_x509_common_name_dns_check.

### <a name="parameters"></a>Parametri

- **certificato** di Puntatore al certificato da verificare.
- **estensione** di Struttura restituita contenente il puntatore e la lunghezza dei dati di estensione.
- **extension_id** Mapping Integer OID dalla tabella precedente.

### <a name="return-values"></a>Valori restituiti

- È stato trovato un OID di estensione specificato **NX_SUCCESS** (0x00) e i dati restituiti.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) è stato rilevato un tag a più byte ASN. 1 (certificato non supportato).
- È stato rilevato il campo ASN. 1 **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) invaild (certificato non valido).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) classe di tag ASN. 1 non valida rilevata (certificato non valido).
- Rilevata estensione **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0X192) non valida
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0X19B) l'OID di estensione specificato non è stato trovato nel certificato fornito.
- **NX_PTR_ERROR** (0x07) o un puntatore di estensione non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Function to parse a Basic Constraints X.509 extension. */
UINT _basic_constraints_extension_parse(NX_SECURE_X509_CERT *certificate)
{
const UCHAR             *current_buffer;
ULONG                    length;
UINT                     status;
NX_SECURE_X509_EXTENSION extension_data;

    /* Find the Basic Constraints extension in the certificate. */
    status = _nx_secure_x509_extension_find(certificate, &extension_data,
                              NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS);

    /* See if extension present - it might be OK if not present! */
    if (status != NX_SUCCESS)
    {
        return(status);
    }

    /* The extension_data structure now points to the raw extension ASN.1
      (DER-encoded). */
    current_buffer = extension_data.nx_secure_x509_extension_data;
    length = extension_data.nx_secure_x509_extension_data_length;

   /* Extension ASN.1 parsing… */

   return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extended_key_usage_extension_parse

## <a name="nx_secure_x509_key_usage_extension_parse"></a>nx_secure_x509_key_usage_extension_parse

Trovare e analizzare un'estensione per l'utilizzo della chiave X. 509 in un certificato X. 509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a>Descrizione

Questo servizio è destinato a essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)*. Eseguirà la ricerca dell'estensione per l'utilizzo delle chiavi e, se presente, restituirà l'utilizzo della chiave bit nel parametro "bit".

I bit, come definito dalla specifica X. 509 (RFC 5280) sono forniti nella tabella seguente. Un operatore AND bit per bit con la maschera di bit appropriata (e il controllo di un valore diverso da zero) fornirà il valore di ogni bit.

Si noti che la codifica DER del bit Elimina gli zeri aggiuntivi, in modo che la posizione effettiva dei bit nei dati del certificato non elaborato sarà probabilmente diversa dalle rispettive posizioni nel bit decodificato. Le maschere di bit fornite sono destinate solo all'uso nei bit decodificati restituiti da *nx_secure_x509_key_usage_extension_parse* e non con i dati del certificato con codifica der non elaborati.

Nel callback di verifica del certificato, il codice restituito dall'errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'utilizzo da parte dell'applicazione. Se si verifica un errore durante il controllo dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare la causa dell'errore.

| Identificatore sicuro NetX                            | Posizione del bit | Descrizione                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE  | 0            | Il certificato può essere usato per le firme digitali                                                                                                               |
| NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION    | 1            | Il certificato può essere usato per verificare le firme digitali diverse da quelle per i certificati e i CRL                                                              |
| NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT   | 2            | Il certificato può essere usato per crittografare le chiavi simmetriche (trasporto chiavi)                                                                                            |
| NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT  | 3            | Il certificato può essere usato per crittografare direttamente i dati utente non elaborati (non comune)                                                                                         |
| NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT      | 4            | Il certificato può essere usato per il contratto chiave (come con Diffie-Hellman)                                                                                           |
| NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN     | 5            | Il certificato può essere usato per firmare e verificare altri certificati (il certificato è un certificato CA o ICA).                                                  |
| NX_SECURE_X509_KEY_USAGE_CRL_SIGN           | 6            | Chiave pubblica del certificato usata per verificare le firme nei CRL                                                                                                  |
| NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY      | 7            | Utilizzato con il bit del contratto chiave (bit 4): quando è impostato, la chiave del certificato può essere utilizzata solo per la crittografia durante il contratto di chiave. Non definito se il bit del contratto chiave non è impostato. |
| NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY      | 8            | Utilizzato con il bit del contratto chiave (bit 4): quando è impostato, la chiave del certificato può essere utilizzata solo per la decrittografia durante il contratto di chiave. Non definito se il bit del contratto chiave non è impostato. |

Maschere di maschera e valori per l'estensione utilizzo chiavi X. 509

### <a name="parameters"></a>Parametri

- **certificato** di Puntatore al certificato da verificare.
- **bit** Restituisce l'intero bit dall'estensione.

### <a name="return-values"></a>Valori restituiti

- È stata rilevata l'estensione utilizzo chiavi **NX_SUCCESS** (0x00) e bit restituito.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) è stato rilevato un tag a più byte ASN. 1 (certificato non supportato).
- È stato rilevato il campo ASN. 1 **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) invaild (certificato non valido).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) classe di tag ASN. 1 non valida rilevata (certificato non valido).
- È stata rilevata un'estensione di **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0X192) non valida. certificato non valido.
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Impossibile trovare l'estensione utilizzo chiavi nel certificato fornito.
- **NX_PTR_ERROR** (0x07) certificato non valido o puntatore bit.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session,
  NX_SECURE_X509_CERT* certificate)
{
UINT status;
USHORT key_usage_bitfield;

    /* Key usage – extract key usage bitfield. */
    status = nx_secure_x509_key_usage_extension_parse(certificate, &key_usage_bitfield);

   /* Check certificate for a few specific key usage bits. */
   if((key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE) == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION)   == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT)  == 0)
    {
        printf("Expected key usage bitfield bits not set!\n");
        return(NX_SECURE_X509_KEY_USAGE_ERROR);
    }

    /* The specified bits were set, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_extended_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extension_find
