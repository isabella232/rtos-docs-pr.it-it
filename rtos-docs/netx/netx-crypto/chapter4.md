---
title: Capitolo 4 - Descrizione Azure RTOS'API Di crittografia NetX
description: Azure RTOS descrizione dell'API Di crittografia NetX
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5bd4cdae28a293ec9ef259bbd29fdb8f8d6dc43f964cbc184290b82ee8f590a3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788801"
---
# <a name="chapter-4---azure-rtos-netx-crypto-api-description"></a>Capitolo 4 - Descrizione Azure RTOS'API Di crittografia NetX

## <a name="nx_crypto_initialize"></a>nx_crypto_initialize

Inizializza la libreria sicura NetX

### <a name="prototype"></a>Prototipo

```c
UINT nx_crypto_initialize(VOID);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il modulo Azure RTOS libreria Crypto NetX. Prima di usare una qualsiasi delle altre funzioni di crittografia, l'applicazione deve chiamare questa funzione per eseguire l'inizializzazione e convalidare l'integrità della libreria. Se non si chiama questa funzione prima di usare altri servizi Di crittografia NetX, verranno restituiti errori.

### <a name="parameters"></a>Parametri

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzata correttamente la libreria di crittografia NetX. Le funzioni della libreria sono ora pronte e possono essere usate.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia non viene inizializzata o non supera il controllo di integrità. L'applicazione non può usare questa libreria.

### <a name="example"></a>Esempio

TODO

## <a name="nx_crypto_module_state_get"></a>nx_crypto_module_state_get

Recuperare lo stato corrente del modulo abilitato per FIPS

### <a name="prototype"></a>Prototipo

```c
UINT nx_crypto_module_state_get(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio è disponibile solo nella libreria di compilazione FIPS. Restituisce lo stato dello stato corrente della libreria Crypto NetX.

### <a name="parameters"></a>Parametri

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **Flag di stato:**
  - NX_CRYPTO_LIBRARY_STATE_UNINITIALIZED 0x00000001
  - NX_CRYPTO_LIBRARY_STATE_POST_IN_PROGRESS 0x00000002
  - NX_CRYPTO_LIBRARY_STATE_INTEGRITY_TEST_FAILED 0x00000004
  - NX_CRYPTO_LIBRARY_STATE_FUNCTIONAL_TEST_FAILED 0x00000008
  - NX_CRYPTO_LIBRARY_STATE_OPERATIONAL 0x80000000
- **Tutti gli altri valori non sono validi.**

### <a name="example"></a>Esempio

TODO

## <a name="_nx_crypto_method_aes_init"></a>_nx_crypto_method_aes_init

Inizializza il blocco di controllo della crittografia AES

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_aes_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo AES con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo AES, la successiva operazione AES usa la stessa chiave e le stesse dimensioni della chiave.

L'applicazione può creare più blocchi di controllo AES, ognuno dei quali rappresenta una sessione. Una chiave viene assegnata a un blocco di controllo. La successiva operazione di crittografia o decrittografia può fare riferimento allo stesso blocco di controllo AES senza la necessità di inizializzare nuovamente il blocco di controllo AES. Se la chiave per la sessione viene modificata, l'applicazione deve inizializzare nuovamente il blocco di controllo AES con la chiave aggiornata.

La chiamata a _ *nx_crypto_method_aes_init()* aggiorna automaticamente una chiave configurata in precedenza e le dimensioni della chiave alla nuova chiave.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia AES valido. Sono disponibili i metodi di crittografia AES predefiniti seguenti:
  - *crypto_method_aes_cbc_128*
  - *crypto_method_aes_cbc_192*
  - *crypto_method_aes_cbc_256*
  - *crypto_method_aes_ctr_128*
  - *crypto_method_aes_ctr_192*
  - *crypto_method_aes_ctr_256*
  - *crypto_method_aes_xcbc_128*
  - *crypto_method_aes_ccm_8_128*
- **chiave** Punta a un buffer contenente la chiave AES
- **key_size_in_bits** Dimensioni della chiave, in bit. I valori validi sono:
  - *NX_CRYPTO_AES_KEY_SIZE_128_BITS*
  - *NX_CRYPTO_AES_KEY_SIZE_192_BITS*
  - *NX_CRYPTO_AES_KEY_SIZE_256_BITS*
  - **Tutti gli altri valori non sono validi.**
- **handle** Questo servizio restituisce un handle al chiamante. L'handle dipende dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo AES. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per AES, le dimensioni dei metadati devono *essere sizeof(NX_AES)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo AES con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR (0x07)** Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.
- **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) Le dimensioni della chiave non sono valide per AES.

## <a name="_nx_crypto_method_aes_operation"></a>_nx_crypto_method_aes_operation

Eseguire un'operazione AES (crittografia o decrittografia).

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_aes_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione di crittografia o decrittografia AES. Il blocco di controllo AES deve essere stato inizializzato con _ *nx_crypto_method_aes_init()*. L'algoritmo AES da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

