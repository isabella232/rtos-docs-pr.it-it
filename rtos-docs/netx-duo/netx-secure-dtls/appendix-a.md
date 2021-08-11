---
title: Appendice A - Azure RTOS restituiti/codici di errore di NetX Secure DTLS
description: Elenca i possibili codici di errore che possono essere restituiti dai Azure RTOS NetX Secure DTLS.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: reference
ms.service: rtos
ms.openlocfilehash: f4994a5014d3691b4a78f225fb68b475bf5a8cdab630162a94130f321be09da5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782439"
---
# <a name="appendix-a-azure-rtos-netx-secure-dtls-returnerror-codes"></a>Appendice A: Azure RTOS restituiti/codici di errore di NetX Secure DTLS

## <a name="netx-secure-tlsdtls-return-codes"></a>Codici restituiti netx secure TLS/DTLS

La tabella 1 seguente elenca i possibili codici di errore che possono essere restituiti dai Azure RTOS NetX Secure DTLS. Si noti che i servizi possono anche restituire codici di errore UDP o IP: i valori TLS iniziano alle 0x101 e i valori TCP/IP/UDP sono inferiori 0x100. I valori restituiti X.509 iniziano 0x181. Fare riferimento alla documentazione di NetX TCP/IP/UDP per informazioni sui valori restituiti IP e UDP e vedere di seguito per i valori X.509.

