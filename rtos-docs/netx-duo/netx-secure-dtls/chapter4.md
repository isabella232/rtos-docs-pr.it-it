---
title: Capitolo 4 - Descrizione dei Azure RTOS DTLS sicuri di NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX Secure DTLS elencati in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 45966e7c8ea9be18bf294e8a7540e7226e803f29ae4f3ad3faaa29e4939c2ed8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801843"
---
# <a name="chapter-4-description-of-azure-rtos-netx-secure-dtls-services"></a>Capitolo 4: Descrizione dei Azure RTOS DTLS sicuri di NetX

Questo capitolo contiene una descrizione di tutti Azure RTOS netx secure DTLS (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla macro **NX_SECURE_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- [nx_secure_dtls_client_session_start](#nx_secure_dtls_client_session_start)
- [nx_secure_dtls_packet_allocate](#nx_secure_dtls_packet_allocate)
- [nx_secure_dtls_psk_add](#nx_secure_dtls_psk_add)
- [nx_secure_dtls_server_create](#nx_secure_dtls_server_create)
- [nx_secure_dtls_server_delete](#nx_secure_dtls_server_delete)
- [nx_secure_dtls_server_local_certificate_add](#nx_secure_dtls_server_local_certificate_add)
- [nx_secure_dtls_server_local_certificate_remove](#nx_secure_dtls_server_local_certificate_remove)
- [nx_secure_dtls_server_notify_set](#nx_secure_dtls_server_notify_set)
- [nx_secure_dtls_server_psk_add](#nx_secure_dtls_server_psk_add)
- [nx_secure_dtls_server_session_send](#nx_secure_dtls_server_session_send)
- [nx_secure_dtls_server_session_start](#nx_secure_dtls_server_session_start)
- [nx_secure_dtls_server_start](#nx_secure_dtls_server_start)
- [nx_secure_dtls_server_stop](#nx_secure_dtls_server_stop)
- [nx_secure_dtls_server_trusted_certificate_add](#nx_secure_dtls_server_trusted_certificate_add)
- [nx_secure_dtls_server_trusted_certificate_remove](#nx_secure_dtls_server_trusted_certificate_remove)
- [nx_secure_dtls_server_x509_client_verify_configure](#nx_secure_dtls_server_x509_client_verify_configure)
- [nx_secure_dtls_server_x509_client_verify_disable](#nx_secure_dtls_server_x509_client_verify_disable)
- [nx_secure_dtls_session_client_info_get](#nx_secure_dtls_session_client_info_get)
- [nx_secure_dtls_session_create](#nx_secure_dtls_session_create)
- [nx_secure_dtls_session_delete](#nx_secure_dtls_session_delete)
- [nx_secure_dtls_session_end](#nx_secure_dtls_session_end)
- [nx_secure_dtls_session_local_certificate_add](#nx_secure_dtls_session_local_certificate_add)
- [nx_secure_dtls_session_local_certificate_remove](#nx_secure_dtls_session_local_certificate_remove)
- [nx_secure_dtls_session_receive](#nx_secure_dtls_session_receive)
- [nx_secure_dtls_session_reset](#nx_secure_dtls_session_reset)
- [nx_secure_dtls_ session_send](#nx_secure_dtls_-session_send)
- [nx_secure_dtls_session_trusted_certificate_add](#nx_secure_dtls_session_trusted_certificate_add)
- [nx_secure_dtls_session_trusted_certificate_remove](#nx_secure_dtls_session_trusted_certificate_remove)


## <a name="nx_secure_dtls_client_session_start"></a>nx_secure_dtls_client_session_start

Avviare una sessione client DTLS protetta da NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_client_session_start(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        NX_UDP_SOCKET *udp_socket,
                        NXD_ADDRESS *ip_address, UINT port,
                        UINT wait_option);

```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione client DTLS, connettendosi al server all'indirizzo IP e alla porta UDP specificati, usando il socket UDP fornito per le comunicazioni di rete.

Il blocco di controllo della sessione DTLS deve essere inizializzato prima di chiamare questo servizio usando nx_secure_dtls_session_create. Inoltre, il client DTLS richiede che almeno un certificato ca attendibile sia stato aggiunto alla sessione usando nx_secure_dtls_session_trusted_certificate_add o le chiavi precondidite siano abilitate e configurate.

### <a name="parameters"></a>Parametri

- **dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.
- **udp_socket** Socket UDP inizializzato che verrà usato per stabilire le comunicazioni di rete con il server DTLS remoto.
- **ip_address** Puntatore alla struttura di indirizzi IP contenente l'indirizzo del server DTLS remoto.
- **porta** Socket UDP inizializzato che verrà usato per stabilire le comunicazioni di rete con il server DTLS remoto.
- **wait_option** Opzione di sospensione per il tentativo di connessione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Assegnazione del certificato alla sessione completata.
- **NX_NOT_CONNECTED** (0x38) Il server non può essere raggiunto all'indirizzo e alla porta specificata.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Un tipo di messaggio TLS/DTLS ricevuto non è corretto.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Una crittografia fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) L'elaborazione del messaggio durante l'handshake TLS non è riuscita.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio in arrivo non ha superato un controllo MAC hash.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) L'invio di un socket TCP sottostante non è riuscito.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Un messaggio in arrivo ha un campo di lunghezza non valido.
- **NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) Un messaggio ChangeCipherSpec in ingresso non è corretto.
- **NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) Un certificato TLS in ingresso non è utilizzabile per identificare il server DTLS remoto.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) La crittografia a chiave pubblica fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) L'host remoto non ha indicato ciphersuit supportati dallo stack DTLS sicuro NetX.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio DTLS ricevuto ha una versione DTLS sconosciuta nell'intestazione.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Un messaggio DTLS ricevuto ha una versione DTLS nota ma non supportata nell'intestazione.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Un'allocazione interna di pacchetti TLS non è riuscita.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) L'host remoto ha fornito un certificato non valido.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) L'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.
- **NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) Una voce nella tabella ciphersuite ha un puntatore a funzione NULL.
- **NX_PTR_ERROR** (0x07) Sessione, socket o puntatore indirizzo non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                           &nx_crypto_tls_ciphers,
                                           crypto_metadata,
                                           sizeof(crypto_metadata),
                                           packet_buffer,
                                           sizeof(packet_buffer),
                                           REMOTE_CERT_NUMBER,
                                           remote_certs_buffer,
                                           sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
       Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                      trusted_cert_der,
                                      trusted_cert_der_len,
                                      NX_NULL, 0, NX_NULL, 0,
                                      NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                   &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                  &udp_socket, &server_ip,
                                                  4443,
                                                  NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
      /* Error! */
      return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_session_receive, nx_secure_dtls_session_send,
- nx_secure_dtls_session_create

## <a name="nx_secure_dtls_packet_allocate"></a>nx_secure_dtls_packet_allocate

Allocare un pacchetto per una sessione DTLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_packet_allocate(
                              NX_SECURE_DTLS_SESSION *session_ptr,
                         NX_PACKET_POOL *pool_ptr,
                         NX_PACKET **packet_ptr,
                              ULONG wait_option);

```

### <a name="description"></a>Descrizione

Questo servizio alloca un NX_PACKET per la sessione DTLS attiva specificata dal NX_PACKET_POOL. Questo servizio deve essere chiamato dall'applicazione per allocare pacchetti di dati da inviare tramite una connessione DTLS. La sessione DTLS deve essere inizializzata prima di chiamare questo servizio.

Il pacchetto allocato viene inizializzato correttamente in modo che i dati di intestazione e piè di pagina DTLS possano essere aggiunti dopo che i dati del pacchetto sono stati popolati. In caso contrario, il comportamento è identico *nx_packet_allocate*.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS.
- **pool_ptr** Puntatore a un NX_PACKET_POOL da cui allocare il pacchetto.
- **packet_ptr** Puntatore di output al pacchetto appena allocato.
- **wait_option** Opzione di sospensione per l'allocazione dei pacchetti.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'allocazione dei pacchetti è riuscita.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) L'allocazione dei pacchetti sottostante non è riuscita.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione DTLS fornita non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a new DTLS packet from the previously created packet pool and
previously initialized DTLS session.   */

status = nx_secure_dtls_packet_allocate(&dtls_session, &pool_0, &packet_ptr,
                                                              NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in
the variable packet_ptr.  */

```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize, nx_secure_dtls_session_create,
- nx_secure_dtls_session_trusted_certificate_add,
- nx_secure_dtls_session_send, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_end, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_psk_add"></a>nx_secure_dtls_psk_add

Aggiungere una chiave precondi shared a una sessione DTLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_psk_add(NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una chiave precondi shared (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo sessione DTLS. La chiave PSK viene usata al posto di un certificato digitale quando le ciphersuit PSK sono abilitate e usate.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.
- **pre_shared_key** Valore PSK effettivo.
- **psk_length** Lunghezza del valore PSK.
- **psk_identity** Stringa usata per identificare questo valore PSK.
- **identity_length** Lunghezza dell'identità PSK.
- **hint** Stringa usata per indicare il gruppo di psk tra cui scegliere in un server TLS.
- **hint_length** Lunghezza della stringa di hint.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta corretta di PSK.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione DTLS non valido.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Impossibile aggiungere un'altra chiave PSK.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_psk_add(&dtls_session, psk,
                            sizeof(psk), “psk_1”, 4,
                            “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */


```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_psk_add, nx_secure_dtls_client_session_create

## <a name="nx_secure_dtls_server_create"></a>nx_secure_dtls_server_create

Creare un server NetX Secure DTLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_create(
                NX_SECURE_DTLS_SERVER *server_ptr, NX_IP *ip_ptr,
                UINT port, ULONG timeout, VOID *session_buffer,
                UINT session_buffer_size,
                const NX_SECURE_TLS_CRYPTO *crypto_table,
                VOID *crypto_metadata_buffer, ULONG crypto_metadata_size,
                UCHAR *packet_reassembly_buffer,
                UINT packet_reassembly_buffer_size,
                UINT (*connect_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session,
                              NXD_ADDRESS *ip_address, UINT port),
                UINT (*receive_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session)));

```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza di un server DTLS per gestire le richieste DTLS in ingresso su una determinata porta UDP. A causa del fatto che UDP è senza stato, le richieste DTLS provenienti da più client possono essere inviate su una singola porta mentre altre sessioni DTLS sono attive. Il server è quindi necessario per mantenere le sessioni attive e instradare correttamente i messaggi in ingresso al gestore appropriato.

Il ip_ptr punta a un'istanza NX_IP da usare per il socket UDP interno associato al server DTLS (e archiviato nel blocco NX_SECURE_DTLS_SERVER controllo). L'istanza IP e la porta vengono usate per definire l'interfaccia UDP su cui viene creata un'istanza del server con il nx_secure_dtls_server_start servizio.

Il parametro buffer di sessione viene usato per contenere i blocchi di controllo per tutte le possibili sessioni DTLS simultanee per il server DTLS. Deve essere allocato con una dimensione pari a un multiplo pari delle dimensioni della struttura NX_SECURE_DTLS_SESSION blocco di controllo.

Per calcolare le dimensioni dei metadati necessarie, è possibile usare nx_secure_tls_metadata_size_calculate api.

Il parametro packet_reassembly_buffer viene usato da DTLS per riassemblare datagrammi UDP in un record DTLS completo ai fini della decrittografia e deve essere sufficientemente grande da contenere il record DTLS più grande previsto (16 KB è la dimensione massima del record DTLS, ma molte applicazioni non inviano tale quantità di dati in un singolo record).

La connect_notify di callback viene richiamata ogni volta che un nuovo client DTLS si connette al server. L'applicazione deve quindi avviare la sessione DTLS usando il servizio *nx_secure_dtls_server_session_start*. Anche se la sessione può essere avviata nel callback stesso, è consigliabile usare il callback solo per notificare al thread dell'applicazione (o al thread DTLS dedicato creato dall'applicazione) la connessione quando il callback viene richiamato dal thread IP usato per elaborare tutte le elaborazioni di rete di livello inferiore (ad esempio UDP). Questo può essere semplice come salvare il parametro di sessione DTLS (fornito come parametro al callback) e richiamare nx_secure_dtls_server_session_start nell'altro thread. Il callback connect_notify deve in genere restituire NX_SUCCESS.

La routine di callback receive_notify viene richiamata ogni volta che viene ricevuto un record DTLS che corrisponde a una sessione DTLS esistente (l'indirizzo IP dell'host remoto e la porta vengono usati per identificare una sessione esistente). Rappresenta i "dati dell'applicazione" crittografati e inviati tramite DTLS. L'applicazione deve chiamare il *nx_secure_dtls_session_receive* nella sessione DTLS specificata per recuperare i dati ricevuti. Come per il callback connect_receive, è consigliabile passare la sessione a un altro thread per gestire l'elaborazione del messaggio quando il callback viene richiamato dal thread IP. Il callback receive_notify deve in genere restituire NX_SUCCESS.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **ip_ptr** Puntatore a un blocco NX_IP di controllo inizializzato da utilizzare come interfaccia di rete per il server DTLS.
- **porta** Porta UDP locale a cui è associato il socket UDP del server DTLS.
- **timeout** Valore di timeout da utilizzare per le operazioni di rete.
- **session_buffer** Spazio del buffer per contenere blocchi di controllo per tutte NX_SECURE_DTLS_SESSION assegnate a questa istanza del server DTLS.
- **session_buffer_size** Dimensioni del buffer di sessione. Questo determina il numero di sessioni DTLS assegnate al server DTLS.
- **crypto_table** Puntatore a una struttura di tabella di crittografia TLS/DTLS usata per tutte le operazioni di crittografia.
- **crypto_metadata_buffer** Spazio del buffer per i calcoli delle operazioni di crittografia e informazioni sullo stato.
- **crypto_metadata_size** Dimensione del buffer dei metadati.
- **packet_reassembly_buffer** Buffer usato da DTLS per riassemblare i dati UDP in record DTLS per la decrittografia.
- **packet_reassembly_buffer_size** Dimensioni del buffer di riassemblaggio. In genere deve essere maggiore di 16 KB, ma può essere più piccolo a seconda dell'applicazione.
- **connect_notify** Routine di callback richiamata ogni volta che un client DTLS remoto tenta di connettersi a questo server DTLS.
- **receive_notify** Callback richiamato ogni volta che i dati dell'applicazione vengono ricevuti in una sessione DTLS esistente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_PARAMETERS** (0x4D) Spazio del buffer insufficiente per sessioni, riassemblaggio di pacchetti o crittografia.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
    *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE, dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                        device_cert_der_len, NX_NULL, 0,
                        device_cert_key_der, device_cert_key_der_len,
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);

        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                           NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                                                   &send_packet, NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data,
        let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done, stop the server
    instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add

## <a name="nx_secure_dtls_server_delete"></a>nx_secure_dtls_server_delete

Liberare le risorse usate da un server DTLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_delete(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio libera le risorse allocate a un'istanza del server DTLS, incluso il socket UDP interno usato dal server.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del server completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_STILL_BOUND** (0x42) il socket UDP è ancora associato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
*ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer, sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);


    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                         NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                        &packet_pool,
                                                        &send_packet,
                                                        NX_IP_PERIODIC_RATE);

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_server_local_certificate_add"></a>nx_secure_dtls_server_local_certificate_add

Aggiungere un certificato di identità del server locale a un server DTLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_local_certificate_add(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                 NX_SECURE_X509_CERT *certificate,
                                 UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un certificato di identità del server locale a un'istanza del server DTLS. È necessario almeno un certificato di identità per la connessione dei client a un server DTLS, a meno che non venga usato un meccanismo di autenticazione alternativo, ad esempio chiavi precondizioni.

Il cert_id è un identificatore numerico diverso da zero per il certificato. In questo modo il certificato può essere facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X.509 presente nell'archivio server DTLS. Per altre informazioni sui certificati server X.509, vedere la Guida dell'utente di NetX Secure TLS.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **certificato** Puntatore a una struttura di certificato X.509 inizializzata in precedenza.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato al server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_PARAMETERS** (0x4D) È stato passato un ID certificato 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

*Vedere le informazioni di *nx_secure_dtls_server_create* per un esempio più completo.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                            certificate_der_data,
                            sizeof(certificate_der_data),
                            NX_NULL, 0,
                            certificate_key_der_data,
                            sizeof(certificate_key_der_data),
                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_local_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_local_certificate_remove"></a>nx_secure_dtls_server_local_certificate_remove

Rimuovere un certificato di identità del server locale da un server DTLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_local_certificate_remove(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                   UCHAR *common_name,
                                   UINT common_name_length,
                                   UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio rimuove un certificato di identità del server locale da un'istanza del server DTLS. È necessario almeno un certificato di identità per la connessione dei client a un server DTLS, a meno che non venga usato un meccanismo di autenticazione alternativo, ad esempio chiavi precondizioni.

Il certificato da rimuovere può essere identificato dal relativo nome comune X.509 o dal cert_id numerico assegnato nella chiamata *a nx_secure_dtls_server_local_certificate_add*. Il cert_id viene usato solo per identificare il certificato e viene gestito dall'applicazione. Se si usa il nome comune anziché l'identificatore di certificato numerico, il cert_id parametro deve essere impostato su 0.

> [!NOTE]
> La rimozione di un certificato durante l'elaborazione di un handshake DTLS comporta un comportamento imprevisto. Il servizio *nx_secure_dtls_server_stop* deve essere chiamato prima di rimuovere i certificati.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **common_name** X.509 CommonName del certificato da rimuovere. Se viene usato, passare cert_id come zero.
- **common_name_length** Lunghezza della common_name stringa in byte.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS. Se viene usato, passare NX_NULL per il parametro common_name.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rimozione del certificato dal server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Non è stato trovato alcun certificato corrispondente cert_id o common_name nel server DTLS specificato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        certificate_der_data,
                                        sizeof(certificate_der_data),
                                        NX_NULL, 0, certificate_key_der_data,
                                        sizeof(certificate_key_der_data),
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                     &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);

    /* At some point in the future we decide to remove the certificate we added.
    We can use the certificate identifier we passed into the call to
    nx_secure_dtls_local_certificate_add (value = 1); */
    status = nx_secure_dtls_server_local_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_notify_set"></a>nx_secure_dtls_server_notify_set

Assegnare routine di callback di notifica facoltative a un server DTLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_notify_set(
                         NX_SECURE_DTLS_SERVER *server_ptr,
                         UINT (*disconnect_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session),
                         UINT (*error_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session,
                                      UINT error_code));

```

### <a name="description"></a>Descrizione

Questo servizio può essere usato per aggiungere routine di callback di notifica facoltative a un server DTLS. Entrambi i parametri di callback possono essere passati come NX_NULL se si desidera un solo callback.

Il disconnect_notify callback viene richiamato quando un client remoto termina una sessione DTLS. Il dtls_session parametro è l'istanza di sessione che è stata chiusa. Il callback deve in genere restituire NX_SUCCESS.

Il error_notify callback viene richiamato ogni volta che si verifica un errore o un timeout DTLS. Il dtls_session è l'istanza di sessione per cui si è verificato l'errore e error_code è il codice di stato numerico per l'errore che ha causato il problema (vedere Appendice A)

Codici di errore/restituzione sicura NetX per un elenco di codici di errore che possono essere restituiti. Il callback deve in genere restituire NX_SUCCESS.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **disconnect_notify** Routine di callback richiamata ogni volta che un host client remoto chiude una sessione DTLS.
- **error_notify** Routine di callback richiamata ogni volta che DTLS rileva un errore o un timeout.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Assegnazione riuscita delle routine di callback.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

UINT disconnect_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
NXD_ADDRESS client_ip_addr;
UINT client_port;
UINT local_port;

    /* We have received a disconnection notice (CloseNotify message) from a
       remote client. Application can use the dtls_session parameter for any
       desired processing. */

    /* See what client disconnected by extracting its IP address and port.
       NOTE: depending on how the session ended, the client information may
             no longer be available. */
    status  = nx_secure_dtls_session_client_info_get(dtls_session,
                                                    &ip_addr,
                                                    &client_port,
                                                    &local_port);

    return(NX_SUCCESS);
}

UINT error_notify(NX_SECURE_DTLS_SESSION *dtls_session, UINT error_code)
{
    /* The DTLS server has encountered an error or timeout condition. We
    can use the error_code parameter to determine the error and we
    can insect the dtls_session for more information. */

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Other setup (e.g. certificates) goes here … */

    status = nx_secure_dtls_server_notify_set(&dtls_server, disconnect_notify,
                                                                 error_notify);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop

## <a name="nx_secure_dtls_server_psk_add"></a>nx_secure_dtls_server_psk_add

Aggiungere una chiave precondi shared a un server DTLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_psk_add(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *pre_shared_key, UINT psk_length,
                                UCHAR *psk_identity,
                                UINT identity_length, UCHAR *hint,
                                UINT hint_length);

```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una chiave precondi shared (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo server DTLS. La chiave PSK viene usata al posto di un certificato digitale quando le ciphersuit PSK sono abilitate e usate.

La chiave PSK aggiunta viene replicata in tutte le sessioni DTLS assegnate al server DTLS (tramite il buffer di sessione specificato nella chiamata a nx_secure_dtls_server_create).

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **pre_shared_key** Valore PSK effettivo.
- **psk_length** Lunghezza del valore PSK.
- **psk_identity** Stringa usata per identificare questo valore PSK.
- **identity_length** Lunghezza dell'identità PSK.
- **hint** Stringa usata per indicare il gruppo di psk tra cui scegliere in un server TLS.
- **hint_length** Lunghezza della stringa di hint.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta corretta di PSK.
- **NX_PTR_ERROR** (0x07) Puntatore al server DTLS non valido.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Impossibile aggiungere un'altra chiave PSK.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_server_psk_add(&dtls_server, psk, sizeof(psk), “psk_1”,
   4, “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_psk_add, nx_secure_dtls_server_create

## <a name="nx_secure_dtls_server_session_send"></a>nx_secure_dtls_server_session_send

Inviare dati tramite una sessione DTLS stabilita con un server NetX Secure DTLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_session_send(
                                NX_SECURE_DTLS_SESSION *session_ptr,
                               NX_PACKET *packet_ptr);

```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto di dati su una sessione del server DTLS stabilita a un host client DTLS remoto. La sessione utilizzata viene ottenuta nella routine receive_notify callback fornita a nx_secure_dtls_session_create.

I dati forniti nel pacchetto, che devono essere allocati tramite *nx_secure_dtls_packet_allocate ,* vengono crittografati usando le routine e i parametri di crittografia della sessione DTLS e quindi inviati all'host remoto tramite la porta UDP interna del server DTLS all'indirizzo IP e alla porta del client collegato (archiviati nella sessione DTLS).

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS ottenuta receive_notify routine di callback fornita dall'applicazione.
- **packet_ptr** Puntatore a un'istanza NX_PACKET allocata in precedenza e popolata con i dati dell'applicazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Si è verificato un errore nell'operazione di invio UDP sottostante.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;


/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key
    and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        device_cert_der,
                                        device_cert_der_len,
                                        NX_NULL,
                                        0, device_cert_key_der,
                                        device_cert_key_der_len,
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

}

/* If not processing connections or received data, let the thread sleep. */
if(!connect_flag && !receive_flag)
{
    tx_thread_sleep(100);
}
    }

    /* Server processing is done, stop the server instance
    from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_create,
- nx_secure_dtls_server_session_start, nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add

## <a name="nx_secure_dtls_server_session_start"></a>nx_secure_dtls_server_session_start

Avviare una sessione DTLS da un server NetX Secure DTLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_session_start(
                 NX_SECURE_DTLS_SESSION *session_ptr, UINT wait_option);

```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione del server DTLS eseguendo l'handshake DTLS sul lato server quando un client DTLS remoto si è connesso al server e ha richiesto una connessione DTLS.

La sessione DTLS viene ottenuta nella routine connect_notify callback fornita a nx_secure_dtls_server_create.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS ottenuta da un callback del connect_notify DTLS.
- **wait_option** Valore di attesa ThreadX da usare per le operazioni di rete.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Non è stato possibile allocare un pacchetto di handshake DTLS (pool di pacchetti vuoto).
- **NX_SECURE_TLS_INVALID_PACKET** (0x104) i dati che non erano un record DTLS valido.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Non è stato possibile eseguire correttamente l'hashing di un record DTLS (errore di crittografia).
- **NX_SECURE_TLS_PADDING_CHECK_FAILED** controllo della 0x12A (0x12A) di crittografia.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Ha generato un avviso dall'host remoto durante l'handshake DTLS.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Ricevuto un messaggio non riconosciuto durante l'handshake DTLS.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) È stato rigenerato un record DTLS con una lunghezza non valida.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) Ha ricevuto un clientHello senza crittografia DTLS supportata.
- **NX_SECURE_TLS_BAD_COMPRESSION_METHOD** (0x118) Ha riappiato un clientHello con un metodo di compressione sconosciuto.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) di handshake generico (non specificato), in genere a causa di problemi con l'elaborazione dell'estensione.
- **NX_SECURE_TLS_UNSUPPORTED_FEATURE** (0x130) Una funzionalità non ancora supportata è stata richiamata durante l'handshake DTLS.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) È stato rilevato un crittografico sconosciuto (è stato indicato un errore di crittografia interno).
- **NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) Ha riappiato un record DTLS con una versione DTLS non corrispondente.
- **NX_SECURE_TLS_FINISHED_HASH_FAILURE** (0x115) Non è stato possibile convalidare l'hash dell'handshake DTLS, la sessione non è valida.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) l'invio UDP interno non è riuscito.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
* DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len, NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                    &packet_pool, &send_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done,
    stop the server instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_create, nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add

## <a name="nx_secure_dtls_server_start"></a>nx_secure_dtls_server_start

Avviare un'istanza del server NetX Secure DTLS in ascolto sulla porta UDP configurata

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_start(
                  NX_SECURE_DTLS_SERVER *server_ptr);

```

### <a name="description"></a>Descrizione

Questo servizio avvia un server DTLS. Al termine della chiamata, il server è attivo e inizierà a elaborare le richieste in ingresso dai client DTLS. L'istanza del server deve essere stata configurata con il *servizio nx_secure_dtls_server_create*.

> [!NOTE]
> Questo servizio associa la porta UDP del server DTLS interna alla porta locale configurata, quindi la maggior parte dei problemi riscontrati dovrà essere a che fare con le comunicazioni UDP e la configurazione di rete.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio del server riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_NOT_ENABLED** UDP (0x14) non abilitato.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta UDP disponibile.
- **NX_INVALID_PORT** (0x46) Porta UDP non valida.
- **NX_ALREADY_BOUND** (0x22) UDP già associata.
- **NX_PORT_UNAVAILABLE** (0x23) UDP non disponibile per l'uso.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                &send_packet, NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
                (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_stop, nx_secure_dtls_server_create,
- nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,
- nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_server_stop"></a>nx_secure_dtls_server_stop

Arrestare un'istanza del server NetX Secure DTLS attiva

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_stop(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'ascolto di un server DTLS sulla porta UDP configurata e reimposta tutte le sessioni DTLS associate, interrompendo eventuali comunicazioni DTLS in corso.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS attiva.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto riuscito del server.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* We have exited the processing loop, stop the server. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,
- nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_server_trusted_certificate_add"></a>nx_secure_dtls_server_trusted_certificate_add

Aggiungere un certificato CA attendibile a un server NetX Secure DTLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_trusted_certificate_add(
                                         NX_SECURE_DTLS_SERVER *server_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un certificato CA attendibile o intermedio a un'istanza del server DTLS e assegnato a tutte le sessioni interne del server DTLS. Questa operazione è necessaria solo se l'autenticazione del certificato client X.509 è abilitata *usando nx_secure_dtls_server_x509_client_verify_configure*. Il certificato aggiunto verrà usato per verificare i certificati X.509 client in ingresso.

Il cert_id è un identificatore numerico diverso da zero per il certificato. In questo modo il certificato può essere facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X.509 presente nell'archivio server DTLS. Per altre informazioni sui certificati server X.509, vedere la Guida dell'utente di NetX Secure TLS.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **certificato** Puntatore a una struttura di certificato X.509 inizializzata in precedenza.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato al server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_PARAMETERS** (0x4D) È stato passato un ID certificato 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

*Vedere le informazioni di *nx_secure_dtls_server_create* per un esempio più completo.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0, NX_NULL,
                                            0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add trusted CA certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_local_certificate_add,
- nx_secure_dtls_server_trusted_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_trusted_certificate_remove"></a>nx_secure_dtls_server_trusted_certificate_remove

Rimuovere un certificato ca attendibile da un server DTLS sicuro NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_server_trusted_certificate_remove(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *common_name,
                                UINT common_name_length,
                                UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio rimuove un certificato ca attendibile da un'istanza del server DTLS. I certificati ca attendibili sono necessari solo per un server DTLS per cui la verifica del certificato client X.509 è stata abilitata chiamando *nx_secure_dtls_server_x509_client_verify_configure*.

Il certificato da rimuovere può essere identificato dal relativo nome comune X.509 o dal cert_id numerico assegnato nella chiamata a *nx_secure_dtls_server_trusted_certificate_add*. Il cert_id viene usato solo per identificare il certificato e viene gestito dall'applicazione. Se si usa il nome comune anziché l'identificatore di certificato numerico, il cert_id parametro deve essere impostato su 0.

> [!NOTE]
> La rimozione di un certificato durante l'elaborazione di un handshake DTLS può comportare un comportamento imprevisto. Il servizio *nx_secure_dtls_server_stop* deve essere chiamato prima di rimuovere i certificati.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **common_name** X.509 CommonName del certificato da rimuovere. Se viene usato, passare cert_id come zero.
- **common_name_length** Lunghezza della common_name stringa in byte.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS. Se viene usato, passare NX_NULL per il parametro common_name.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rimozione del certificato dal server DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Non è stato trovato alcun certificato corrispondente cert_id o common_name nel server DTLS specificato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                                    certificate_der_data,
                                                    sizeof(certificate_der_data),
                                                    NX_NULL, 0, NX_NULL, 0,
                                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                       &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);


/* At some point in the future we decide to remove the certificate we added. We can
       use the certificate identifier we passed into the call to
       nx_secure_dtls_trusted_certificate_add (value = 1); */
    status = nx_secure_dtls_server_trusted_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_x509_client_verify_configure"></a>nx_secure_dtls_server_x509_client_verify_configure

Configurare un server DTLS sicuro NetX per richiedere e verificare i certificati client

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_server_x509_client_verify_configure(
                           NX_SECURE_DTLS_SERVER *server_ptr,
                               UINT certs_per_session,
                               UCHAR *certs_buffer, ULONG buffer_size);

```

### <a name="description"></a>Descrizione

Questo servizio configura un server DTLS per richiedere e verificare i certificati client DTLS. Questa funzionalità facoltativa viene usata quando si desiderano certificati X.509 per l'autenticazione client al posto di altri meccanismi,ad esempio una chiave precondidizione.

> [!IMPORTANT]
> *Quando un server DTLS è configurato per verificare i certificati client tramite questo servizio, è necessario aggiungere almeno un certificato CA attendibile al server usando nx_secure_dtls_server_trusted_certificate_add oppure il server rifiuterà tutte le connessioni client in ingresso perché non sarà in grado di verificare i certificati client nell'archivio attendibile.*

Dopo aver chiamato questo servizio, l'istanza del server DTLS richiederà (una volta avviato) i certificati client come parte dell'handshake DTLS. Supponendo che il client sia configurato correttamente con un certificato di identità (e una catena di certificati associata, se applicabile), il server DTLS richiede l'allocazione della memoria per elaborare i dati del certificato client. Questa memoria viene passata come *parametro certs_buffer.*

Il certs_buffer deve essere ridimensionato per supportare la catena di certificati prevista più grande da un client DTLS, volte il numero di sessioni *del server DTLS.* Il buffer viene suddiviso tra le sessioni disponibili usando *il parametro certs_per_session* che rappresenta il numero massimo previsto di certificati in una catena di certificati client. Il buffer deve anche fornire spazio per la struttura NX_SECURE_X509_CERT dati utilizzata per analizzare i dati del certificato.

Il calcolo delle dimensioni del buffer appropriate può essere eseguito con la formula seguente:

```C
buffer_size = (# of DTLS sessions in server) *
                (certs_per_session) *
                (    maximum expected certificate size +
                      sizeof(NX_SECURE_X509_CERT)    )

```

- Il numero di sessioni DTLS è determinato dalle dimensioni del buffer di sessione passato in nx_secure_dtls_server_create.
- certs_per_session deve essere impostato sul numero massimo previsto di certificati in qualsiasi catena di certificati client.
- Le dimensioni massime previste del certificato dipendono dall'applicazione, dalle dimensioni delle chiavi e da altri fattori, ma 2 KB è in genere sufficiente.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.
- **certs_per_session** Numero di certificati da allocare a ogni sessione del server DTLS.
- **certs_buffer** Spazio del buffer per i dati del certificato in ingresso.
- **buffer_size** Dimensioni del buffer del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Configurazione corretta della verifica client X.509.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_PARAMETERS** (0x4D) Archivio certificati non valido (istanza DTLSserver non initalizzata?).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                                    sizeof(certificate_der_data),
                                    NX_NULL, 0,
                                    NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_x509_client_verify_disable,
- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_x509_client_verify_disable"></a>nx_secure_dtls_server_x509_client_verify_disable

Disabilita la verifica del certificato X.509 client per un server NetX Secure DTLS

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_server_x509_client_verify_disable(
                           NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita la verifica del certificato client X.509 in un server DTLS. Il servizio non ha alcun effetto se la verifica del certificato client X.509 non è abilitata.

> [!NOTE]
> La disabilitazione dell'autenticazione client in un'istanza del server DTLS attiva può comportare un comportamento imprevedibile. Il nx_secure_dtls_server_stop deve essere chiamato prima di modificare lo stato del server.

### <a name="parameters"></a>Parametri

- **server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Disabilitazione dell'autenticazione client X.509 completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                        sizeof(certificate_der_data), NX_NULL, 0,
                        NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before changing state. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* Disable X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_disable(&dtls_server);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_x509_client_verify_configure,
- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_client_info_get"></a>nx_secure_dtls_session_client_info_get

Ottenere informazioni sul client remoto da una sessione del server DTLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_session_client_info_get(
                                    NX_SECURE_DTLS_SESSION *session_ptr,
                                    NXD_ADDRESS *client_ip_address,
                                    UINT *client_port, UINT *local_port);

```

### <a name="description"></a>Descrizione

Questo servizio restituisce le informazioni di rete su un client DTLS connesso a una sessione specifica del server DTLS. Le informazioni restituite sono costituite dall'indirizzo IP e dalla porta UDP del client remoto, nonché dalla porta del server locale a cui è connesso il client.

In generale, l'istanza di sessione DTLS sarà quella ottenuta nella chiamata di una delle routine di callback di notifica DTLS(ad esempio, i callback connect_notify o receive_notify passati in nx_secure_dtls_server_create).

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione del server DTLS attiva.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del server completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_SOCKET** (0x13) Il socket UDP associato non è valido (sessione non inizializzata?).
- **NX_NOT_CONNECTED** (0x38) il socket UDP non è connesso: la connessione client è stata interrotta o non è ancora stata stabilita.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array
   or list in case a new connection is
   attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
                                                            *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    NXD_ADDRESS client_ip;
    UINT client_port, server_port;

    /* Get DTLS client information which can be used in filtering or associating
       the DTLS session with application data (e.g. a session pointer table). */
    status = nx_secure_dtls_session_client_info_get(dtls_session, &client_ip,
   &client_port, &server_port);

    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_server_start, nx_secure_dtls_server_stop,
- nx_secure_dtls_server_create, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_session_create"></a>nx_secure_dtls_session_create

Creare e configurare una sessione DTLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_session_create(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        VOID *metadata_buffer, ULONG metadata_size,
                        UCHAR *packet_reassembly_buffer,
                        UINT packet_reassembly_buffer_size,
                        UINT certs_number,
                        UCHAR *remote_certificate_buffer,
                        ULONG remote_certificate_buffer_size));

```

### <a name="description"></a>Descrizione

Questo servizio crea e configura una sessione DTLS. In genere, verrà usato per creare sessioni client DTLS poiché le sessioni del server DTLS vengono gestite con il meccanismo del server DTLS (vedere *nx_secure_dtls_server_create*), ma in alcuni casi un'applicazione deve creare una singola istanza di sessione del server DTLS autonomo, nel qual caso questo servizio può essere usato <sup>7.</sup>

I parametri configurano le informazioni e l'allocazione di memoria necessarie per creare un'istanza di una sessione DTLS. Il crypto_table è una tabella TLS contenente tutte le routine crittografiche necessarie per la crittografia e l'autenticazione TLS/DTLS. Il metadata_buffer viene usato per le caclulation di crittografia (vedere nx_secure_tls_metadata_size_calculate nella Guida utente di NetX Secure TLS) e il packet_reassembly_buffer viene usato per riassemblare i datagrammi UDP in un record DTLS completo per la decrittografia.

I certs_number e remote_certificate_buffer sono necessari per i client DTLS che necessitano di spazio per archiviare ed elaborare la catena di certificati del server DTLS in ingresso. Il buffer deve essere in grado di contenere le dimensioni massime previste della catena di certificati per qualsiasi server a cui si connetterà. Il buffer è suddiviso per il numero di certificati previsti (parametro certs_number) e deve essere sufficientemente grande da contenere una struttura NX_SECURE_X509_CERT per ogni certificato. Le dimensioni del buffer possono essere determinate usando la formula seguente:

```C
remote_certificate_buffer_size = (certs_number) *
                 (maximum cert size + sizeof(NX_SECURE_X509_CERT))
```

- certs_number è il numero massimo previsto di certificati nella catena di certificati del server
- Le dimensioni massime del certificato dipendono dalle dimensioni delle chiavi usate e dalle informazioni nel certificato, ma in genere sono sufficienti 2 KB.

**7** La creazione di sessioni del server DTLS con questa routine non è consigliata e presenta alcune limitazioni. Il problema principale è che la sessione non gestirà correttamente altre connessioni client, poiché UDP è senza connessione, un secondo client può legalmente inviare dati alla porta UDP del server quando una sessione DTLS precedente è ancora attiva, causando la chiusura della sessione del server con un errore.

### <a name="parameters"></a>Parametri

- **dtls_session** Puntatore a una struttura di sessione DTLS non inizializzata.
- **crypto_table** Puntatore a una struttura di tabella di crittografia TLS/DTLS usata per tutte le operazioni di crittografia.
- **crypto_metadata_buffer** Spazio del buffer per i calcoli delle operazioni di crittografia e informazioni sullo stato.
- **crypto_metadata_size** Dimensione del buffer dei metadati.
- **packet_reassembly_buffer** Buffer usato da DTLS per riassemblare i dati UDP in record DTLS per la decrittografia.
- **packet_reassembly_buffer_size** Dimensioni del buffer di riassemblaggio. In genere deve essere maggiore di 16 KB, ma può essere più piccolo a seconda dell'applicazione.
- **certs_number** Numero massimo previsto di certificati nella catena di certificati del server remoto.
- **remote_certificate_buffer** Spazio del buffer per i dati del certificato in ingresso.
- **remote_certificate_buffer_size** Dimensioni del buffer del certificato.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione della sessione completata.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione o buffer non valido.
- **NX_INVALID_PARAMETERS** (0x4D) Spazio del buffer insufficiente per il riassemblaggio dei pacchetti, i certificati o la crittografia.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
    &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                            &udp_socket, &server_ip,
                                            4443,
                                            NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session,
                                            &receive_packet,
                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_client_session_start,nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send

## <a name="nx_secure_dtls_session_delete"></a>nx_secure_dtls_session_delete

Liberare le risorse usate da una sessione DTLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_session_delete(
                        NX_SECURE_DTLS_SESSION *dtls_session);

```

### <a name="description"></a>Descrizione

Questo servizio elimina una sessione DTLS, liberando tutte le risorse allocate al momento della creazione.

### <a name="parameters"></a>Parametri

- **dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione della sessione completata.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione o buffer non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                        trusted_cert_der,
                                        trusted_cert_der_len,
                                        NX_NULL, 0, NX_NULL, 0,
                                        NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                    &udp_socket,
                                                    &server_ip, 4443,
                                                    NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                &receive_packet,
                                                NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_session_end"></a>nx_secure_dtls_session_end

Arrestare una sessione DTLS protetta di NetX attiva

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_session_end(NX_SECURE_DTLS_SESSION *dtls_session,
                                UINT wait_option);

```

### <a name="description"></a>Descrizione

Questo servizio termina una sessione DTLS attiva inviando un avviso CLOSENotify TLS/DTLS all'host remoto. L'indirizzo IP e la porta usati sono quelli usati nella chiamata precedente a nx_secure_dtls_session_send.

### <a name="parameters"></a>Parametri

- **dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.
- **wait_option** Valore di attesa ThreadX da usare per le operazioni di rete.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione della sessione completata.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione o buffer non valido.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Impossibile allocare pacchetti per l'avviso CloseNotify.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) Probabile errore interno: routine crittografica non riconosciuta.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) L'invio UDP sottostante non è riuscito.
- **NX_IP_ADDRESS_ERROR** (0x21) Errore con indirizzo IP dell'host remoto.
- **NX_NOT_BOUND** (0x24) Socket UDP sottostante non associato alla porta.
- **NX_INVALID_PORT** (0x46) Porta UDP non valida.
- **NX_PORT_UNAVAILABLE** (0x23) la porta UDP non è disponibile per l'uso.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session,
                                        NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

    }

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_session_local_certificate_add"></a>nx_secure_dtls_session_local_certificate_add

Aggiungere un certificato di identità locale a una sessione DTLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_session_local_certificate_add(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            NX_SECURE_X509_CERT *certificate,
                            UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un certificato di identità locale a un'istanza di sessione DTLS. In generale, questo servizio verrà usato quando una sessione client DTLS deve fornire un certificato di identità a un host server remoto. Si tratta di una configurazione facoltativa per DTLS, quindi un certificato non è generalmente necessario per i client DTLS. Un certificato di identità richiede una chiave privata associata.

Il cert_id è un identificatore numerico diverso da zero per il certificato. In questo modo il certificato può essere facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X.509 presente nell'archivio certificati DTLS. Per altre informazioni sui certificati X.509, vedere la Guida dell'utente di NetX Secure TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.
- **certificato** Puntatore a una struttura di certificato X.509 inizializzata in precedenza.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato alla sessione DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_PARAMETERS** (0x4D) È stato passato un ID certificato 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

*Vedere le informazioni di *nx_secure_dtls_session_create* per un esempio più completo.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity
certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

/* Create a TLS session for our socket. Ciphers and metadata defined
   elsewhere. See nx_secure_tls_session_create reference for more
   information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
{
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
}

/* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

/* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                              &certificate, 1);

    /* Initialize local server identity certificate with key and
    add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                        certificate_der_data,
                        sizeof(certificate_der_data),
                        NX_NULL, 0,
                        certificate_key_der_data,
                        sizeof(certificate_key_der_data),
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                    &certificate, 1);

/* Set up IP address of remote host. */
server_ip.nxd_ip_version = NX_IP_VERSION_V4;
server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


/* Now we can start the DTLS session as normal. */
status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                    &udp_socket, &server_ip, 4443,
                                    NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_local_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_local_certificate_remove"></a>nx_secure_dtls_session_local_certificate_remove

Rimuovere un certificato di identità locale da una sessione DTLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_session_local_certificate_remove(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         UCHAR *common_name,
                                         UINT common_name_length, UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio rimuove un certificato di identità locale da un'istanza di sessione DTLS usando un numero ID certificato (assegnato quando il certificato è stato aggiunto con nx_secure_dtls_session_local_certificate_add) o il campo CommonName X.509.

Se il common_name viene usato per trovare la corrispondenza con il certificato, il parametro cert_id deve essere impostato su 0. Se cert_id viene usato, common_name deve essere passato un valore di NX_NULL.

Il cert_id è un identificatore numerico diverso da zero per il certificato. In questo modo il certificato può essere facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X.509 presente nell'archivio certificati DTLS. Per altre informazioni sui certificati X.509, vedere la Guida dell'utente di NetX Secure TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.
- **common_name** Puntatore alla stringa CommonName di cui trovare la corrispondenza.
- **common_name_length** Lunghezza della common_name stringa.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rimozione del certificato dalla sessione DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Non è stato trovato alcun certificato corrispondente cert_id o common_name nella sessione DTLS specificata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

*Vedere le informazioni di *nx_secure_dtls_session_create* per un esempio più completo.

```C

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

        /* Initialize local server identity certificate with key
        and add to server. */
        status = nx_secure_x509_certificate_initialize(&certificate,
                                certificate_der_data,
                                sizeof(certificate_der_data),
                                NX_NULL, 0,
                                certificate_key_der_data,
                                sizeof(certificate_key_der_data),
                                NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

        /* Add local server identity certificate to DTLS server with ID of 1. */
        status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                            &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
        &udp_socket, &server_ip, 4443,
        NX_IP_PERIODIC_RATE);

        /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
        status = nx_secure_dtls_session_local_certificate_remove(&client_dtls_session,
                                                                NX_NULL, 0, 1);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_local_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_receive"></a>nx_secure_dtls_session_receive

Ricevere i dati dell'applicazione tramite una sessione DTLS sicura NetX stabilita

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_session_receive(
                                NX_SECURE_DTLS_SESSION *dtls_session,
                                NX_PACKET **packet_ptr_ptr,
                                UINT wait_option);

```

### <a name="description"></a>Descrizione

Questo servizio restituisce i dati dell'applicazione ricevuti da una sessione DTLS attiva. La sessione DTLS può essere una sessione del server DTLS (gestita da un'istanza del server DTLS) o una sessione client DTLS. Il pacchetto restituito può essere elaborato usando uno dei servizi API NX_PACKET (per altre informazioni, vedere la documentazione di NetX).

### <a name="parameters"></a>Parametri

- **dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.
- **packet_ptr_ptr** Puntatore a un NX_PACKET puntatore per il pacchetto restituito.
- **wait_option** Valore di attesa ThreadX da usare per le operazioni di rete.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ricezione riuscita del pacchetto di dati dell'applicazione.
- **NX_PTR_ERROR** (0x07) Sessione o puntatore a pacchetto non valido.
- **NX_NOT_ENABLED** (0x14) UDP non è abilitato.
- **NX_NOT_BOUND** socket UDP (0x24) non associato alla porta.
- **NX_SECURE_TLS_INVALID_PACKET** (0x104) I dati che non erano un record DTLS valido.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Non è stato possibile eseguire correttamente l'hashing di un record DTLS (errore di crittografia).
- **NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) Errore di controllo della spaziatura interna della crittografia.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Ha generato un avviso dall'host remoto.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0x102) Ha ricevuto un messaggio non riconosciuto.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) È stato recevied un record DTLS con una lunghezza non valida.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) È stato rilevato un ciphersuite sconosciuto (indica un errore di crittografia interno).
- **NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) Ha riappiato un record DTLS con una versione DTLS non corrispondente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_end,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_session_reset"></a>nx_secure_dtls_session_reset

Cancellare i dati in un'istanza di sessione DTLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_dtls_session_reset(NX_SECURE_DTLS_SESSION *dtls_session);
```

### <a name="description"></a>Descrizione

Questo servizio reimposta una sessione DTLS, cancellando tutti i dati crittografici e consentendo di usare nuovamente la struttura per una nuova sessione. I dati persistenti, ad esempio gli archivi certificati, vengono mantenuti in modo che nx_secure_dtls_session_create non sia necessario chiamare ripetutamente.

### <a name="parameters"></a>Parametri

- **dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Reimpostazione della sessione completata.
- **NX_PTR_ERROR** (0x07) Sessione o puntatore al buffer non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_reset(&client_dtls_session);

    /* A new session can now be started using the same structure. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,



    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_-session_send"></a>nx_secure_dtls_ session_send

Inviare dati tramite una sessione DTLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_session_send(NX_SECURE_DTLS_SESSION *session_ptr,
                                          NX_PACKET *packet_ptr,
                                          NXD_ADDRESS *ip_address, UINT port);

```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto di dati tramite una sessione DTLS stabilita a un host DTLS remoto all'indirizzo IP e alla porta specificata. La sessione usata è una sessione client DTLS attiva. Si noti che l'indirizzo IP e la porta vengono forniti a causa della natura senza stato di UDP, ma in genere devono corrispondere all'indirizzo e alla porta usati per avviare la sessione in nx_secure_dtls_session_start.

I dati forniti nel pacchetto, che devono essere allocati usando *nx_secure_dtls_packet_allocate*, vengono crittografati usando le routine e i parametri di crittografia della sessione DTLS e quindi inviati all'host remoto tramite il socket UDP della sessione DTLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione client DTLS attiva.
- **packet_ptr** Puntatore a un'istanza NX_PACKET allocata in precedenza e popolata con i dati dell'applicazione.
- **ip_address** Puntatore a una NXD_ADDRESS contenente l'indirizzo IP dell'host remoto.
- **porta** Porta UDP nell'host remoto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio del pacchetto riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Si è verificato un errore nell'operazione di invio UDP sottostante.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
    /* Error! */
    return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_create

## <a name="nx_secure_dtls_session_trusted_certificate_add"></a>nx_secure_dtls_session_trusted_certificate_add

Aggiungere un certificato CA attendibile a una sessione DTLS sicura NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_session_trusted_certificate_add(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un certificato X.509 CA attendibile o intermedio a un'istanza di sessione DTLS. Un client DTLS richiede almeno un certificato attendibile per convalidare i certificati del server remoto, a meno che non venga usato un meccanismo di autenticazione alternativo, ad esempio chiavi precondi condivise. Un certificato attendibile in genere non dispone di una chiave privata.

Il cert_id è un identificatore numerico diverso da zero per il certificato. In questo modo il certificato può essere facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X.509 presente nell'archivio certificati DTLS. Per altre informazioni sui certificati X.509, vedere il Manuale dell'utente di NetX Secure TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.
- **certificato** Puntatore a una struttura di certificati X.509 inizializzata in precedenza.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato alla sessione DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_INVALID_PARAMETERS** (0x4D) È stato passato un ID certificato 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

*Vedere le informazioni di *nx_secure_dtls_session_create* per un esempio più completo.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                            trusted_cert_der,
                                            trusted_cert_der_len,
                                            NX_NULL, 0, NX_NULL, 0,
                                            NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the trusted store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                      &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);

    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
         &udp_socket, &server_ip, 4443,
         NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_trusted_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_trusted_certificate_remove"></a>nx_secure_dtls_session_trusted_certificate_remove

Rimuovere un certificato ca attendibile da una sessione DTLS sicura netx

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_dtls_session_trusted_certificate_remove(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *common_name,
                            UINT common_name_length, UINT cert_id);

```

### <a name="description"></a>Descrizione

Questo servizio rimuove un certificato CA attendibile da un'istanza di sessione DTLS usando un numero di ID certificato (assegnato quando il certificato è stato aggiunto con nx_secure_dtls_session_trusted_certificate_add) o il campo CommonName X.509.

Se il common_name viene usato per trovare la corrispondenza con il certificato, cert_id parametro deve essere impostato su 0. Se cert_id viene usato , common_name deve essere passato il valore NX_NULL.

Il cert_id è un identificatore numerico diverso da zero per il certificato. In questo modo il certificato può essere facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X.509 presente nell'archivio certificati DTLS. Per altre informazioni sui certificati X.509, vedere il Manuale dell'utente di NetX Secure TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.
- **common_name** Puntatore alla stringa CommonName di cui trovare una corrispondenza.
- **common_name_length** Lunghezza della common_name stringa.
- **cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rimozione del certificato dalla sessione DTLS completata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido passato.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Nessun certificato corrispondente al cert_id o common_name trovato nella sessione DTLS specificata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

*Vedere le informazioni di *nx_secure_dtls_session_create* per un esempio più completo.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL, 0,
                                    NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
    status = nx_secure_dtls_session_trusted_certificate_remove(&client_dtls_session,
                                                                    NX_NULL, 0, 1);
}

```

### <a name="see-also"></a>Vedere anche

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_trusted_certificate_add,
- nx_secure_x509_certificate_initialize