La dimensione del buffer di input deve essere un multiplo di 16 byte. Le dimensioni dei dati decrittografati sono le stesse delle dimensioni dei dati di input. Se i dati crittografati sono stati riempiti per ottenere un multiplo pari delle dimensioni del blocco AES, la spaziatura interna verrà inclusa nel buffer di output e deve essere gestita dall'applicazione.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo AES.

Quando l'operazione è NX_CRYPTO_SET_ADDITIONAL_DATA e l'algoritmo è AES-CCM8, l'input punta a dati aggiuntivi e input_length_in_byte è la lunghezza dei dati aggiuntivi.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. Le operzioni valide sono:
  - *NX_CRYPTO_ENCRYPT*
  - *NX_CRYPTO_DECRYPT*
  - *NX_CRYPTO_AUTHENTICATE (solo AES-XCBC)*
  - *NX_CRYPTO_SET_ADDITIONAL_DATA (solo AES-CCM8)*
- **handle** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia AES valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato *nel nx_crypto_method_aes_init().*
- **input_data** Punta a un buffer contenente dati di testo crittografati. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte. Le dimensioni dei dati di input devono essere un multiplo di 16 byte.
- **iv_ptr** Puntatore al vettore iniziale. Non sono presenti restrizioni per il buffer IV.
- **iv_size** Dimensioni del blocco Vettore iniziale, in byte. Questo campo deve essere 16.
- **output_buffer** Puntatore all'area di memoria per AES per archiviare i dati non crittografati. L'applicazione deve allocare spazio per il buffer di output. Il buffer di output può sovrapporsi al buffer di input. Il buffer di output può sovrapporsi al buffer di input se condividono lo stesso indirizzo iniziale.
- **output_buffer_size** Dimensioni del buffer di output in byte. Le dimensioni del buffer di output devono essere almeno uguali alle dimensioni del buffer di input e le dimensioni del buffer di output devono essere un multiplo di 16 byte.
- **crypto_metadata** Puntatore al blocco di controllo AES usato in *_nx_crypto_method_aes_init() \* . \**
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per AES, le dimensioni dei metadati devono *essere sizeof(NX_AES)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback:** questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione AES è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo AES non valido**.

## <a name="_nx_crypto_method_aes_cleanup"></a>_nx_crypto_method_aes_cleanup

Pulire il blocco di controllo AES.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_aes_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo AES dopo aver determinato che questa sessione AES non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo AES usato in *_nx_crypto_method_aes_init() \* . \**

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione AES completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_3des_init"></a>_nx_crypto_method_3des_init

Inizializzare il blocco di controllo 3DES.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_3des_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo Triple DES (3DES) con le tre stringhe chiave specificate. Le stringhe chiave devono essere di 8 byte ciascuna. Le tre chiavi DES devono essere concatenate in memoria contigua di buffer a 24 byte. Per la compilazione conforme a FIPS, le tre chiavi devono essere diverse da ognuna o la funzione restituirà l'NX_CRYPTO_INVALID_KEY errore. Dopo l'inizializzazione del blocco di controllo 3DES, le operazioni 3DES successive useranno le stesse chiavi.

Un'applicazione può creare più blocchi di controllo 3DES, ognuno dei quali rappresenta una sessione. Una chiave viene assegnata a un blocco di controllo e le successive operazioni di crittografia o decrittografia possono fare riferimento allo stesso blocco di controllo senza dover eseguire di nuovo l'inizializzazione. Se la chiave per una sessione viene modificata, l'applicazione dovrà inizializzare nuovamente il blocco di controllo con la chiave aggiornata.

La chiamata *a _ nx_crypto_method_3des_init()* aggiorna automaticamente una chiave configurata in precedenza per le nuove chiavi.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia 3DES valido. È disponibile il metodo di crittografia 3DES predefinito seguente: ***crypto_method_3des***
- **chiave** Punta a un buffer contenente la chiave DES tre (3)
- **key_size_in_bits** Deve essere 192 (3 chiavi, ogni 64 bit).
- **handle** Questo servizio restituisce un handle al chiamante. L'handle identifica il blocco di controllo 3DES da inizializzare. Le operazioni 3DES successive (crittografia, decrittografia e pulizia) usano questo handle per accedere al blocco di controllo 3DES
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo 3DES. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per 3DES, le dimensioni dei metadati devono *essere sizeof(NX_3DES)*

### <a name="return-value"></a>Valore restituito

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo 3DES con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR (0x07)** Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.
- **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) La dimensione della chiave non è valida per 3DES.

## <a name="_nx_crypto_method_3des_operation"></a>_nx_crypto_method_3des_operation

