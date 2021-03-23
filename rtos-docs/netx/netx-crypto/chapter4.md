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
# <a name="chapter-4---azure-rtos-netx-crypto-api-description"></a><span data-ttu-id="aeebb-103">Capitolo 4-Descrizione dell'API Crypto NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="aeebb-103">Chapter 4 - Azure RTOS NetX Crypto API description</span></span>

## <a name="nx_crypto_initialize"></a><span data-ttu-id="aeebb-104">nx_crypto_initialize</span><span class="sxs-lookup"><span data-stu-id="aeebb-104">nx_crypto_initialize</span></span>

<span data-ttu-id="aeebb-105">Inizializza la libreria protetta NetX</span><span class="sxs-lookup"><span data-stu-id="aeebb-105">Initializes the NetX Secure Library</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-106">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-106">Prototype</span></span>

```c
UINT nx_crypto_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="aeebb-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-107">Description</span></span>

<span data-ttu-id="aeebb-108">Questa funzione Inizializza il modulo libreria di crittografia NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="aeebb-108">This function initializes the Azure RTOS NetX Crypto library module.</span></span> <span data-ttu-id="aeebb-109">Prima di utilizzare qualsiasi altra funzione di crittografia, l'applicazione deve chiamare questa funzione per eseguire l'inizializzazione e per convalidare l'integrità della libreria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-109">Before using any of the other cryptographic functions, the application must call this function to perform initialization and to validate the integrity of the library.</span></span> <span data-ttu-id="aeebb-110">La mancata chiamata di questa funzione prima di usare altri servizi di crittografia NetX comporterà la restituzione di errori.</span><span class="sxs-lookup"><span data-stu-id="aeebb-110">Failure to call this function before using other NetX Crypto services will result in errors being returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-111">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-111">Parameters</span></span>

- <span data-ttu-id="aeebb-112">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="aeebb-112">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-113">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-113">Return Values</span></span>

- <span data-ttu-id="aeebb-114">**NX_CRYPTO_SUCCESS** (0x00) la libreria di crittografia NETX inizializzata è riuscita.</span><span class="sxs-lookup"><span data-stu-id="aeebb-114">**NX_CRYPTO_SUCCESS** (0x00) Successful initialized NetX Crypto library.</span></span> <span data-ttu-id="aeebb-115">Le funzioni della libreria sono ora pronte e possono essere utilizzate.</span><span class="sxs-lookup"><span data-stu-id="aeebb-115">The library functions are now ready, and can be used.</span></span>
- <span data-ttu-id="aeebb-116">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) non è possibile inizializzare la libreria di crittografia oppure il controllo di integrità non riesce.</span><span class="sxs-lookup"><span data-stu-id="aeebb-116">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library fails to initialize, or fails the integrity check.</span></span> <span data-ttu-id="aeebb-117">L'applicazione non può usare questa libreria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-117">Application cannot use this library.</span></span>

### <a name="example"></a><span data-ttu-id="aeebb-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="aeebb-118">Example</span></span>

<span data-ttu-id="aeebb-119">TODO</span><span class="sxs-lookup"><span data-stu-id="aeebb-119">TODO</span></span>

## <a name="nx_crypto_module_state_get"></a><span data-ttu-id="aeebb-120">nx_crypto_module_state_get</span><span class="sxs-lookup"><span data-stu-id="aeebb-120">nx_crypto_module_state_get</span></span>

<span data-ttu-id="aeebb-121">Recuperare lo stato corrente del modulo abilitato per FIPS</span><span class="sxs-lookup"><span data-stu-id="aeebb-121">Retrieve the current status of the FIPS-enabled module</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-122">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-122">Prototype</span></span>

```c
UINT nx_crypto_module_state_get(VOID);
```

### <a name="description"></a><span data-ttu-id="aeebb-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-123">Description</span></span>

<span data-ttu-id="aeebb-124">Questo servizio è disponibile solo nella libreria di compilazione FIPS.</span><span class="sxs-lookup"><span data-stu-id="aeebb-124">This service is only available in the FIPS build library.</span></span> <span data-ttu-id="aeebb-125">Restituisce lo stato corrente della libreria di crittografia NetX.</span><span class="sxs-lookup"><span data-stu-id="aeebb-125">It returns the state of the current state of the NetX Crypto library.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-126">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-126">Parameters</span></span>

- <span data-ttu-id="aeebb-127">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="aeebb-127">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-128">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-128">Return Values</span></span>

- <span data-ttu-id="aeebb-129">**Flag di stato:**</span><span class="sxs-lookup"><span data-stu-id="aeebb-129">**Status Flag:**</span></span>
  - <span data-ttu-id="aeebb-130">NX_CRYPTO_LIBRARY_STATE_UNINITIALIZED 0x00000001</span><span class="sxs-lookup"><span data-stu-id="aeebb-130">NX_CRYPTO_LIBRARY_STATE_UNINITIALIZED 0x00000001</span></span>
  - <span data-ttu-id="aeebb-131">NX_CRYPTO_LIBRARY_STATE_POST_IN_PROGRESS 0x00000002</span><span class="sxs-lookup"><span data-stu-id="aeebb-131">NX_CRYPTO_LIBRARY_STATE_POST_IN_PROGRESS 0x00000002</span></span>
  - <span data-ttu-id="aeebb-132">NX_CRYPTO_LIBRARY_STATE_INTEGRITY_TEST_FAILED 0x00000004</span><span class="sxs-lookup"><span data-stu-id="aeebb-132">NX_CRYPTO_LIBRARY_STATE_INTEGRITY_TEST_FAILED 0x00000004</span></span>
  - <span data-ttu-id="aeebb-133">NX_CRYPTO_LIBRARY_STATE_FUNCTIONAL_TEST_FAILED 0x00000008</span><span class="sxs-lookup"><span data-stu-id="aeebb-133">NX_CRYPTO_LIBRARY_STATE_FUNCTIONAL_TEST_FAILED 0x00000008</span></span>
  - <span data-ttu-id="aeebb-134">NX_CRYPTO_LIBRARY_STATE_OPERATIONAL 0x80000000</span><span class="sxs-lookup"><span data-stu-id="aeebb-134">NX_CRYPTO_LIBRARY_STATE_OPERATIONAL 0x80000000</span></span>
- <span data-ttu-id="aeebb-135">**Tutti gli altri valori non sono validi.**</span><span class="sxs-lookup"><span data-stu-id="aeebb-135">**All other values are invalid.**</span></span>

### <a name="example"></a><span data-ttu-id="aeebb-136">Esempio</span><span class="sxs-lookup"><span data-stu-id="aeebb-136">Example</span></span>

<span data-ttu-id="aeebb-137">TODO</span><span class="sxs-lookup"><span data-stu-id="aeebb-137">TODO</span></span>

## <a name="_nx_crypto_method_aes_init"></a><span data-ttu-id="aeebb-138">_nx_crypto_method_aes_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-138">_nx_crypto_method_aes_init</span></span>

<span data-ttu-id="aeebb-139">Inizializza il blocco di controllo Crypto AES</span><span class="sxs-lookup"><span data-stu-id="aeebb-139">Initializes the AES crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-140">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-140">Prototype</span></span>

```c
UINT _nx_crypto_method_aes_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-141">Description</span></span>

<span data-ttu-id="aeebb-142">Questa funzione Inizializza il blocco di controllo AES con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-142">This function initializes the AES control block with the given key string.</span></span> <span data-ttu-id="aeebb-143">Una volta inizializzato il blocco di controllo AES, l'operazione AES successiva utilizzerà la stessa chiave e la stessa dimensione della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-143">Once the AES control block is initialized, subsequent AES operation will be using the same key and key size.</span></span>

<span data-ttu-id="aeebb-144">L'applicazione può creare più blocchi di controllo AES, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-144">Application may create multiple AES control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-145">Una chiave viene assegnata a un blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-145">A key is assigned to a control block.</span></span> <span data-ttu-id="aeebb-146">L'operazione di crittografia o decrittografia successiva può fare riferimento allo stesso blocco di controllo AES senza la necessità di inizializzare nuovamente il blocco di controllo AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-146">Subsequent encryption or decryption operation can reference to the same AES control block without the need to re-initialize the AES control block.</span></span> <span data-ttu-id="aeebb-147">Se la chiave per la sessione viene modificata, l'applicazione deve inizializzare nuovamente il blocco di controllo AES con la chiave aggiornata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-147">If the key for the session is changed, application needs to re-initialize AES control block with the updated key.</span></span>

<span data-ttu-id="aeebb-148">La chiamata a _ *nx_crypto_method_aes_init ()* consente di aggiornare automaticamente una chiave e una dimensione della chiave configurate in precedenza alla nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-148">Calling _ *nx_crypto_method_aes_init()* automatically updates a previously configured key and key size to the new key.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-149">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-149">Parameters</span></span>

- <span data-ttu-id="aeebb-150">**Metodo** Puntatore a un blocco di controllo del metodo di crittografia AES valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-150">**method** Pointer to a valid AES crypto method control block.</span></span> <span data-ttu-id="aeebb-151">Sono disponibili i metodi di crittografia AES predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-151">The following pre-defined AES crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-152">*crypto_method_aes_cbc_128*</span><span class="sxs-lookup"><span data-stu-id="aeebb-152">*crypto_method_aes_cbc_128*</span></span>
  - <span data-ttu-id="aeebb-153">*crypto_method_aes_cbc_192*</span><span class="sxs-lookup"><span data-stu-id="aeebb-153">*crypto_method_aes_cbc_192*</span></span>
  - <span data-ttu-id="aeebb-154">*crypto_method_aes_cbc_256*</span><span class="sxs-lookup"><span data-stu-id="aeebb-154">*crypto_method_aes_cbc_256*</span></span>
  - <span data-ttu-id="aeebb-155">*crypto_method_aes_ctr_128*</span><span class="sxs-lookup"><span data-stu-id="aeebb-155">*crypto_method_aes_ctr_128*</span></span>
  - <span data-ttu-id="aeebb-156">*crypto_method_aes_ctr_192*</span><span class="sxs-lookup"><span data-stu-id="aeebb-156">*crypto_method_aes_ctr_192*</span></span>
  - <span data-ttu-id="aeebb-157">*crypto_method_aes_ctr_256*</span><span class="sxs-lookup"><span data-stu-id="aeebb-157">*crypto_method_aes_ctr_256*</span></span>
  - <span data-ttu-id="aeebb-158">*crypto_method_aes_xcbc_128*</span><span class="sxs-lookup"><span data-stu-id="aeebb-158">*crypto_method_aes_xcbc_128*</span></span>
  - <span data-ttu-id="aeebb-159">*crypto_method_aes_ccm_8_128*</span><span class="sxs-lookup"><span data-stu-id="aeebb-159">*crypto_method_aes_ccm_8_128*</span></span>
- <span data-ttu-id="aeebb-160">**chiave** di Punta a un buffer contenente la chiave AES</span><span class="sxs-lookup"><span data-stu-id="aeebb-160">**key** Points to a buffer containing the AES key</span></span>
- <span data-ttu-id="aeebb-161">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-161">**key_size_in_bits** Size of the key, in bits.</span></span> <span data-ttu-id="aeebb-162">I valori validi sono:</span><span class="sxs-lookup"><span data-stu-id="aeebb-162">Valid values are:</span></span>
  - <span data-ttu-id="aeebb-163">*NX_CRYPTO_AES_KEY_SIZE_128_BITS*</span><span class="sxs-lookup"><span data-stu-id="aeebb-163">*NX_CRYPTO_AES_KEY_SIZE_128_BITS*</span></span>
  - <span data-ttu-id="aeebb-164">*NX_CRYPTO_AES_KEY_SIZE_192_BITS*</span><span class="sxs-lookup"><span data-stu-id="aeebb-164">*NX_CRYPTO_AES_KEY_SIZE_192_BITS*</span></span>
  - <span data-ttu-id="aeebb-165">*NX_CRYPTO_AES_KEY_SIZE_256_BITS*</span><span class="sxs-lookup"><span data-stu-id="aeebb-165">*NX_CRYPTO_AES_KEY_SIZE_256_BITS*</span></span>
  - <span data-ttu-id="aeebb-166">**Tutti gli altri valori non sono validi.**</span><span class="sxs-lookup"><span data-stu-id="aeebb-166">**All other values are invalid.**</span></span>
- <span data-ttu-id="aeebb-167">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-167">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-168">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-168">The handle is implementation-dependent, and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-169">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-169">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-170">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-170">**crypto_metadata** Pointer to a valid memory space for the AES control block.</span></span> <span data-ttu-id="aeebb-171">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-171">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-172">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-172">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-173">Per AES, le dimensioni dei metadati devono essere *sizeof (NX_AES)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-173">For AES, the metadata size must be *sizeof(NX_AES)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-174">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-174">Return Values</span></span>

- <span data-ttu-id="aeebb-175">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo AES con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-175">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the AES control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-176">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-176">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-177">**NX_PTR_ERROR (0x07)** Puntatore alla chiave non valido o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-177">**NX_PTR_ERROR (0x07)** Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-178">Le dimensioni della chiave **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) non sono valide per AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-178">**NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) Key size is not a valid for AES.</span></span>

## <a name="_nx_crypto_method_aes_operation"></a><span data-ttu-id="aeebb-179">_nx_crypto_method_aes_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-179">_nx_crypto_method_aes_operation</span></span>

<span data-ttu-id="aeebb-180">Eseguire un'operazione AES (crittografia o decrittografia).</span><span class="sxs-lookup"><span data-stu-id="aeebb-180">Perform an AES operation (encryption or decryption).</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-181">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-181">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-182">Description</span></span>

<span data-ttu-id="aeebb-183">Questa funzione esegue l'operazione di crittografia o decrittografia AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-183">This function performs AES encryption or decryption operation.</span></span> <span data-ttu-id="aeebb-184">Il blocco di controllo AES deve essere stato inizializzato con _ *nx_crypto_method_aes_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-184">The AES control block must have been initialized with _ *nx_crypto_method_aes_init()*.</span></span> <span data-ttu-id="aeebb-185">L'algoritmo AES da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-185">The AES algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-186">La dimensione del buffer di input deve essere un multiplo di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-186">The input buffer size must be a multiple of 16 bytes.</span></span> <span data-ttu-id="aeebb-187">Le dimensioni dei dati decrittografati hanno le stesse dimensioni della dimensione dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-187">The size of the decrypted data is the same size of the input data size.</span></span> <span data-ttu-id="aeebb-188">Se i dati crittografati sono stati riempiti per ottenere un multiplo pari delle dimensioni del blocco AES, la spaziatura interna verrà inclusa nel buffer di output e deve essere gestita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-188">If the encrypted data was padded to achieve an even multiple of the AES block size, the padding will be included in the output buffer and must be handled by the application.</span></span>

<span data-ttu-id="aeebb-189">Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-189">This operation does not keep state information, and does not alter the key material in the AES control block.</span></span>

<span data-ttu-id="aeebb-190">Quando l'op è NX_CRYPTO_SET_ADDITIONAL_DATA e algoritmo è AES-CCM8, l'input punta a dati aggiuntivi e input_length_in_byte è la lunghezza dei dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="aeebb-190">When the op is NX_CRYPTO_SET_ADDITIONAL_DATA and algoritm is AES-CCM8, the input points to additional data and input_length_in_byte is the length of additional data.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-191">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-191">Parameters</span></span>