| **Nome errore**                                        | **Valore** | **Descrizione**                                                                                                                                               |
| ----------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_TLS_SUCCESS                              | 0x00      | Funzione restituita correttamente. (uguale a NX_SUCCESS).                                                                                                        |
| NX_SECURE_TLS_SESSION_UNINITIALIZED               | 0x101     | Ciclo principale TLS chiamato con socket non inizializzato.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE          | 0x102     | Il livello di record TLS ha ricevuto un tipo di messaggio non riconosciuto.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                       | 0x103     | Errore interno: stato non riconosciuto.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                      | 0x104     | Errore interno: il pacchetto ricevuto non contiene dati TLS.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                 | 0x105     | Il ciphersuite scelto non è supportato: errore interno per il server, per il client significa che l'host remoto ha inviato un errore di crittografia (errore o attacco).            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                  | 0x106     | Quando si esegue una crittografia o una decrittografia, la crittografia scelta è disabilitata o non disponibile.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                   | 0x107     | Si è verificato un errore durante l'elaborazione dei messaggi durante l'handshake.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE           | 0x108     | Un record in ingresso aveva un MAC che non corrisponde a quello generato.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                    | 0x109     | L'invio TCP in uscita di un record non è riuscito per qualche motivo.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH           | 0x10A     | Una lunghezza di un messaggio in arrivo non è corretta (in genere una lunghezza diversa da uno nell'intestazione, come nei messaggi di certificato)                               |
| NX_SECURE_TLS_BAD_CIPHERSPEC                      | 0x10B     | Un messaggio ChangeCipherSpec in ingresso non è corretto.                                                                                                           |
| NX_SECURE_TLS_INVALID_SERVER_CERT                | 0x10C     | Un certificato del server in ingresso non è stato analizzato correttamente.                                                                                                       |
| NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER          | 0x10D     | Un certificato fornito da un server ha specificato un'operazione di chiave pubblica che non è possibile supportare.                                                                        |
| NX_SECURE_TLS_NO_SUPPORTED_CIPHERS               | 0x10E     | Ricevuto clientHello senza ciphersuit supportati.                                                                                                        |
| NX_SECURE_TLS_UNKNOWN_TLS_VERSION                | 0x10F     | Un record in ingresso ha una versione di TLS non riconosciuta.                                                                                                   |
| NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION            | 0x110     | Un record in ingresso ha una versione di TLS valida, ma non è supportata.                                                                                     |
| NX_SECURE_TLS_ALLOCATE_PACKET_FAILED             | 0x111     | Un'allocazione di pacchetti interna per un messaggio TLS non è riuscita.                                                                                                       |
| NX_SECURE_TLS_INVALID_CERTIFICATE                 | 0x112     | Un certificato X509 non è stato analizzato correttamente.                                                                                                                  |
| NX_SECURE_TLS_NO_CLOSE_RESPONSE                  | 0x113     | Durante la chiusura di una sessione TLS, non ha ricevuto closeNotify dall'host remoto.                                                                               |
| NX_SECURE_TLS_ALERT_RECEIVED                      | 0x114     | L'host remoto ha inviato un avviso che indica un errore e chiude la connessione.                                                                                |
| NX_SECURE_TLS_FINISHED_HASH_FAILURE              | 0x115     | L'hash del messaggio di fine ricevuto non corrisponde all'hash generato locale: danneggiamento dell'handshake.                                                              |
| NX_SECURE_TLS_UNKNOWN_CERT_SIG_ALGORITHM        | 0x116     | Un certificato durante la verifica aveva un algoritmo di firma non supportato.                                                                                     |
| NX_SECURE_TLS_CERTIFICATE_SIG_CHECK_FAILED      | 0x117     | Un controllo di verifica della firma del certificato non è riuscito. I dati del certificato non corrispondono alla firma.                                                                 |
| NX_SECURE_TLS_BAD_COMPRESSION_METHOD             | 0x118     | Ricevuto un messaggio Hello con un metodo di compressione non supportato.                                                                                              |
| NX_SECURE_TLS_CERTIFICATE_NOT_FOUND              | 0x119     | In un'operazione su un elenco di certificati non è stato trovato alcun certificato corrispondente.                                                                                     |
| NX_SECURE_TLS_INVALID_SELF_SIGNED_CERT          | 0x11A     | L'host remoto ha inviato un certificato autofirmato NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES non è definito.                                              |
| NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND      | 0x11B     | È stato ricevuto un certificato remoto con un'autorità emittente non presente nell'archivio attendibile locale.                                                                              |
| NX_SECURE_TLS_OUT_OF_ORDER_MESSAGE              | 0x11C     | Un messaggio DTLS è stato ricevuto nell'ordine errato. Un datagramma eliminato è probabilmente il responsabile.                                                                    |
| NX_SECURE_TLS_INVALID_REMOTE_HOST                | 0x11D     | È stato ricevuto un pacchetto da un host remoto non riconosciuto.                                                                                            |
| NX_SECURE_TLS_INVALID_EPOCH                       | 0x11E     | Un messaggio DTLS è stato ricevuto e corrisponde a una sessione DTLS, ma ha un periodo errato e deve essere ignorato.                                                   |
| NX_SECURE_TLS_REPEAT_MESSAGE_RECEIVED            | 0x11F     | È stato ricevuto un messaggio DTLS con un numero di sequenza già visto. Ignorarlo.                                                                           |
| NX_SECURE_TLS_NEED_DTLS_SESSION                  | 0x120     | È stata usata una sessione TLS in un'API DTLS non inizializzata per DTLS.                                                                                       |
| NX_SECURE_TLS_NEED_TLS_SESSION                   | 0x121     | È stata usata una sessione TLS in un'API TLS inizializzata per DTLS e non per TLS.                                                                                |
| NX_SECURE_TLS_SEND_ADDRESS_MISMATCH              | 0x122     | Il chiamante ha tentato di inviare dati tramite una sessione DTLS con un indirizzo IP o una porta che non corrisponde alla sessione.                                                  |
| NX_SECURE_TLS_NO_FREE_DTLS_SESSIONS             | 0x123     | Una nuova connessione ha tentato di ottenere una sessione DTLS dalla cache, ma non è disponibile.                                                                        |
| NX_SECURE_DTLS_SESSION_NOT_FOUND                 | 0x124     | Il chiamante ha cercato una sessione DTLS, ma l'indirizzo IP e la porta non corrispondono ad alcuna voce nella cache.                                             |
| NX_SECURE_TLS_NO_MORE_PSK_SPACE                 | 0x125     | Il chiamante ha tentato di aggiungere una chiave PSK a una sessione TLS, ma non c'era più spazio nella sessione specificata.                                                          |
| NX_SECURE_TLS_NO_MATCHING_PSK                    | 0x126     | Un host remoto ha fornito un hint di identità PSK che non corrisponde ad alcun nell'archivio locale.                                                                         |
| NX_SECURE_TLS_CLOSE_NOTIFY_RECEIVED              | 0x127     | Una sessione TLS ha ricevuto un avviso CloseNotify dall'host remoto che indica che la sessione è stata completata.                                                           |
| NX_SECURE_TLS_NO_AVAILABLE_SESSIONS              | 0x128     | Non sono disponibili sessioni TLS in un oggetto TLS per gestire una connessione.                                                                                         |
| NX_SECURE_TLS_NO_CERT_SPACE_ALLOCATED           | 0x129     | Non è stato allocato alcuno spazio per i certificati remoti in ingresso.                                                                                          |
| NX_SECURE_TLS_PADDING_CHECK_FAILED               | 0x12A     | Il riempimento della crittografia in un messaggio in arrivo non è corretto.                                                                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_TYPE        | 0x12B     | Durante l'elaborazione di certificateVerifyRequest, il server remoto non ha fornito alcun tipo di certificato supportato.                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_ALG         | 0x12C     | Durante l'elaborazione di certificateVerifyRequest, il server remoto non ha fornito alcun algoritmo di firma supportato.                                                 |
| NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE            | 0x12D     | Spazio buffer del certificato insufficiente allocato per un certificato.                                                                                              |
| NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED           | 0x12E     | La versione del protocollo in un record TLS in ingresso non corrisponde alla versione della sessione stabilita.                                                          |
| NX_SECURE_TLS_NO_RENEGOTIATION_ERROR             | 0x12F     | È stato ricevuto un messaggio HelloRequest, ma non è in corso una nuova negoziazione.                                                                                           |
| NX_SECURE_TLS_UNSUPPORTED_FEATURE                 | 0x130     | È stata rilevata una funzionalità disabilitata durante una sessione TLS o un handshake.                                                                                |
| NX_SECURE_TLS_CERTIFICATE_VERIFY_FAILURE         | 0x131     | Un messaggio CertificateVerify da un client remoto non è riuscito a verificare il certificato client.                                                                     |
| NX_SECURE_TLS_EMPTY_REMOTE_CERTIFICATE_RECEIVED | 0x132     | L'host remoto ha inviato un messaggio di certificato vuoto.                                                                                                            |
| NX_SECURE_TLS_RENEGOTIATION_EXTENSION_ERROR      | 0x133     | Si è verificato un errore durante l'elaborazione o l'invio di un'estensione Indicazione di rinerezione sicura.                                                                     |
| NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE     | 0x134     | È stato effettuato un tentativo di rinegoziazione della sessione con una sessione TLS non attiva.                                                                                |
| NX_SECURE_TLS_PACKET_BUFFER_TOO_SMALL           | 0x135     | TLS ha ricevuto un record troppo grande per il buffer di pacchetti assegnato. Impossibile elaborare il record.                                                   |
| NX_SECURE_TLS_EXTENSION_NOT_FOUND                | 0x136     | Un'estensione specificata non è stata ricevuta dall'host remoto durante l'handshake TLS.                                                                         |
| NX_SECURE_TLS_SNI_EXTENSION_INVALID              | 0x137     | TLS ha ricevuto un'estensione Indicazione nome server non valida.                                                                                                     |
| NX_SECURE_TLS_CERT_ID_INVALID                    | 0x138     | L'applicazione ha tentato di aggiungere un certificato del server con un valore di ID certificato non valido (probabilmente 0).                                                                |
| NX_SECURE_TLS_CERT_ID_DUPLICATE                  | 0x139     | L'applicazione ha tentato di aggiungere un certificato server con un ID certificato già presente nell'archivio locale.                                                       |
| NX_SECURE_TLS_RENEGOTIATION_FAILURE               | 0x13A     | L'host remoto non ha fornito l'estensione secure renegotiation indication o lo pseudo-ciphersuite SCSV, quindi non è possibile eseguire una rinegoziazione sicura.     |
| NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE             | 0x13B     | Nel tentativo di eseguire un'operazione di crittografia, una delle voci nella tabella ciphersuite (o uno dei relativi puntatori a funzione) è stata impostata in modo non corretto su NULL. |

**Tabella 1: Codici restituiti di errore di NetX Secure TLS**

## <a name="netx-secure-x509-return-codes"></a>Codici restituiti netx secure X.509

La tabella 2 seguente elenca i possibili codici di errore che possono essere restituiti dai servizi NetX Secure X.509. Si noti che i servizi possono restituire anche altri codici di errore. I valori restituiti X.509 iniziano 0x181, i valori TLS iniziano 0x101 e i valori TCP/IP sono inferiori 0x100. Per informazioni sui valori restituiti TCP/IP e superiori per i valori restituiti TLS, vedere la documentazione di NetX TCP/IP.

| **Nome errore**                                   | **Valore** | **Descrizione**                                                                                                        |
| ------------------------------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_SUCCESS                        | 0x00      | Stato restituito riuscito. (Uguale a NX_SUCCESS)                                                                        |
| NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED    | 0x181     | È stato rilevato un tag ASN.1 multi-byte, attualmente non supportato.                                                       |
| NX_SECURE_X509_ASN1_LENGTH_TOO_LONG        | 0x182     | Rilevato un valore di lunghezza più lungo di quello che è possibile gestire.                                                                  |
| NX_SECURE_X509_FOUND_NON_ZERO_PADDING      | 0x183     | Previsto un valore di spaziatura interna pari a 0: ha ottenuto un valore diverso.                                                               |
| NX_SECURE_X509_MISSING_PUBLIC_KEY           | 0x184     | X509 prevedeva una chiave pubblica ma non ne trovava una.                                                                        |
| NX_SECURE_X509_INVALID_PUBLIC_KEY           | 0x185     | È stata trovata una chiave pubblica, ma non è valida o ha un formato non corretto.                                                      |
| NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE | 0x186     | Il blocco ASN.1 di primo livello non è una sequenza: certificato X509 non valido.                                                |
| NX_SECURE_X509_MISSING_SIGNATURE_ALGORITHM  | 0x187     | L'identificatore dell'algoritmo di firma previsto non è stato trovato.                                                           |
| NX_SECURE_X509_INVALID_CERTIFICATE_DATA     | 0x188     | Il formato dei dati dell'identità del certificato non è valido.                                                                     |
| NX_SECURE_X509_UNEXPECTED_ASN1_TAG          | 0x189     | Era previsto un tag ASN.1 specifico per il formato X509, ma è stato ottenuto un altro elemento.                                      |
| NX_SECURE_PKCS1_INVALID_PRIVATE_KEY         | 0x18A     | È stato passato un file di chiave privata PKCS#1, ma la formattazione non è corretta.                                            |
| NX_SECURE_X509_CHAIN_TOO_SHORT              | 0x18B     | Una catena di certificati X509 era troppo breve per contenere l'intera catena durante la creazione della catena.                                |
| NX_SECURE_X509_CHAIN_VERIFY_FAILURE         | 0x18C     | Non è stato possibile verificare una catena di certificati X509 (errore catch-all).                                                 |
| NX_SECURE_X509_PKCS7_PARSING_FAILED         | 0x18D     | L'analisi di una firma con codifica PKCS #7 X.509 non è riuscita.                                                                     |
| NX_SECURE_X509_CERTIFICATE_NOT_FOUND        | 0x18E     | Durante la ricerca di un certificato non è stata trovata alcuna voce corrispondente.                                                              |
| NX_SECURE_X509_INVALID_VERSION               | 0x18F     | Un certificato include un campo non compatibile con la versione specificata.                                           |
| NX_SECURE_X509_INVALID_TAG_CLASS            | 0x190     | Un certificato include un tag ASN.1 con un valore di classe tag non valido.                                                   |
| NX_SECURE_X509_INVALID_EXTENSIONS            | 0x191     | Un certificato includeva un TLV di estensioni, ma che non contiene una sequenza.                                          |
| NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE   | 0x192     | Un certificato includeva una sequenza di estensione non valida X.509.                                                   |
| NX_SECURE_X509_CERTIFICATE_EXPIRED           | 0x193     | Un certificato ha un campo "non dopo" inferiore all'ora corrente.                                             |
| NX_SECURE_X509_CERTIFICATE_NOT_YET_VALID   | 0x194     | Un certificato ha un campo "non prima" maggiore dell'ora corrente.                                         |
| NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH     | 0x195     | Un nome comune del certificato o il nome alternativo del soggetto non corrisponde a un TLD DNS specificato.                                           |
| NX_SECURE_X509_INVALID_DATE_FORMAT          | 0x196     | Un certificato conteneva un campo data che non è in un formato ricognito.                                               |
| NX_SECURE_X509_CRL_ISSUER_MISMATCH          | 0x197     | Un CRL e un certificato forniti non sono stati rilasciati dalla stessa autorità di certificazione.                                      |
| NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED  | 0x198     | Un controllo della firma CRL non è riuscito rispetto all'autorità emittente.                                                                       |
| NX_SECURE_X509_CRL_CERTIFICATE_REVOKED      | 0x199     | È stato trovato un certificato in un CRL valido e pertanto è stato revocato.                                                 |
| NX_SECURE_X509_WRONG_SIGNATURE_METHOD       | 0x19A     | Durante il tentativo di convalidare una firma, il metodo di firma non corrisponde al metodo previsto.                          |
| NX_SECURE_X509_EXTENSION_NOT_FOUND          | 0x19B     | Durante la ricerca di un'estensione non è stata trovata alcuna estensione con un ID corrispondente.                                                |
| NX_SECURE_X509_ALT_NAME_NOT_FOUND          | 0x19C     | È stato cercato un nome in un'estensione subjectAltName ma non è stato trovato.                                               |
| NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE    | 0x19D     | Tipo di chiave privata specificato sconosciuto o non valido.                                                                         |
| NX_SECURE_X509_NAME_STRING_TOO_LONG        | 0x19E     | Passata una stringa di nome troppo lunga per un buffer interno (nome DNS e così via).                                        |
| NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND    | 0x19F     | Durante la ricerca di un'estensione Utilizzo chiavi esteso, l'OID di utilizzo della chiave specificato non è stato trovato.                               |
| NX_SECURE_X509_KEY_USAGE_ERROR              | 0x1A0     | Deve essere restituito dal callback dell'applicazione se si verifica un errore nell'utilizzo della chiave durante un controllo di verifica del certificato. |

**Tabella 2 - Codici restituiti di errore X.509 di NetX Secure**