Crittografare o decrittografare con 3DES.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_3des_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue un'operazione di crittografia o decrittografia 3DES. Il blocco di controllo 3DES deve essere stato inizializzato con _ *nx_crypto_method_3des_init().* L'algoritmo 3DES da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

La dimensione del buffer di input deve essere un multiplo di 8 byte. Le dimensioni dei dati decrittografati sono le stesse delle dimensioni dei dati di input. Se i dati crittografati sono stati riempiti per ottenere un multiplo pari delle dimensioni del blocco 3DES, la spaziatura interna verrà inclusa nel buffer di output e deve essere gestita dall'applicazione.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo 3DES.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. Le operazioni valide sono:
  - *NX_CRYPTO_ENCRYPT*
  - *NX_CRYPTO_DECRYPT*
- **handle** Handle inizializzato da *_nx_crypto_method_3des_init()*.
- **metodo** Puntatore al metodo di crittografia 3DES valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato *nel nx_crypto_method_3des_init().*
- **input_data** Punta a un buffer contenente dati di testo crittografati.
Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte. Le dimensioni dei dati di input devono essere un multiplo di 8 byte.
- **iv_ptr** Puntatore al vettore iniziale. Non sono presenti restrizioni per il buffer IV.
- **iv_size** Dimensioni del blocco Vettore iniziale, in byte. Questo campo deve essere 8.
- **output_buffer** Puntatore all'area di memoria per 3DES per archiviare i dati non crittografati. L'applicazione deve allocare spazio per il buffer di output. Il buffer di output può sovrapporsi al buffer di input. Il buffer di output può sovrapporsi al buffer di input se condividono lo stesso indirizzo iniziale.
- **output_buffer_size** Dimensioni del buffer di output in byte. Le dimensioni del buffer di output devono essere almeno uguali alle dimensioni del buffer di input e le dimensioni del buffer di output devono essere un multiplo di 8 byte.
- **crypto_metadata** Puntatore al blocco di controllo 3DES usato in *_nx_crypto_method_3des_init().*
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per 3DES, le dimensioni dei metadati devono *essere sizeof(NX_3DES)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="description"></a>Descrizione

Questa funzione esegue la crittografia 3DES. Il blocco di controllo 3DES deve essere stato inizializzato con _ *nx_crypto_moethod_3des_init()*. Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo 3DES. Si noti che la spaziatura interna non viene aggiunta da questa funzione, quindi il chiamante dovrà gestire la spaziatura interna prima di richiamare l'operazione di crittografia.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo 3DES con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR (0x07)** Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_3des_cleanup"></a>_nx_crypto_method_3des_cleanup

Pulire il blocco di controllo 3DES.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_3des_cleanup(VOID *crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo 3DES dopo aver determinato che questa sessione 3DES non è più necessaria.

### <a name="parameters"></a>Parametri

- **handle** Handle inizializzato da *_nx_crypto_method_3des_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) È stata completata la pulizia della sessione 3DES.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_drbg_init"></a>_nx_crypto_method_drbg_init

Inizializza il blocco di controllo crittografico DRBG

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_drbg_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo DRBG con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo DRBG, l'operazione DRBG successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo DRBG, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo DRBG avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo DRBG abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia DRBG valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_drbg*
- **chiave** Questo campo non viene usato per DRBG.
- **key_size_in_bits** Questo campo non viene usato per DRBG.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle dipende dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo DRBG. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per DRBG, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_DRBG)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo DRBG con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_drbg_operation"></a>_nx_crypto_method_drbg_operation

Eseguire un'operazione DRBG

### <a name="prototype"></a>Prototipo