- <span data-ttu-id="aeebb-192">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-192">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-193">Opertions validi sono:</span><span class="sxs-lookup"><span data-stu-id="aeebb-193">Valid opertions are:</span></span>
  - <span data-ttu-id="aeebb-194">*NX_CRYPTO_ENCRYPT*</span><span class="sxs-lookup"><span data-stu-id="aeebb-194">*NX_CRYPTO_ENCRYPT*</span></span>
  - <span data-ttu-id="aeebb-195">*NX_CRYPTO_DECRYPT*</span><span class="sxs-lookup"><span data-stu-id="aeebb-195">*NX_CRYPTO_DECRYPT*</span></span>
  - <span data-ttu-id="aeebb-196">*NX_CRYPTO_AUTHENTICATE (solo AES-XCBC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-196">*NX_CRYPTO_AUTHENTICATE (AES-XCBC only)*</span></span>
  - <span data-ttu-id="aeebb-197">*NX_CRYPTO_SET_ADDITIONAL_DATA (solo AES-CCM8)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-197">*NX_CRYPTO_SET_ADDITIONAL_DATA (AES-CCM8 only)*</span></span>
- <span data-ttu-id="aeebb-198">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-198">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-199">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-199">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-200">**Metodo** Puntatore al metodo crittografico AES valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-200">**method** Pointer to the valid AES crypto method.</span></span> <span data-ttu-id="aeebb-201">Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_aes_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-201">The crypto method used here must be the same used in the *nx_crypto_method_aes_init().*</span></span>
- <span data-ttu-id="aeebb-202">**input_data** Punta a un buffer contenente dati di testo crittografati.</span><span class="sxs-lookup"><span data-stu-id="aeebb-202">**input_data** Points to a buffer containing encrypted text data.</span></span> <span data-ttu-id="aeebb-203">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-203">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-204">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-204">**input_data_size** Size of the input data, in bytes.</span></span> <span data-ttu-id="aeebb-205">Le dimensioni dei dati di input devono essere un multiplo di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-205">The input data size must be a multiple of 16 bytes.</span></span>
- <span data-ttu-id="aeebb-206">**iv_ptr** Puntatore al vettore iniziale.</span><span class="sxs-lookup"><span data-stu-id="aeebb-206">**iv_ptr** Pointer to the Initial Vector.</span></span> <span data-ttu-id="aeebb-207">Non esistono restrizioni sul buffer IV.</span><span class="sxs-lookup"><span data-stu-id="aeebb-207">There are no restrictions on the IV buffer.</span></span>
- <span data-ttu-id="aeebb-208">**iv_size** Dimensione del blocco del vettore iniziale, in byte questo campo deve essere 16.</span><span class="sxs-lookup"><span data-stu-id="aeebb-208">**iv_size** Size of the Initial Vector block, in bytes This field must be 16.</span></span>
- <span data-ttu-id="aeebb-209">**output_buffer** Puntatore all'area di memoria per AES per archiviare i dati di testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-209">**output_buffer** Pointer to the memory area for AES to store the clear text data.</span></span> <span data-ttu-id="aeebb-210">L'applicazione deve allocare spazio per il buffer di output.</span><span class="sxs-lookup"><span data-stu-id="aeebb-210">Application must allocate space for the output buffer.</span></span> <span data-ttu-id="aeebb-211">Il buffer di output può sovrapporsi al buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-211">Output buffer may overlap with input buffer.</span></span> <span data-ttu-id="aeebb-212">Il buffer di output può sovrapporsi al buffer di input se condivide lo stesso indirizzo iniziale.</span><span class="sxs-lookup"><span data-stu-id="aeebb-212">The output buffer may overlap with the input buffer if they share the same starting address.</span></span>
- <span data-ttu-id="aeebb-213">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-213">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="aeebb-214">La dimensione del buffer di output deve essere uguale almeno alla dimensione del buffer di input e la dimensione del buffer di output deve essere un multiplo di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-214">Output buffer size must be at least the same of the input buffer size, and the output buffer size must be a multiple of 16 bytes.</span></span>
- <span data-ttu-id="aeebb-215">**crypto_metadata** Puntatore al blocco di controllo AES utilizzato nel *_nx_crypto_method_aes_init () \* . \**</span><span class="sxs-lookup"><span data-stu-id="aeebb-215">**crypto_metadata** Pointer to the AES control block used in *_nx_crypto_method_aes_init()\*.\**</span></span>
- <span data-ttu-id="aeebb-216">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-216">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-217">Per AES, le dimensioni dei metadati devono essere *sizeof (NX_AES)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-217">For AES, the metadata size must *sizeof(NX_AES)*</span></span>
- <span data-ttu-id="aeebb-218">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-218">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-219">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-219">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-220">**nx_crypto_hw_process_callback** : questo campo non è usato nell'implementazione software di NETX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-220">**nx_crypto_hw_process_callback** - This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-221">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-221">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-222">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-222">Return Values</span></span>

- <span data-ttu-id="aeebb-223">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-223">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the AES operation.</span></span>
- <span data-ttu-id="aeebb-224">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-224">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-225">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-225">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-226">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) algoritmo AES non valido specificato \* \*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-226">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid AES algorithm being specified\*\*.</span></span>

## <a name="_nx_crypto_method_aes_cleanup"></a><span data-ttu-id="aeebb-227">_nx_crypto_method_aes_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-227">_nx_crypto_method_aes_cleanup</span></span>

<span data-ttu-id="aeebb-228">Pulire il blocco di controllo AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-228">Clean up the AES control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-229">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-229">Prototype</span></span>

```c
UINT _nx_crypto_method_aes_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-230">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-230">Description</span></span>

<span data-ttu-id="aeebb-231">L'applicazione chiama questa funzione per pulire il blocco di controllo AES dopo aver determinato che questa sessione AES non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-231">Application calls this function to clean up the AES control block after it determines this AES session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-232">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-232">Parameters</span></span>

- <span data-ttu-id="aeebb-233">**crypto_metadata** Puntatore al blocco di controllo AES utilizzato nel *_nx_crypto_method_aes_init () \* . \**</span><span class="sxs-lookup"><span data-stu-id="aeebb-233">**crypto_metadata** Pointer to the AES control block used in *_nx_crypto_method_aes_init()\*.\**</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-234">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-234">Return Values</span></span>

- <span data-ttu-id="aeebb-235">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione AES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-235">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the AES session.</span></span>
- <span data-ttu-id="aeebb-236">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-236">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_3des_init"></a><span data-ttu-id="aeebb-237">_nx_crypto_method_3des_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-237">_nx_crypto_method_3des_init</span></span>

<span data-ttu-id="aeebb-238">Inizializzare il blocco di controllo 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-238">Initialize the 3DES control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-239">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-239">Prototype</span></span>

```c
UINT _nx_crypto_method_3des_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-240">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-240">Description</span></span>

<span data-ttu-id="aeebb-241">Questa funzione Inizializza il blocco di controllo Triple DES (3DES) con le tre stringhe chiave specificate.</span><span class="sxs-lookup"><span data-stu-id="aeebb-241">This function initializes the Triple DES (3DES) control block with the given three key strings.</span></span> <span data-ttu-id="aeebb-242">Le stringhe di chiave devono essere di 8 byte ciascuna.</span><span class="sxs-lookup"><span data-stu-id="aeebb-242">The key strings must be 8 bytes each.</span></span> <span data-ttu-id="aeebb-243">Le tre chiavi DES devono essere concatenate nella memoria contigua del buffer a 24 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-243">The three DES keys must be concatenated into contiguous memory of 24-byte buffer.</span></span> <span data-ttu-id="aeebb-244">Per la compilazione conforme a FIPS, le tre chiavi devono essere diverse da ciascuna o la funzione restituirà l'errore NX_CRYPTO_INVALID_KEY.</span><span class="sxs-lookup"><span data-stu-id="aeebb-244">For FIPS-compliant build, the three keys must be different from each or the function will return the NX_CRYPTO_INVALID_KEY error.</span></span> <span data-ttu-id="aeebb-245">Una volta inizializzato il blocco di controllo 3DES, le operazioni 3DES successive utilizzeranno le stesse chiavi.</span><span class="sxs-lookup"><span data-stu-id="aeebb-245">Once the 3DES control block is initialized, subsequent 3DES operations will use the same keys.</span></span>

<span data-ttu-id="aeebb-246">Un'applicazione può creare più blocchi di controllo 3DES, ognuno di essi che rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-246">An application may create multiple 3DES control blocks, each representing a session.</span></span> <span data-ttu-id="aeebb-247">Una chiave viene assegnata a un blocco di controllo e le successive operazioni di crittografia o decrittografia possono fare riferimento allo stesso blocco di controllo senza che sia necessario eseguire di nuovo l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-247">A key is assigned to a control block and subsequent encryption or decryption operations can reference the same control block without needing to re-initialize.</span></span> <span data-ttu-id="aeebb-248">Se la chiave per una sessione viene modificata, l'applicazione dovrà inizializzare nuovamente il blocco di controllo con la chiave aggiornata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-248">If the key for a session is changed, the application will need to re-initialize the control block with the updated key.</span></span>

<span data-ttu-id="aeebb-249">La chiamata a _ *nx_crypto_method_3des_init ()* consente di aggiornare automaticamente una chiave configurata in precedenza alle nuove chiavi.</span><span class="sxs-lookup"><span data-stu-id="aeebb-249">Calling _ *nx_crypto_method_3des_init()* automatically updates a previously configured key to the new keys.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-250">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-250">Parameters</span></span>

- <span data-ttu-id="aeebb-251">**Metodo** Puntatore a un blocco di controllo del metodo crittografico 3DES valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-251">**method** Pointer to a valid 3DES crypto method control block.</span></span> <span data-ttu-id="aeebb-252">È disponibile il seguente metodo di crittografia 3DES predefinito: ***crypto_method_3des***</span><span class="sxs-lookup"><span data-stu-id="aeebb-252">The following pre-defined 3DES crypto method is available: ***crypto_method_3des***</span></span>
- <span data-ttu-id="aeebb-253">**chiave** di Punta a un buffer contenente il tre (3) tasto DES</span><span class="sxs-lookup"><span data-stu-id="aeebb-253">**key** Points to a buffer containing the three (3) DES key</span></span>
- <span data-ttu-id="aeebb-254">**key_size_in_bits** Deve essere 192 (3 chiavi, ogni 64 bit).</span><span class="sxs-lookup"><span data-stu-id="aeebb-254">**key_size_in_bits** Must be 192 (3 keys, each 64 bits).</span></span>
- <span data-ttu-id="aeebb-255">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-255">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-256">L'handle identifica il blocco di controllo 3DES inizializzato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-256">The handle identifies the 3DES control block being initialized.</span></span> <span data-ttu-id="aeebb-257">Le operazioni 3DES successive (crittografia, decrittografia e pulizia) utilizzano questo handle per accedere al blocco di controllo 3DES</span><span class="sxs-lookup"><span data-stu-id="aeebb-257">Subsequent 3DES operations (encryption, decryption, and cleanup) use this handle to access the 3DES control block</span></span>
- <span data-ttu-id="aeebb-258">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-258">**crypto_metadata** Pointer to a valid memory space for the 3DES control block.</span></span> <span data-ttu-id="aeebb-259">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-259">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-260">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-260">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-261">Per 3DES, le dimensioni dei metadati devono essere *sizeof (NX_3DES)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-261">For 3DES, the metadata size must be *sizeof(NX_3DES)*</span></span>

### <a name="return-value"></a><span data-ttu-id="aeebb-262">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="aeebb-262">Return Value</span></span>

- <span data-ttu-id="aeebb-263">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo 3DES con la chiave e la dimensione della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-263">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the 3DES control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-264">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-264">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-265">**NX_PTR_ERROR (0x07)** Puntatore alla chiave non valido o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-265">**NX_PTR_ERROR (0x07)** Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-266">Le dimensioni della chiave **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) non sono valide per 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-266">**NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) Key size is not a valid for 3DES.</span></span>

## <a name="_nx_crypto_method_3des_operation"></a><span data-ttu-id="aeebb-267">_nx_crypto_method_3des_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-267">_nx_crypto_method_3des_operation</span></span>

<span data-ttu-id="aeebb-268">Crittografare o decrittografare con 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-268">Encrypt or Decrypt with 3DES.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-269">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-269">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-270">Description</span></span>

<span data-ttu-id="aeebb-271">Questa funzione esegue l'operazione di crittografia o decrittografia 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-271">This function performs 3DES encryption or decryption operation.</span></span> <span data-ttu-id="aeebb-272">Il blocco di controllo 3DES deve essere stato inizializzato con _ *nx_crypto_method_3des_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-272">The 3DES control block must have been initialized with _ *nx_crypto_method_3des_init()*.</span></span> <span data-ttu-id="aeebb-273">L'algoritmo 3DES da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-273">The 3DES algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-274">La dimensione del buffer di input deve essere un multiplo di 8 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-274">The input buffer size must be a multiple of 8 bytes.</span></span> <span data-ttu-id="aeebb-275">Le dimensioni dei dati decrittografati hanno le stesse dimensioni della dimensione dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-275">The size of the decrypted data is the same size of the input data size.</span></span> <span data-ttu-id="aeebb-276">Se i dati crittografati sono stati riempiti per ottenere un multiplo pari delle dimensioni del blocco 3DES, la spaziatura interna verrà inclusa nel buffer di output e deve essere gestita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-276">If the encrypted data was padded to achieve an even multiple of the 3DES block size, the padding will be included in the output buffer and must be handled by the application.</span></span>

<span data-ttu-id="aeebb-277">Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-277">This operation does not keep state information, and does not alter the key material in the 3DES control block.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-278">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-278">Parameters</span></span>

- <span data-ttu-id="aeebb-279">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-279">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-280">Le operazioni valide sono:</span><span class="sxs-lookup"><span data-stu-id="aeebb-280">Valid operations are:</span></span>
  - <span data-ttu-id="aeebb-281">*NX_CRYPTO_ENCRYPT*</span><span class="sxs-lookup"><span data-stu-id="aeebb-281">*NX_CRYPTO_ENCRYPT*</span></span>
  - <span data-ttu-id="aeebb-282">*NX_CRYPTO_DECRYPT*</span><span class="sxs-lookup"><span data-stu-id="aeebb-282">*NX_CRYPTO_DECRYPT*</span></span>
- <span data-ttu-id="aeebb-283">**Gestisci** Handle inizializzato da *_nx_crypto_method_3des_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-283">**handle** The handle initialized by *_nx_crypto_method_3des_init()*.</span></span>
- <span data-ttu-id="aeebb-284">**Metodo** Puntatore al metodo crittografico 3DES valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-284">**method** Pointer to the valid 3DES crypto method.</span></span> <span data-ttu-id="aeebb-285">Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_3des_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-285">The crypto method used here must be the same used in the *nx_crypto_method_3des_init().*</span></span>
- <span data-ttu-id="aeebb-286">**input_data** Punta a un buffer contenente dati di testo crittografati.</span><span class="sxs-lookup"><span data-stu-id="aeebb-286">**input_data** Points to a buffer containing encrypted text data.</span></span>
<span data-ttu-id="aeebb-287">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-287">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-288">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-288">**input_data_size** Size of the input data, in bytes.</span></span> <span data-ttu-id="aeebb-289">Le dimensioni dei dati di input devono essere un multiplo di 8 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-289">The input data size must be a multiple of 8 bytes.</span></span>
- <span data-ttu-id="aeebb-290">**iv_ptr** Puntatore al vettore iniziale.</span><span class="sxs-lookup"><span data-stu-id="aeebb-290">**iv_ptr** Pointer to the Initial Vector.</span></span> <span data-ttu-id="aeebb-291">Non esistono restrizioni sul buffer IV.</span><span class="sxs-lookup"><span data-stu-id="aeebb-291">There are no restrictions on the IV buffer.</span></span>
- <span data-ttu-id="aeebb-292">**iv_size** Dimensione del blocco del vettore iniziale, in byte questo campo deve essere 8.</span><span class="sxs-lookup"><span data-stu-id="aeebb-292">**iv_size** Size of the Initial Vector block, in bytes This field must be 8.</span></span>
- <span data-ttu-id="aeebb-293">**output_buffer** Puntatore all'area di memoria per 3DES per archiviare i dati di testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-293">**output_buffer** Pointer to the memory area for 3DES to store the clear text data.</span></span> <span data-ttu-id="aeebb-294">L'applicazione deve allocare spazio per il buffer di output.</span><span class="sxs-lookup"><span data-stu-id="aeebb-294">Application must allocate space for the output buffer.</span></span> <span data-ttu-id="aeebb-295">Il buffer di output può sovrapporsi al buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-295">Output buffer may overlap with input buffer.</span></span> <span data-ttu-id="aeebb-296">Il buffer di output può sovrapporsi al buffer di input se condivide lo stesso indirizzo iniziale.</span><span class="sxs-lookup"><span data-stu-id="aeebb-296">The output buffer may overlap with the input buffer if they share the same starting address.</span></span>
- <span data-ttu-id="aeebb-297">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-297">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="aeebb-298">La dimensione del buffer di output deve essere uguale almeno alla dimensione del buffer di input e la dimensione del buffer di output deve essere un multiplo di 8 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-298">Output buffer size must be at least the same of the input buffer size, and the output buffer size must be a multiple of 8 bytes.</span></span>
- <span data-ttu-id="aeebb-299">**crypto_metadata** Puntatore al blocco di controllo 3DES utilizzato nel *_nx_crypto_method_3des_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-299">**crypto_metadata** Pointer to the 3DES control block used in *_nx_crypto_method_3des_init()*.</span></span>
- <span data-ttu-id="aeebb-300">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-300">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-301">Per 3DES, le dimensioni dei metadati devono essere *sizeof (NX_3DES)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-301">For 3DES, the metadata size must be *sizeof(NX_3DES)*</span></span>
- <span data-ttu-id="aeebb-302">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-302">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-303">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-303">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-304">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-304">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-305">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-305">Any values passed in are silently ignored.</span></span>

