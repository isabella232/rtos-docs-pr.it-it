---
title: Capitolo 4-Descrizione dell'API Crypto NetX di Azure RTO
description: Descrizione dell'API Crypto NetX di Azure RTO
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 04e732bc1fd6012636aab3a57391829f529724cf
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822715"
---
# <a name="chapter-4---azure-rtos-netx-crypto-api-description"></a>Capitolo 4-Descrizione dell'API Crypto NetX di Azure RTO

## <a name="nx_crypto_initialize"></a>nx_crypto_initialize

Inizializza la libreria protetta NetX

### <a name="prototype"></a>Prototipo

```c
UINT nx_crypto_initialize(VOID);
```

### <a name="description"></a>Descrizione

Questa funzione Inizializza il modulo libreria di crittografia NetX di Azure RTO. Prima di utilizzare qualsiasi altra funzione di crittografia, l'applicazione deve chiamare questa funzione per eseguire l'inizializzazione e per convalidare l'integrità della libreria. La mancata chiamata di questa funzione prima di usare altri servizi di crittografia NetX comporterà la restituzione di errori.

### <a name="parameters"></a>Parametri

- **Nessuno**

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) la libreria di crittografia NETX inizializzata è riuscita. Le funzioni della libreria sono ora pronte e possono essere utilizzate.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) non è possibile inizializzare la libreria di crittografia oppure il controllo di integrità non riesce. L'applicazione non può usare questa libreria.

### <a name="example"></a>Esempio

TODO

## <a name="nx_crypto_module_state_get"></a>nx_crypto_module_state_get

Recuperare lo stato corrente del modulo abilitato per FIPS

### <a name="prototype"></a>Prototipo