```c
UINT __nx_crypto_method_drbg_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione DRBG. Il blocco di controllo DRBG deve essere stato inizializzato con _ *nx_crypto_method_drbg_init()*. L'algoritmo DRBG da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo. Per impostazione predefinita, per DRBG viene usato AES-128.

Quando l'operazione viene NX_CRYPTO_DRBG_OPTIONS_SET, l'input punta NX_CRYPTO_DRBG_OPTIONS struttura . Quando l'operazione viene NX_CRYPTO_DRBG_INSTANTIATE, il tasto punta a nonce, l'input punta alla stringa di personalizzazione. Quando l'operazione viene NX_CRYPTO_DRBG_RESEED o NX_CRYPTO_DRBG_GENERATE, l'input punta a un input aggiuntivo.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_DRBG_OPTIONS_SET*
  - *NX_CRYPTO_DRBG_INSTANTIATE*
  - *NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia DRBG valido. Il metodo crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_drbg_init().*
- **chiave** Puntatore al nonce per l'operazione di creazione dell'istanza. Questo campo non viene usato per altre operazioni.
- **key_size_in_bits** Dimensioni del nonce, in bit. Questo campo non viene usato per altre operazioni.
- **input** Quando op è NX_CRYPTO_DRBG_OPTIONS_SET, questo campo punta alle opzioni DRBG. Quando op è NX_CRYPTO_DRBG_INSTANTIATE, questo campo punta alla stringa di personalizzazione. Quando op è NX_CRYPTO_DRBG_RESEED o NX_CRYPTO_DRBG_GENERATE, questo campo punta a dati di input aggiuntivi.
- **input_length_in_byte** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene usato per DRBG.
- **output** Quando op è NX_CRYPTO_DRBG_GENERATE, questo campo punta all'area di memoria per il DRBG generato. In caso contrario, questo campo non viene usato.
- **output_length_in_byte** Dimensione in byte del buffer di output.
- **crypto_metadata** Puntatore al blocco di controllo DRBG usato in *_nx_crypto_method_drbg_init()*.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per DRBG, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_DRBG)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione DRBG è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Algoritmo DRBG non valido specificato.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_drbg_cleanup"></a>_nx_crypto_method_drbg_cleanup

Pulire il blocco di controllo DRBG.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_drbg_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo DRBG dopo aver determinato che la sessione DRBG non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo DRBG usato in *_nx_crypto_method_drbg_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione DRBG completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_ecdh_init"></a>_nx_crypto_method_ecdh_init

Inizializza il blocco di controllo della crittografia ECDH

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdh_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo ECDH con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo ECDH, l'operazione ECDH successiva deve usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo ECDH, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo ECDH avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo ECDH abbandona la sessione corrente e ne attiva una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia ECDH valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_ecdh*
- **chiave** Questo campo non viene usato per ECDH.
- **key_size_in_bits** Questo campo non viene usato per ECDH.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle è dipendente dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo ECDH. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per ECDH, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_ECDH)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo ECDH con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_ecdh_operation"></a>_nx_crypto_method_ecdh_operation

Eseguire un'operazione ECDH

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdh_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue un'operazione ECDH. Il blocco di controllo ECDH deve essere stato inizializzato con _ *nx_crypto_method_ecdh_init()*. L'algoritmo ECDH da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Quando l'operazione è NX_CRYPTO_EC_CURVE_SET, l'input punta al metodo di crittografia a curva ellittica. Quando l'operazione viene NX_CRYPTO_EC_KEY_PAIR_GENERATE, l'output punta NX_CRYPTO_EXTENDED_OUTPUT struttura e la coppia di chiavi viene copiata in nx_crypto_extended_output_data. Quando l'operazione viene NX_CRYPTO_DH_SETUP, la chiave pubblica viene restituita a nx_crypto_extended_output_data. Quando l'operazione viene NX_CRYPTO_DH_KEY_PAIR_IMPORT, l'input punta alla chiave pubblica e la chiave punta alla chiave privata. Quando l'operazione viene NX_CRYPTO_DH_PRIVATE_KEY_EXPORT, la chiave privata viene copiata in nx_crypto_extended_output_data. Quando l'operazione viene NX_CRYPTO_DH_CALCULATE, l'input punta alla chiave pubblica remota e il segreto condiviso viene copiato in nx_crypto_extended_output_data.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_EC_CURVE_SET*
  - *NX_CRYPTO_DH_SETUP*
  - *NX_CRYPTO_DH_CALCULATE*
  - *NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*
  - *NX_CRYPTO_DH_KEY_PAIR_GENERATE*
  - *NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*
- **handle** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia ECDH valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_ecdh_init().*
- **chiave** Quando op è NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo punta alla chiave privata. In caso contrario, questo campo non viene usato per ECDH.
- **key_size_in_bits** Dimensione della chiave, in bit.
- **input** Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo punta al metodo di crittografia a curva ellittica. Quando op è NX_CRYPTO_DH_SETUP, questo campo non viene usato. Quando op è NX_CRYPTO_DH_CALCULATE, questo campo punta a un buffer contenente dati di testo di input. Quando op è NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo punta alla chiave pubblica.
- **input_length_in_byte** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per ECDH.
- **output** Quando op è NX_CRYPTO_EC_CURVE_SET o NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo non viene usato. Quando op è NX_CRYPTO_DH_SETUP, questo campo punta all'area di memoria per la chiave pubblica ECDH generata. Quando op è NX_CRYPTO_DH_CALCULATE, questo campo punta all'area di memoria per il segreto condiviso ECDH generato.
- **output_length_in_byte** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo ECDH usato in *_nx_crypto_method_ecdh_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per ECDH, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_ECDH)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione ECDH è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo ECDH non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_ecdh_cleanup"></a>_nx_crypto_method_ecdh_cleanup

Pulire il blocco di controllo ECDH.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdh_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo ECDH dopo aver determinato che questa sessione ECDH non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo ECDH usato in *_nx_crypto_method_ecdh_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione ECDH completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_ecdsa_init"></a>_nx_crypto_method_ecdsa_init

Inizializza il blocco di controllo della crittografia ECDSA

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdsa_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo ECDSA con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo ECDSA, l'operazione ECDSA successiva deve usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo ECDSA, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo ECDSA avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo ECDSA abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo crittografico ECDSA valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_ecdsa*
- **chiave** Questo campo non viene usato per ECDSA.
- **key_size_in_bits** Questo campo non viene usato per ECDSA.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle dipende dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo ECDSA. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per ECDSA, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_ECDSA)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo ECDSA con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_ecdsa_operation"></a>_nx_crypto_method_ecdsa_operation

Eseguire un'operazione ECDSA

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdsa_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione ECDSA. Il blocco di controllo ECDSA deve essere stato inizializzato con _ *nx_crypto_method_ecdsa_init()*. L'algoritmo ECDSA da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Quando l'operazione viene NX_CRYPTO_EC_CURVE_SET, l'input punta al metodo crittografico curva ellittica. Quando l'operazione viene NX_CRYPTO_EC_KEY_PAIR_GENERATE, l'output punta NX_CRYPTO_EXTENDED_OUTPUT struttura e la coppia di chiavi viene copiata in nx_crypto_extended_output_data.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_EC_CURVE_SET*
  - *NX_CRYPTO_AUTHENTICATE*
  - *NX_CRYPTO_VERIFY*
- **handle** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia ECDSA valido. Il metodo crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_ecdsa_init().*
- **chiave** Punta alla chiave quando op è NX_CRYPTO_VERIFY. Non sono presenti restrizioni sul buffer delle chiavi. Questo campo non viene usato per altri valori di op.
- **key_size_in_bits** Dimensioni della chiave, in bit.
- **input** Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo punta al metodo di crittografia Elliptic Curve. In caso contrario, questo campo punta a un buffer contenente dati di testo di input.
- **input_length_in_byte** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per ECDSA.
- **output** Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo non viene usato. Quando op è NX_CRYPTO_AUTHENTICATE, questo campo punta all'area di memoria per la firma ECDSA generata. Quando op è NX_CRYPTO_VERIFY, questo campo punta all'area di memoria per la firma ECDSA verificata.
- **output_length_in_byte** Dimensione in byte del buffer di output.
- **crypto_metadata** Puntatore al blocco di controllo ECDSA usato in *_nx_crypto_method_ecdsa_init()*.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per ECDSA, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_ECDSA)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione ECDSA è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Algoritmo ECDSA non valido specificato.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_ecdsa_cleanup"></a>_nx_crypto_method_ecdsa_cleanup

Pulire il blocco di controllo ECDSA.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdsa_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo ECDSA dopo aver determinato che questa sessione ECDSA non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo ECDSA usato in *_nx_crypto_method_ecdsa_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) È stata completata la pulizia della sessione ECDSA.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_hmac_md5_init"></a>_nx_crypto_method_hmac_md5_init

Inizializza il blocco di controllo della crittografia MD5 HMAC

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo MD5 HMAC con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo MD5 HMAC, l'operazione HMAC MD5 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo MD5 HMAC, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo MD5 HMAC avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo MD5 HMAC abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC MD5 valido.
Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_md5*
- **chiave** Punta alla chiave. Non sono presenti restrizioni sul buffer delle chiavi.
- **key_size_in_bits** Dimensioni della chiave, in bit.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle dipende dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo MD5 HMAC. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per HMAC MD5, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_MD5_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo MD5 HMAC con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_md5_operation"></a>_nx_crypto_method_hmac_md5_operation

Eseguire un'operazione hash HMAC MD5.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_md5_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue un'operazione hash HMAC MD5. Il blocco di controllo MD5 HMAC deve essere stato inizializzato con _ *nx_crypto_method_hmac_md5_init().* L'algoritmo HMAC MD5 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'operazione NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 16 byte.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo HMAC MD5.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia HMAC MD5 valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato *nel nx_crypto_method_hmac_md5_init().*
- **chiave** Punta alla chiave. Non sono presenti restrizioni per il buffer della chiave.
- **key_size_in_bits** Dimensione della chiave, in bit.
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per HMAC MD5.
- **iv_size** Questo campo non viene usato per HMAC MD5.
- **output_buffer** Puntatore all'area di memoria per l'hash MD5 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC MD5 usato in *_nx_crypto_method_hmac_md5_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per HMAC MD5, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_MD5_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione HMAC MD5 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo HMAC MD5 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_hmac_sha1_init"></a>_nx_crypto_method_hmac_sha1_init

Inizializza il blocco di controllo crittografico HMAC SHA1

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo HMAC SHA1 con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo HMAC SHA1, l'operazione HMAC SHA1 successiva deve usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC SHA1, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC SHA1 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo HMAC SHA1 abbandona la sessione corrente e ne attiva una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia HMAC SHA1 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_sha1*
- **chiave** Punta alla chiave. Non sono presenti restrizioni per il buffer della chiave.
- **key_size_in_bits** Dimensione della chiave, in bit.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle è dipendente dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA1. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per HMAC SHA1, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA1_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo HMAC SHA1 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_sha1_operation"></a>_nx_crypto_method_hmac_sha1_operation

Eseguire un'operazione hash HMAC SHA1

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha1_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione hash HMAC SHA1. Il blocco di controllo SHA1 HMAC deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha1_init()*. L'algoritmo HMAC SHA1 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 20 byte.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia HMAC SHA1 valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha1_init().*
- **chiave** Punta alla chiave. Non sono presenti restrizioni per il buffer della chiave.
- **key_size_in_bits** Dimensione della chiave, in bit.
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per HMAC SHA1.
- **iv_size** Questo campo non viene usato per HMAC SHA1.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA1 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA1 usato in *_nx_crypto_method_hmac_sha1_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per HMAC SHA1, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA1_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione HMAC SHA1 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** specificato un 0x20004 HMAC SHA1 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_hmac_sha1_cleanup"></a>_nx_crypto_method_hmac_sha1_cleanup

Pulire il blocco di controllo HMAC SHA1.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA1 dopo aver determinato che questa sessione HMAC SHA1 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA1 usato in *_nx_crypto_method_hmac_sha1_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione HMAC SHA1 completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_hmac_sha256_init"></a>_nx_crypto_method_hmac_sha256_init

Inizializza il blocco di controllo crittografico HMAC SHA256

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo HMAC SHA256 con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo HMAC SHA256, l'operazione HMAC SHA256 successiva deve usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC SHA256, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC SH256 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo HMAC SHA256 abbandona la sessione corrente e ne attiva una nuova con una nuova chiave.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia HMAC SHA256 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_sha224*
  - *crypto_method_hmac_sha256*
- **chiave** Punta alla chiave. Non sono presenti restrizioni per il buffer della chiave.
- **key_size_in_bits** Dimensione della chiave, in bit.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle è dipendente dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA256. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per HMAC SHA256, le dimensioni dei metadati devono *essere sizeof(NX_CRYTPO_SHA256_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo HMAC SHA256 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_sha256_operation"></a>_nx_crypto_method_hmac_sha256_operation

Eseguire un'operazione hash HMAC SHA256

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha256_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione hash HMAC SHA256. Il blocco di controllo HMAC SHA256 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha256_init()*. L'algoritmo HMAC SHA256 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 32 byte per SHA256 o di 28 byte per SHA224.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia HMAC SHA256 valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha256_init().*
- **chiave** Punta alla chiave. Non sono presenti restrizioni per il buffer della chiave.
- **key_size_in_bits** Dimensione della chiave, in bit.
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per HMAC SHA256.
- **iv_size** Questo campo non viene usato per HMAC SHA256.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA256 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA256 usato in *_nx_crypto_method_hmac_sha256_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per HMAC SHA256, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA256_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione HMAC SHA256 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** specificato un 0x20004 HMAC SHA256 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_hmac_sha256_cleanup"></a>_nx_crypto_method_hmac_sha256_cleanup

Pulire il blocco di controllo HMAC SHA256.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA256 dopo aver determinato che questa sessione HMAC SHA256 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA256 usato in *_nx_crypto_method_hmac_sha256_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione HMAC SHA256 completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_hmac_sha512_init"></a>_nx_crypto_method_hmac_sha512_init

Inizializza il blocco di controllo crittografico HMAC SHA512

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo HMAC SHA512 con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo HMAC SHA512, l'operazione HMAC SHA512 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC SHA512, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC SH512 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo HMAC SHA512 abbandona la sessione corrente e ne indica una nuova con una nuova chiave.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo crypto HMAC SHA512 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_sha384*
  - *crypto_method_hmac_sha512*
- **chiave** Punta alla chiave. Non sono presenti restrizioni sul buffer delle chiavi.
- **key_size_in_bits** Dimensioni della chiave, in bit.
- **handle** Questo servizio restituisce un handle al chiamante. L'handle dipende dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA512. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per HMAC SHA512, le dimensioni dei metadati devono essere *sizeof(NX_CRYPTO_SHA512_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo HMAC SHA512 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_sha512_operation"></a>_nx_crypto_method_hmac_sha512_operation

Eseguire l'operazione hash HMAC SHA512

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha512_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione hash HMAC SHA512. Il blocco di controllo HMAC SHA512 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha512_init()*. L'algoritmo SHA512 HMAC da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 64 byte per SHA512 o di 48 byte per SHA384.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia HMAC SHA512 valido. Il metodo crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha512_init().*
- **chiave** Punta alla chiave. Non sono presenti restrizioni sul buffer delle chiavi.
- **key_size_in_bits** Dimensioni della chiave, in bit.
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni sul buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per HMAC SHA512.
- **iv_size** Questo campo non viene usato per HMAC SHA512.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA512 HMAC generato.
- **output_buffer_size** Dimensione in byte del buffer di output.
- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA512 usato in *_nx_crypto_method_hmac_sha512_init()*.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per HMAC SHA512, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA512_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione HMAC SHA512 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo HMAC SHA512 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_hmac_sha512_cleanup"></a>_nx_crypto_method_hmac_sha512_cleanup

Pulire il blocco di controllo HMAC SHA512.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA512 dopo aver determinato che questa sessione HMAC SHA512 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA512 usato in *_nx_crypto_method_hmac_sha512_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) È stata completata la pulizia della sessione HMAC SHA512.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.

### <a name="example"></a>Esempio 

## <a name="_nx_crypto_method_md5_init"></a>_nx_crypto_method_md5_init

Inizializza il blocco di controllo della crittografia MD5

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo MD5 con la stringa di chiave specificata. Dopo l'inizializzazione del blocco di controllo MD5, l'operazione MD5 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo MD5, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo MD5 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo MD5 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia MD5 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_md5*
- **chiave** Questo campo non viene usato per MD5.
- **key_size_in_bits** Questo campo non viene usato per MD5
- **handle** Questo servizio restituisce un handle al chiamante. L'handle dipende dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo MD5. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per MD5, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_MD5)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo MD5 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.

### <a name="example"></a>Esempio

## <a name="_nx_crypto_method_md5_operation"></a>_nx_crypto_method_md5_operation

Eseguire un'operazione hash MD5.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_md5_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue un'operazione hash MD5. Il blocco di controllo MD5 deve essere stato inizializzato con _ *nx_crypto_method_md5_init()*. L'algoritmo MD5 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 16 byte.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo MD5.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia MD5 valido. Il metodo crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_md5_init().*
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni sul buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per MD5.
- **iv_size** Questo campo non viene usato per MD5.
- **output_buffer** Puntatore all'area di memoria per l'hash MD5 generato.
- **output_buffer_size** Dimensione in byte del buffer di output. Per MD5 le dimensioni del buffer devono essere di 16 byte.
- **crypto_metadata** Puntatore al blocco di controllo MD5 usato in *_nx_crypto_method_md5_init()*.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per MD5, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_MD5)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione MD5 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo MD5 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_md5_cleanup"></a>_nx_crypto_method_md5_cleanup

Pulire il blocco di controllo MD5.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_md5_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo MD5 dopo aver determinato che questa sessione MD5 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo MD5 usato in *_nx_crypto_method_md5_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione MD5 completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_sha1_init"></a>_nx_crypto_method_sha1_init

Inizializza il blocco di controllo della crittografia SHA1

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo SHA1 con la stringa di chiave specificata. Dopo l'inizializzazione del blocco di controllo SHA1, l'operazione SHA1 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo SHA1, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo SHA1 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo SHA1 abbandona la sessione corrente e ne indica una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia SHA1 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_sha1*
- **chiave** Questo campo non viene usato per SHA1.
- **key_size_in_bits** Questo campo non viene usato per SHA1
- **handle** Questo servizio restituisce un handle al chiamante. L'handle è dipendente dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA1. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensioni, in byte, dell'area crypto_metadata corrente. Per SHA1, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA1)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco SHA1control con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria crypto è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_sha1_operation"></a>_nx_crypto_method_sha1_operation

Eseguire un'operazione hash SHA1

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha1_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione hash SHA1. Il blocco di controllo SHA1 deve essere stato inizializzato con _ *nx_crypto_method_sha1_init()*. L'algoritmo SHA1 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 20 byte.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria Crypto NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia SHA1 valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato *nel nx_crypto_method_sha1_init().*
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per SHA1.
- **iv_size** Questo campo non viene usato per SHA1.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA1 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per SHA1 le dimensioni del buffer devono essere di 20 byte.
- **crypto_metadata** Puntatore al blocco di controllo SHA1 usato in *_nx_crypto_method_sha1_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per SHA1, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA1)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione SHA1 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) È stato specificato un algoritmo SHA1 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

### <a name="example"></a>Esempio

## <a name="_nx_crypto_method_sha1_cleanup"></a>_nx_crypto_method_sha1_cleanup

Pulire il blocco di controllo SHA1.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo SHA1 dopo aver determinato che questa sessione SHA1 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo SHA1 usato in *_nx_crypto_method_sha1_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione SHA1 completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_sha256_init"></a>_nx_crypto_method_sha256_init

Inizializza il blocco di controllo della crittografia SHA256

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size)
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo SHA256 con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo SHA256, l'operazione SHA256 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo SHA256, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo SHA256 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo SHA256 abbandona la sessione corrente e ne attiva una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia SHA256 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_sha256*
  - *crypto_method_sha224*
- **chiave** Questo campo non viene usato per SHA256.
- **key_size_in_bits** Questo campo non viene usato per SHA256
- **handle** Questo servizio restituisce un handle al chiamante. L'handle è dipendente dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA256. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per SHA256, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA256)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo SHA256 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_sha256_operation"></a>_nx_crypto_method_sha256_operation

Eseguire un'operazione hash SHA256

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha256_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione hash SHA256. Il blocco di controllo SHA256 deve essere stato inizializzato con _ ***nx_crypto_method_sha256_init().*** L'algoritmo SHA256 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 32 byte per SHA256 o di 28 byte per SHA224.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia SHA256 valido. Il metodo di crittografia usato qui deve essere lo stesso usato in _ *nx_crypto_method_sha256_init().*
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per SHA256.
- **iv_size** Questo campo non viene usato per SHA256.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA256 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per SHA256 le dimensioni del buffer devono essere di 32 byte. Per SHA224 le dimensioni del buffer devono essere di 28 byte.
- **crypto_metadata** Puntatore al blocco di controllo SHA2 usato in *_nx_crypto_method_sha2_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per SHA256, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA256)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione SHA256 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo SHA256 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_sha256_cleanup"></a>_nx_crypto_method_sha256_cleanup

Pulire il blocco di controllo SHA256.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo SHA256 dopo aver determinato che questa sessione SHA256 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo SHA256 usato in *_nx_crypto_method_sha256_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione SHA256 completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.

## <a name="_nx_crypto_method_sha512_init"></a>_nx_crypto_method_sha512_init

Inizializza il blocco di controllo della crittografia SHA512

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Descrizione

Questa funzione inizializza il blocco di controllo SHA512 con la stringa chiave specificata. Dopo l'inizializzazione del blocco di controllo SHA512, l'operazione SHA512 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo SHA512, ognuno dei quali rappresenta una sessione. L'inizializzazione del blocco di controllo SHA512 avvia una nuova sessione di calcolo hash. La nuova inizializzazione del blocco di controllo SHA512 abbandona la sessione corrente e ne attiva una nuova.

### <a name="parameters"></a>Parametri

- **metodo** Puntatore a un blocco di controllo del metodo di crittografia SHA512 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_sha512*
  - *crypto_method_sha384*
- **chiave** Questo campo non viene usato per SHA512.
- **key_size_in_bits** Questo campo non viene usato per SHA512
- **handle** Questo servizio restituisce un handle al chiamante. L'handle è dipendente dall'implementazione e non viene usato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA512. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per SHA512, le dimensioni dei metadati devono *essere sizeof(NX_CRYPTO_SHA512)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Inizializzazione riuscita del blocco di controllo SHA512 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido alla chiave, crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_sha512_operation"></a>_nx_crypto_method_sha512_operation

Eseguire un'operazione hash SHA512

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha512_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT status));
```