### <a name="description"></a><span data-ttu-id="aeebb-306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-306">Description</span></span>

<span data-ttu-id="aeebb-307">Questa funzione esegue la crittografia 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-307">This function performs 3DES encryption.</span></span> <span data-ttu-id="aeebb-308">Il blocco di controllo 3DES deve essere stato inizializzato con _ *nx_crypto_moethod_3des_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-308">The 3DES control block must have been initialized with _ *nx_crypto_moethod_3des_init()*.</span></span> <span data-ttu-id="aeebb-309">Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-309">This operation does not keep state information, and does not alter the key material in the 3DES control block.</span></span> <span data-ttu-id="aeebb-310">Si noti che la spaziatura interna non viene aggiunta da questa funzione in modo che il chiamante debba gestire la spaziatura interna prima di richiamare l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="aeebb-310">Note that padding is not added by this function so the caller will need to handle padding before invoking the encryption operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-311">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-311">Return Values</span></span>

- <span data-ttu-id="aeebb-312">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo 3DES con la chiave e la dimensione della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-312">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the 3DES control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-313">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-313">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-314">**NX_PTR_ERROR (0x07)** Puntatore alla chiave non valido o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-314">**NX_PTR_ERROR (0x07)** Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_3des_cleanup"></a><span data-ttu-id="aeebb-315">_nx_crypto_method_3des_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-315">_nx_crypto_method_3des_cleanup</span></span>

<span data-ttu-id="aeebb-316">Pulire il blocco di controllo 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-316">Clean up the 3DES control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-317">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-317">Prototype</span></span>

```c
UINT _nx_crypto_method_3des_cleanup(VOID *crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-318">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-318">Description</span></span>

<span data-ttu-id="aeebb-319">L'applicazione chiama questa funzione per pulire il blocco di controllo 3DES dopo aver determinato che questa sessione 3DES non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-319">Application calls this function to clean up the 3DES control block after it determines this 3DES session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-320">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-320">Parameters</span></span>

- <span data-ttu-id="aeebb-321">**Gestisci** Handle inizializzato da *_nx_crypto_method_3des_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-321">**handle** The handle initialized by *_nx_crypto_method_3des_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-322">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-322">Return Values</span></span>

- <span data-ttu-id="aeebb-323">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione 3DES.</span><span class="sxs-lookup"><span data-stu-id="aeebb-323">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the 3DES session.</span></span>
- <span data-ttu-id="aeebb-324">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-324">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_drbg_init"></a><span data-ttu-id="aeebb-325">_nx_crypto_method_drbg_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-325">_nx_crypto_method_drbg_init</span></span>

<span data-ttu-id="aeebb-326">Inizializza il blocco di controllo Crypto DRBG</span><span class="sxs-lookup"><span data-stu-id="aeebb-326">Initializes the DRBG crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-327">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-327">Prototype</span></span>

```c
UINT _nx_crypto_method_drbg_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-328">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-328">Description</span></span>

<span data-ttu-id="aeebb-329">Questa funzione Inizializza il blocco di controllo DRBG con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-329">This function initializes the DRBG control block with the given key string.</span></span> <span data-ttu-id="aeebb-330">Una volta inizializzato il blocco di controllo DRBG, l'operazione DRBG successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-330">Once the DRBG control block is initialized, subsequent DRBG operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-331">L'applicazione può creare più blocchi di controllo DRBG, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-331">Application may create multiple DRBG control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-332">L'inizializzazione del blocco di controllo DRBG avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-332">Initializing the DRBG control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-333">La reinizializzazione del blocco di controllo DRBG abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-333">Re-initializing the DRBG control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-334">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-334">Parameters</span></span>

- <span data-ttu-id="aeebb-335">**Metodo** Puntatore a un blocco di controllo del metodo Crypto DRBG valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-335">**method** Pointer to a valid DRBG crypto method control block.</span></span> <span data-ttu-id="aeebb-336">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-336">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-337">*crypto_method_drbg*</span><span class="sxs-lookup"><span data-stu-id="aeebb-337">*crypto_method_drbg*</span></span>
- <span data-ttu-id="aeebb-338">**chiave** di Questo campo non viene utilizzato per DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-338">**key** This field is not used for DRBG.</span></span>
- <span data-ttu-id="aeebb-339">**key_size_in_bits** Questo campo non viene utilizzato per DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-339">**key_size_in_bits** This field is not used for DRBG.</span></span>
- <span data-ttu-id="aeebb-340">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-340">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-341">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-341">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-342">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-342">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-343">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-343">**crypto_metadata** Pointer to a valid memory space for the DRBG control block.</span></span> <span data-ttu-id="aeebb-344">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-344">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-345">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-345">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-346">Per DRBG, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_DRBG)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-346">For DRBG, the metadata size must be *sizeof(NX_CRYPTO_DRBG)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-347">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-347">Return Values</span></span>

- <span data-ttu-id="aeebb-348">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo DRBG con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-348">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the DRBG control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-349">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-349">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-350">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-350">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_drbg_operation"></a><span data-ttu-id="aeebb-351">_nx_crypto_method_drbg_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-351">_nx_crypto_method_drbg_operation</span></span>

<span data-ttu-id="aeebb-352">Eseguire l'operazione DRBG</span><span class="sxs-lookup"><span data-stu-id="aeebb-352">Perform DRBG operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-353">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-353">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-354">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-354">Description</span></span>

<span data-ttu-id="aeebb-355">Questa funzione esegue l'operazione DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-355">This function performs DRBG operation.</span></span> <span data-ttu-id="aeebb-356">Il blocco di controllo DRBG deve essere stato inizializzato con _ *nx_crypto_method_drbg_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-356">The DRBG control block must have been initialized with _ *nx_crypto_method_drbg_init()*.</span></span> <span data-ttu-id="aeebb-357">L'algoritmo DRBG da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-357">The DRBG algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span> <span data-ttu-id="aeebb-358">Per impostazione predefinita, viene usato AES-128 per DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-358">By default AES-128 is used for DRBG.</span></span>

<span data-ttu-id="aeebb-359">Quando si NX_CRYPTO_DRBG_OPTIONS_SET l'operazione, l'input punta alla struttura NX_CRYPTO_DRBG_OPTIONS.</span><span class="sxs-lookup"><span data-stu-id="aeebb-359">When the operation is NX_CRYPTO_DRBG_OPTIONS_SET, the input points to NX_CRYPTO_DRBG_OPTIONS structure.</span></span> <span data-ttu-id="aeebb-360">Quando si NX_CRYPTO_DRBG_INSTANTIATE l'operazione, la chiave punta a nonce, i punti di input alla stringa di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-360">When the operation is NX_CRYPTO_DRBG_INSTANTIATE, the key points to nonce, input points to personalization string.</span></span> <span data-ttu-id="aeebb-361">Quando l'operazione viene NX_CRYPTO_DRBG_RESEED o NX_CRYPTO_DRBG_GENERATE, l'input punta a input aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-361">When the operation is NX_CRYPTO_DRBG_RESEED or NX_CRYPTO_DRBG_GENERATE, the input points to additional input.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-362">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-362">Parameters</span></span>

- <span data-ttu-id="aeebb-363">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-363">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-364">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-364">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-365">*NX_CRYPTO_DRBG_OPTIONS_SET*</span><span class="sxs-lookup"><span data-stu-id="aeebb-365">*NX_CRYPTO_DRBG_OPTIONS_SET*</span></span>
  - <span data-ttu-id="aeebb-366">*NX_CRYPTO_DRBG_INSTANTIATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-366">*NX_CRYPTO_DRBG_INSTANTIATE*</span></span>
  - <span data-ttu-id="aeebb-367">*NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-367">*NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*</span></span>
- <span data-ttu-id="aeebb-368">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-368">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-369">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-369">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-370">**Metodo** Puntatore al metodo di crittografia DRBG valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-370">**method** Pointer to the valid DRBG crypto method.</span></span> <span data-ttu-id="aeebb-371">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_drbg_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-371">The crypto method used here must be the same used in the _ *nx_crypto_method_drbg_init().*</span></span>
- <span data-ttu-id="aeebb-372">**chiave** di Puntatore al parametro nonce per l'operazione di creazione dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="aeebb-372">**key** Pointer to the the nonce for the instantiate operation.</span></span> <span data-ttu-id="aeebb-373">Questo campo non viene utilizzato per altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="aeebb-373">This field is not used for other operations.</span></span>
- <span data-ttu-id="aeebb-374">**key_size_in_bits** Dimensioni del parametro nonce in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-374">**key_size_in_bits** Size of the nonce, in bits.</span></span> <span data-ttu-id="aeebb-375">Questo campo non viene utilizzato per altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="aeebb-375">This field is not used for other operations.</span></span>
- <span data-ttu-id="aeebb-376">**input** di Quando op è NX_CRYPTO_DRBG_OPTIONS_SET, questo campo fa riferimento alle opzioni di DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-376">**input** When op is NX_CRYPTO_DRBG_OPTIONS_SET, this field points to DRBG options.</span></span> <span data-ttu-id="aeebb-377">Quando op è NX_CRYPTO_DRBG_INSTANTIATE, questo campo punta alla stringa di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-377">When op is NX_CRYPTO_DRBG_INSTANTIATE, this field points to personalization string.</span></span> <span data-ttu-id="aeebb-378">Quando op è NX_CRYPTO_DRBG_RESEED o NX_CRYPTO_DRBG_GENERATE, questo campo punta a dati di input aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="aeebb-378">When op is NX_CRYPTO_DRBG_RESEED or NX_CRYPTO_DRBG_GENERATE, this field points to additional input data.</span></span>
- <span data-ttu-id="aeebb-379">**input_length_in_byte** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-379">**input_length_in_byte** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-380">**iv_ptr** Questo campo non viene utilizzato per DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-380">**iv_ptr** This field is not used for DRBG.</span></span>
- <span data-ttu-id="aeebb-381">**output** di Quando op è NX_CRYPTO_DRBG_GENERATE, questo campo fa riferimento all'area di memoria per il DRBG generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-381">**output** When op is NX_CRYPTO_DRBG_GENERATE, this field points to the memory area for the generated DRBG.</span></span> <span data-ttu-id="aeebb-382">In caso contrario, questo campo non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-382">Otherwise, this field is not used.</span></span>
- <span data-ttu-id="aeebb-383">**output_length_in_byte** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-383">**output_length_in_byte** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-384">**crypto_metadata** Puntatore al blocco di controllo DRBG utilizzato nel *_nx_crypto_method_drbg_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-384">**crypto_metadata** Pointer to the DRBG control block used in *_nx_crypto_method_drbg_init()*.</span></span>
- <span data-ttu-id="aeebb-385">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-385">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-386">Per DRBG, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_DRBG)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-386">For DRBG, the metadata size must *sizeof(NX_CRYPTO_DRBG)*</span></span>
- <span data-ttu-id="aeebb-387">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-387">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-388">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-388">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-389">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-389">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-390">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-390">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-391">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-391">Return Values</span></span>

- <span data-ttu-id="aeebb-392">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-392">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the DRBG operation.</span></span>
- <span data-ttu-id="aeebb-393">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-393">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-394">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-394">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-395">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo DRBG non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-395">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid DRBG algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-396">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-396">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_drbg_cleanup"></a><span data-ttu-id="aeebb-397">_nx_crypto_method_drbg_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-397">_nx_crypto_method_drbg_cleanup</span></span>

<span data-ttu-id="aeebb-398">Pulire il blocco di controllo DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-398">Clean up the DRBG control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-399">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-399">Prototype</span></span>