```c
UINT nx_crypto_module_state_get(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio è disponibile solo nella libreria di compilazione FIPS. Restituisce lo stato corrente della libreria di crittografia NetX.

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

Inizializza il blocco di controllo Crypto AES

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

Questa funzione Inizializza il blocco di controllo AES con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo AES, l'operazione AES successiva utilizzerà la stessa chiave e la stessa dimensione della chiave.

L'applicazione può creare più blocchi di controllo AES, ognuno rappresenta una sessione. Una chiave viene assegnata a un blocco di controllo. L'operazione di crittografia o decrittografia successiva può fare riferimento allo stesso blocco di controllo AES senza la necessità di inizializzare nuovamente il blocco di controllo AES. Se la chiave per la sessione viene modificata, l'applicazione deve inizializzare nuovamente il blocco di controllo AES con la chiave aggiornata.

La chiamata a _ *nx_crypto_method_aes_init ()* consente di aggiornare automaticamente una chiave e una dimensione della chiave configurate in precedenza alla nuova chiave.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo di crittografia AES valido. Sono disponibili i metodi di crittografia AES predefiniti seguenti:
  - *crypto_method_aes_cbc_128*
  - *crypto_method_aes_cbc_192*
  - *crypto_method_aes_cbc_256*
  - *crypto_method_aes_ctr_128*
  - *crypto_method_aes_ctr_192*
  - *crypto_method_aes_ctr_256*
  - *crypto_method_aes_xcbc_128*
  - *crypto_method_aes_ccm_8_128*
- **chiave** di Punta a un buffer contenente la chiave AES
- **key_size_in_bits** Dimensione della chiave in bit. I valori validi sono:
  - *NX_CRYPTO_AES_KEY_SIZE_128_BITS*
  - *NX_CRYPTO_AES_KEY_SIZE_192_BITS*
  - *NX_CRYPTO_AES_KEY_SIZE_256_BITS*
  - **Tutti gli altri valori non sono validi.**
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo AES. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per AES, le dimensioni dei metadati devono essere *sizeof (NX_AES)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo AES con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR (0x07)** Puntatore alla chiave non valido o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.
- Le dimensioni della chiave **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) non sono valide per AES.

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

Questa funzione esegue l'operazione di crittografia o decrittografia AES. Il blocco di controllo AES deve essere stato inizializzato con _ *nx_crypto_method_aes_init ()*. L'algoritmo AES da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

La dimensione del buffer di input deve essere un multiplo di 16 byte. Le dimensioni dei dati decrittografati hanno le stesse dimensioni della dimensione dei dati di input. Se i dati crittografati sono stati riempiti per ottenere un multiplo pari delle dimensioni del blocco AES, la spaziatura interna verrà inclusa nel buffer di output e deve essere gestita dall'applicazione.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo AES.

Quando l'op è NX_CRYPTO_SET_ADDITIONAL_DATA e algoritmo è AES-CCM8, l'input punta a dati aggiuntivi e input_length_in_byte è la lunghezza dei dati aggiuntivi.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Opertions validi sono:
  - *NX_CRYPTO_ENCRYPT*
  - *NX_CRYPTO_DECRYPT*
  - *NX_CRYPTO_AUTHENTICATE (solo AES-XCBC)*
  - *NX_CRYPTO_SET_ADDITIONAL_DATA (solo AES-CCM8)*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo crittografico AES valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_aes_init ().*
- **input_data** Punta a un buffer contenente dati di testo crittografati. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input. Le dimensioni dei dati di input devono essere un multiplo di 16 byte.
- **iv_ptr** Puntatore al vettore iniziale. Non esistono restrizioni sul buffer IV.
- **iv_size** Dimensione del blocco del vettore iniziale, in byte questo campo deve essere 16.
- **output_buffer** Puntatore all'area di memoria per AES per archiviare i dati di testo non crittografato. L'applicazione deve allocare spazio per il buffer di output. Il buffer di output può sovrapporsi al buffer di input. Il buffer di output può sovrapporsi al buffer di input se condivide lo stesso indirizzo iniziale.
- **output_buffer_size** Dimensioni del buffer di output in byte. La dimensione del buffer di output deve essere uguale almeno alla dimensione del buffer di input e la dimensione del buffer di output deve essere un multiplo di 16 byte.
- **crypto_metadata** Puntatore al blocco di controllo AES utilizzato nel *_nx_crypto_method_aes_init () \* . \**
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per AES, le dimensioni dei metadati devono essere *sizeof (NX_AES)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** : questo campo non è usato nell'implementazione software di NETX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione AES.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) algoritmo AES non valido specificato * *.

## <a name="_nx_crypto_method_aes_cleanup"></a>_nx_crypto_method_aes_cleanup

Pulire il blocco di controllo AES.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_aes_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo AES dopo aver determinato che questa sessione AES non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo AES utilizzato nel *_nx_crypto_method_aes_init () \* . \**

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione AES.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

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

Questa funzione Inizializza il blocco di controllo Triple DES (3DES) con le tre stringhe chiave specificate. Le stringhe di chiave devono essere di 8 byte ciascuna. Le tre chiavi DES devono essere concatenate nella memoria contigua del buffer a 24 byte. Per la compilazione conforme a FIPS, le tre chiavi devono essere diverse da ciascuna o la funzione restituirà l'errore NX_CRYPTO_INVALID_KEY. Una volta inizializzato il blocco di controllo 3DES, le operazioni 3DES successive utilizzeranno le stesse chiavi.

Un'applicazione può creare più blocchi di controllo 3DES, ognuno di essi che rappresenta una sessione. Una chiave viene assegnata a un blocco di controllo e le successive operazioni di crittografia o decrittografia possono fare riferimento allo stesso blocco di controllo senza che sia necessario eseguire di nuovo l'inizializzazione. Se la chiave per una sessione viene modificata, l'applicazione dovrà inizializzare nuovamente il blocco di controllo con la chiave aggiornata.

La chiamata a _ *nx_crypto_method_3des_init ()* consente di aggiornare automaticamente una chiave configurata in precedenza alle nuove chiavi.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo crittografico 3DES valido. È disponibile il seguente metodo di crittografia 3DES predefinito: ***crypto_method_3des***
- **chiave** di Punta a un buffer contenente il tre (3) tasto DES
- **key_size_in_bits** Deve essere 192 (3 chiavi, ogni 64 bit).
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle identifica il blocco di controllo 3DES inizializzato. Le operazioni 3DES successive (crittografia, decrittografia e pulizia) utilizzano questo handle per accedere al blocco di controllo 3DES
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo 3DES. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per 3DES, le dimensioni dei metadati devono essere *sizeof (NX_3DES)*

### <a name="return-value"></a>Valore restituito

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo 3DES con la chiave e la dimensione della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR (0x07)** Puntatore alla chiave non valido o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.
- Le dimensioni della chiave **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) non sono valide per 3DES.

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

Questa funzione esegue l'operazione di crittografia o decrittografia 3DES. Il blocco di controllo 3DES deve essere stato inizializzato con _ *nx_crypto_method_3des_init ()*. L'algoritmo 3DES da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

La dimensione del buffer di input deve essere un multiplo di 8 byte. Le dimensioni dei dati decrittografati hanno le stesse dimensioni della dimensione dei dati di input. Se i dati crittografati sono stati riempiti per ottenere un multiplo pari delle dimensioni del blocco 3DES, la spaziatura interna verrà inclusa nel buffer di output e deve essere gestita dall'applicazione.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo 3DES.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Le operazioni valide sono:
  - *NX_CRYPTO_ENCRYPT*
  - *NX_CRYPTO_DECRYPT*
- **Gestisci** Handle inizializzato da *_nx_crypto_method_3des_init ()*.
- **Metodo** Puntatore al metodo crittografico 3DES valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_3des_init ().*
- **input_data** Punta a un buffer contenente dati di testo crittografati.
Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input. Le dimensioni dei dati di input devono essere un multiplo di 8 byte.
- **iv_ptr** Puntatore al vettore iniziale. Non esistono restrizioni sul buffer IV.
- **iv_size** Dimensione del blocco del vettore iniziale, in byte questo campo deve essere 8.
- **output_buffer** Puntatore all'area di memoria per 3DES per archiviare i dati di testo non crittografato. L'applicazione deve allocare spazio per il buffer di output. Il buffer di output può sovrapporsi al buffer di input. Il buffer di output può sovrapporsi al buffer di input se condivide lo stesso indirizzo iniziale.
- **output_buffer_size** Dimensioni del buffer di output in byte. La dimensione del buffer di output deve essere uguale almeno alla dimensione del buffer di input e la dimensione del buffer di output deve essere un multiplo di 8 byte.
- **crypto_metadata** Puntatore al blocco di controllo 3DES utilizzato nel *_nx_crypto_method_3des_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per 3DES, le dimensioni dei metadati devono essere *sizeof (NX_3DES)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="description"></a>Descrizione

Questa funzione esegue la crittografia 3DES. Il blocco di controllo 3DES deve essere stato inizializzato con _ *nx_crypto_moethod_3des_init ()*. Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo 3DES. Si noti che la spaziatura interna non viene aggiunta da questa funzione in modo che il chiamante debba gestire la spaziatura interna prima di richiamare l'operazione di crittografia.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo 3DES con la chiave e la dimensione della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR (0x07)** Puntatore alla chiave non valido o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_3des_cleanup"></a>_nx_crypto_method_3des_cleanup

Pulire il blocco di controllo 3DES.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_3des_cleanup(VOID *crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo 3DES dopo aver determinato che questa sessione 3DES non è più necessaria.

### <a name="parameters"></a>Parametri

- **Gestisci** Handle inizializzato da *_nx_crypto_method_3des_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione 3DES.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_drbg_init"></a>_nx_crypto_method_drbg_init

Inizializza il blocco di controllo Crypto DRBG

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

Questa funzione Inizializza il blocco di controllo DRBG con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo DRBG, l'operazione DRBG successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo DRBG, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo DRBG avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo DRBG abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo Crypto DRBG valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_drbg*
- **chiave** di Questo campo non viene utilizzato per DRBG.
- **key_size_in_bits** Questo campo non viene utilizzato per DRBG.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo DRBG. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per DRBG, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_DRBG)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo DRBG con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_drbg_operation"></a>_nx_crypto_method_drbg_operation

Eseguire l'operazione DRBG

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

Questa funzione esegue l'operazione DRBG. Il blocco di controllo DRBG deve essere stato inizializzato con _ *nx_crypto_method_drbg_init ()*. L'algoritmo DRBG da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* . Per impostazione predefinita, viene usato AES-128 per DRBG.

Quando si NX_CRYPTO_DRBG_OPTIONS_SET l'operazione, l'input punta alla struttura NX_CRYPTO_DRBG_OPTIONS. Quando si NX_CRYPTO_DRBG_INSTANTIATE l'operazione, la chiave punta a nonce, i punti di input alla stringa di personalizzazione. Quando l'operazione viene NX_CRYPTO_DRBG_RESEED o NX_CRYPTO_DRBG_GENERATE, l'input punta a input aggiuntivo.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_DRBG_OPTIONS_SET*
  - *NX_CRYPTO_DRBG_INSTANTIATE*
  - *NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo di crittografia DRBG valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_drbg_init ().*
- **chiave** di Puntatore al parametro nonce per l'operazione di creazione dell'istanza. Questo campo non viene utilizzato per altre operazioni.
- **key_size_in_bits** Dimensioni del parametro nonce in bit. Questo campo non viene utilizzato per altre operazioni.
- **input** di Quando op è NX_CRYPTO_DRBG_OPTIONS_SET, questo campo fa riferimento alle opzioni di DRBG. Quando op è NX_CRYPTO_DRBG_INSTANTIATE, questo campo punta alla stringa di personalizzazione. Quando op è NX_CRYPTO_DRBG_RESEED o NX_CRYPTO_DRBG_GENERATE, questo campo punta a dati di input aggiuntivi.
- **input_length_in_byte** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per DRBG.
- **output** di Quando op è NX_CRYPTO_DRBG_GENERATE, questo campo fa riferimento all'area di memoria per il DRBG generato. In caso contrario, questo campo non viene utilizzato.
- **output_length_in_byte** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo DRBG utilizzato nel *_nx_crypto_method_drbg_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per DRBG, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_DRBG)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione DRBG.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo DRBG non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_drbg_cleanup"></a>_nx_crypto_method_drbg_cleanup

Pulire il blocco di controllo DRBG.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_drbg_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo DRBG dopo aver determinato che questa sessione DRBG non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo DRBG utilizzato nel *_nx_crypto_method_drbg_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione DRBG.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_ecdh_init"></a>_nx_crypto_method_ecdh_init

Inizializza il blocco di controllo Crypto ECDH

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

Questa funzione Inizializza il blocco di controllo ECDH con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo ECDH, l'operazione ECDH successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo ECDH, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo ECDH avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo ECDH abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo Crypto ECDH valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_ecdh*
- **chiave** di Questo campo non viene utilizzato per ECDH.
- **key_size_in_bits** Questo campo non viene utilizzato per ECDH.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo ECDH. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per ECDH, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDH)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo ECDH con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_ecdh_operation"></a>_nx_crypto_method_ecdh_operation

Eseguire l'operazione ECDH

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

Questa funzione esegue l'operazione ECDH. Il blocco di controllo ECDH deve essere stato inizializzato con _ *nx_crypto_method_ecdh_init ()*. L'algoritmo ECDH da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Quando si NX_CRYPTO_EC_CURVE_SET l'operazione, l'input punta al metodo di crittografia a curva ellittica. Quando si NX_CRYPTO_EC_KEY_PAIR_GENERATE l'operazione, l'output punta alla struttura NX_CRYPTO_EXTENDED_OUTPUT e la coppia di chiavi viene copiata in nx_crypto_extended_output_data. Quando si NX_CRYPTO_DH_SETUP l'operazione, la chiave pubblica viene restituita nx_crypto_extended_output_data. Quando si NX_CRYPTO_DH_KEY_PAIR_IMPORT l'operazione, i punti di input alla chiave pubblica e ai punti chiave alla chiave privata. Quando si NX_CRYPTO_DH_PRIVATE_KEY_EXPORT l'operazione, la chiave privata viene copiata nx_crypto_extended_output_data. Quando si NX_CRYPTO_DH_CALCULATE l'operazione, i punti di input alla chiave pubblica remota e al segreto condiviso vengono copiati in nx_crypto_extended_output_data.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_EC_CURVE_SET*
  - *NX_CRYPTO_DH_SETUP*
  - *NX_CRYPTO_DH_CALCULATE*
  - *NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*
  - *NX_CRYPTO_DH_KEY_PAIR_GENERATE*
  - *NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo di crittografia ECDH valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_ecdh_init ().*
- **chiave** di Quando op è NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo punta alla chiave privata. In caso contrario, questo campo non viene utilizzato per ECDH.
- **key_size_in_bits** Dimensione della chiave in bit.
- **input** di Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo fa riferimento al metodo Crypto a curva ellittica. Quando op è NX_CRYPTO_DH_SETUP, questo campo non viene utilizzato. Quando op è NX_CRYPTO_DH_CALCULATE, questo campo punta a un buffer contenente dati di input di testo. Quando op è NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo punta alla chiave pubblica.
- **input_length_in_byte** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per ECDH.
- **output** di Quando op è NX_CRYPTO_EC_CURVE_SET o NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo non viene utilizzato. Quando op è NX_CRYPTO_DH_SETUP, questo campo fa riferimento all'area di memoria per la chiave pubblica ECDH generata. Quando op è NX_CRYPTO_DH_CALCULATE, questo campo fa riferimento all'area di memoria per il segreto condiviso ECDH generato.
- **output_length_in_byte** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo ECDH utilizzato nel *_nx_crypto_method_ecdh_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per ECDH, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDH)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione ECDH.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo ECDH non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_ecdh_cleanup"></a>_nx_crypto_method_ecdh_cleanup

Pulire il blocco di controllo ECDH.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdh_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo ECDH dopo aver determinato che questa sessione ECDH non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo ECDH utilizzato nel *_nx_crypto_method_ecdh_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione ECDH.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_ecdsa_init"></a>_nx_crypto_method_ecdsa_init

Inizializza il blocco di controllo Crypto ECDSA

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

Questa funzione Inizializza il blocco di controllo ECDSA con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo ECDSA, l'operazione ECDSA successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo ECDSA, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo ECDSA avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo ECDSA abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo Crypto ECDSA valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_ecdsa*
- **chiave** di Questo campo non viene utilizzato per ECDSA.
- **key_size_in_bits** Questo campo non viene utilizzato per ECDSA.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo ECDSA. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per ECDSA, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDSA)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo ECDSA con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_ecdsa_operation"></a>_nx_crypto_method_ecdsa_operation

Eseguire l'operazione ECDSA

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

Questa funzione esegue l'operazione ECDSA. Il blocco di controllo ECDSA deve essere stato inizializzato con _ *nx_crypto_method_ecdsa_init ()*. L'algoritmo ECDSA da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Quando si NX_CRYPTO_EC_CURVE_SET l'operazione, l'input punta al metodo di crittografia a curva ellittica. Quando si NX_CRYPTO_EC_KEY_PAIR_GENERATE l'operazione, l'output punta alla struttura NX_CRYPTO_EXTENDED_OUTPUT e la coppia di chiavi viene copiata in nx_crypto_extended_output_data.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_EC_CURVE_SET*
  - *NX_CRYPTO_AUTHENTICATE*
  - *NX_CRYPTO_VERIFY*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo di crittografia ECDSA valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_ecdsa_init ().*
- **chiave** di Punta alla chiave quando op è NX_CRYPTO_VERIFY. Non sono previste restrizioni per il buffer di chiave. Questo campo non viene usato per altri valori di op.
- **key_size_in_bits** Dimensione della chiave in bit.
- **input** di Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo fa riferimento al metodo Crypto a curva ellittica. In caso contrario, questo campo punta a un buffer che contiene dati di testo di input.
- **input_length_in_byte** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per ECDSA.
- **output** di Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo non viene utilizzato. Quando op è NX_CRYPTO_AUTHENTICATE, questo campo fa riferimento all'area di memoria per la firma ECDSA generata. Quando op è NX_CRYPTO_VERIFY, questo campo fa riferimento all'area di memoria per la firma ECDSA verificata.
- **output_length_in_byte** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo ECDSA utilizzato nel *_nx_crypto_method_ecdsa_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per ECDSA, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDSA)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione ECDsa.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo ECDSA non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_ecdsa_cleanup"></a>_nx_crypto_method_ecdsa_cleanup

Pulire il blocco di controllo ECDSA.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_ecdsa_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo ECDSA dopo aver determinato che questa sessione ECDSA non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo ECDSA utilizzato nel *_nx_crypto_method_ecdsa_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione ECDsa.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_hmac_md5_init"></a>_nx_crypto_method_hmac_md5_init

Inizializza il blocco di controllo crittografico HMAC MD5

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

Questa funzione Inizializza il blocco di controllo HMAC MD5 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo HMAC MD5, l'operazione HMAC MD5 successiva dovrà utilizzare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC MD5, ognuno di essi rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC MD5 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo HMAC MD5 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC MD5 valido.
Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_md5*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC MD5. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo HMAC MD5 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_md5_operation"></a>_nx_crypto_method_hmac_md5_operation

Eseguire un'operazione hash MD5 HMAC.

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

Questa funzione esegue l'operazione hash MD5 HMAC. Il blocco di controllo HMAC MD5 deve essere stato inizializzato con _ *nx_crypto_method_hmac_md5_init ()*. L'algoritmo MD5 HMAC da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 16 byte.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo HMAC MD5.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo crittografico HMAC MD5 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_hmac_md5_init ().*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per HMAC MD5.
- **iv_size** Questo campo non viene utilizzato per HMAC MD5.
- **output_buffer** Puntatore all'area di memoria per l'hash MD5 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC MD5 utilizzato nel *_nx_crypto_method_hmac_md5_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC MD5.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0X20004) non è stato specificato un algoritmo MD5 HMAC non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

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

Questa funzione Inizializza il blocco di controllo HMAC SHA1 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo HMAC SHA1, l'operazione HMAC SHA1 successiva dovrà utilizzare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC SHA1, ognuno di essi rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC SHA1 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo HMAC SHA1 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_sha1*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA1. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco SHA1control HMAC con la chiave e la dimensione della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_sha1_operation"></a>_nx_crypto_method_hmac_sha1_operation

Esegui operazione hash SHA1 HMAC

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

Questa funzione esegue l'operazione hash SHA1 HMAC. Il blocco di controllo HMAC SHA1 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha1_init ()*. L'algoritmo HMAC SHA1 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 20 byte.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo crittografico HMAC SHA1 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha1_init ().*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per HMAC SHA1.
- **iv_size** Questo campo non viene utilizzato per HMAC SHA1.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA1 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA1 utilizzato nel *_nx_crypto_method_hmac_sha1_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC SHA1.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo HMAC SHA1 non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_hmac_sha1_cleanup"></a>_nx_crypto_method_hmac_sha1_cleanup

Pulire il blocco di controllo HMAC SHA1.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA1 dopo aver determinato che questa sessione HMAC SHA1 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA1 utilizzato nel *_nx_crypto_method_hmac_sha1_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione HMAC SHA1.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

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

Questa funzione Inizializza il blocco di controllo HMAC SHA256 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo HMAC SHA256, l'operazione HMAC SHA256 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC SHA256, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC SH256 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo HMAC SHA256 abbandona la sessione corrente e ne crea una nuova con una nuova chiave.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC SHA256 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_sha224*
  - *crypto_method_hmac_sha256*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA256. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYTPO_SHA256_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo HMAC SHA256 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_sha256_operation"></a>_nx_crypto_method_hmac_sha256_operation

Esegui operazione hash SHA256 HMAC

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

Questa funzione esegue l'operazione hash SHA256 HMAC. Il blocco di controllo HMAC SHA256 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha256_init ()*. L'algoritmo SHA256 HMAC da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 32 byte per SHA256 o di 28 byte per SHA224.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo crittografico HMAC SHA256 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha256_init ().*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per SHA256 HMAC.
- **iv_size** Questo campo non viene utilizzato per SHA256 HMAC.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA256 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA256 usato nella *_nx_crypto_method_hmac_sha256_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA256_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC SHA256.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA256 HMAC non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_hmac_sha256_cleanup"></a>_nx_crypto_method_hmac_sha256_cleanup

Pulire il blocco di controllo HMAC SHA256.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA256 dopo aver determinato che questa sessione SHA256 HMAC non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA256 usato nella *_nx_crypto_method_hmac_sha256_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione HMAC SHA256.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

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

Questa funzione Inizializza il blocco di controllo HMAC SHA512 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo HMAC SHA512, l'operazione HMAC SHA512 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo HMAC SHA512, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo HMAC SH512 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo HMAC SHA512 abbandona la sessione corrente e ne crea una nuova con una nuova chiave.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC SHA512 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_hmac_sha384*
  - *crypto_method_hmac_sha512*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA512. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512_HMAC)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo HMAC SHA512 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_hmac_sha512_operation"></a>_nx_crypto_method_hmac_sha512_operation

Esegui operazione hash SHA512 HMAC

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

Questa funzione esegue l'operazione hash SHA512 HMAC. Il blocco di controllo HMAC SHA512 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha512_init ()*. L'algoritmo SHA512 HMAC da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 64 byte per SHA512 o di 48 byte per SHA384.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo crittografico HMAC SHA512 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha512_init ().*
- **chiave** di Punta alla chiave. Non sono previste restrizioni per il buffer di chiave.
- **key_size_in_bits** Dimensione della chiave in bit.
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per SHA512 HMAC.
- **iv_size** Questo campo non viene utilizzato per SHA512 HMAC.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA512 HMAC generato.
- **output_buffer_size** Dimensioni del buffer di output in byte.
- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA512 usato nella *_nx_crypto_method_hmac_sha512_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per HMAC SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512_HMAC)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC SHA512.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA512 HMAC non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_hmac_sha512_cleanup"></a>_nx_crypto_method_hmac_sha512_cleanup

Pulire il blocco di controllo HMAC SHA512.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_hmac_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA512 dopo aver determinato che questa sessione SHA512 HMAC non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo HMAC SHA512 usato nella *_nx_crypto_method_hmac_sha512_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione HMAC SHA512.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

### <a name="example"></a>Esempio 

## <a name="_nx_crypto_method_md5_init"></a>_nx_crypto_method_md5_init

Inizializza il blocco di controllo Crypto MD5

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

Questa funzione Inizializza il blocco di controllo MD5 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo MD5, l'operazione MD5 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo MD5, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo MD5 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo MD5 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo di crittografia MD5 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_md5*
- **chiave** di Questo campo non viene usato per MD5.
- **key_size_in_bits** Questo campo non viene usato per MD5
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo MD5. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo MD5 con la chiave e la dimensione della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

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

Questa funzione esegue l'operazione hash MD5. Il blocco di controllo MD5 deve essere stato inizializzato con _ *nx_crypto_method_md5_init ()*. L'algoritmo MD5 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 16 byte.

Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo MD5.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo di crittografia MD5 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_md5_init ().*
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene usato per MD5.
- **iv_size** Questo campo non viene usato per MD5.
- **output_buffer** Puntatore all'area di memoria per l'hash MD5 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per MD5 la dimensione del buffer deve essere di 16 byte.
- **crypto_metadata** Puntatore al blocco di controllo MD5 utilizzato nel *_nx_crypto_method_md5_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione MD5.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) algoritmo MD5 non valido specificato.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_md5_cleanup"></a>_nx_crypto_method_md5_cleanup

Pulire il blocco di controllo MD5.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_md5_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo MD5 dopo aver determinato che questa sessione MD5 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo MD5 utilizzato nel *_nx_crypto_method_md5_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione MD5.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_sha1_init"></a>_nx_crypto_method_sha1_init

Inizializza il blocco di controllo Crypto SHA1

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

Questa funzione Inizializza il blocco di controllo SHA1 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo SHA1, l'operazione SHA1 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo SHA1, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo SHA1 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo SHA1 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo crittografico SHA1 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_sha1*
- **chiave** di Questo campo non viene usato per SHA1.
- **key_size_in_bits** Questo campo non viene usato per SHA1
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA1. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco SHA1control con la chiave e la dimensione della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_sha1_operation"></a>_nx_crypto_method_sha1_operation

Esegui operazione hash SHA1

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

Questa funzione esegue l'operazione hash SHA1. Il blocco di controllo SHA1 deve essere stato inizializzato con _ *nx_crypto_method_sha1_init ()*. L'algoritmo SHA1 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 20 byte.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo crittografico SHA1 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_sha1_init ().*
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene usato per SHA1.
- **iv_size** Questo campo non viene usato per SHA1.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA1 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per SHA1 la dimensione del buffer deve essere di 20 byte.
- **crypto_metadata** Puntatore al blocco di controllo SHA1 utilizzato nel *_nx_crypto_method_sha1_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione SHA1.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) algoritmo SHA1 non valido specificato.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

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

- **crypto_metadata** Puntatore al blocco di controllo SHA1 utilizzato nel *_nx_crypto_method_sha1_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione SHA1.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_sha256_init"></a>_nx_crypto_method_sha256_init

Inizializza il blocco di controllo Crypto SHA256

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

Questa funzione Inizializza il blocco di controllo SHA256 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo SHA256, l'operazione SHA256 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo SHA256, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo SHA256 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo SHA256 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo Crypto SHA256 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_sha256*
  - *crypto_method_sha224*
- **chiave** di Questo campo non viene utilizzato per SHA256.
- **key_size_in_bits** Questo campo non viene utilizzato per SHA256
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA256. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA256)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo SHA256 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_sha256_operation"></a>_nx_crypto_method_sha256_operation

Eseguire l'operazione hash SHA256

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

Questa funzione esegue l'operazione hash SHA256. Il blocco di controllo SHA256 deve essere stato inizializzato con _ ***nx_crypto_method_sha256_init ()***. L'algoritmo SHA256 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 32 byte per SHA256 o di 28 byte per SHA224.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo di crittografia SHA256 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_sha256_init ().*
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per SHA256.
- **iv_size** Questo campo non viene utilizzato per SHA256.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA256 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per SHA256, le dimensioni del buffer devono essere pari a 32 byte. Per SHA224, la dimensione del buffer deve essere di 28 byte.
- **crypto_metadata** Puntatore al blocco di controllo SHA2 utilizzato nel *_nx_crypto_method_sha2_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA256)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione SHA256.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA256 non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_sha256_cleanup"></a>_nx_crypto_method_sha256_cleanup

Pulire il blocco di controllo SHA256.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo SHA256 dopo aver determinato che questa sessione SHA256 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo SHA256 utilizzato nel *_nx_crypto_method_sha256_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione SHA256.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.

## <a name="_nx_crypto_method_sha512_init"></a>_nx_crypto_method_sha512_init

Inizializza il blocco di controllo Crypto SHA512

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

Questa funzione Inizializza il blocco di controllo SHA512 con la stringa di chiave specificata. Una volta inizializzato il blocco di controllo SHA512, l'operazione SHA512 successiva dovrà usare lo stesso blocco di controllo.

L'applicazione può creare più blocchi di controllo SHA512, ognuno rappresenta una sessione. L'inizializzazione del blocco di controllo SHA512 avvia una nuova sessione di calcolo hash. La reinizializzazione del blocco di controllo SHA512 abbandona la sessione corrente e ne crea una nuova.

### <a name="parameters"></a>Parametri

- **Metodo** Puntatore a un blocco di controllo del metodo Crypto SHA512 valido. Sono disponibili i metodi di crittografia predefiniti seguenti:
  - *crypto_method_sha512*
  - *crypto_method_sha384*
- **chiave** di Questo campo non viene utilizzato per SHA512.
- **key_size_in_bits** Questo campo non viene utilizzato per SHA512
- **Gestisci** Questo servizio restituisce un handle per il chiamante. L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione. L'applicazione deve passare NULL per l'handle.
- **crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA512. L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512)*

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo SHA512 con la chiave e le dimensioni della chiave.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.

## <a name="_nx_crypto_method_sha512_operation"></a>_nx_crypto_method_sha512_operation

Eseguire l'operazione hash SHA512

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

Questa funzione esegue l'operazione hash SHA512. Il blocco di controllo SHA512 deve essere stato inizializzato con _ *nx_crypto_method_sha512_init ()*. L'algoritmo SHA512 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .

Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 64 byte per SHA512 o di 48 byte per SHA384.

### <a name="parameters"></a>Parametri

- **operazione operativa** Tipo di operazione da eseguire. Operazione valida:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **Metodo** Puntatore al metodo di crittografia SHA512 valido. Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_sha512_init ().*
- **input_data** Punta a un buffer che contiene dati di testo di input. Non sono previste restrizioni per il buffer di input.
- **input_data_size** Dimensioni in byte dei dati di input.
- **iv_ptr** Questo campo non viene utilizzato per SHA512.
- **iv_size** Questo campo non viene utilizzato per SHA512.
- **output_buffer** Puntatore all'area di memoria per l'hash SHA512 generato.
- **output_buffer_size** Dimensioni del buffer di output in byte. Per SHA512, le dimensioni del buffer devono essere pari a 64 byte. Per SHA384, le dimensioni del buffer devono essere pari a 48 byte.
- **crypto_metadata** Puntatore al blocco di controllo SHA512 utilizzato nel *_nx_crypto_method_sha512_init ()*.
- **crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata. Per SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512)*
- **packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.
- **nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library. Qualsiasi valore passato viene ignorato automaticamente.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione SHA512.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.
- **NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA512 non valido.
- Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.

## <a name="_nx_crypto_method_sha512_cleanup"></a>_nx_crypto_method_sha512_cleanup

Pulire il blocco di controllo SHA512.

### <a name="prototype"></a>Prototipo

```c
UINT _nx_crypto_method_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Descrizione

L'applicazione chiama questa funzione per pulire il blocco di controllo SHA512 dopo aver determinato che questa sessione SHA512 non è più necessaria.

### <a name="parameters"></a>Parametri

- **crypto_metadata** Puntatore al blocco di controllo SHA512 utilizzato nel *_nx_crypto_method_sha512_init ()*.

### <a name="return-values"></a>Valori restituiti

- **NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione SHA512.
- **NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.