### <a name="description"></a>Descrizione

Questa funzione esegue l'operazione hash SHA512. Il blocco di controllo SHA512 deve essere stato inizializzato con _ *nx_crypto_method_sha512_init().* L'algoritmo SHA512 da eseguire si basa sull'algoritmo specificato nel blocco *di controllo* del metodo.

Per *l'NX_CRYPTO_HASH_CALCULATE* finale, le dimensioni del buffer di output devono essere di 64 byte per SHA512 o di 48 byte per SHA384.

### <a name="parameters"></a>Parametri

- **op** Tipo di operazione da eseguire. L'operazione valida è:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **metodo** Puntatore al metodo di crittografia SHA512 valido. Il metodo di crittografia usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_sha512_init().*
- **input_data** Punta a un buffer contenente dati di testo di input. Non sono presenti restrizioni per il buffer di input.
- **input_data_size** Dimensioni dei dati di input, in byte.
- **iv_ptr** Questo campo non viene usato per SHA512.
- **iv_size** Questo campo non viene usato per SHA512.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA512 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per SHA512 le dimensioni del buffer devono essere di 64 byte. Per SHA384 le dimensioni del buffer devono essere di 48 byte.
- **crypto_metadata** Puntatore al blocco di controllo SHA512 usato in *_nx_crypto_method_sha512_init()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata dati. Per SHA512, la dimensione dei metadati deve *essere sizeof(NX_CRYPTO_SHA512)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software della libreria di crittografia NetX. Tutti i valori passati vengono ignorati automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) L'operazione SHA512 è stata eseguita correttamente.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Specificato algoritmo SHA512 non valido.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Dimensioni del buffer di output non valide.

## <a name="_nx_crypto_method_sha512_cleanup"></a>_nx_crypto_method_sha512_cleanup

Pulire il blocco di controllo SHA512.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo SHA512 dopo aver determinato che questa sessione SHA512 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo SHA512 usato in *_nx_crypto_method_sha512_init()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) Pulizia della sessione SHA512 completata.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) La libreria di crittografia è in uno stato non valido e non può essere usata.