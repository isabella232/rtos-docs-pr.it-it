---
title: Appendice A-codici di errore e restituzione di DTLS di Azure RTO NetX sicuri
description: Elenca i possibili codici di errore che possono essere restituiti da Azure RTO NetX Secure DTLS Services.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: reference
ms.service: rtos
ms.openlocfilehash: f14f27167a95a1b9d3ebbdf0d903be7b043ccb28
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821602"
---
# <a name="appendix-a-azure-rtos-netx-secure-dtls-returnerror-codes"></a>Appendice A: codici di errore di restituzione/errore di DTLS di Azure RTO NetX

## <a name="netx-secure-tlsdtls-return-codes"></a>Codici restituiti NetX Secure TLS/DTLS

La tabella 1 seguente elenca i possibili codici di errore che possono essere restituiti da Azure RTO NetX Secure DTLS Services. Si noti che i servizi possono restituire anche codici di errore UDP o IP: i valori TLS iniziano con 0x101 e i valori TCP/IP/UDP sono inferiori a 0x100. I valori restituiti X. 509 iniziano da 0x181. Per informazioni sui valori restituiti IP e UDP e per i valori X. 509, vedere la documentazione di NetX TCP/IP/UDP.

| **Nome errore**                                        | **Valore** | **Descrizione**                                                                                                                                               |
| ----------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_TLS_SUCCESS                              | 0x00      | Funzione restituita correttamente. (Uguale a NX_SUCCESS).                                                                                                        |
| NX_SECURE_TLS_SESSION_UNINITIALIZED               | 0x101     | Il ciclo principale TLS è stato chiamato con socket non inizializzato.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE          | 0x102     | Il livello di record TLS ha ricevuto un tipo di messaggio non riconosciuto.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                       | 0x103     | Errore interno: stato non riconosciuto.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                      | 0x104     | Errore interno: il pacchetto ricevuto non contiene dati TLS.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                 | 0x105     | Il ciphersuite scelto non è supportato-errore interno per il server. per il client significa che l'host remoto ha inviato un ciphersuite errato (errore o attacco).            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                  | 0x106     | Per la crittografia o la decrittografia, la crittografia scelta è disabilitata o non disponibile.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                   | 0x107     | Un elemento nell'elaborazione del messaggio durante l'handshake non è riuscito.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE           | 0x108     | Un record in ingresso ha un MAC che non corrisponde a quello generato.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                    | 0x109     | L'invio TCP in uscita di un record non è riuscito per qualche motivo.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH           | 0x10A     | Un messaggio in arrivo ha una lunghezza errata (in genere una lunghezza diversa da una nell'intestazione, come nei messaggi del certificato)                               |
| NX_SECURE_TLS_BAD_CIPHERSPEC                      | 0x10B     | Un messaggio ChangeCipherSpec in ingresso non è corretto.                                                                                                           |
| NX_SECURE_TLS_INVALID_SERVER_CERT                | 0x10C     | Un certificato server in ingresso non è stato analizzato correttamente.                                                                                                       |
| NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER          | 0x10D     | Un certificato fornito da un server specifica un'operazione a chiave pubblica che non è supportata.                                                                        |
| NX_SECURE_TLS_NO_SUPPORTED_CIPHERS               | 0x10E     | È stato ricevuto un ClientHello senza ciphersuites supportato.                                                                                                        |
| NX_SECURE_TLS_UNKNOWN_TLS_VERSION                | 0x10F     | Un record in ingresso ha una versione TLS non riconosciuta.                                                                                                   |
| NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION            | 0x110     | Un record in ingresso ha una versione di TLS valida, ma non è supportata.                                                                                     |
| NX_SECURE_TLS_ALLOCATE_PACKET_FAILED             | 0x111     | Un'allocazione di pacchetti interna per un messaggio TLS non è riuscita.                                                                                                       |
| NX_SECURE_TLS_INVALID_CERTIFICATE                 | 0x112     | Un certificato X509 non è stato analizzato correttamente.                                                                                                                  |
| NX_SECURE_TLS_NO_CLOSE_RESPONSE                  | 0x113     | Durante la chiusura di una sessione TLS, non ha ricevuto un CloseNotify dall'host remoto.                                                                               |
| NX_SECURE_TLS_ALERT_RECEIVED                      | 0x114     | L'host remoto ha inviato un avviso, che indica un errore e chiude la connessione.                                                                                |
| NX_SECURE_TLS_FINISHED_HASH_FAILURE              | 0x115     | L'hash del messaggio finale ricevuto non corrisponde al danneggiamento dell'handshake hash generato localmente.                                                              |
| NX_SECURE_TLS_UNKNOWN_CERT_SIG_ALGORITHM        | 0x116     | Un certificato durante la verifica ha un algoritmo di firma non supportato.                                                                                     |
| NX_SECURE_TLS_CERTIFICATE_SIG_CHECK_FAILED      | 0x117     | Verifica della verifica della firma del certificato non riuscita. i dati del certificato non corrispondono alla firma.                                                                 |
| NX_SECURE_TLS_BAD_COMPRESSION_METHOD             | 0x118     | Ricevuto un messaggio Hello con un metodo di compressione non supportato.                                                                                              |
| NX_SECURE_TLS_CERTIFICATE_NOT_FOUND              | 0x119     | In un'operazione in un elenco di certificati non è stato trovato alcun certificato corrispondente.                                                                                     |
| NX_SECURE_TLS_INVALID_SELF_SIGNED_CERT          | 0x11A     | L'host remoto ha inviato un certificato autofirmato e NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES non è definito.                                              |
| NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND      | 0x11B     | Un certificato remoto è stato ricevuto con un'autorità emittente non presente nell'archivio attendibile locale.                                                                              |
| NX_SECURE_TLS_OUT_OF_ORDER_MESSAGE              | 0x11C     | Un messaggio DTLS è stato ricevuto nell'ordine errato. un datagramma eliminato è probabilmente il colpevole.                                                                    |
| NX_SECURE_TLS_INVALID_REMOTE_HOST                | 0x11D     | Un pacchetto è stato ricevuto da un host remoto che non è stato riconosciuto.                                                                                            |
| NX_SECURE_TLS_INVALID_EPOCH                       | 0x11E     | Un messaggio DTLS è stato ricevuto e corrisponde a una sessione DTLS ma ha avuto un periodo errato e deve essere ignorato.                                                   |
| NX_SECURE_TLS_REPEAT_MESSAGE_RECEIVED            | 0x11F     | È stato ricevuto un messaggio DTLS con un numero di sequenza già visualizzato. ignorarlo.                                                                           |
| NX_SECURE_TLS_NEED_DTLS_SESSION                  | 0x120     | Una sessione TLS è stata usata in un'API DTLS che non è stata inizializzata per DTLS.                                                                                       |
| NX_SECURE_TLS_NEED_TLS_SESSION                   | 0x121     | Una sessione TLS è stata usata in un'API TLS inizializzata per DTLS e non TLS.                                                                                |
| NX_SECURE_TLS_SEND_ADDRESS_MISMATCH              | 0x122     | Il chiamante ha tentato di inviare i dati su una sessione DTLS con un indirizzo IP o una porta che non corrisponde alla sessione.                                                  |
| NX_SECURE_TLS_NO_FREE_DTLS_SESSIONS             | 0x123     | Una nuova connessione ha tentato di ottenere una sessione DTLS dalla cache, ma non ne erano disponibili.                                                                        |
| NX_SECURE_DTLS_SESSION_NOT_FOUND                 | 0x124     | Il chiamante ha cercato una sessione DTLS, ma l'indirizzo IP e la porta specificati non corrispondono ad alcuna voce nella cache.                                             |
| NX_SECURE_TLS_NO_MORE_PSK_SPACE                 | 0x125     | Il chiamante ha tentato di aggiungere una PSK a una sessione TLS, ma non c'era più spazio nella sessione specificata.                                                          |
| NX_SECURE_TLS_NO_MATCHING_PSK                    | 0x126     | Un host remoto ha fornito un hint di identità PSK che non corrisponde a nessuno nell'archivio locale.                                                                         |
| NX_SECURE_TLS_CLOSE_NOTIFY_RECEIVED              | 0x127     | Una sessione TLS ha ricevuto un avviso CloseNotify dall'host remoto che indica che la sessione è stata completata.                                                           |
| NX_SECURE_TLS_NO_AVAILABLE_SESSIONS              | 0x128     | Non sono disponibili sessioni TLS in un oggetto TLS per gestire una connessione.                                                                                         |
| NX_SECURE_TLS_NO_CERT_SPACE_ALLOCATED           | 0x129     | Non è stato allocato alcuno spazio di certificati per i certificati remoti in ingresso.                                                                                          |
| NX_SECURE_TLS_PADDING_CHECK_FAILED               | 0x12A     | La spaziatura interna della crittografia in un messaggio in arrivo non è corretta.                                                                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_TYPE        | 0x12B     | Durante l'elaborazione di un CertificateVerifyRequest, non è stato fornito alcun tipo di certificato supportato dal server remoto.                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_ALG         | 0x12C     | Durante l'elaborazione di un CertificateVerifyRequest, nessun algoritmo di firma supportato è stato fornito dal server remoto.                                                 |
| NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE            | 0x12D     | Spazio del buffer del certificato non sufficiente allocato per un certificato.                                                                                              |
| NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED           | 0x12E     | La versione del protocollo in un record TLS in ingresso non corrisponde alla versione della sessione stabilita.                                                          |
| NX_SECURE_TLS_NO_RENEGOTIATION_ERROR             | 0x12F     | È stato ricevuto un messaggio HelloRequest, ma non si tratta di un nuovo negoziato.                                                                                           |
| NX_SECURE_TLS_UNSUPPORTED_FEATURE                 | 0x130     | È stata rilevata una funzionalità disabilitata durante un handshake o una sessione TLS.                                                                                |
| NX_SECURE_TLS_CERTIFICATE_VERIFY_FAILURE         | 0x131     | Un messaggio CertificateVerify da un client remoto non è riuscito a verificare il certificato client.                                                                     |
| NX_SECURE_TLS_EMPTY_REMOTE_CERTIFICATE_RECEIVED | 0x132     | L'host remoto ha inviato un messaggio di certificato vuoto.                                                                                                            |
| NX_SECURE_TLS_RENEGOTIATION_EXTENSION_ERROR      | 0x133     | Si è verificato un errore durante l'elaborazione di un oggetto o l'invio di un'estensione di indicazione Renegotation sicura.                                                                     |
| NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE     | 0x134     | È stata tentata una rinegoziazione della sessione con una sessione TLS non attiva.                                                                                |
| NX_SECURE_TLS_PACKET_BUFFER_TOO_SMALL           | 0x135     | TLS ha ricevuto un record troppo grande per il buffer di pacchetti assegnato. Non è stato possibile elaborare il record.                                                   |
| NX_SECURE_TLS_EXTENSION_NOT_FOUND                | 0x136     | Un'estensione specificata non è stata ricevuta dall'host remoto durante l'handshake TLS.                                                                         |
| NX_SECURE_TLS_SNI_EXTENSION_INVALID              | 0x137     | TLS ha ricevuto un'estensione di Indicazione nome server non valida.                                                                                                     |
| NX_SECURE_TLS_CERT_ID_INVALID                    | 0x138     | L'applicazione ha tentato di aggiungere un certificato del server con un valore ID certificato non valido (probabilmente 0).                                                                |
| NX_SECURE_TLS_CERT_ID_DUPLICATE                  | 0x139     | L'applicazione ha tentato di aggiungere un certificato del server con un ID certificato già presente nell'archivio locale.                                                       |
| NX_SECURE_TLS_RENEGOTIATION_FAILURE               | 0x13A     | L'host remoto non ha fornito l'estensione per l'indicazione di rinegoziazione sicura o lo pseudo-ciphersuite SCSV, quindi non è possibile eseguire la rinegoziazione sicura.     |
| NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE             | 0x13B     | Nel tentativo di eseguire un'operazione di crittografia, una delle voci della tabella ciphersuite (o uno dei relativi puntatori a funzione) è stata impostata in modo errato su NULL. |

**Tabella 1 – codici di errore TLS NetX sicuri**

## <a name="netx-secure-x509-return-codes"></a>Codici restituiti X. 509 NetX Secure

La tabella 2 seguente elenca i possibili codici di errore che possono essere restituiti da NetX Secure X. 509 Services. Si noti che i servizi possono restituire anche altri codici di errore. I valori restituiti X. 509 iniziano da 0x181, i valori TLS iniziano da 0x101 e i valori TCP/IP sono sotto 0x100. Per informazioni sui valori restituiti TCP/IP e versioni successive per i valori restituiti TLS, vedere la documentazione di NetX TCP/IP.

| **Nome errore**                                   | **Valore** | **Descrizione**                                                                                                        |
| ------------------------------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_SUCCESS                        | 0x00      | Stato restituito correttamente. (Uguale a NX_SUCCESS)                                                                        |
| NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED    | 0x181     | È stato rilevato un tag ASN. 1 a più byte, attualmente non supportato.                                                       |
| NX_SECURE_X509_ASN1_LENGTH_TOO_LONG        | 0x182     | È stato rilevato un valore di lunghezza superiore a quello che è possibile gestire.                                                                  |
| NX_SECURE_X509_FOUND_NON_ZERO_PADDING      | 0x183     | Previsto un valore di riempimento pari a 0-ha un valore diverso.                                                               |
| NX_SECURE_X509_MISSING_PUBLIC_KEY           | 0x184     | X509 prevede una chiave pubblica ma non ne è stata trovata una.                                                                        |
| NX_SECURE_X509_INVALID_PUBLIC_KEY           | 0x185     | È stata trovata una chiave pubblica, ma il formato non è valido o non è corretto.                                                      |
| NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE | 0x186     | Il blocco ASN. 1 di primo livello non è un certificato X509 non valido per la sequenza.                                                |
| NX_SECURE_X509_MISSING_SIGNATURE_ALGORITHM  | 0x187     | È previsto un identificatore di algoritmo di firma non trovato.                                                           |
| NX_SECURE_X509_INVALID_CERTIFICATE_DATA     | 0x188     | Il formato dei dati di identità del certificato non è valido.                                                                     |
| NX_SECURE_X509_UNEXPECTED_ASN1_TAG          | 0x189     | Era previsto un tag ASN. 1 specifico per il formato X509, ma è stato ottenuto un altro elemento.                                      |
| NX_SECURE_PKCS1_INVALID_PRIVATE_KEY         | 0x18A     | Un file di chiave privata PKCS # 1 è stato passato, ma la formattazione non era corretta.                                            |
| NX_SECURE_X509_CHAIN_TOO_SHORT              | 0x18B     | Una catena di certificati X509 è troppo corta per mantenere l'intera catena durante la creazione della catena.                                |
| NX_SECURE_X509_CHAIN_VERIFY_FAILURE         | 0x18C     | Non è stato possibile verificare una catena di certificati X509 (errore catch-all).                                                 |
| NX_SECURE_X509_PKCS7_PARSING_FAILED         | 0x18D     | L'analisi di una firma con codifica PKCS # 7 di X. 509 non è riuscita.                                                                     |
| NX_SECURE_X509_CERTIFICATE_NOT_FOUND        | 0x18E     | Nella ricerca di un certificato non è stata trovata alcuna voce corrispondente.                                                              |
| NX_SECURE_X509_INVALID_VERSION               | 0x18F     | Un certificato include un campo che non è compatibile con la versione specificata.                                           |
| NX_SECURE_X509_INVALID_TAG_CLASS            | 0x190     | Un certificato include un tag ASN. 1 con un valore di classe di tag non valido.                                                   |
| NX_SECURE_X509_INVALID_EXTENSIONS            | 0x191     | Un certificato includeva un TLV di estensioni ma non conteneva una sequenza.                                          |
| NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE   | 0x192     | Un certificato include una sequenza di estensioni non valida X. 509.                                                   |
| NX_SECURE_X509_CERTIFICATE_EXPIRED           | 0x193     | Un certificato aveva un campo "non dopo" che era minore dell'ora corrente.                                             |
| NX_SECURE_X509_CERTIFICATE_NOT_YET_VALID   | 0x194     | Un certificato aveva un campo "not before" che era maggiore dell'ora corrente.                                         |
| NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH     | 0x195     | Un nome comune del certificato o un nome alternativo del soggetto non corrisponde a un TLD DNS specificato.                                           |
| NX_SECURE_X509_INVALID_DATE_FORMAT          | 0x196     | Un certificato contiene un campo relativo alla data che non è in un formato recognixed.                                               |
| NX_SECURE_X509_CRL_ISSUER_MISMATCH          | 0x197     | Un CRL e un certificato specificati non sono stati rilasciati dalla stessa autorità di certificazione.                                      |
| NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED  | 0x198     | Verifica della firma CRL non riuscita rispetto all'emittente.                                                                       |
| NX_SECURE_X509_CRL_CERTIFICATE_REVOKED      | 0x199     | Un certificato è stato trovato in un elenco CRL valido e pertanto è stato revocato.                                                 |
| NX_SECURE_X509_WRONG_SIGNATURE_METHOD       | 0x19A     | Nel tentativo di convalidare una firma il metodo di firma non corrisponde al metodo previsto.                          |
| NX_SECURE_X509_EXTENSION_NOT_FOUND          | 0x19B     | Per la ricerca di un'estensione non è stata trovata alcuna estensione con un ID corrispondente.                                                |
| NX_SECURE_X509_ALT_NAME_NOT_FOUND          | 0x19C     | È stato cercato un nome in un'estensione subjectAltName ma non è stato trovato.                                               |
| NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE    | 0x19D     | Il tipo di chiave privata specificato è sconosciuto o non valido.                                                                         |
| NX_SECURE_X509_NAME_STRING_TOO_LONG        | 0x19E     | È stata passata una stringa del nome troppo lungo per un buffer interno (nome DNS e così via).                                        |
| NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND    | 0x19F     | Durante la ricerca di un'estensione per l'utilizzo della chiave estesa non è stato trovato l'OID di utilizzo della chiave specificato.                               |
| NX_SECURE_X509_KEY_USAGE_ERROR              | 0x1A0     | Per essere restituito dal callback dell'applicazione se si verifica un errore durante l'utilizzo della chiave durante un controllo di verifica del certificato. |

**Tabella 2: codici restituiti degli errori X. 509 NetX**