```c
UINT _nx_crypto_method_drbg_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-400">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-400">Description</span></span>

<span data-ttu-id="aeebb-401">L'applicazione chiama questa funzione per pulire il blocco di controllo DRBG dopo aver determinato che questa sessione DRBG non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-401">Application calls this function to clean up the DRBG control block after it determines this DRBG session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-402">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-402">Parameters</span></span>

- <span data-ttu-id="aeebb-403">**crypto_metadata** Puntatore al blocco di controllo DRBG utilizzato nel *_nx_crypto_method_drbg_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-403">**crypto_metadata** Pointer to the DRBG control block used in *_nx_crypto_method_drbg_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-404">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-404">Return Values</span></span>

- <span data-ttu-id="aeebb-405">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione DRBG.</span><span class="sxs-lookup"><span data-stu-id="aeebb-405">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the DRBG session.</span></span>
- <span data-ttu-id="aeebb-406">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-406">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_ecdh_init"></a><span data-ttu-id="aeebb-407">_nx_crypto_method_ecdh_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-407">_nx_crypto_method_ecdh_init</span></span>

<span data-ttu-id="aeebb-408">Inizializza il blocco di controllo Crypto ECDH</span><span class="sxs-lookup"><span data-stu-id="aeebb-408">Initializes the ECDH crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-409">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-409">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdh_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-410">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-410">Description</span></span>

<span data-ttu-id="aeebb-411">Questa funzione Inizializza il blocco di controllo ECDH con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-411">This function initializes the ECDH control block with the given key string.</span></span> <span data-ttu-id="aeebb-412">Una volta inizializzato il blocco di controllo ECDH, l'operazione ECDH successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-412">Once the ECDH control block is initialized, subsequent ECDH operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-413">L'applicazione può creare più blocchi di controllo ECDH, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-413">Application may create multiple ECDH control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-414">L'inizializzazione del blocco di controllo ECDH avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-414">Initializing the ECDH control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-415">La reinizializzazione del blocco di controllo ECDH abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-415">Re-initializing the ECDH control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-416">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-416">Parameters</span></span>

- <span data-ttu-id="aeebb-417">**Metodo** Puntatore a un blocco di controllo del metodo Crypto ECDH valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-417">**method** Pointer to a valid ECDH crypto method control block.</span></span> <span data-ttu-id="aeebb-418">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-418">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-419">*crypto_method_ecdh*</span><span class="sxs-lookup"><span data-stu-id="aeebb-419">*crypto_method_ecdh*</span></span>
- <span data-ttu-id="aeebb-420">**chiave** di Questo campo non viene utilizzato per ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-420">**key** This field is not used for ECDH.</span></span>
- <span data-ttu-id="aeebb-421">**key_size_in_bits** Questo campo non viene utilizzato per ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-421">**key_size_in_bits** This field is not used for ECDH.</span></span>
- <span data-ttu-id="aeebb-422">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-422">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-423">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-423">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-424">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-424">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-425">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-425">**crypto_metadata** Pointer to a valid memory space for the ECDH control block.</span></span> <span data-ttu-id="aeebb-426">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-426">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-427">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-427">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-428">Per ECDH, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDH)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-428">For ECDH, the metadata size must be *sizeof(NX_CRYPTO_ECDH)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-429">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-429">Return Values</span></span>

- <span data-ttu-id="aeebb-430">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo ECDH con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-430">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the ECDH control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-431">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-431">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-432">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-432">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_ecdh_operation"></a><span data-ttu-id="aeebb-433">_nx_crypto_method_ecdh_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-433">_nx_crypto_method_ecdh_operation</span></span>

<span data-ttu-id="aeebb-434">Eseguire l'operazione ECDH</span><span class="sxs-lookup"><span data-stu-id="aeebb-434">Perform ECDH operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-435">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-435">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-436">Description</span></span>

<span data-ttu-id="aeebb-437">Questa funzione esegue l'operazione ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-437">This function performs ECDH operation.</span></span> <span data-ttu-id="aeebb-438">Il blocco di controllo ECDH deve essere stato inizializzato con _ *nx_crypto_method_ecdh_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-438">The ECDH control block must have been initialized with _ *nx_crypto_method_ecdh_init()*.</span></span> <span data-ttu-id="aeebb-439">L'algoritmo ECDH da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-439">The ECDH algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-440">Quando si NX_CRYPTO_EC_CURVE_SET l'operazione, l'input punta al metodo di crittografia a curva ellittica.</span><span class="sxs-lookup"><span data-stu-id="aeebb-440">When the operation is NX_CRYPTO_EC_CURVE_SET, the input points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="aeebb-441">Quando si NX_CRYPTO_EC_KEY_PAIR_GENERATE l'operazione, l'output punta alla struttura NX_CRYPTO_EXTENDED_OUTPUT e la coppia di chiavi viene copiata in nx_crypto_extended_output_data.</span><span class="sxs-lookup"><span data-stu-id="aeebb-441">When the operation is NX_CRYPTO_EC_KEY_PAIR_GENERATE, the output points to NX_CRYPTO_EXTENDED_OUTPUT structure and the key pair is copied to nx_crypto_extended_output_data.</span></span> <span data-ttu-id="aeebb-442">Quando si NX_CRYPTO_DH_SETUP l'operazione, la chiave pubblica viene restituita nx_crypto_extended_output_data.</span><span class="sxs-lookup"><span data-stu-id="aeebb-442">When the operation is NX_CRYPTO_DH_SETUP, the public key is returned to nx_crypto_extended_output_data.</span></span> <span data-ttu-id="aeebb-443">Quando si NX_CRYPTO_DH_KEY_PAIR_IMPORT l'operazione, i punti di input alla chiave pubblica e ai punti chiave alla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-443">When the operation is NX_CRYPTO_DH_KEY_PAIR_IMPORT, the input points to public key and key points to private key.</span></span> <span data-ttu-id="aeebb-444">Quando si NX_CRYPTO_DH_PRIVATE_KEY_EXPORT l'operazione, la chiave privata viene copiata nx_crypto_extended_output_data.</span><span class="sxs-lookup"><span data-stu-id="aeebb-444">When the operation is NX_CRYPTO_DH_PRIVATE_KEY_EXPORT, the private key is copied to nx_crypto_extended_output_data.</span></span> <span data-ttu-id="aeebb-445">Quando si NX_CRYPTO_DH_CALCULATE l'operazione, i punti di input alla chiave pubblica remota e al segreto condiviso vengono copiati in nx_crypto_extended_output_data.</span><span class="sxs-lookup"><span data-stu-id="aeebb-445">When the operation is NX_CRYPTO_DH_CALCULATE, the input points to remote public key and the shared secret is copied to nx_crypto_extended_output_data.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-446">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-446">Parameters</span></span>

- <span data-ttu-id="aeebb-447">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-447">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-448">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-448">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-449">*NX_CRYPTO_EC_CURVE_SET*</span><span class="sxs-lookup"><span data-stu-id="aeebb-449">*NX_CRYPTO_EC_CURVE_SET*</span></span>
  - <span data-ttu-id="aeebb-450">*NX_CRYPTO_DH_SETUP*</span><span class="sxs-lookup"><span data-stu-id="aeebb-450">*NX_CRYPTO_DH_SETUP*</span></span>
  - <span data-ttu-id="aeebb-451">*NX_CRYPTO_DH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-451">*NX_CRYPTO_DH_CALCULATE*</span></span>
  - <span data-ttu-id="aeebb-452">*NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*</span><span class="sxs-lookup"><span data-stu-id="aeebb-452">*NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*</span></span>
  - <span data-ttu-id="aeebb-453">*NX_CRYPTO_DH_KEY_PAIR_GENERATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-453">*NX_CRYPTO_DH_KEY_PAIR_GENERATE*</span></span>
  - <span data-ttu-id="aeebb-454">*NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*</span><span class="sxs-lookup"><span data-stu-id="aeebb-454">*NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*</span></span>
- <span data-ttu-id="aeebb-455">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-455">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-456">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-456">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-457">**Metodo** Puntatore al metodo di crittografia ECDH valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-457">**method** Pointer to the valid ECDH crypto method.</span></span> <span data-ttu-id="aeebb-458">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_ecdh_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-458">The crypto method used here must be the same used in the _ *nx_crypto_method_ecdh_init().*</span></span>
- <span data-ttu-id="aeebb-459">**chiave** di Quando op è NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo punta alla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-459">**key** When op is NX_CRYPTO_DH_IMPORT_KEY_PAIR, this field points to private key.</span></span> <span data-ttu-id="aeebb-460">In caso contrario, questo campo non viene utilizzato per ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-460">Otherwise, this field is not used for ECDH.</span></span>
- <span data-ttu-id="aeebb-461">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-461">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-462">**input** di Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo fa riferimento al metodo Crypto a curva ellittica.</span><span class="sxs-lookup"><span data-stu-id="aeebb-462">**input** When op is NX_CRYPTO_EC_CURVE_SET, this field points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="aeebb-463">Quando op è NX_CRYPTO_DH_SETUP, questo campo non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-463">When op is NX_CRYPTO_DH_SETUP, this field is not used.</span></span> <span data-ttu-id="aeebb-464">Quando op è NX_CRYPTO_DH_CALCULATE, questo campo punta a un buffer contenente dati di input di testo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-464">When op is NX_CRYPTO_DH_CALCULATE, this field points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-465">Quando op è NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo punta alla chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="aeebb-465">When op is NX_CRYPTO_DH_IMPORT_KEY_PAIR, this field points to public key.</span></span>
- <span data-ttu-id="aeebb-466">**input_length_in_byte** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-466">**input_length_in_byte** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-467">**iv_ptr** Questo campo non viene utilizzato per ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-467">**iv_ptr** This field is not used for ECDH.</span></span>
- <span data-ttu-id="aeebb-468">**output** di Quando op è NX_CRYPTO_EC_CURVE_SET o NX_CRYPTO_DH_IMPORT_KEY_PAIR, questo campo non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-468">**output** When op is NX_CRYPTO_EC_CURVE_SET or NX_CRYPTO_DH_IMPORT_KEY_PAIR, this field is not used.</span></span> <span data-ttu-id="aeebb-469">Quando op è NX_CRYPTO_DH_SETUP, questo campo fa riferimento all'area di memoria per la chiave pubblica ECDH generata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-469">When op is NX_CRYPTO_DH_SETUP, this field points to the memory area for the generated ECDH public key.</span></span> <span data-ttu-id="aeebb-470">Quando op è NX_CRYPTO_DH_CALCULATE, questo campo fa riferimento all'area di memoria per il segreto condiviso ECDH generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-470">When op is NX_CRYPTO_DH_CALCULATE, this field points to the memory area for the generated ECDH shared secret.</span></span>
- <span data-ttu-id="aeebb-471">**output_length_in_byte** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-471">**output_length_in_byte** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-472">**crypto_metadata** Puntatore al blocco di controllo ECDH utilizzato nel *_nx_crypto_method_ecdh_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-472">**crypto_metadata** Pointer to the ECDH control block used in *_nx_crypto_method_ecdh_init()*.</span></span>
- <span data-ttu-id="aeebb-473">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-473">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-474">Per ECDH, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDH)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-474">For ECDH, the metadata size must *sizeof(NX_CRYPTO_ECDH)*</span></span>
- <span data-ttu-id="aeebb-475">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-475">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-476">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-476">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-477">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-477">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-478">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-478">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-479">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-479">Return Values</span></span>

- <span data-ttu-id="aeebb-480">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-480">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the ECDH operation.</span></span>
- <span data-ttu-id="aeebb-481">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-481">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-482">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-482">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-483">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo ECDH non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-483">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid ECDH algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-484">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-484">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_ecdh_cleanup"></a><span data-ttu-id="aeebb-485">_nx_crypto_method_ecdh_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-485">_nx_crypto_method_ecdh_cleanup</span></span>

<span data-ttu-id="aeebb-486">Pulire il blocco di controllo ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-486">Clean up the ECDH control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-487">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-487">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdh_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-488">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-488">Description</span></span>

<span data-ttu-id="aeebb-489">L'applicazione chiama questa funzione per pulire il blocco di controllo ECDH dopo aver determinato che questa sessione ECDH non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-489">Application calls this function to clean up the ECDH control block after it determines this ECDH session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-490">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-490">Parameters</span></span>

- <span data-ttu-id="aeebb-491">**crypto_metadata** Puntatore al blocco di controllo ECDH utilizzato nel *_nx_crypto_method_ecdh_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-491">**crypto_metadata** Pointer to the ECDH control block used in *_nx_crypto_method_ecdh_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-492">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-492">Return Values</span></span>

- <span data-ttu-id="aeebb-493">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione ECDH.</span><span class="sxs-lookup"><span data-stu-id="aeebb-493">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the ECDH session.</span></span>
- <span data-ttu-id="aeebb-494">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-494">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_ecdsa_init"></a><span data-ttu-id="aeebb-495">_nx_crypto_method_ecdsa_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-495">_nx_crypto_method_ecdsa_init</span></span>

<span data-ttu-id="aeebb-496">Inizializza il blocco di controllo Crypto ECDSA</span><span class="sxs-lookup"><span data-stu-id="aeebb-496">Initializes the ECDSA crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-497">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-497">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdsa_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-498">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-498">Description</span></span>

<span data-ttu-id="aeebb-499">Questa funzione Inizializza il blocco di controllo ECDSA con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-499">This function initializes the ECDSA control block with the given key string.</span></span> <span data-ttu-id="aeebb-500">Una volta inizializzato il blocco di controllo ECDSA, l'operazione ECDSA successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-500">Once the ECDSA control block is initialized, subsequent ECDSA operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-501">L'applicazione può creare più blocchi di controllo ECDSA, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-501">Application may create multiple ECDSA control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-502">L'inizializzazione del blocco di controllo ECDSA avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-502">Initializing the ECDSA control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-503">La reinizializzazione del blocco di controllo ECDSA abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-503">Re-initializing the ECDSA control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-504">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-504">Parameters</span></span>

- <span data-ttu-id="aeebb-505">**Metodo** Puntatore a un blocco di controllo del metodo Crypto ECDSA valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-505">**method** Pointer to a valid ECDSA crypto method control block.</span></span> <span data-ttu-id="aeebb-506">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-506">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-507">*crypto_method_ecdsa*</span><span class="sxs-lookup"><span data-stu-id="aeebb-507">*crypto_method_ecdsa*</span></span>
- <span data-ttu-id="aeebb-508">**chiave** di Questo campo non viene utilizzato per ECDSA.</span><span class="sxs-lookup"><span data-stu-id="aeebb-508">**key** This field is not used for ECDSA.</span></span>
- <span data-ttu-id="aeebb-509">**key_size_in_bits** Questo campo non viene utilizzato per ECDSA.</span><span class="sxs-lookup"><span data-stu-id="aeebb-509">**key_size_in_bits** This field is not used for ECDSA.</span></span>
- <span data-ttu-id="aeebb-510">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-510">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-511">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-511">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-512">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-512">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-513">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo ECDSA.</span><span class="sxs-lookup"><span data-stu-id="aeebb-513">**crypto_metadata** Pointer to a valid memory space for the ECDSA control block.</span></span> <span data-ttu-id="aeebb-514">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-514">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-515">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-515">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-516">Per ECDSA, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDSA)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-516">For ECDSA, the metadata size must be *sizeof(NX_CRYPTO_ECDSA)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-517">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-517">Return Values</span></span>

- <span data-ttu-id="aeebb-518">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo ECDSA con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-518">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the ECDSA control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-519">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-519">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-520">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-520">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_ecdsa_operation"></a><span data-ttu-id="aeebb-521">_nx_crypto_method_ecdsa_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-521">_nx_crypto_method_ecdsa_operation</span></span>

<span data-ttu-id="aeebb-522">Eseguire l'operazione ECDSA</span><span class="sxs-lookup"><span data-stu-id="aeebb-522">Perform ECDSA operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-523">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-523">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-524">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-524">Description</span></span>

<span data-ttu-id="aeebb-525">Questa funzione esegue l'operazione ECDSA.</span><span class="sxs-lookup"><span data-stu-id="aeebb-525">This function performs ECDSA operation.</span></span> <span data-ttu-id="aeebb-526">Il blocco di controllo ECDSA deve essere stato inizializzato con _ *nx_crypto_method_ecdsa_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-526">The ECDSA control block must have been initialized with _ *nx_crypto_method_ecdsa_init()*.</span></span> <span data-ttu-id="aeebb-527">L'algoritmo ECDSA da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-527">The ECDSA algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-528">Quando si NX_CRYPTO_EC_CURVE_SET l'operazione, l'input punta al metodo di crittografia a curva ellittica.</span><span class="sxs-lookup"><span data-stu-id="aeebb-528">When the operation is NX_CRYPTO_EC_CURVE_SET, the input points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="aeebb-529">Quando si NX_CRYPTO_EC_KEY_PAIR_GENERATE l'operazione, l'output punta alla struttura NX_CRYPTO_EXTENDED_OUTPUT e la coppia di chiavi viene copiata in nx_crypto_extended_output_data.</span><span class="sxs-lookup"><span data-stu-id="aeebb-529">When the operation is NX_CRYPTO_EC_KEY_PAIR_GENERATE, the output points to NX_CRYPTO_EXTENDED_OUTPUT structure and the key pair is copied to nx_crypto_extended_output_data.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-530">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-530">Parameters</span></span>

- <span data-ttu-id="aeebb-531">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-531">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-532">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-532">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-533">*NX_CRYPTO_EC_CURVE_SET*</span><span class="sxs-lookup"><span data-stu-id="aeebb-533">*NX_CRYPTO_EC_CURVE_SET*</span></span>
  - <span data-ttu-id="aeebb-534">*NX_CRYPTO_AUTHENTICATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-534">*NX_CRYPTO_AUTHENTICATE*</span></span>
  - <span data-ttu-id="aeebb-535">*NX_CRYPTO_VERIFY*</span><span class="sxs-lookup"><span data-stu-id="aeebb-535">*NX_CRYPTO_VERIFY*</span></span>
- <span data-ttu-id="aeebb-536">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-536">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-537">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-537">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-538">**Metodo** Puntatore al metodo di crittografia ECDSA valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-538">**method** Pointer to the valid ECDSA crypto method.</span></span> <span data-ttu-id="aeebb-539">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_ecdsa_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-539">The crypto method used here must be the same used in the _ *nx_crypto_method_ecdsa_init().*</span></span>
- <span data-ttu-id="aeebb-540">**chiave** di Punta alla chiave quando op è NX_CRYPTO_VERIFY.</span><span class="sxs-lookup"><span data-stu-id="aeebb-540">**key** Points to the key when op is NX_CRYPTO_VERIFY.</span></span> <span data-ttu-id="aeebb-541">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-541">There are not restrictions on key buffer.</span></span> <span data-ttu-id="aeebb-542">Questo campo non viene usato per altri valori di op.</span><span class="sxs-lookup"><span data-stu-id="aeebb-542">This field is not used for other values of op.</span></span>
- <span data-ttu-id="aeebb-543">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-543">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-544">**input** di Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo fa riferimento al metodo Crypto a curva ellittica.</span><span class="sxs-lookup"><span data-stu-id="aeebb-544">**input** When op is NX_CRYPTO_EC_CURVE_SET, this field points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="aeebb-545">In caso contrario, questo campo punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-545">Otherwise, this field points to a buffer containing input text data.</span></span>
- <span data-ttu-id="aeebb-546">**input_length_in_byte** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-546">**input_length_in_byte** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-547">**iv_ptr** Questo campo non viene utilizzato per ECDSA.</span><span class="sxs-lookup"><span data-stu-id="aeebb-547">**iv_ptr** This field is not used for ECDSA.</span></span>
- <span data-ttu-id="aeebb-548">**output** di Quando op è NX_CRYPTO_EC_CURVE_SET, questo campo non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-548">**output** When op is NX_CRYPTO_EC_CURVE_SET, this field is not used.</span></span> <span data-ttu-id="aeebb-549">Quando op è NX_CRYPTO_AUTHENTICATE, questo campo fa riferimento all'area di memoria per la firma ECDSA generata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-549">When op is NX_CRYPTO_AUTHENTICATE, this field points to the memory area for the generated ECDSA signature.</span></span> <span data-ttu-id="aeebb-550">Quando op è NX_CRYPTO_VERIFY, questo campo fa riferimento all'area di memoria per la firma ECDSA verificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-550">When op is NX_CRYPTO_VERIFY, this field points to the memory area for the verified ECDSA signature.</span></span>
- <span data-ttu-id="aeebb-551">**output_length_in_byte** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-551">**output_length_in_byte** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-552">**crypto_metadata** Puntatore al blocco di controllo ECDSA utilizzato nel *_nx_crypto_method_ecdsa_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-552">**crypto_metadata** Pointer to the ECDSA control block used in *_nx_crypto_method_ecdsa_init()*.</span></span>
- <span data-ttu-id="aeebb-553">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-553">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-554">Per ECDSA, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_ECDSA)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-554">For ECDSA, the metadata size must *sizeof(NX_CRYPTO_ECDSA)*</span></span>
- <span data-ttu-id="aeebb-555">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-555">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-556">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-556">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-557">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-557">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-558">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-558">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-559">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-559">Return Values</span></span>

- <span data-ttu-id="aeebb-560">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione ECDsa.</span><span class="sxs-lookup"><span data-stu-id="aeebb-560">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the ECDSA operation.</span></span>
- <span data-ttu-id="aeebb-561">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-561">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-562">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-562">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-563">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo ECDSA non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-563">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid ECDSA algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-564">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-564">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_ecdsa_cleanup"></a><span data-ttu-id="aeebb-565">_nx_crypto_method_ecdsa_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-565">_nx_crypto_method_ecdsa_cleanup</span></span>

<span data-ttu-id="aeebb-566">Pulire il blocco di controllo ECDSA.</span><span class="sxs-lookup"><span data-stu-id="aeebb-566">Clean up the ECDSA control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-567">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-567">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdsa_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-568">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-568">Description</span></span>

<span data-ttu-id="aeebb-569">L'applicazione chiama questa funzione per pulire il blocco di controllo ECDSA dopo aver determinato che questa sessione ECDSA non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-569">Application calls this function to clean up the ECDSA control block after it determines this ECDSA session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-570">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-570">Parameters</span></span>

- <span data-ttu-id="aeebb-571">**crypto_metadata** Puntatore al blocco di controllo ECDSA utilizzato nel *_nx_crypto_method_ecdsa_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-571">**crypto_metadata** Pointer to the ECDSA control block used in *_nx_crypto_method_ecdsa_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-572">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-572">Return Values</span></span>

- <span data-ttu-id="aeebb-573">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione ECDsa.</span><span class="sxs-lookup"><span data-stu-id="aeebb-573">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the ECDSA session.</span></span>
- <span data-ttu-id="aeebb-574">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-574">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_hmac_md5_init"></a><span data-ttu-id="aeebb-575">_nx_crypto_method_hmac_md5_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-575">_nx_crypto_method_hmac_md5_init</span></span>

<span data-ttu-id="aeebb-576">Inizializza il blocco di controllo crittografico HMAC MD5</span><span class="sxs-lookup"><span data-stu-id="aeebb-576">Initializes the HMAC MD5 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-577">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-577">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-578">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-578">Description</span></span>

<span data-ttu-id="aeebb-579">Questa funzione Inizializza il blocco di controllo HMAC MD5 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-579">This function initializes the HMAC MD5 control block with the given key string.</span></span> <span data-ttu-id="aeebb-580">Una volta inizializzato il blocco di controllo HMAC MD5, l'operazione HMAC MD5 successiva dovrà utilizzare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-580">Once the HMAC MD5 control block is initialized, subsequent HMAC MD5 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-581">L'applicazione può creare più blocchi di controllo HMAC MD5, ognuno di essi rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-581">Application may create multiple HMAC MD5 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-582">L'inizializzazione del blocco di controllo HMAC MD5 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-582">Initializing the HMAC MD5 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-583">La reinizializzazione del blocco di controllo HMAC MD5 abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-583">Re-initializing the HMAC MD5 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-584">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-584">Parameters</span></span>

- <span data-ttu-id="aeebb-585">**Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC MD5 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-585">**method** Pointer to a valid HMAC MD5 crypto method control block.</span></span>
<span data-ttu-id="aeebb-586">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-586">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-587">*crypto_method_hmac_md5*</span><span class="sxs-lookup"><span data-stu-id="aeebb-587">*crypto_method_hmac_md5*</span></span>
- <span data-ttu-id="aeebb-588">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-588">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-589">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-589">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-590">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-590">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-591">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-591">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-592">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-592">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-593">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-593">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-594">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-594">**crypto_metadata** Pointer to a valid memory space for the HMAC MD5 control block.</span></span> <span data-ttu-id="aeebb-595">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-595">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-596">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-596">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-597">Per HMAC MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-597">For HMAC MD5, the metadata size must be *sizeof(NX_CRYPTO_MD5_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-598">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-598">Return Values</span></span>

- <span data-ttu-id="aeebb-599">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo HMAC MD5 con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-599">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC MD5 control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-600">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-600">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-601">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-601">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_md5_operation"></a><span data-ttu-id="aeebb-602">_nx_crypto_method_hmac_md5_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-602">_nx_crypto_method_hmac_md5_operation</span></span>

<span data-ttu-id="aeebb-603">Eseguire un'operazione hash MD5 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-603">Perform an HMAC MD5 hash operation.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-604">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-604">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-605">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-605">Description</span></span>

<span data-ttu-id="aeebb-606">Questa funzione esegue l'operazione hash MD5 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-606">This function performs HMAC MD5 hash operation.</span></span> <span data-ttu-id="aeebb-607">Il blocco di controllo HMAC MD5 deve essere stato inizializzato con _ *nx_crypto_method_hmac_md5_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-607">The HMAC MD5 control block must have been initialized with _ *nx_crypto_method_hmac_md5_init()*.</span></span> <span data-ttu-id="aeebb-608">L'algoritmo MD5 HMAC da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-608">The HMAC MD5 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-609">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-609">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 16 bytes.</span></span>

<span data-ttu-id="aeebb-610">Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo HMAC MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-610">This operation does not keep state information, and does not alter the key material in the HMAC MD5 control block.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-611">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-611">Parameters</span></span>

- <span data-ttu-id="aeebb-612">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-612">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-613">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-613">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-614">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-614">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-615">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-615">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-616">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-616">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-617">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-617">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-618">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-618">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-619">**Metodo** Puntatore al metodo crittografico HMAC MD5 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-619">**method** Pointer to the valid HMAC MD5 crypto method.</span></span> <span data-ttu-id="aeebb-620">Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_hmac_md5_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-620">The crypto method used here must be the same used in the *nx_crypto_method_hmac_md5_init().*</span></span>
- <span data-ttu-id="aeebb-621">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-621">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-622">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-622">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-623">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-623">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-624">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-624">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-625">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-625">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-626">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-626">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-627">**iv_ptr** Questo campo non viene utilizzato per HMAC MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-627">**iv_ptr** This field is not used for HMAC MD5.</span></span>
- <span data-ttu-id="aeebb-628">**iv_size** Questo campo non viene utilizzato per HMAC MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-628">**iv_size** This field is not used for HMAC MD5.</span></span>
- <span data-ttu-id="aeebb-629">**output_buffer** Puntatore all'area di memoria per l'hash MD5 HMAC generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-629">**output_buffer** Pointer to the memory area for the generated HMAC MD5 hash.</span></span>
- <span data-ttu-id="aeebb-630">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-630">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-631">**crypto_metadata** Puntatore al blocco di controllo HMAC MD5 utilizzato nel *_nx_crypto_method_hmac_md5_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-631">**crypto_metadata** Pointer to the HMAC MD5 control block used in *_nx_crypto_method_hmac_md5_init()*.</span></span>
- <span data-ttu-id="aeebb-632">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-632">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-633">Per HMAC MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-633">For HMAC MD5, the metadata size must *sizeof(NX_CRYPTO_MD5_HMAC)*</span></span>
- <span data-ttu-id="aeebb-634">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-634">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-635">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-635">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-636">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-636">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-637">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-637">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-638">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-638">Return Values</span></span>

- <span data-ttu-id="aeebb-639">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-639">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC MD5 operation.</span></span>
- <span data-ttu-id="aeebb-640">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-640">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-641">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-641">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-642">**NX_CRYPTO_INVALID_ALGORITHM** (0X20004) non è stato specificato un algoritmo MD5 HMAC non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-642">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC MD5 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-643">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-643">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha1_init"></a><span data-ttu-id="aeebb-644">_nx_crypto_method_hmac_sha1_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-644">_nx_crypto_method_hmac_sha1_init</span></span>

<span data-ttu-id="aeebb-645">Inizializza il blocco di controllo crittografico HMAC SHA1</span><span class="sxs-lookup"><span data-stu-id="aeebb-645">Initializes the HMAC SHA1 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-646">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-646">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-647">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-647">Description</span></span>

<span data-ttu-id="aeebb-648">Questa funzione Inizializza il blocco di controllo HMAC SHA1 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-648">This function initializes the HMAC SHA1 control block with the given key string.</span></span> <span data-ttu-id="aeebb-649">Una volta inizializzato il blocco di controllo HMAC SHA1, l'operazione HMAC SHA1 successiva dovrà utilizzare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-649">Once the HMAC SHA1 control block is initialized, subsequent HMAC SHA1 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-650">L'applicazione può creare più blocchi di controllo HMAC SHA1, ognuno di essi rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-650">Application may create multiple HMAC SHA1 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-651">L'inizializzazione del blocco di controllo HMAC SHA1 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-651">Initializing the HMAC SHA1 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-652">La reinizializzazione del blocco di controllo HMAC SHA1 abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-652">Re-initializing the HMAC SHA1 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-653">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-653">Parameters</span></span>

- <span data-ttu-id="aeebb-654">**Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-654">**method** Pointer to a valid HMAC SHA1 crypto method control block.</span></span> <span data-ttu-id="aeebb-655">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-655">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-656">*crypto_method_hmac_sha1*</span><span class="sxs-lookup"><span data-stu-id="aeebb-656">*crypto_method_hmac_sha1*</span></span>
- <span data-ttu-id="aeebb-657">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-657">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-658">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-658">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-659">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-659">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-660">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-660">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-661">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-661">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-662">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-662">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-663">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-663">**crypto_metadata** Pointer to a valid memory space for the HMAC SHA1 control block.</span></span> <span data-ttu-id="aeebb-664">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-664">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-665">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-665">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-666">Per HMAC SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-666">For HMAC SHA1, the metadata size must be *sizeof(NX_CRYPTO_SHA1_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-667">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-667">Return Values</span></span>

- <span data-ttu-id="aeebb-668">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco SHA1control HMAC con la chiave e la dimensione della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-668">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC SHA1control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-669">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-669">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-670">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-670">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_sha1_operation"></a><span data-ttu-id="aeebb-671">_nx_crypto_method_hmac_sha1_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-671">_nx_crypto_method_hmac_sha1_operation</span></span>

<span data-ttu-id="aeebb-672">Esegui operazione hash SHA1 HMAC</span><span class="sxs-lookup"><span data-stu-id="aeebb-672">Perform HMAC SHA1 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-673">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-673">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-674">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-674">Description</span></span>

<span data-ttu-id="aeebb-675">Questa funzione esegue l'operazione hash SHA1 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-675">This function performs HMAC SHA1 hash operation.</span></span> <span data-ttu-id="aeebb-676">Il blocco di controllo HMAC SHA1 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha1_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-676">The HMAC SHA1 control block must have been initialized with _ *nx_crypto_method_hmac_sha1_init()*.</span></span> <span data-ttu-id="aeebb-677">L'algoritmo HMAC SHA1 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-677">The HMAC SHA1 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-678">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 20 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-678">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 20 bytes.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-679">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-679">Parameters</span></span>

- <span data-ttu-id="aeebb-680">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-680">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-681">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-681">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-682">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-682">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-683">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-683">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-684">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-684">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-685">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-685">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-686">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-686">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-687">**Metodo** Puntatore al metodo crittografico HMAC SHA1 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-687">**method** Pointer to the valid HMAC SHA1 crypto method.</span></span> <span data-ttu-id="aeebb-688">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha1_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-688">The crypto method used here must be the same used in the _ *nx_crypto_method_hmac_sha1_init().*</span></span>
- <span data-ttu-id="aeebb-689">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-689">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-690">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-690">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-691">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-691">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-692">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-692">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-693">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-693">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-694">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-694">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-695">**iv_ptr** Questo campo non viene utilizzato per HMAC SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-695">**iv_ptr** This field is not used for HMAC SHA1.</span></span>
- <span data-ttu-id="aeebb-696">**iv_size** Questo campo non viene utilizzato per HMAC SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-696">**iv_size** This field is not used for HMAC SHA1.</span></span>
- <span data-ttu-id="aeebb-697">**output_buffer** Puntatore all'area di memoria per l'hash SHA1 HMAC generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-697">**output_buffer** Pointer to the memory area for the generated HMAC SHA1 hash.</span></span>
- <span data-ttu-id="aeebb-698">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-698">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-699">**crypto_metadata** Puntatore al blocco di controllo HMAC SHA1 utilizzato nel *_nx_crypto_method_hmac_sha1_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-699">**crypto_metadata** Pointer to the HMAC SHA1 control block used in *_nx_crypto_method_hmac_sha1_init()*.</span></span>
- <span data-ttu-id="aeebb-700">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-700">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-701">Per HMAC SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-701">For HMAC SHA1, the metadata size must *sizeof(NX_CRYPTO_SHA1_HMAC)*</span></span>
- <span data-ttu-id="aeebb-702">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-702">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-703">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-703">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-704">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-704">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-705">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-705">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-706">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-706">Return Values</span></span>

- <span data-ttu-id="aeebb-707">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-707">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC SHA1 operation.</span></span>
- <span data-ttu-id="aeebb-708">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-708">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-709">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-709">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-710">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo HMAC SHA1 non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-710">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC SHA1 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-711">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-711">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha1_cleanup"></a><span data-ttu-id="aeebb-712">_nx_crypto_method_hmac_sha1_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-712">_nx_crypto_method_hmac_sha1_cleanup</span></span>

<span data-ttu-id="aeebb-713">Pulire il blocco di controllo HMAC SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-713">Clean up the HMAC SHA1 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-714">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-714">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-715">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-715">Description</span></span>

<span data-ttu-id="aeebb-716">L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA1 dopo aver determinato che questa sessione HMAC SHA1 non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-716">Application calls this function to clean up the HMAC SHA1 control block after it determines this HMAC SHA1 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-717">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-717">Parameters</span></span>

- <span data-ttu-id="aeebb-718">**crypto_metadata** Puntatore al blocco di controllo HMAC SHA1 utilizzato nel *_nx_crypto_method_hmac_sha1_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-718">**crypto_metadata** Pointer to the HMAC SHA1 control block used in *_nx_crypto_method_hmac_sha1_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-719">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-719">Return Values</span></span>

- <span data-ttu-id="aeebb-720">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione HMAC SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-720">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the HMAC SHA1 session.</span></span>
- <span data-ttu-id="aeebb-721">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-721">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_hmac_sha256_init"></a><span data-ttu-id="aeebb-722">_nx_crypto_method_hmac_sha256_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-722">_nx_crypto_method_hmac_sha256_init</span></span>

<span data-ttu-id="aeebb-723">Inizializza il blocco di controllo crittografico HMAC SHA256</span><span class="sxs-lookup"><span data-stu-id="aeebb-723">Initializes the HMAC SHA256 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-724">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-724">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-725">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-725">Description</span></span>

<span data-ttu-id="aeebb-726">Questa funzione Inizializza il blocco di controllo HMAC SHA256 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-726">This function initializes the HMAC SHA256 control block with the given key string.</span></span> <span data-ttu-id="aeebb-727">Una volta inizializzato il blocco di controllo HMAC SHA256, l'operazione HMAC SHA256 successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-727">Once the HMAC SHA256 control block is initialized, subsequent HMAC SHA256 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-728">L'applicazione può creare più blocchi di controllo HMAC SHA256, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-728">Application may create multiple HMAC SHA256 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-729">L'inizializzazione del blocco di controllo HMAC SH256 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-729">Initializing the HMAC SH256 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-730">La reinizializzazione del blocco di controllo HMAC SHA256 abbandona la sessione corrente e ne crea una nuova con una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-730">Re-initializing the HMAC SHA256 control block abandons the current session and stars a new one with a new key.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-731">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-731">Parameters</span></span>

- <span data-ttu-id="aeebb-732">**Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC SHA256 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-732">**method** Pointer to a valid HMAC SHA256 crypto method control block.</span></span> <span data-ttu-id="aeebb-733">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-733">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-734">*crypto_method_hmac_sha224*</span><span class="sxs-lookup"><span data-stu-id="aeebb-734">*crypto_method_hmac_sha224*</span></span>
  - <span data-ttu-id="aeebb-735">*crypto_method_hmac_sha256*</span><span class="sxs-lookup"><span data-stu-id="aeebb-735">*crypto_method_hmac_sha256*</span></span>
- <span data-ttu-id="aeebb-736">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-736">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-737">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-737">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-738">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-738">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-739">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-739">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-740">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-740">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-741">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-741">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-742">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-742">**crypto_metadata** Pointer to a valid memory space for the HMAC SHA256 control block.</span></span> <span data-ttu-id="aeebb-743">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-743">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-744">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-744">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-745">Per HMAC SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYTPO_SHA256_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-745">For HMAC SHA256, the metadata size must be *sizeof(NX_CRYTPO_SHA256_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-746">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-746">Return Values</span></span>

- <span data-ttu-id="aeebb-747">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo HMAC SHA256 con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-747">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC SHA256 control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-748">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-748">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-749">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-749">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_sha256_operation"></a><span data-ttu-id="aeebb-750">_nx_crypto_method_hmac_sha256_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-750">_nx_crypto_method_hmac_sha256_operation</span></span>

<span data-ttu-id="aeebb-751">Esegui operazione hash SHA256 HMAC</span><span class="sxs-lookup"><span data-stu-id="aeebb-751">Perform HMAC SHA256 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-752">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-752">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-753">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-753">Description</span></span>

<span data-ttu-id="aeebb-754">Questa funzione esegue l'operazione hash SHA256 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-754">This function performs HMAC SHA256 hash operation.</span></span> <span data-ttu-id="aeebb-755">Il blocco di controllo HMAC SHA256 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha256_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-755">The HMAC SHA256 control block must have been initialized with _ *nx_crypto_method_hmac_sha256_init()*.</span></span> <span data-ttu-id="aeebb-756">L'algoritmo SHA256 HMAC da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-756">The HMAC SHA256 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-757">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 32 byte per SHA256 o di 28 byte per SHA224.</span><span class="sxs-lookup"><span data-stu-id="aeebb-757">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 32 bytes for SHA256, or 28 bytes for SHA224.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-758">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-758">Parameters</span></span>

- <span data-ttu-id="aeebb-759">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-759">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-760">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-760">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-761">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-761">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-762">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-762">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-763">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-763">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-764">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-764">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-765">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-765">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-766">**Metodo** Puntatore al metodo crittografico HMAC SHA256 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-766">**method** Pointer to the valid HMAC SHA256 crypto method.</span></span> <span data-ttu-id="aeebb-767">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha256_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-767">The crypto method used here must be the same used in the _ *nx_crypto_method_hmac_sha256_init().*</span></span>
- <span data-ttu-id="aeebb-768">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-768">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-769">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-769">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-770">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-770">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-771">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-771">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-772">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-772">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-773">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-773">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-774">**iv_ptr** Questo campo non viene utilizzato per SHA256 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-774">**iv_ptr** This field is not used for HMAC SHA256.</span></span>
- <span data-ttu-id="aeebb-775">**iv_size** Questo campo non viene utilizzato per SHA256 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-775">**iv_size** This field is not used for HMAC SHA256.</span></span>
- <span data-ttu-id="aeebb-776">**output_buffer** Puntatore all'area di memoria per l'hash SHA256 HMAC generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-776">**output_buffer** Pointer to the memory area for the generated HMAC SHA256 hash.</span></span>
- <span data-ttu-id="aeebb-777">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-777">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-778">**crypto_metadata** Puntatore al blocco di controllo HMAC SHA256 usato nella *_nx_crypto_method_hmac_sha256_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-778">**crypto_metadata** Pointer to the HMAC SHA256 control block used in *_nx_crypto_method_hmac_sha256_init()*.</span></span>
- <span data-ttu-id="aeebb-779">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-779">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-780">Per HMAC SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA256_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-780">For HMAC SHA256, the metadata size must *sizeof(NX_CRYPTO_SHA256_HMAC)*</span></span>
- <span data-ttu-id="aeebb-781">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-781">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-782">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-782">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-783">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-783">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-784">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-784">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-785">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-785">Return Values</span></span>

- <span data-ttu-id="aeebb-786">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-786">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC SHA256 operation.</span></span>
- <span data-ttu-id="aeebb-787">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-787">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-788">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-788">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-789">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA256 HMAC non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-789">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC SHA256 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-790">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-790">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha256_cleanup"></a><span data-ttu-id="aeebb-791">_nx_crypto_method_hmac_sha256_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-791">_nx_crypto_method_hmac_sha256_cleanup</span></span>

<span data-ttu-id="aeebb-792">Pulire il blocco di controllo HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-792">Clean up the HMAC SHA256 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-793">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-793">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-794">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-794">Description</span></span>

<span data-ttu-id="aeebb-795">L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA256 dopo aver determinato che questa sessione SHA256 HMAC non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-795">Application calls this function to clean up the HMAC SHA256 control block after it determines this HMAC SHA256 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-796">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-796">Parameters</span></span>

- <span data-ttu-id="aeebb-797">**crypto_metadata** Puntatore al blocco di controllo HMAC SHA256 usato nella *_nx_crypto_method_hmac_sha256_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-797">**crypto_metadata** Pointer to the HMAC SHA256 control block used in *_nx_crypto_method_hmac_sha256_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-798">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-798">Return Values</span></span>

- <span data-ttu-id="aeebb-799">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-799">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the HMAC SHA256 session.</span></span>
- <span data-ttu-id="aeebb-800">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-800">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_hmac_sha512_init"></a><span data-ttu-id="aeebb-801">_nx_crypto_method_hmac_sha512_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-801">_nx_crypto_method_hmac_sha512_init</span></span>

<span data-ttu-id="aeebb-802">Inizializza il blocco di controllo crittografico HMAC SHA512</span><span class="sxs-lookup"><span data-stu-id="aeebb-802">Initializes the HMAC SHA512 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-803">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-803">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-804">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-804">Description</span></span>

<span data-ttu-id="aeebb-805">Questa funzione Inizializza il blocco di controllo HMAC SHA512 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-805">This function initializes the HMAC SHA512 control block with the given key string.</span></span> <span data-ttu-id="aeebb-806">Una volta inizializzato il blocco di controllo HMAC SHA512, l'operazione HMAC SHA512 successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-806">Once the HMAC SHA512 control block is initialized, subsequent HMAC SHA512 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-807">L'applicazione può creare più blocchi di controllo HMAC SHA512, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-807">Application may create multiple HMAC SHA512 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-808">L'inizializzazione del blocco di controllo HMAC SH512 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-808">Initializing the HMAC SH512 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-809">La reinizializzazione del blocco di controllo HMAC SHA512 abbandona la sessione corrente e ne crea una nuova con una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-809">Re-initializing the HMAC SHA512 control block abandons the current session and stars a new one with a new key.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-810">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-810">Parameters</span></span>

- <span data-ttu-id="aeebb-811">**Metodo** Puntatore a un blocco di controllo del metodo crittografico HMAC SHA512 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-811">**method** Pointer to a valid HMAC SHA512 crypto method control block.</span></span> <span data-ttu-id="aeebb-812">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-812">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-813">*crypto_method_hmac_sha384*</span><span class="sxs-lookup"><span data-stu-id="aeebb-813">*crypto_method_hmac_sha384*</span></span>
  - <span data-ttu-id="aeebb-814">*crypto_method_hmac_sha512*</span><span class="sxs-lookup"><span data-stu-id="aeebb-814">*crypto_method_hmac_sha512*</span></span>
- <span data-ttu-id="aeebb-815">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-815">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-816">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-816">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-817">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-817">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-818">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-818">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-819">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-819">The handle is implementation-dependent, and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-820">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-820">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-821">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo HMAC SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-821">**crypto_metadata** Pointer to a valid memory space for the HMAC SHA512 control block.</span></span> <span data-ttu-id="aeebb-822">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-822">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-823">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-823">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-824">Per HMAC SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-824">For HMAC SHA512, the metadata size must be *sizeof(NX_CRYPTO_SHA512_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-825">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-825">Return Values</span></span>

- <span data-ttu-id="aeebb-826">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo HMAC SHA512 con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-826">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC SHA512 control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-827">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-827">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-828">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-828">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_sha512_operation"></a><span data-ttu-id="aeebb-829">_nx_crypto_method_hmac_sha512_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-829">_nx_crypto_method_hmac_sha512_operation</span></span>

<span data-ttu-id="aeebb-830">Esegui operazione hash SHA512 HMAC</span><span class="sxs-lookup"><span data-stu-id="aeebb-830">Perform HMAC SHA512 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-831">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-831">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-832">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-832">Description</span></span>

<span data-ttu-id="aeebb-833">Questa funzione esegue l'operazione hash SHA512 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-833">This function performs HMAC SHA512 hash operation.</span></span> <span data-ttu-id="aeebb-834">Il blocco di controllo HMAC SHA512 deve essere stato inizializzato con _ *nx_crypto_method_hmac_sha512_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-834">The HMAC SHA512 control block must have been initialized with _ *nx_crypto_method_hmac_sha512_init()*.</span></span> <span data-ttu-id="aeebb-835">L'algoritmo SHA512 HMAC da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-835">The HMAC SHA512 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-836">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 64 byte per SHA512 o di 48 byte per SHA384.</span><span class="sxs-lookup"><span data-stu-id="aeebb-836">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 64 bytes for SHA512, or 48 bytes for SHA384.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-837">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-837">Parameters</span></span>

- <span data-ttu-id="aeebb-838">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-838">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-839">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-839">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-840">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-840">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-841">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-841">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-842">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-842">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-843">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-843">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-844">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-844">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-845">**Metodo** Puntatore al metodo crittografico HMAC SHA512 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-845">**method** Pointer to the valid HMAC SHA512 crypto method.</span></span> <span data-ttu-id="aeebb-846">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_hmac_sha512_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-846">The crypto method used here must be the same used in the _ *nx_crypto_method_hmac_sha512_init().*</span></span>
- <span data-ttu-id="aeebb-847">**chiave** di Punta alla chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-847">**key** Points to the key.</span></span> <span data-ttu-id="aeebb-848">Non sono previste restrizioni per il buffer di chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-848">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="aeebb-849">**key_size_in_bits** Dimensione della chiave in bit.</span><span class="sxs-lookup"><span data-stu-id="aeebb-849">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="aeebb-850">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-850">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-851">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-851">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-852">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-852">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-853">**iv_ptr** Questo campo non viene utilizzato per SHA512 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-853">**iv_ptr** This field is not used for HMAC SHA512.</span></span>
- <span data-ttu-id="aeebb-854">**iv_size** Questo campo non viene utilizzato per SHA512 HMAC.</span><span class="sxs-lookup"><span data-stu-id="aeebb-854">**iv_size** This field is not used for HMAC SHA512.</span></span>
- <span data-ttu-id="aeebb-855">**output_buffer** Puntatore all'area di memoria per l'hash SHA512 HMAC generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-855">**output_buffer** Pointer to the memory area for the generated HMAC SHA512 hash.</span></span>
- <span data-ttu-id="aeebb-856">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-856">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="aeebb-857">**crypto_metadata** Puntatore al blocco di controllo HMAC SHA512 usato nella *_nx_crypto_method_hmac_sha512_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-857">**crypto_metadata** Pointer to the HMAC SHA512 control block used in *_nx_crypto_method_hmac_sha512_init()*.</span></span>
- <span data-ttu-id="aeebb-858">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-858">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-859">Per HMAC SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-859">For HMAC SHA512, the metadata size must *sizeof(NX_CRYPTO_SHA512_HMAC)*</span></span>
- <span data-ttu-id="aeebb-860">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-860">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-861">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-861">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-862">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-862">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-863">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-863">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-864">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-864">Return Values</span></span>

- <span data-ttu-id="aeebb-865">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione HMAC SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-865">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC SHA512 operation.</span></span>
- <span data-ttu-id="aeebb-866">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-866">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-867">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-867">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-868">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA512 HMAC non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-868">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC SHA512 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-869">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-869">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha512_cleanup"></a><span data-ttu-id="aeebb-870">_nx_crypto_method_hmac_sha512_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-870">_nx_crypto_method_hmac_sha512_cleanup</span></span>

<span data-ttu-id="aeebb-871">Pulire il blocco di controllo HMAC SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-871">Clean up the HMAC SHA512 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-872">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-872">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-873">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-873">Description</span></span>

<span data-ttu-id="aeebb-874">L'applicazione chiama questa funzione per pulire il blocco di controllo HMAC SHA512 dopo aver determinato che questa sessione SHA512 HMAC non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-874">Application calls this function to clean up the HMAC SHA512 control block after it determines this HMAC SHA512 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-875">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-875">Parameters</span></span>

- <span data-ttu-id="aeebb-876">**crypto_metadata** Puntatore al blocco di controllo HMAC SHA512 usato nella *_nx_crypto_method_hmac_sha512_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-876">**crypto_metadata** Pointer to the HMAC SHA512 control block used in *_nx_crypto_method_hmac_sha512_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-877">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-877">Return Values</span></span>

- <span data-ttu-id="aeebb-878">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione HMAC SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-878">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the HMAC SHA512 session.</span></span>
- <span data-ttu-id="aeebb-879">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-879">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

### <a name="example"></a><span data-ttu-id="aeebb-880">Esempio</span><span class="sxs-lookup"><span data-stu-id="aeebb-880">Example</span></span> 

## <a name="_nx_crypto_method_md5_init"></a><span data-ttu-id="aeebb-881">_nx_crypto_method_md5_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-881">_nx_crypto_method_md5_init</span></span>

<span data-ttu-id="aeebb-882">Inizializza il blocco di controllo Crypto MD5</span><span class="sxs-lookup"><span data-stu-id="aeebb-882">Initializes the MD5 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-883">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-883">Prototype</span></span>

```c
UINT _nx_crypto_method_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-884">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-884">Description</span></span>

<span data-ttu-id="aeebb-885">Questa funzione Inizializza il blocco di controllo MD5 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-885">This function initializes the MD5 control block with the given key string.</span></span> <span data-ttu-id="aeebb-886">Una volta inizializzato il blocco di controllo MD5, l'operazione MD5 successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-886">Once the MD5 control block is initialized, subsequent MD5 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-887">L'applicazione può creare più blocchi di controllo MD5, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-887">Application may create multiple MD5 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-888">L'inizializzazione del blocco di controllo MD5 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-888">Initializing the MD5 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-889">La reinizializzazione del blocco di controllo MD5 abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-889">Re-initializing the MD5 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-890">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-890">Parameters</span></span>

- <span data-ttu-id="aeebb-891">**Metodo** Puntatore a un blocco di controllo del metodo di crittografia MD5 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-891">**method** Pointer to a valid MD5 crypto method control block.</span></span> <span data-ttu-id="aeebb-892">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-892">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-893">*crypto_method_md5*</span><span class="sxs-lookup"><span data-stu-id="aeebb-893">*crypto_method_md5*</span></span>
- <span data-ttu-id="aeebb-894">**chiave** di Questo campo non viene usato per MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-894">**key** This field is not used for MD5.</span></span>
- <span data-ttu-id="aeebb-895">**key_size_in_bits** Questo campo non viene usato per MD5</span><span class="sxs-lookup"><span data-stu-id="aeebb-895">**key_size_in_bits** This field is not used for MD5</span></span>
- <span data-ttu-id="aeebb-896">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-896">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-897">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-897">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-898">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-898">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-899">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-899">**crypto_metadata** Pointer to a valid memory space for the MD5 control block.</span></span> <span data-ttu-id="aeebb-900">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-900">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-901">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-901">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-902">Per MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-902">For MD5, the metadata size must be *sizeof(NX_CRYPTO_MD5)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-903">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-903">Return Values</span></span>

- <span data-ttu-id="aeebb-904">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo MD5 con la chiave e la dimensione della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-904">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the MD5 control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-905">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-905">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-906">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-906">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

### <a name="example"></a><span data-ttu-id="aeebb-907">Esempio</span><span class="sxs-lookup"><span data-stu-id="aeebb-907">Example</span></span>

## <a name="_nx_crypto_method_md5_operation"></a><span data-ttu-id="aeebb-908">_nx_crypto_method_md5_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-908">_nx_crypto_method_md5_operation</span></span>

<span data-ttu-id="aeebb-909">Eseguire un'operazione hash MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-909">Perform an MD5 hash operation.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-910">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-910">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-911">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-911">Description</span></span>

<span data-ttu-id="aeebb-912">Questa funzione esegue l'operazione hash MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-912">This function performs MD5 hash operation.</span></span> <span data-ttu-id="aeebb-913">Il blocco di controllo MD5 deve essere stato inizializzato con _ *nx_crypto_method_md5_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-913">The MD5 control block must have been initialized with _ *nx_crypto_method_md5_init()*.</span></span> <span data-ttu-id="aeebb-914">L'algoritmo MD5 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-914">The MD5 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-915">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-915">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 16 bytes.</span></span>

<span data-ttu-id="aeebb-916">Questa operazione non mantiene le informazioni sullo stato e non modifica il materiale della chiave nel blocco di controllo MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-916">This operation does not keep state information and does not alter the key material in the MD5 control block.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-917">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-917">Parameters</span></span>

- <span data-ttu-id="aeebb-918">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-918">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-919">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-919">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-920">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-920">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-921">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-921">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-922">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-922">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-923">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-923">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-924">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-924">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-925">**Metodo** Puntatore al metodo di crittografia MD5 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-925">**method** Pointer to the valid MD5 crypto method.</span></span> <span data-ttu-id="aeebb-926">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_md5_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-926">The crypto method used here must be the same used in the _ *nx_crypto_method_md5_init().*</span></span>
- <span data-ttu-id="aeebb-927">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-927">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-928">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-928">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-929">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-929">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-930">**iv_ptr** Questo campo non viene usato per MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-930">**iv_ptr** This field is not used for MD5.</span></span>
- <span data-ttu-id="aeebb-931">**iv_size** Questo campo non viene usato per MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-931">**iv_size** This field is not used for MD5.</span></span>
- <span data-ttu-id="aeebb-932">**output_buffer** Puntatore all'area di memoria per l'hash MD5 generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-932">**output_buffer** Pointer to the memory area for the generated MD5 hash.</span></span>
- <span data-ttu-id="aeebb-933">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-933">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="aeebb-934">Per MD5 la dimensione del buffer deve essere di 16 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-934">For MD5 the buffer size must be 16 bytes.</span></span>
- <span data-ttu-id="aeebb-935">**crypto_metadata** Puntatore al blocco di controllo MD5 utilizzato nel *_nx_crypto_method_md5_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-935">**crypto_metadata** Pointer to the MD5 control block used in *_nx_crypto_method_md5_init()*.</span></span>
- <span data-ttu-id="aeebb-936">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-936">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-937">Per MD5, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_MD5)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-937">For MD5, the metadata size must *sizeof(NX_CRYPTO_MD5)*</span></span>
- <span data-ttu-id="aeebb-938">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-938">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-939">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-939">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-940">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-940">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-941">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-941">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-942">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-942">Return Values</span></span>

- <span data-ttu-id="aeebb-943">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-943">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the MD5 operation.</span></span>
- <span data-ttu-id="aeebb-944">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-944">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-945">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-945">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-946">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) algoritmo MD5 non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-946">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid MD5 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-947">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-947">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_md5_cleanup"></a><span data-ttu-id="aeebb-948">_nx_crypto_method_md5_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-948">_nx_crypto_method_md5_cleanup</span></span>

<span data-ttu-id="aeebb-949">Pulire il blocco di controllo MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-949">Clean up the MD5 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-950">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-950">Prototype</span></span>

```c
UINT _nx_crypto_method_md5_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-951">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-951">Description</span></span>

<span data-ttu-id="aeebb-952">L'applicazione chiama questa funzione per pulire il blocco di controllo MD5 dopo aver determinato che questa sessione MD5 non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-952">Application calls this function to clean up the MD5 control block after it determines this MD5 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-953">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-953">Parameters</span></span>

- <span data-ttu-id="aeebb-954">**crypto_metadata** Puntatore al blocco di controllo MD5 utilizzato nel *_nx_crypto_method_md5_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-954">**crypto_metadata** Pointer to the MD5 control block used in *_nx_crypto_method_md5_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-955">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-955">Return Values</span></span>

- <span data-ttu-id="aeebb-956">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione MD5.</span><span class="sxs-lookup"><span data-stu-id="aeebb-956">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the MD5 session.</span></span>
- <span data-ttu-id="aeebb-957">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-957">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_sha1_init"></a><span data-ttu-id="aeebb-958">_nx_crypto_method_sha1_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-958">_nx_crypto_method_sha1_init</span></span>

<span data-ttu-id="aeebb-959">Inizializza il blocco di controllo Crypto SHA1</span><span class="sxs-lookup"><span data-stu-id="aeebb-959">Initializes the SHA1 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-960">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-960">Prototype</span></span>

```c
UINT _nx_crypto_method_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-961">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-961">Description</span></span>

<span data-ttu-id="aeebb-962">Questa funzione Inizializza il blocco di controllo SHA1 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-962">This function initializes the SHA1 control block with the given key string.</span></span> <span data-ttu-id="aeebb-963">Una volta inizializzato il blocco di controllo SHA1, l'operazione SHA1 successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-963">Once the SHA1 control block is initialized, subsequent SHA1 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-964">L'applicazione può creare più blocchi di controllo SHA1, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-964">Application may create multiple SHA1 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-965">L'inizializzazione del blocco di controllo SHA1 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-965">Initializing the SHA1 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-966">La reinizializzazione del blocco di controllo SHA1 abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-966">Re-initializing the SHA1 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-967">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-967">Parameters</span></span>

- <span data-ttu-id="aeebb-968">**Metodo** Puntatore a un blocco di controllo del metodo crittografico SHA1 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-968">**method** Pointer to a valid SHA1 crypto method control block.</span></span> <span data-ttu-id="aeebb-969">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-969">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-970">*crypto_method_sha1*</span><span class="sxs-lookup"><span data-stu-id="aeebb-970">*crypto_method_sha1*</span></span>
- <span data-ttu-id="aeebb-971">**chiave** di Questo campo non viene usato per SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-971">**key** This field is not used for SHA1.</span></span>
- <span data-ttu-id="aeebb-972">**key_size_in_bits** Questo campo non viene usato per SHA1</span><span class="sxs-lookup"><span data-stu-id="aeebb-972">**key_size_in_bits** This field is not used for SHA1</span></span>
- <span data-ttu-id="aeebb-973">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-973">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-974">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-974">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-975">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-975">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-976">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-976">**crypto_metadata** Pointer to a valid memory space for the SHA1 control block.</span></span> <span data-ttu-id="aeebb-977">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-977">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-978">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-978">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-979">Per SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-979">For SHA1, the metadata size must be *sizeof(NX_CRYPTO_SHA1)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-980">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-980">Return Values</span></span>

- <span data-ttu-id="aeebb-981">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco SHA1control con la chiave e la dimensione della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-981">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the SHA1control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-982">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-982">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-983">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-983">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_sha1_operation"></a><span data-ttu-id="aeebb-984">_nx_crypto_method_sha1_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-984">_nx_crypto_method_sha1_operation</span></span>

<span data-ttu-id="aeebb-985">Esegui operazione hash SHA1</span><span class="sxs-lookup"><span data-stu-id="aeebb-985">Perform SHA1 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-986">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-986">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-987">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-987">Description</span></span>

<span data-ttu-id="aeebb-988">Questa funzione esegue l'operazione hash SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-988">This function performs SHA1 hash operation.</span></span> <span data-ttu-id="aeebb-989">Il blocco di controllo SHA1 deve essere stato inizializzato con _ *nx_crypto_method_sha1_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-989">The SHA1 control block must have been initialized with _ *nx_crypto_method_sha1_init()*.</span></span> <span data-ttu-id="aeebb-990">L'algoritmo SHA1 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-990">The SHA1 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-991">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 20 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-991">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 20 bytes.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-992">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-992">Parameters</span></span>

- <span data-ttu-id="aeebb-993">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-993">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-994">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-994">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-995">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-995">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-996">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-996">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-997">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-997">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-998">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-998">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-999">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-999">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-1000">**Metodo** Puntatore al metodo crittografico SHA1 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1000">**method** Pointer to the valid SHA1 crypto method.</span></span> <span data-ttu-id="aeebb-1001">Il metodo Crypto usato in questo caso deve essere lo stesso usato nella *nx_crypto_method_sha1_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1001">The crypto method used here must be the same used in the *nx_crypto_method_sha1_init().*</span></span>
- <span data-ttu-id="aeebb-1002">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1002">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-1003">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1003">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-1004">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1004">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-1005">**iv_ptr** Questo campo non viene usato per SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1005">**iv_ptr** This field is not used for SHA1.</span></span>
- <span data-ttu-id="aeebb-1006">**iv_size** Questo campo non viene usato per SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1006">**iv_size** This field is not used for SHA1.</span></span>
- <span data-ttu-id="aeebb-1007">**output_buffer** Puntatore all'area di memoria per l'hash SHA1 generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1007">**output_buffer** Pointer to the memory area for the generated SHA1 hash.</span></span>
- <span data-ttu-id="aeebb-1008">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1008">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="aeebb-1009">Per SHA1 la dimensione del buffer deve essere di 20 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1009">For SHA1 the buffer size must be 20 bytes.</span></span>
- <span data-ttu-id="aeebb-1010">**crypto_metadata** Puntatore al blocco di controllo SHA1 utilizzato nel *_nx_crypto_method_sha1_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1010">**crypto_metadata** Pointer to the SHA1 control block used in *_nx_crypto_method_sha1_init()*.</span></span>
- <span data-ttu-id="aeebb-1011">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1011">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-1012">Per SHA1, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA1)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1012">For SHA1, the metadata size must *sizeof(NX_CRYPTO_SHA1)*</span></span>
- <span data-ttu-id="aeebb-1013">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1013">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1014">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1014">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-1015">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1015">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1016">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1016">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1017">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1017">Return Values</span></span>

- <span data-ttu-id="aeebb-1018">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1018">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the SHA1 operation.</span></span>
- <span data-ttu-id="aeebb-1019">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1019">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-1020">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1020">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-1021">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) algoritmo SHA1 non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1021">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid SHA1 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-1022">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1022">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

### <a name="example"></a><span data-ttu-id="aeebb-1023">Esempio</span><span class="sxs-lookup"><span data-stu-id="aeebb-1023">Example</span></span>

## <a name="_nx_crypto_method_sha1_cleanup"></a><span data-ttu-id="aeebb-1024">_nx_crypto_method_sha1_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-1024">_nx_crypto_method_sha1_cleanup</span></span>

<span data-ttu-id="aeebb-1025">Pulire il blocco di controllo SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1025">Clean up the SHA1 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1026">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1026">Prototype</span></span>

```c
UINT _nx_crypto_method_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-1027">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1027">Description</span></span>

<span data-ttu-id="aeebb-1028">L'applicazione chiama questa funzione per pulire il blocco di controllo SHA1 dopo aver determinato che questa sessione SHA1 non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1028">Application calls this function to clean up the SHA1 control block after it determines this SHA1 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1029">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1029">Parameters</span></span>

- <span data-ttu-id="aeebb-1030">**crypto_metadata** Puntatore al blocco di controllo SHA1 utilizzato nel *_nx_crypto_method_sha1_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1030">**crypto_metadata** Pointer to the SHA1 control block used in *_nx_crypto_method_sha1_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1031">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1031">Return Values</span></span>

- <span data-ttu-id="aeebb-1032">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione SHA1.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1032">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the SHA1 session.</span></span>
- <span data-ttu-id="aeebb-1033">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1033">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_sha256_init"></a><span data-ttu-id="aeebb-1034">_nx_crypto_method_sha256_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-1034">_nx_crypto_method_sha256_init</span></span>

<span data-ttu-id="aeebb-1035">Inizializza il blocco di controllo Crypto SHA256</span><span class="sxs-lookup"><span data-stu-id="aeebb-1035">Initializes the SHA256 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1036">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1036">Prototype</span></span>

```c
UINT _nx_crypto_method_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size)
```

### <a name="description"></a><span data-ttu-id="aeebb-1037">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1037">Description</span></span>

<span data-ttu-id="aeebb-1038">Questa funzione Inizializza il blocco di controllo SHA256 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1038">This function initializes the SHA256 control block with the given key string.</span></span> <span data-ttu-id="aeebb-1039">Una volta inizializzato il blocco di controllo SHA256, l'operazione SHA256 successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1039">Once the SHA256 control block is initialized, subsequent SHA256 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-1040">L'applicazione può creare più blocchi di controllo SHA256, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1040">Application may create multiple SHA256 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-1041">L'inizializzazione del blocco di controllo SHA256 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1041">Initializing the SHA256 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-1042">La reinizializzazione del blocco di controllo SHA256 abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1042">Re-initializing the SHA256 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1043">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1043">Parameters</span></span>

- <span data-ttu-id="aeebb-1044">**Metodo** Puntatore a un blocco di controllo del metodo Crypto SHA256 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1044">**method** Pointer to a valid SHA256 crypto method control block.</span></span> <span data-ttu-id="aeebb-1045">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-1045">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-1046">*crypto_method_sha256*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1046">*crypto_method_sha256*</span></span>
  - <span data-ttu-id="aeebb-1047">*crypto_method_sha224*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1047">*crypto_method_sha224*</span></span>
- <span data-ttu-id="aeebb-1048">**chiave** di Questo campo non viene utilizzato per SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1048">**key** This field is not used for SHA256.</span></span>
- <span data-ttu-id="aeebb-1049">**key_size_in_bits** Questo campo non viene utilizzato per SHA256</span><span class="sxs-lookup"><span data-stu-id="aeebb-1049">**key_size_in_bits** This field is not used for SHA256</span></span>
- <span data-ttu-id="aeebb-1050">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1050">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-1051">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1051">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-1052">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1052">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-1053">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1053">**crypto_metadata** Pointer to a valid memory space for the SHA256 control block.</span></span> <span data-ttu-id="aeebb-1054">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1054">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-1055">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1055">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-1056">Per SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA256)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1056">For SHA256, the metadata size must be *sizeof(NX_CRYPTO_SHA256)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1057">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1057">Return Values</span></span>

- <span data-ttu-id="aeebb-1058">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo SHA256 con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1058">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the SHA256 control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-1059">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1059">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-1060">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1060">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_sha256_operation"></a><span data-ttu-id="aeebb-1061">_nx_crypto_method_sha256_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-1061">_nx_crypto_method_sha256_operation</span></span>

<span data-ttu-id="aeebb-1062">Eseguire l'operazione hash SHA256</span><span class="sxs-lookup"><span data-stu-id="aeebb-1062">Perform SHA256 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1063">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1063">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-1064">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1064">Description</span></span>

<span data-ttu-id="aeebb-1065">Questa funzione esegue l'operazione hash SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1065">This function performs SHA256 hash operation.</span></span> <span data-ttu-id="aeebb-1066">Il blocco di controllo SHA256 deve essere stato inizializzato con _ ***nx_crypto_method_sha256_init ()***.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1066">The SHA256 control block must have been initialized with _ ***nx_crypto_method_sha256_init()***.</span></span> <span data-ttu-id="aeebb-1067">L'algoritmo SHA256 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-1067">The SHA256 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-1068">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 32 byte per SHA256 o di 28 byte per SHA224.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1068">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 32 bytes for SHA256, or 28 bytes for SHA224.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1069">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1069">Parameters</span></span>

- <span data-ttu-id="aeebb-1070">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1070">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-1071">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-1071">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-1072">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1072">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-1073">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1073">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-1074">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1074">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-1075">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1075">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1076">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1076">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-1077">**Metodo** Puntatore al metodo di crittografia SHA256 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1077">**method** Pointer to the valid SHA256 crypto method.</span></span> <span data-ttu-id="aeebb-1078">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_sha256_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1078">The crypto method used here must be the same used in the _ *nx_crypto_method_sha256_init().*</span></span>
- <span data-ttu-id="aeebb-1079">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1079">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-1080">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1080">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-1081">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1081">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-1082">**iv_ptr** Questo campo non viene utilizzato per SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1082">**iv_ptr** This field is not used for SHA256.</span></span>
- <span data-ttu-id="aeebb-1083">**iv_size** Questo campo non viene utilizzato per SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1083">**iv_size** This field is not used for SHA256.</span></span>
- <span data-ttu-id="aeebb-1084">**output_buffer** Puntatore all'area di memoria per l'hash SHA256 generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1084">**output_buffer** Pointer to the memory area for the generated SHA256 hash.</span></span>
- <span data-ttu-id="aeebb-1085">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1085">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="aeebb-1086">Per SHA256, le dimensioni del buffer devono essere pari a 32 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1086">For SHA256 the buffer size must be 32 bytes.</span></span> <span data-ttu-id="aeebb-1087">Per SHA224, la dimensione del buffer deve essere di 28 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1087">For SHA224 the buffer size must be 28 bytes.</span></span>
- <span data-ttu-id="aeebb-1088">**crypto_metadata** Puntatore al blocco di controllo SHA2 utilizzato nel *_nx_crypto_method_sha2_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1088">**crypto_metadata** Pointer to the SHA2 control block used in *_nx_crypto_method_sha2_init()*.</span></span>
- <span data-ttu-id="aeebb-1089">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1089">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-1090">Per SHA256, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA256)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1090">For SHA256, the metadata size must *sizeof(NX_CRYPTO_SHA256)*</span></span>
- <span data-ttu-id="aeebb-1091">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1091">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1092">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1092">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-1093">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1093">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1094">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1094">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1095">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1095">Return Values</span></span>

- <span data-ttu-id="aeebb-1096">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1096">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the SHA256 operation.</span></span>
- <span data-ttu-id="aeebb-1097">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1097">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-1098">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1098">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-1099">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA256 non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1099">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid SHA256 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-1100">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1100">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_sha256_cleanup"></a><span data-ttu-id="aeebb-1101">_nx_crypto_method_sha256_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-1101">_nx_crypto_method_sha256_cleanup</span></span>

<span data-ttu-id="aeebb-1102">Pulire il blocco di controllo SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1102">Clean up the SHA256 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1103">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1103">Prototype</span></span>

```c
UINT _nx_crypto_method_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-1104">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1104">Description</span></span>

<span data-ttu-id="aeebb-1105">L'applicazione chiama questa funzione per pulire il blocco di controllo SHA256 dopo aver determinato che questa sessione SHA256 non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1105">Application calls this function to clean up the SHA256 control block after it determines this SHA256 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1106">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1106">Parameters</span></span>

- <span data-ttu-id="aeebb-1107">**crypto_metadata** Puntatore al blocco di controllo SHA256 utilizzato nel *_nx_crypto_method_sha256_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1107">**crypto_metadata** Pointer to the SHA256 control block used in *_nx_crypto_method_sha256_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1108">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1108">Return Values</span></span>

- <span data-ttu-id="aeebb-1109">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione SHA256.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1109">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the SHA256 session.</span></span>
- <span data-ttu-id="aeebb-1110">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1110">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_sha512_init"></a><span data-ttu-id="aeebb-1111">_nx_crypto_method_sha512_init</span><span class="sxs-lookup"><span data-stu-id="aeebb-1111">_nx_crypto_method_sha512_init</span></span>

<span data-ttu-id="aeebb-1112">Inizializza il blocco di controllo Crypto SHA512</span><span class="sxs-lookup"><span data-stu-id="aeebb-1112">Initializes the SHA512 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1113">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1113">Prototype</span></span>

```c
UINT _nx_crypto_method_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="aeebb-1114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1114">Description</span></span>

<span data-ttu-id="aeebb-1115">Questa funzione Inizializza il blocco di controllo SHA512 con la stringa di chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1115">This function initializes the SHA512 control block with the given key string.</span></span> <span data-ttu-id="aeebb-1116">Una volta inizializzato il blocco di controllo SHA512, l'operazione SHA512 successiva dovrà usare lo stesso blocco di controllo.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1116">Once the SHA512 control block is initialized, subsequent SHA512 operation shall be using the same control block.</span></span>

<span data-ttu-id="aeebb-1117">L'applicazione può creare più blocchi di controllo SHA512, ognuno rappresenta una sessione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1117">Application may create multiple SHA512 control blocks, each represents a session.</span></span> <span data-ttu-id="aeebb-1118">L'inizializzazione del blocco di controllo SHA512 avvia una nuova sessione di calcolo hash.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1118">Initializing the SHA512 control block starts a new hash computation session.</span></span> <span data-ttu-id="aeebb-1119">La reinizializzazione del blocco di controllo SHA512 abbandona la sessione corrente e ne crea una nuova.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1119">Re-initializing the SHA512 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1120">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1120">Parameters</span></span>

- <span data-ttu-id="aeebb-1121">**Metodo** Puntatore a un blocco di controllo del metodo Crypto SHA512 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1121">**method** Pointer to a valid SHA512 crypto method control block.</span></span> <span data-ttu-id="aeebb-1122">Sono disponibili i metodi di crittografia predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aeebb-1122">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="aeebb-1123">*crypto_method_sha512*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1123">*crypto_method_sha512*</span></span>
  - <span data-ttu-id="aeebb-1124">*crypto_method_sha384*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1124">*crypto_method_sha384*</span></span>
- <span data-ttu-id="aeebb-1125">**chiave** di Questo campo non viene utilizzato per SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1125">**key** This field is not used for SHA512.</span></span>
- <span data-ttu-id="aeebb-1126">**key_size_in_bits** Questo campo non viene utilizzato per SHA512</span><span class="sxs-lookup"><span data-stu-id="aeebb-1126">**key_size_in_bits** This field is not used for SHA512</span></span>
- <span data-ttu-id="aeebb-1127">**Gestisci** Questo servizio restituisce un handle per il chiamante.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1127">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="aeebb-1128">L'handle è dipendente dall'implementazione e non viene utilizzato in questa implementazione.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1128">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="aeebb-1129">L'applicazione deve passare NULL per l'handle.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1129">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="aeebb-1130">**crypto_metadata** Puntatore a uno spazio di memoria valido per il blocco di controllo SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1130">**crypto_metadata** Pointer to a valid memory space for the SHA512 control block.</span></span> <span data-ttu-id="aeebb-1131">L'indirizzo iniziale dello spazio di memoria deve essere allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1131">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="aeebb-1132">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1132">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-1133">Per SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1133">For SHA512, the metadata size must be *sizeof(NX_CRYPTO_SHA512)*</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1134">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1134">Return Values</span></span>

- <span data-ttu-id="aeebb-1135">**NX_CRYPTO_SUCCESS** (0x00) inizializzazione corretta del blocco di controllo SHA512 con la chiave e le dimensioni della chiave.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1135">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the SHA512 control block with the key and key size.</span></span>
- <span data-ttu-id="aeebb-1136">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1136">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-1137">**NX_PTR_ERROR** (0x07) puntatore non valido alla chiave o crypto_metadata o crypto_metadata_size non valido oppure crypto_metadata non è allineato a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1137">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_sha512_operation"></a><span data-ttu-id="aeebb-1138">_nx_crypto_method_sha512_operation</span><span class="sxs-lookup"><span data-stu-id="aeebb-1138">_nx_crypto_method_sha512_operation</span></span>

<span data-ttu-id="aeebb-1139">Eseguire l'operazione hash SHA512</span><span class="sxs-lookup"><span data-stu-id="aeebb-1139">Perform SHA512 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1140">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1140">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="aeebb-1141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1141">Description</span></span>

<span data-ttu-id="aeebb-1142">Questa funzione esegue l'operazione hash SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1142">This function performs SHA512 hash operation.</span></span> <span data-ttu-id="aeebb-1143">Il blocco di controllo SHA512 deve essere stato inizializzato con _ *nx_crypto_method_sha512_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1143">The SHA512 control block must have been initialized with _ *nx_crypto_method_sha512_init()*.</span></span> <span data-ttu-id="aeebb-1144">L'algoritmo SHA512 da eseguire è basato sull'algoritmo specificato nel blocco di controllo *Method* .</span><span class="sxs-lookup"><span data-stu-id="aeebb-1144">The SHA512 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="aeebb-1145">Per l'operazione di *NX_CRYPTO_HASH_CALCULATE* finale, la dimensione del buffer di output deve essere di 64 byte per SHA512 o di 48 byte per SHA384.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1145">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 64 bytes for SHA512, or 48 bytes for SHA384.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1146">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1146">Parameters</span></span>

- <span data-ttu-id="aeebb-1147">**operazione operativa** Tipo di operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1147">**op** Type of operation to perform.</span></span> <span data-ttu-id="aeebb-1148">Operazione valida:</span><span class="sxs-lookup"><span data-stu-id="aeebb-1148">Valid operation is:</span></span>
  - <span data-ttu-id="aeebb-1149">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1149">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="aeebb-1150">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1150">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="aeebb-1151">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1151">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="aeebb-1152">**Gestisci** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1152">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1153">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1153">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-1154">**Metodo** Puntatore al metodo di crittografia SHA512 valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1154">**method** Pointer to the valid SHA512 crypto method.</span></span> <span data-ttu-id="aeebb-1155">Il metodo Crypto usato in questo caso deve essere lo stesso usato in _ *nx_crypto_method_sha512_init ().*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1155">The crypto method used here must be the same used in the _ *nx_crypto_method_sha512_init().*</span></span>
- <span data-ttu-id="aeebb-1156">**input_data** Punta a un buffer che contiene dati di testo di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1156">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="aeebb-1157">Non sono previste restrizioni per il buffer di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1157">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="aeebb-1158">**input_data_size** Dimensioni in byte dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1158">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="aeebb-1159">**iv_ptr** Questo campo non viene utilizzato per SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1159">**iv_ptr** This field is not used for SHA512.</span></span>
- <span data-ttu-id="aeebb-1160">**iv_size** Questo campo non viene utilizzato per SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1160">**iv_size** This field is not used for SHA512.</span></span>
- <span data-ttu-id="aeebb-1161">**output_buffer** Puntatore all'area di memoria per l'hash SHA512 generato.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1161">**output_buffer** Pointer to the memory area for the generated SHA512 hash.</span></span>
- <span data-ttu-id="aeebb-1162">**output_buffer_size** Dimensioni del buffer di output in byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1162">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="aeebb-1163">Per SHA512, le dimensioni del buffer devono essere pari a 64 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1163">For SHA512 the buffer size must be 64 bytes.</span></span> <span data-ttu-id="aeebb-1164">Per SHA384, le dimensioni del buffer devono essere pari a 48 byte.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1164">For SHA384 the buffer size must be 48 bytes.</span></span>
- <span data-ttu-id="aeebb-1165">**crypto_metadata** Puntatore al blocco di controllo SHA512 utilizzato nel *_nx_crypto_method_sha512_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1165">**crypto_metadata** Pointer to the SHA512 control block used in *_nx_crypto_method_sha512_init()*.</span></span>
- <span data-ttu-id="aeebb-1166">**crypto_metadata_size** Dimensione, in byte, dell'area crypto_metadata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1166">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="aeebb-1167">Per SHA512, le dimensioni dei metadati devono essere *sizeof (NX_CRYPTO_SHA512)*</span><span class="sxs-lookup"><span data-stu-id="aeebb-1167">For SHA512, the metadata size must *sizeof(NX_CRYPTO_SHA512)*</span></span>
- <span data-ttu-id="aeebb-1168">**packet_ptr** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1168">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1169">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1169">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="aeebb-1170">**nx_crypto_hw_process_callback** Questo campo non viene usato nell'implementazione software di NetX Crypto Library.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1170">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="aeebb-1171">Qualsiasi valore passato viene ignorato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1171">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1172">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1172">Return Values</span></span>

- <span data-ttu-id="aeebb-1173">**NX_CRYPTO_SUCCESS** (0x00) ha eseguito correttamente l'operazione SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1173">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the SHA512 operation.</span></span>
- <span data-ttu-id="aeebb-1174">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1174">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="aeebb-1175">**NX_PTR_ERROR** (0x07) puntatore di input non valido o lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1175">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="aeebb-1176">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) è stato specificato un algoritmo SHA512 non valido.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1176">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid SHA512 algorithm being specified.</span></span>
- <span data-ttu-id="aeebb-1177">Dimensioni del buffer di output **NX_CRYPTO_INVALID_BUFFER_SIZE** (0X20005) non valide.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1177">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_sha512_cleanup"></a><span data-ttu-id="aeebb-1178">_nx_crypto_method_sha512_cleanup</span><span class="sxs-lookup"><span data-stu-id="aeebb-1178">_nx_crypto_method_sha512_cleanup</span></span>

<span data-ttu-id="aeebb-1179">Pulire il blocco di controllo SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1179">Clean up the SHA512 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="aeebb-1180">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aeebb-1180">Prototype</span></span>

```c
UINT _nx_crypto_method_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="aeebb-1181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aeebb-1181">Description</span></span>

<span data-ttu-id="aeebb-1182">L'applicazione chiama questa funzione per pulire il blocco di controllo SHA512 dopo aver determinato che questa sessione SHA512 non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1182">Application calls this function to clean up the SHA512 control block after it determines this SHA512 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="aeebb-1183">Parametri</span><span class="sxs-lookup"><span data-stu-id="aeebb-1183">Parameters</span></span>

- <span data-ttu-id="aeebb-1184">**crypto_metadata** Puntatore al blocco di controllo SHA512 utilizzato nel *_nx_crypto_method_sha512_init ()*.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1184">**crypto_metadata** Pointer to the SHA512 control block used in *_nx_crypto_method_sha512_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="aeebb-1185">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aeebb-1185">Return Values</span></span>

- <span data-ttu-id="aeebb-1186">**NX_CRYPTO_SUCCESS** (0x00) ha eliminato correttamente la sessione SHA512.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1186">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the SHA512 session.</span></span>
- <span data-ttu-id="aeebb-1187">**NX_CRYPTO_INVALID_LIBRARY** (0X20001) la libreria di crittografia è in uno stato non valido e non può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="aeebb-1187">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>